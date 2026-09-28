---
title: "🚀 Tự động tạo và gửi chứng chỉ cá nhân hóa với n8n, VerifiEmail, HTMLcsstoImg & Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình nhận thông tin, xác thực email, tạo chứng chỉ ảnh PNG chất lượng cao và gửi qua Gmail."
slug: "tu-dong-tao-va-gui-chung-chi-voi-n8n"
tags: [n8n, automation, no-code, gmail, google-sheets, ai-automation]
keywords: [n8n workflow, tự động hóa chứng chỉ, htmlcss to image, verifiemail, google sheets logging]
---

# 🚀 Tự động tạo và gửi chứng chỉ cá nhân hóa với n8n, VerifiEmail, HTMLcsstoImg & Gmail

Việc thiết kế, tạo và gửi chứng chỉ thủ công cho học viên, người tham gia sự kiện hay khóa học thường tốn rất nhiều thời gian và dễ xảy ra sai sót. Các sếp có đang gặp tình trạng nhân sự phải tự copy tên từng người, tạo file ảnh, check xem email có tồn tại không rồi mới lọ mọ gửi từng cái qua email? 

Quên cách làm thủ công đó đi! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hóa 100% giúp nhận dữ liệu qua Webhook, xác thực email, thiết kế chứng chỉ HTML/CSS chuyên nghiệp, convert sang ảnh PNG nét căng và gửi thẳng đến inbox người nhận, đồng thời lưu log tự động vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Từ lúc nhận request qua Webhook đến khi gửi email chứng chỉ chỉ mất vài giây mà không cần con người nhúng tay.
- **Xác thực email thông minh**: Sử dụng VerifiEmail để loại bỏ các email rác, email giả mạo hoặc sai cú pháp trước khi xử lý, tiết kiệm tài nguyên hệ thống.
- **Chứng chỉ chuyên nghiệp**: Tự động render mã HTML/CSS thành ảnh PNG sắc nét (1200x850px) với huy hiệu vàng, chữ ký và thông tin tùy chỉnh.
- **Lưu trữ minh bạch**: Tự động đồng bộ toàn bộ dữ liệu phát hành vào Google Sheets để tra cứu và làm audit trail bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản VerifiEmail**: Lấy API Key tại [verifi.email](https://verifi.email).
- **Tài khoản HTMLcsstoImg**: Lấy User ID và API Key tại [htmlcsstoimg.com](https://htmlcsstoimg.com).
- **Tài khoản Google (Gmail & Google Sheets)**: Để cấu hình OAuth2 gửi email và lưu log.
- **Tài khoản Slack** (Tùy chọn): Nếu muốn nhận cảnh báo lỗi qua Slack.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn JSON của workflow (hoặc tải file JSON từ nguồn) và paste trực tiếp vào giao diện n8n Editor của mình. Workflow gồm 12 nodes được thiết kế sẵn cấu trúc logic rõ ràng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Certificate Request Webhook**: Nhận POST request chứa thông tin học viên (`name`, `course`, `date`, `email`, v.v.). Hãy lấy URL test hoặc production để tích hợp với hệ thống bên ngoài (Landing page, Form, CRM).
- **Verifi Email**: Kết nối credential VerifiEmail API để kiểm tra tính hợp lệ của email (RFC compliance, MX records, chặn email tạm thời).
- **If (Validation Checkpoint)**: Kiểm tra điều kiện logic (Email phải `valid = true` và các trường `name`, `course`, `date` không được để trống).
- **Generate HTML Certificate & Code in JavaScript**: Tạo cấu trúc HTML chứng chỉ với nền gradient tím bắt mắt, font chữ sang trọng (Playfair Display & Montserrat) và tự động sinh `certificateId` nếu thiếu.
- **HTML/CSS to Image**: Kết nối API của HTMLcsstoImg để chuyển đổi mã HTML thành ảnh PNG chất lượng cao.
- **Send Certificate Email (Gmail)**: Cấu hình Gmail OAuth2 để gửi thư chúc mừng kèm link ảnh chứng chỉ và CTA chia sẻ LinkedIn.
- **Log to Google Sheets**: Tạo một Google Sheet có tên `"Certificates Log"` với các cột: `Certificate ID`, `Recipient Name`, `Course`, `Email`, `Completion Date`, `Generated At`, `Certificate URL`, `Status`, `Instructor`, `Duration`. Node này sẽ dùng tính năng `appendOrUpdate` dựa trên `Certificate ID` để tránh trùng lặp.
- **Error Handling (On Workflow Error, Format Error Details, Send Slack Alert)**: Luồng phụ giúp bắt lỗi hệ thống và gửi thông báo về Slack (nếu các sếp bật tính năng này).

#### 3. Kích hoạt ⚡️
- Test thử bằng cURL hoặc Postman với dữ liệu JSON mẫu:
```bash
curl -X POST https://n8n.yourdomain.com/webhook/certificate-generator \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test User",
    "course": "Advanced JavaScript Programming",
    "date": "2025-10-04",
    "email": "test@gmail.com",
    "instructor": "Jane Smith",
    "duration": "40 hours"
  }'
```
- Kiểm tra kết quả ở Gmail, Google Sheets và bật trạng thái **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm node "Respond to Webhook"**: Mặc định workflow sẽ kết thúc sau khi ghi log. Các sếp nên bổ sung node *Respond to Webhook* ở cuối luồng chính để trả về mã 200 kèm thông tin `certificateUrl` cho hệ thống gọi API biết.
- **Tích hợp Telegram/Zalo**: Thay vì chỉ dùng Slack để nhận cảnh báo lỗi, các sếp có thể đổi sang Telegram Bot để nhận thông báo tức thời ngay trên điện thoại cá nhân.
- **Lưu trữ ảnh Cloudinary/S3**: Nếu muốn lưu trữ lâu dài độc lập với HTMLcsstoImg, có thể thêm bước tải ảnh về và đẩy lên AWS S3 hoặc Google Drive cá nhân.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các tổ chức giáo dục, trung tâm đào tạo hoặc ban tổ chức sự kiện muốn tự động hóa hoàn toàn khâu vinh danh và cấp chứng chỉ. Hãy triển khai ngay hôm nay để nâng tầm chuyên nghiệp cho hệ thống của các sếp!