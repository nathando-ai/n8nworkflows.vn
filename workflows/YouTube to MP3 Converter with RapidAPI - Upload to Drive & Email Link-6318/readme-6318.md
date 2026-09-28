---
title: "🎵 Tự động chuyển đổi YouTube thành MP3 và gửi link qua email - Workflow n8n"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi video YouTube thành MP3, lưu trữ trên Google Drive và gửi link tải xuống qua email - giải pháp hoàn toàn không cần code"
slug: "tu-dong-chuyen-doi-youtube-thanh-mp3-va-gui-email"
tags: [n8n, automation, no-code, youtube, google-drive]
keywords: [n8n workflow, tự động hóa, chuyển đổi video, mp3, google drive, email]
---

# 🎵 Tự động chuyển đổi YouTube thành MP3 và gửi link qua email - Workflow n8n

[Các sếp] có bao giờ gặp tình huống này không? Bạn hay phải chuyển đổi video YouTube thành file MP3 để nghe khi di chuyển, nhưng lại phải làm thủ công từng bước: tải video, chuyển đổi, lưu trữ và gửi link cho người dùng. Quá tốn thời gian và dễ xảy ra lỗi!

Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài phút, mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình chuyển đổi và gửi email trong vài giây
- **Chính xác 100%**: Không còn lỗi do thao tác thủ công
- **Tự động hóa hoàn toàn**: Không cần can thiệp của con người
- **Tăng trải nghiệm người dùng**: Người dùng nhận được file MP3 ngay lập tức qua email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập API
- Tài khoản email SMTP để gửi thông báo
- API key từ dịch vụ chuyển đổi YouTube sang MP3 (ví dụ: RapidAPI)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn "From JSON" và dán nội dung JSON của workflow vào ô nhập liệu
4. Nhấn "Import" để hoàn tất

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần phải cấu hình lại các node quan trọng sau:

1. **n8n Form Trigger**:
   - Cấu hình form để nhận 2 trường dữ liệu: YouTube URL và email người dùng
   - Ví dụ cấu hình:
     ```json
     {
       "YouTube URL": "text",
       "Email": "email"
     }
     ```

2. **HTTP Request (Node chuyển đổi YouTube sang MP3)**:
   - Cấu hình endpoint API của dịch vụ chuyển đổi
   - Thêm header Authorization với API key của bạn
   - Ví dụ cấu hình:
     ```json
     {
       "method": "POST",
       "url": "https://api.example.com/convert",
       "headers": {
         "Authorization": "Bearer YOUR_API_KEY"
       },
       "body": {
         "url": "{{$node["n8n Form Trigger"].json["YouTube URL"]}}"
       }
     }
     ```

3. **Wait**:
   - Thiết lập thời gian chờ phù hợp với dịch vụ chuyển đổi của bạn (thông thường 30-60 giây)

4. **Google Drive**:
   - Cấu hình credentials Google API
   - Chọn thư mục lưu trữ trên Google Drive
   - Ví dụ cấu hình:
     ```json
     {
       "operation": "upload",
       "resource": "file",
       "options": {
         "folderId": "YOUR_FOLDER_ID"
       }
     }
     ```

5. **Google Drive set permissions (Share)**:
   - Cấu hình quyền chia sẻ là "Anyone with the link"
   - Ví dụ cấu hình:
     ```json
     {
       "operation": "share",
       "resource": "file",
       "options": {
         "role": "reader",
         "type": "anyone"
       }
     }
     ```

6. **Send Email**:
   - Cấu hình credentials SMTP
   - Thiết lập nội dung email với link tải xuống
   - Ví dụ cấu hình:
     ```json
     {
       "to": "{{$node["n8n Form Trigger"].json["Email"]}}",
       "subject": "Your MP3 file is ready!",
       "text": "Download your MP3 file here: {{ $node["Google Drive set permissions"].json["webViewLink"] }}"
     }
     ```

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần:
1. Kiểm tra workflow bằng cách chạy thử với dữ liệu mẫu
2. Nhấn "Active" để kích hoạt workflow
3. Truy cập vào form và thử chuyển đổi một video YouTube để kiểm tra toàn bộ quy trình

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm thông báo Slack**: Kết nối với node Slack để nhận thông báo khi có yêu cầu mới
2. **Lưu log hoạt động**: Thêm node để lưu log các yêu cầu chuyển đổi
3. **Xử lý lỗi**: Thêm node xử lý lỗi để gửi email thông báo khi có lỗi xảy ra
4. **Tối ưu hóa lưu trữ**: Thiết lập lịch tự động xóa các file MP3 cũ sau một khoảng thời gian

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình chuyển đổi YouTube sang MP3, lưu trữ trên Google Drive và gửi link qua email. Với chỉ vài bước cấu hình đơn giản, các sếp có thể tiết kiệm hàng giờ làm việc mỗi ngày và cung cấp dịch vụ tốt hơn cho khách hàng.

Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa với n8n! 🚀