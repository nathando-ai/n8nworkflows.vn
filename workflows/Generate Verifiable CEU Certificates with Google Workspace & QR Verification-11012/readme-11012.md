---
title: "🚀 Tự động hóa tạo chứng chỉ CEU xác thực tích hợp QR Code với Google Workspace và n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động phát hành chứng chỉ CEU, xác thực email, tạo mã QR và lưu trữ toàn bộ lịch sử lên Google Workspace chỉ với n8n."
slug: "tu-dong-hoa-tao-chung-chi-ceu-google-workspace-qr-code"
tags: [n8n, automation, no-code, google-workspace, pdf-generation, slack]
keywords: [n8n workflow, tạo chứng chỉ tự động, CEU certificate, Google Sheets, Gmail automation, QR code verification]
---

# 🚀 Tự động hóa tạo chứng chỉ CEU xác thực tích hợp QR Code với Google Workspace và n8n

Việc cấp phát chứng chỉ đào tạo, chứng nhận CEU (Continuing Education Units) thủ công thường chiếm rất nhiều thời gian của đội ngũ vận hành: từ việc kiểm tra thông tin, xác thực email học viên, thiết kế file PDF, gửi email cá nhân hóa cho đến việc lưu trữ log báo cáo. 

Nếu các sếp đang tìm kiếm một giải pháp tự động hóa 100% không cần code để giải quyết trọn gói quy trình này, thì đây chính là workflow chuẩn xác nhất được thiết kế bởi chuyên gia Jitesh Dugar.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận dữ liệu từ form, xử lý và trả kết quả ngay lập tức mà không cần can thiệp thủ công.
- **Xác thực thông minh:** Kiểm tra tính hợp lệ của email học viên (chống email rác, kiểm tra MX record) trước khi phát hành chứng chỉ.
- **Bảo mật & Chống giả mạo:** Tự động sinh mã định danh duy nhất (Certificate ID) đi kèm mã QR xác thực trên từng chứng chỉ PDF chuyên nghiệp.
- **Đồng bộ đa nền tảng:** Tự động gửi email kèm file PDF cho học viên, lưu bản sao lên Google Drive, bắn thông báo về Slack và ghi log chi tiết vào Google Sheets.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản & API Keys:**
  - **Verif.Email API** (tại `verifi.email`) để kiểm tra email.
  - **PDFMunk / HTML to PDF API** (tại `pdfmunk.com`) để render HTML thành file PDF chứng chỉ.
  - **Google Workspace Credentials:** Tài khoản Google để kết nối Google Drive, Google Sheets và Gmail (OAuth2).
  - **Slack Workspace** (Tùy chọn) để nhận thông báo thời gian thực.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow hoặc tải file JSON gốc.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp vào giao diện).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với hệ thống của các sếp, hãy chú ý cấu hình các node quan trọng sau:

- **Webhook Trigger:** 
  - Lấy đường dẫn Webhook URL và gắn vào form đăng ký (Typeform, Google Forms qua Make/Zapier, hoặc Webflow/WordPress form).
  - Nhận dữ liệu dạng `POST` bao gồm thông tin học viên (Tên, Email, Khóa học...).
- **Validate Required Fields & Check Domain Verified:**
  - Các node `if` này giúp lọc các yêu cầu thiếu thông tin hoặc domain email không hợp lệ, trả về trạng thái qua `Stop: Incomplete Data` / `Stop: Domain Not Verified`.
- **Verifi Email:** 
  - Kết nối credentials của `Verif.Email API` để lọc bỏ các email ảo, email rác.
- **Generate Certificate ID & QR:** 
  - Node `function` chạy đoạn script tùy chỉnh để tạo mã định danh chứng chỉ duy nhất và tạo chuỗi URL mã QR xác thực.
- **HTML to PDF:** 
  - Kết nối dịch vụ chuyển đổi HTML sang PDF (`htmlcsstopdfApi`). Các sếp cần chỉnh sửa template HTML chứa tên công ty, logo và nội dung chứng chỉ theo thương hiệu riêng.
- **Upload to Google Drive & Send Email (Gmail):** 
  - Cấu hình thư mục lưu trữ trên Google Drive.
  - Thiết lập Gmail OAuth2 để tự động gửi email cá nhân hóa kèm file chứng chỉ PDF vừa tải về từ node `Download File`.
- **Log to Google Sheets & Notify Organizers (Slack):** 
  - Kết nối `Google SheetsOAuth2Api`, chọn file Google Sheets quản lý học viên và trỏ tới đúng tab/sheet để ghi log dữ liệu (`append`).
  - Cấu hình kênh Slack nhận thông báo mỗi khi có học viên hoàn thành và nhận chứng chỉ.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng cách gửi một dữ liệu `POST` mẫu qua Webhook.
- Kiểm tra toàn bộ luồng từ việc nhận data, xác thực email, tạo PDF đến gửi mail và ghi log.
- Nếu mọi thứ xanh mướt (success), hãy bật công tắc **Active workflow** để hệ thống chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Zalo / Telegram:** Ngoài Slack, các sếp có thể thêm node Telegram Bot để bắn thông báo ngay lập tức về điện thoại của đội ngũ chăm sóc khách hàng.
- **Lưu trữ backup:** Thêm một bước gửi thông tin về CRM (như HubSpot hoặc Zoho CRM) để dễ dàng quản lý hành trình học tập của khách hàng.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger vào workflow để nếu có lỗi phát sinh trong quá trình tạo PDF hay gửi mail, hệ thống sẽ tự động cảnh báo về nhóm kỹ thuật.

### 📌 Kết luận
Workflow tạo chứng chỉ CEU tích hợp mã QR xác thực này là một "vũ khí" cực kỳ lợi hại giúp tự động hóa khâu hậu đào tạo, nâng cao sự chuyên nghiệp và tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy triển khai ngay lên hệ thống n8n của các sếp và tận hưởng sự thảnh thơi!