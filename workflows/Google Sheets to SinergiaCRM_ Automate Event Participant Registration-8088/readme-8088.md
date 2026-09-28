---
title: "🚀 Tự động hóa đăng ký sự kiện từ Google Sheets lên SinergiaCRM với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đồng bộ danh sách người tham gia sự kiện từ Google Sheets sang SinergiaCRM, kiểm tra trùng lặp thông qua mã NIF và cập nhật trạng thái xử lý."
slug: "tu-dong-hoa-dang-ky-su-kien-google-sheets-sinergiacrm-n8n"
tags: [n8n, automation, no-code, google-sheets, sinergiacrm, crm]
keywords: [n8n workflow, tự động hóa google sheets, sinergia crm, quản lý sự kiện n8n, #tech4good]
---

# 🚀 Tự động hóa đăng ký sự kiện từ Google Sheets lên SinergiaCRM

Trong các tổ chức phi lợi nhuận (NGO) hoặc doanh nghiệp thường xuyên tổ chức sự kiện, việc nhập liệu thủ công thông tin người tham gia từ các file đăng ký (Google Sheets) lên hệ thống CRM thường tốn rất nhiều thời gian và dễ xảy ra sai sót. Workflow n8n này do chuyên gia **Javier Quilez Cabello** phát triển sẽ giúp tự động hóa toàn bộ quy trình: lắng nghe dòng mới từ Google Sheets, kiểm tra sự tồn tại của người dùng qua mã định danh (NIF), tự động tạo mới liên hệ (Contact) hoặc cập nhật quan hệ và đăng ký sự kiện (Registration) vào **SinergiaCRM** một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Loại bỏ hoàn toàn khâu copy-paste thủ công từ Google Sheets lên CRM.
- **Kiểm tra thông minh:** Tự động tra cứu xem người tham gia đã tồn tại trong hệ thống dựa trên mã NIF (`stic_identification_number_c`), tránh tạo trùng lặp dữ liệu.
- **Phân luồng linh hoạt:** Nếu có rồi thì tiến hành tạo quan hệ và đăng ký sự kiện ngay; nếu chưa có, workflow sẽ tạo mới contact trước rồi mới đăng ký.
- **Đồng bộ trạng thái:** Tự động cập nhật cột "Processed" thành "Sí" trên Google Sheets sau khi xử lý thành công để tránh lặp lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã thiết lập sẵn sàng (Cloud hoặc Self-hosted).
- **Google Sheets:** Tài khoản Google có quyền truy cập Google Drive & Sheets (sử dụng `Google Sheets Trigger OAuth2Api` và `Google Sheets OAuth2Api`).
- **SinergiaCRM:** Hệ thống CRM cho lĩnh vực thứ ba với thông tin xác thực OAuth (`SinergiaCRMCredentials`) cùng các module: *Contacts*, *stic_Contacts_Relationships*, và *stic_Registrations*.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ n8n.io (ID: 8088).
- Vào n8n Editor, chọn **Add workflow** -> Nhấn dấu ba chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thành phần sau trong workflow gồm 14 nodes này:

- **Google Sheets Trigger**: 
  - Chọn tài khoản Google Sheets Credentials.
  - Điền đúng Document ID và Sheet Name chứa dữ liệu đăng ký sự kiện.
  - Đảm bảo Google Sheet của các sếp có các cột: `First name`, `Last name`, `NIF`, `Email`, `Relation type`, `Relation date`, `Event ID`, `Registration date`, `To CRM` (giá trị: "Yes"), và `Processed` (giá trị khởi tạo: "No").
- **Find person by NIF** & các node **SinergiaCRM**:
  - Cấu hình credentials cho SinergiaCRM.
  - Kiểm tra các trường dữ liệu tùy chỉnh (custom fields) như `stic_identification_number_c` đã khớp với cấu hình hệ thống SinergiaCRM của các sếp chưa.
  - Cập nhật User ID được gán (ví dụ: `"assigned_user_id": "2"`) nếu cần thiết trong các node tạo liên hệ/đăng ký.
- **Các node IF (IF: to CRM == Yes, IF: Not processed == No, IF: Person exist)**:
  - Đảm bảo các điều kiện lọc hoạt động đúng: Chỉ xử lý các hàng có `To CRM = Yes` và `Processed = No`.
- **Google Sheets: Mark Procesado = Sí / Sí1**:
  - Cấu hình node cập nhật Google Sheets để đổi cột "Processed" thành "Sí" sau khi xử lý thành công nhằm tránh việc xử lý trùng lặp (duplicate).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với một dòng dữ liệu mẫu trên Google Sheets để kiểm tra log.
- Sau khi mọi thứ chạy trơn tru, bật công tắc **Active** ở góc trên bên phải để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Slack** hoặc **Telegram** vào nhánh xử lý thành công hoặc thất bại để nhận thông báo tức thì khi có người đăng ký sự kiện mới.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt các lỗi API từ SinergiaCRM (ví dụ: lỗi định dạng NIF) và gửi cảnh báo về email hoặc chat nội bộ cho đội ngũ quản trị.
- **Mở rộng chiến dịch:** Kết hợp thêm các công cụ như Mautic hoặc Nextcloud để tự động gửi email chào mừng (Welcome Email) ngay sau khi thông tin được ghi nhận vào CRM.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ đắc lực cho các tổ chức phi lợi nhuận và doanh nghiệp trong việc tự động hóa quy trình quản lý sự kiện và CRM. Hãy áp dụng ngay để tiết kiệm thời gian, tối ưu hóa dữ liệu và nâng cao trải nghiệm cho người tham gia!