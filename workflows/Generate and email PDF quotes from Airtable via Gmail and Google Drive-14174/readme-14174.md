---
title: "🚀 Tự động tạo và gửi báo giá PDF từ Airtable qua Gmail và Google Drive với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình tạo báo giá PDF chuyên nghiệp từ Airtable, lưu trữ Google Drive và gửi email cho khách hàng qua Gmail."
slug: "tu-dong-tao-va-gui-bao-gia-pdf-tu-airtable"
tags: [n8n, automation, airtable, google-drive, gmail, pdf, no-code]
keywords: [n8n workflow, tao bao gia tu dong, airtable automation, n8n pdf, gui email tu dong]
---

# 🚀 Tự động tạo và gửi báo giá PDF từ Airtable qua Gmail và Google Drive

Các sếp có còn đang tốn hàng giờ đồng hồ để copy dữ liệu từ Airtable vào Google Docs hoặc Word mỗi khi cần làm một bản báo giá (quote) gửi khách hàng không? Việc làm thủ công này vừa mất thời gian, dễ sai sót lại vừa thiếu chuyên nghiệp khi doanh nghiệp phát triển.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% này sẽ giúp các sếp giải quyết triệt để vấn đề trên. Chỉ cần gọi một Webhook kèm theo Record ID từ Airtable, hệ thống sẽ tự động tính toán, tạo file PDF chuẩn chỉnh, lưu trữ gọn gàng trên Google Drive và gửi thẳng tới hộp thư của khách hàng qua Gmail!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Loại bỏ hoàn toàn các bước thủ công copy-paste dữ liệu tạo báo giá.
- **Chuyên nghiệp & Chính xác:** Tự động tính toán tổng tiền, thuế, các khoản phí và xuất ra file PDF định dạng đẹp mắt, chuẩn thương hiệu.
- **Lưu trữ khoa học:** Tự động đồng bộ file PDF lên Google Drive và cập nhật ngược trạng thái, link file vào Airtable.
- **Chăm sóc khách hàng tức thì:** Gửi email đính kèm báo giá chuyên nghiệp qua Gmail ngay lập tức sau khi kích hoạt.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản & API Keys:**
  - **Airtable Account:** Base chứa bảng Quotes với các cột: `Client Name`, `Client Email`, `Line Items`, `Tax Rate`, `Notes`, `Status`.
  - **Google Drive & Gmail:** Tài khoản Google để kết nối node Drive và Gmail.
  - **PDF.co API Key:** Tài khoản miễn phí tại pdf.co để chuyển đổi HTML sang PDF.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ JSON của workflow (hoặc import file JSON gốc từ nguồn) vào n8n Editor. Workflow này gồm tổng cộng 9 nodes được thiết kế mạch lạc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các điểm sau:

- **Node `Quote Generation Webhook` (Webhook):** Điểm khởi đầu nhận dữ liệu `POST` chứa `recordId` từ Airtable Automation hoặc các ứng dụng bên thứ ba.
- **Node `Configure Settings` (Set):** Nơi các sếp cấu hình thông tin doanh nghiệp gồm: Tên công ty, email, mã màu thương hiệu, địa chỉ và **Google Drive Folder ID** (thư mục lưu trữ PDF).
- **Node `Read Quote from Airtable` & `Update Airtable Status` (Airtable):** 
  - Kết nối tài khoản Airtable Credentials.
  - Trỏ đến đúng Base và Table "Quotes" của các sếp.
  - Node cập nhật trạng thái (`Update Airtable Status`) sẽ đổi status thành "Sent" và đính kèm link Google Drive của file PDF.
- **Node `Build HTML Quote` (Code):** Xử lý logic bóc tách danh sách sản phẩm/dịch vụ (`Line Items`), tính toán tổng phụ (subtotal), tiền thuế (tax) và tổng thanh toán (grand total) để render ra mã HTML đẹp mắt.
- **Node `Convert HTML to PDF` & `Download PDF File` (HTTP Request):** Sử dụng API của pdf.co. Các sếp cần tạo API key tại pdf.co và thêm vào n8n dưới dạng **HTTP Header Auth** credential.
- **Node `Save Google Drive` (Google Drive):** Kết nối tài khoản Google và chọn thư mục lưu trữ file PDF vừa tạo.
- **Node `Email Quote to Client` (Gmail):** Kết nối tài khoản Gmail để gửi email đính kèm file PDF báo giá trực tiếp cho khách hàng (`Client Email`).

#### 3. Kích hoạt ⚡️
- Nhấp **Execute Workflow** và test thử bằng một Record ID thực tế từ Airtable.
- Kiểm tra kết quả trên Gmail, Google Drive và Airtable xem trạng thái đã được cập nhật chưa.
- Sau khi test thành công, bật công tắc **Active** để hệ thống tự động hóa vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm một node thông báo vào kênh nội dung của công ty mỗi khi có một báo giá mới được tạo và gửi thành công cho khách.
- **Lưu log lỗi:** Kết nối nhánh lỗi (Error Trigger) để cảnh báo về Telegram nếu quá trình convert PDF hoặc gửi email gặp sự cố.
- **Tùy biến giao diện HTML:** Chỉnh sửa code trong node `Build HTML Quote` để chèn logo công ty, thay đổi font chữ hoặc màu sắc phù hợp với bộ nhận diện thương hiệu riêng.

### 📌 Kết luận
Tự động hóa quy trình làm báo giá không chỉ giúp tiết kiệm hàng chục giờ làm việc mỗi tháng mà còn nâng tầm chuyên nghiệp trong mắt khách hàng nhờ tốc độ phản hồi chớp nhoáng. Hãy áp dụng ngay workflow này vào hệ thống của doanh nghiệp các sếp nhé!