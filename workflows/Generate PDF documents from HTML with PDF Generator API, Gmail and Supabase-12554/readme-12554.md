---
title: "🚀 Tự động hóa tạo và gửi hóa đơn PDF từ HTML với PDF Generator API, Gmail và Supabase"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn diện quy trình kiểm tra email, tạo file PDF từ HTML template, lưu trữ Supabase và gửi mail cho khách hàng."
slug: "tu-dong-hoa-tao-pdf-tu-html-pdf-generator-api-gmail-supabase"
tags: [n8n, automation, pdf-generator, supabase, gmail, postgres]
keywords: [n8n workflow, tạo pdf tự động, pdf generator api, supabase storage, gửi email tự động n8n]
---

# 🚀 Tự động hóa tạo và gửi PDF từ HTML với PDF Generator API, Gmail và Supabase

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tạo hóa đơn, báo giá hoặc chứng từ thủ công mỗi khi có khách hàng đặt hàng? Việc copy dữ liệu vào file mẫu, xuất PDF, kiểm tra email khách có tồn tại hay không, gửi mail và lưu trữ lại tốn rất nhiều thời gian và dễ xảy ra sai sót.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n hoàn toàn tự động giải quyết triệt để bài toán trên từ A-Z mà không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%**: Tiếp nhận yêu cầu qua Webhook, tự động sinh PDF và gửi đi ngay lập tức.
- **Bảo mật & Chính xác**: Xác thực email khách hàng trước khi xử lý, tránh tình trạng gửi nhầm hoặc email rác nhờ Hunter.io.
- **Lưu trữ chuyên nghiệp**: File PDF sau khi tạo được tự động lưu lên **Supabase Storage** và ghi nhận lịch sử giao dịch vào **Postgres Database**.
- **Chăm sóc khách hàng tức thì**: Gửi trực tiếp file PDF chuyên nghiệp đến email khách hàng qua **Gmail**.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
- **Webhook endpoint**: Điểm nhận dữ liệu JSON đầu vào.
- **Hunter API**: Tài khoản và API Key để xác thực email.
- **PDF Generator API**: Tài khoản và credentials để chuyển đổi HTML thành PDF.
- **Postgres Database**: Lưu trữ template HTML và lịch sử giao dịch.
- **Gmail Account**: Kết nối OAuth2 để gửi email.
- **Supabase Storage**: Bucket lưu trữ các file PDF được xuất ra.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chuẩn xác các node cốt lõi sau:

- **Receive Document Request (Webhook)**: Node khởi chạy, nhận dữ liệu JSON đầu vào qua phương thức `POST`. Hãy copy URL Webhook này để cấu hình ở hệ thống bên ngoài (như CRM, Web app, hoặc Form).
- **Verify Client Email (Hunter)**: Chọn credentials `hunterApi`. Node này sẽ kiểm tra tính hợp lệ của email khách hàng.
- **Email Is Valid? (If)**: Kiểm tra kết quả từ Hunter. Nếu email hợp lệ (`true`), luồng tiếp tục chạy; ngược lại chuyển sang node phản hồi lỗi.
- **Respond – Invalid Email (Respond to Webhook)**: Trả về thông báo lỗi nếu email không tồn tại hoặc không hợp lệ.
- **Load HTML Template & Record Document Transaction (Postgres)**: Cấu hình credentials Postgres để kết nối database của sếp, thực hiện lấy template HTML và lưu lại log giao dịch.
- **Populate HTML Template (Code)**: Node chạy Javascript để đưa dữ liệu từ request vào các biến trong template HTML.
- **Convert HTML to PDF (PDF Generator API)**: Chọn credentials `pdfGeneratorApi` để thực hiệnconvert đoạn HTML hoàn chỉnh thành file PDF chất lượng cao.
- **Upload PDF to Supabase Storage (HTTP Request)**: Cấu hình gọi API của Supabase để tải file PDF lên cloud storage.
- **Send PDF to Client Email (Gmail)**: Kết nối tài khoản Gmail của sếp (OAuth2) để gửi email đính kèm file PDF vừa tạo tới khách hàng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với dữ liệu mẫu được ghim sẵn ở Webhook để kiểm tra toàn bộ luồng.
- Sau khi test thành công, bật trạng thái **Active** cho workflow để hệ thống tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack**: Thêm node Telegram hoặc Slack ngay sau bước tạo PDF thành công để đội ngũ sales nhận được thông báo ngay lập tức.
- **Xử lý lỗi (Error Handling)**: Thêm Error Trigger để nếu quá trình gọi API PDF Generator hoặc Supabase gặp sự cố, hệ thống sẽ tự động cảnh báo vào group chat nội bộ.
- **Tùy biến Email Template**: Sử dụng thêm các thẻ HTML trong node Gmail để làm đẹp email gửi đi thay vì chỉ gửi text thuần.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại giúp tự động hóa khâu xuất chứng từ, hóa đơn từ hệ thống phần mềm của doanh nghiệp. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần cho đội ngũ của các sếp!