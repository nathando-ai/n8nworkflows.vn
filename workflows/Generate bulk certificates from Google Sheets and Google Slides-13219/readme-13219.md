---
title: "🚀 Tự động tạo chứng chỉ hàng loạt từ Google Sheets và Google Slides với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa 100% quy trình tạo chứng chỉ, văn bằng PDF hàng loạt từ Google Sheets và Google Slides, giúp tiết kiệm hàng giờ thao tác thủ công."
slug: "tu-dong-tao-chung-chi-hang-loat-tu-google-sheets-va-google-slides"
tags: [n8n, automation, no-code, google-sheets, google-slides, document-automation]
keywords: [n8n workflow, tạo chứng chỉ tự động, google sheets google slides n8n, bulk certificates automation, tự động hóa tài liệu]
---

# 🚀 Tự động tạo chứng chỉ hàng loạt từ Google Sheets và Google Slides

Mỗi khi tổ chức sự kiện, khóa học hay hội thảo, việc phải ngồi copy tên từng học viên, điền vào mẫu chứng chỉ, xuất ra PDF rồi gửi email thủ công thực sự là một "nỗi ám ảnh" tốn rất nhiều thời gian và dễ xảy ra sai sót. 

Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n cực kỳ thông minh, giúp tự động hóa toàn bộ quy trình: Đọc danh sách từ Google Sheets 👉 Nhân bản template Google Slides 👉 Điền thông tin 👉 Xuất file PDF 👉 Lưu vào Google Drive 👉 Cập nhật trạng thái và dọn dẹp file tạm. Tất cả diễn ra hoàn toàn tự động mà không cần tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Xử lý hàng trăm chứng chỉ chỉ trong vài phút thay vì làm thủ công từng cái.
- **Độ chính xác tuyệt đối:** Loại bỏ hoàn toàn lỗi gõ nhầm tên, sai ngày tháng hay mã chứng chỉ.
- **Vận hành thông minh:** Tự động lọc các dòng chưa xử lý, có cơ chế Rate Limit (chờ 2s) để tránh bị Google API chặn.
- **Tự động dọn dẹp:** File slide tạm được xóa sạch sau khi xuất PDF, giữ cho Google Drive luôn gọn gàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** đã cấp quyền kết nối (OAuth2) cho các dịch vụ: **Google Sheets**, **Google Drive**, và **Google Slides / Google Workspace APIs**.
- **Google Sheet mẫu** chứa danh sách người nhận.
- **Google Slides Template** làm mẫu chứng chỉ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy toàn bộ mã nguồn JSON và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với dữ liệu của các sếp, hãy chú ý cấu hình kỹ các node sau:

- **Google Sheet chuẩn bị sẵn**: Tạo một Google Sheet với các cột: `Name`, `Date`, `CertificateID`, `Processed`, và `DriveLink`. Các dòng dữ liệu mới cần để cột `Processed` ở trạng thái `FALSE`.
- **Google Slides Template**: Tạo một slide mẫu sử dụng các placeholder dạng `{{name}}`, `{{date}}`, `{{certificateid}}`.
- **Node `Read Unproven Recipients` (Google Sheets)**: Chọn credentials Google Sheets, trỏ tới file Sheet của các sếp và thiết lập điều kiện lọc các dòng có `Processed = FALSE`.
- **Các node HTTP Request (`Copy Slides Template`, `Replace Template Placeholders`, `Export to PDF`, `Delete Temporary Slide`)**: 
  - Thay thế các ID mẫu bằng `YOUR_GOOGLE_SHEET_ID`, `YOUR_TEMPLATE_SLIDES_ID`, và `YOUR_OUTPUT_FOLDER_ID` của các sếp.
  - Đảm bảo đã cấu hình đúng Header chứa token xác thực Google API (OAuth2).
- **Node `Save PDF to Drive` (Google Drive)**: Chọn thư mục đích trên Drive để lưu trữ các file PDF chứng chỉ xuất ra.
- **Node `Mark as Processed` (Google Sheets)**: Cấu hình thao tác `update` để ghi ngược đường dẫn `DriveLink` vào file Sheet và đổi trạng thái `Processed` thành `TRUE`.
- **Node `Wait 2s (Rate Limit)` (Wait)**: Giữ nguyên khoảng nghỉ 2 giây giữa các lần lặp để tuân thủ giới hạn gọi API của Google (Rate Limit).

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** và chạy thử với 1 dòng dữ liệu đầu tiên để kiểm tra xem file PDF có được tạo và lưu đúng chỗ không.
- Sau khi test thành công, bật nút **Active** để workflow sẵn sàng hoạt động tự động bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp gửi Email tự động:** Nối thêm node Gmail hoặc SendGrid ngay sau bước cập nhật Google Sheets để tự động gửi file PDF chứng chỉ trực tiếp đến email của từng người nhận.
- **Thông báo qua Telegram/Slack:** Thêm một thông báo tóm tắt vào nhóm chat nội bộ mỗi khi hoàn tất việc tạo batch chứng chỉ hàng loạt.
- **Log lỗi chuyên nghiệp:** Thiết lập đường nhánh lỗi (Error Trigger) để nếu một dòng dữ liệu bị lỗi, hệ thống sẽ ghi log lại thay vì làm gián đoạn toàn bộ quá trình.

### 📌 Kết luận
Việc tự động hóa tạo chứng chỉ hàng loạt chưa bao giờ dễ dàng đến thế với n8n kết hợp cùng Google Workspace. Hãy áp dụng ngay workflow này để tối ưu hóa thời gian vận hành cho các khóa học, sự kiện của doanh nghiệp các sếp nhé!