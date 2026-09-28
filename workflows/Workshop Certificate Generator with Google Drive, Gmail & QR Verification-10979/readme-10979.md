---
title: "🎓 Tự động hóa phát hành chứng chỉ workshop với Google Drive, Gmail & xác thực QR"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình phát hành chứng chỉ workshop thông qua n8n, kết hợp Google Drive, Gmail và xác thực QR. Tiết kiệm thời gian và đảm bảo tính chính xác hoàn toàn."
slug: "tu-dong-hoa-phat-hanh-chung-chi-workshop"
tags: [n8n, automation, no-code, google-drive, gmail, qr-verification]
keywords: [n8n workflow, tự động hóa chứng chỉ, xác thực QR, google drive, gmail]
---

# 🎓 Tự động hóa phát hành chứng chỉ workshop với Google Drive, Gmail & xác thực QR

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý thủ công từ 80% trở lên
- Đảm bảo tính chính xác và nhất quán trong quá trình phát hành chứng chỉ
- Tự động lưu trữ và quản lý chứng chỉ trên Google Drive
- Xác thực QR giúp đảm bảo tính hợp lệ của chứng chỉ
- Tự động thông báo qua email và Slack
- Dễ dàng theo dõi và quản lý dữ liệu đăng ký thông qua Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Drive, Gmail, Google Sheets)
- Tài khoản Slack (cho thông báo)
- API keys từ các dịch vụ: VerifiEmail, HTMLCSStoImage
- Thiết kế mẫu chứng chỉ HTML/CSS (có thể tùy chỉnh sau)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/10979)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Click "Import" để hoàn tất

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Registration** (Node đầu tiên):
   - Đảm bảo đường dẫn webhook là duy nhất và phù hợp với hệ thống của bạn
   - Ví dụ: `https://your-n8n-instance.com/webhook/workshop-registration`

2. **Verifi Email** (Node 12):
   - Cần cấu hình credentials cho VerifiEmail
   - Điền API key từ tài khoản VerifiEmail của bạn

3. **HTML/CSS to Image** (Node 14):
   - Cấu hình credentials cho HTMLCSStoImage
   - Điền API key từ tài khoản HTMLCSStoImage của bạn

4. **Upload to Google Drive** (Node 6):
   - Cấu hình credentials cho Google Drive
   - Chỉ định thư mục lưu trữ chứng chỉ trong Google Drive của bạn
   - Ví dụ: `Workshop Certificates/2023`

5. **Send Certificate Email** (Node 7):
   - Cấu hình credentials cho Gmail
   - Tùy chỉnh mẫu email theo nhu cầu của bạn
   - Đảm bảo email có chứa các biến động như tên người tham gia, mã chứng chỉ, QR code...

6. **Log to Google Sheets** (Node 8):
   - Cấu hình credentials cho Google Sheets
   - Chỉ định spreadsheet và sheet name để lưu trữ dữ liệu
   - Ví dụ: Spreadsheet "Workshop Registrations", Sheet "2023"

7. **Notify Slack Channel** (Node 9):
   - Cấu hình credentials cho Slack
   - Chỉ định channel để nhận thông báo
   - Ví dụ: `#workshop-certificates`

8. **Prepare Certificate HTML** (Node 5):
   - Tùy chỉnh mẫu HTML/CSS của chứng chỉ theo thiết kế của bạn
   - Đảm bảo mẫu chứa các biến động như tên người tham gia, ngày tháng, mã chứng chỉ...

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, click vào nút "Activate" để kích hoạt workflow
2. Thử nghiệm với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
3. Kiểm tra email, Google Drive, Google Sheets và Slack để xác nhận các thông báo và dữ liệu được ghi nhận đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh mẫu chứng chỉ**: Các sếp có thể tùy chỉnh mẫu HTML/CSS để phù hợp với thương hiệu của mình
2. **Thêm thông báo qua Telegram**: Kết nối thêm node Telegram để nhận thông báo thay thế hoặc bổ sung cho Slack
3. **Tạo báo cáo định kỳ**: Sử dụng Google Sheets để tạo báo cáo tự động về số lượng chứng chỉ đã phát hành
4. **Xây dựng hệ thống xác thực nâng cao**: Kết hợp với các dịch vụ xác thực khác để tăng tính bảo mật

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quá trình phát hành chứng chỉ workshop, giúp các sếp tiết kiệm thời gian, đảm bảo tính chính xác và nâng cao trải nghiệm người tham gia. Hãy thử nghiệm và áp dụng ngay để tối ưu hóa quy trình của mình!