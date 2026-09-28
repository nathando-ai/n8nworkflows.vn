---
title: "🚀 Tự động tạo và gửi báo giá cá nhân hóa dạng PDF bằng n8n & OpenAI"
description: "Hướng dẫn xây dựng quy trình tự động hoàn toàn: Nhận form yêu cầu, AI viết nội dung, tạo file PDF từ Google Docs template và gửi email cho khách hàng."
slug: "tu-dong-tao-va-gui-bao-gia-pdf-n8n"
tags: [n8n, automation, no-code, openai, google-docs, gmail]
keywords: [n8n workflow, tạo báo giá tự động, google docs to pdf, openai automation, gửi email tự động n8n]
---

# 🚀 Tự động tạo và gửi báo giá cá nhân hóa dạng PDF bằng n8n & OpenAI

Các sếp trong đội ngũ Sales và Marketing chắc hẳn hiểu rõ cảm giác "ngợp" mỗi khi phải ngồi thủ công soạn từng bản báo giá: Copy mẫu, điền tên khách hàng, chỉnh sửa lại mô tả dịch vụ, xuất file PDF rồi mở Gmail gửi đi. Quy trình này vừa tốn thời gian, vừa dễ nhầm lẫn, lại làm giảm tốc độ chốt đơn.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n **Generate and Send Personalized Quotations PDF**. Quy trình này sẽ tự động hóa 100% từ khâu nhận thông tin từ form đăng ký, dùng OpenAI viết lời mở đầu và tóm tắt phạm vi công việc cực kỳ chuyên nghiệp, cho đến việc tạo tài liệu Google Docs, xuất ra PDF và gửi thẳng tới hộp thư của khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ chốt đơn thần tốc:** Khách hàng nhận được báo giá chuyên nghiệp ngay lập tức sau khi bấm gửi form.
- **Cá nhân hóa thông minh:** OpenAI giúp viết lời chào và tóm tắt dịch vụ phù hợp riêng cho từng khách hàng, tăng tỷ lệ chuyển đổi.
- **Chuẩn hóa thương hiệu:** Sử dụng chung một template Google Docs đẹp mắt, chuyên nghiệp cho toàn bộ team Sales.
- **Hoạt động 24/7:** Không bỏ sót bất kỳ khách hàng tiềm năng nào ngay cả ngoài giờ hành chính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (để tạo nội dung cá nhân hóa).
- **Google Drive / Google Docs** (tài khoản Google cá nhân hoặc Workspace để lưu template và tạo file).
- **Gmail Account** (tài khoản gửi email báo giá tự động).
- **Google Docs Template** chứa các biến (variables) chuẩn bị sẵn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó dán (paste) trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình các node quan trọng sau:

- **Node `Quotation Form` (formTrigger):** 
  - Node này tạo ra một trang form thu thập thông tin khách hàng (tên, email, công ty, dịch vụ, giá tiền, thời hạn hiệu lực, ghi chú...). 
  - Các sếp có thể tùy chỉnh các trường dữ liệu hiển thị trên form cho phù hợp với sản phẩm/dịch vụ của công ty mình.

- **Node `OpenAI Personalize` (openAi):** 
  - Chọn Credentials OpenAI API của các sếp.
  - Cấu hình Prompt để AI tạo ra đoạn `intro` (lời mở đầu) và `scope_summary` (tóm tắt phạm vi công việc) dựa trên thông tin từ form.

- **Node `Copy Template` (googleDrive):** 
  - Cấu hình Google Drive OAuth2.
  - Tạo sẵn một Google Docs Template trên Drive của các sếp với các biến dạng `{{bien}}`, ví dụ: `{{client_name}}`, `{{company_name}}`, `{{client_email}}`, `{{service}}`, `{{price}}`, `{{valid_until}}`, `{{notes}}`, `{{intro}}`, `{{scope_summary}}`.
  - Copy **Document ID** của template đó và dán vào tham số của node này để n8n nhân bản ra một bản sao mới khi chạy.

- **Node `Replace Variables` (googleDocs):** 
  - Cấu hình Google Docs OAuth2.
  - Node này sẽ thực hiện nhiệm vụ điền dữ liệu từ form và nội dung do OpenAI tạo ra vào các vị trí biến `{{...}}` tương ứng trong bản sao Google Docs vừa tạo.

- **Node `Export as PDF` (googleDrive):** 
  - Node này chuyển đổi tài liệu Google Docs vừa điền thông tin thành định dạng tệp PDF để chuẩn bị gửi đi.

- **Node `Send Quotation Email` (gmail):** 
  - Cấu hình Gmail OAuth2 để cho phép n8n gửi email nhân danh tài khoản của các sếp.
  - Thiết lập tiêu đề email, nội dung thông báo và đính kèm tệp PDF vừa xuất bản.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test step** hoặc **Execute Workflow** trên từng node để kiểm tra xem dữ liệu có chảy mượt mà hay không.
- Khi mọi thứ đã chạy trơn tru, các sếp gạt công tắc sang chế độ **Active** để đưa workflow vào hoạt động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu thông tin CRM:** Thêm một node Google Sheets hoặc HubSpot vào sau bước tạo form để lưu lại toàn bộ danh sách khách hàng yêu cầu báo giá.
- **Thông báo nội bộ:** Thêm node Telegram hoặc Slack Bot để bắn một tin nhắn về group nội bộ của team Sales thông báo: *"Vừa có khách hàng X yêu cầu báo giá dịch vụ Y!"*.
- **Theo dõi trạng thái:** Thiết lập thêm một luồng nhắc nhở tự động (Follow-up) sau 3 ngày kể từ khi gửi báo giá nếu khách hàng chưa phản hồi.

### 📌 Kết luận
Việc tự động hóa quy trình tạo và gửi báo giá không chỉ giúp các sếp tiết kiệm hàng chục giờ mỗi tuần mà còn mang lại trải nghiệm cực kỳ chuyên nghiệp trong mắt khách hàng. Hãy "lên đồ" và cài đặt ngay workflow này để tối ưu hóa đội ngũ sales của mình nhé!