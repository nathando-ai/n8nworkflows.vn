---
title: "🚀 Tự Động Tải Video Bilibili → Google Drive & Gửi Email Thông Báo"
description: "Tự động tải video từ Bilibili, lưu lên Google Drive và gửi link qua email chỉ trong vài giây, không cần viết code."
slug: "bilibili-video-downloader-google-drive"
tags: [n8n, automation, no-code, file-management, google-drive, email]
keywords: [n8n workflow, tự động tải video, Google Drive, email notification, Bilibili downloader]
---

# 🚀 Tự Động Tải Video Bilibili → Google Drive & Gửi Email Thông Báo

Bạn đã từng phải **tải video Bilibili thủ công**, lưu trên máy tính rồi mới chia sẻ cho đồng nghiệp hoặc khách hàng?  
Quá trình này tốn thời gian, dễ gây lỗi và không thể tự động hoá.  
Workflow **Bilibili Video Downloader with Google Drive Upload & Email Notification** giải quyết toàn bộ vấn đề chỉ bằng một cú click, **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút xuống còn vài giây.
- **Độ chính xác 100 %**: Không còn lỗi “link sai” hay file không tải hết.
- **Chia sẻ tự động**: Link Google Drive được gửi ngay qua email.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** với quyền **Google Drive API** (OAuth2) đã bật.
- **SMTP server** (Gmail, Outlook, hoặc bất kỳ dịch vụ nào) để gửi email.
- **API Bilibili Downloader** (cung cấp endpoint trả về video URL và metadata).  
- **n8n** đã cài đặt (Self‑hosted hoặc Cloud) và có quyền **Create/Update** workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ nguồn gốc hoặc export từ n8n).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào **Editor → Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình chúng:

| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **On form submission** (formTrigger) | Kích hoạt workflow khi người dùng gửi form chứa URL Bilibili. | - **Form fields**: Tạo trường `videoUrl` (type: Text). |
| **Fetch Bilibili Video Info from API** (httpRequest) | Gửi URL tới API downloader để lấy thông tin video. | - **Method**: `GET` hoặc `POST` tùy API.<br>- **URL**: `https://api.example.com/bilibili?url={{$json["videoUrl"]}}`.<br>- **Headers**: Thêm `Authorization` nếu API yêu cầu. |
| **Check API Response Status** (if) | Kiểm tra `statusCode === 200`. | - **Condition**: `{{$json["statusCode"]}} === 200`.<br>- **True** → tiếp tục download.<br>- **False** → đi tới node **Processing Delay**. |
| **Download Video File** (httpRequest) | Tải video thực tế từ link trả về. | - **Method**: `GET`.<br>- **URL**: `{{$json["data"]["videoUrl"]}}`.<br>- **Response Format**: `File`. |
| **Upload Video to Google Drive** (googleDrive) | Đưa file đã tải lên Google Drive. | - **Operation**: `Upload`.<br>- **Folder ID**: ID thư mục đích trên Drive.<br>- **File Name**: `{{$json["data"]["title"]}}.mp4`.<br>- **Credentials**: Chọn **Google Drive OAuth2 API** đã tạo. |
| **Google Drive Set Permission** (googleDrive) | Đặt quyền chia sẻ cho file vừa tải lên. | - **Operation**: `Share`.<br>- **Resource**: `File`.<br>- **File ID**: `{{$node["Upload Video to Google Drive"].json["id"]}}`.<br>- **Permission**: `Anyone with the link` → `reader`. |
| **Success Notification Email with Drive Link** (emailSend) | Gửi email thành công kèm link Drive. | - **To**: `{{$json["email"]}}` (lấy từ form).<br>- **Subject**: `✅ Video Bilibili của bạn đã sẵn sàng`. <br>- **HTML Body**: Bao gồm link `https://drive.google.com/file/d/{{$node["Upload Video to Google Drive"].json["id"]}}/view`. |
| **Processing Delay** (wait) | Đợi ngắn (5‑10 giây) trước khi gửi email thất bại, tránh spam. | - **Time**: `5` seconds (có thể tùy chỉnh). |
| **Failure Notification Email** (emailSend) | Thông báo lỗi khi tải hoặc upload thất bại. | - **To**: `{{$json["email"]}}`.<br>- **Subject**: `❌ Không thể tải video Bilibili`. <br>- **HTML Body**: Mô tả ngắn lỗi và đề nghị thử lại. |

> **Lưu ý:** Đảm bảo **Credentials** cho Google Drive và SMTP đã được **Saved** trong n8n → **Credentials** trước khi gán vào node.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** với dữ liệu mẫu (điền URL Bilibili và email).  
2. Kiểm tra log từng node để xác nhận không lỗi.  
3. Khi mọi thứ ổn, bật **Active** (Toggle ở góc phải) để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Sau node gửi email thành công, dùng node **Slack** hoặc **Telegram** để thông báo ngay trong kênh nội bộ.  
- **Lưu log chi tiết**: Dùng node **Google Sheets** hoặc **Airtable** để ghi lại mỗi lần tải (URL, thời gian, trạng thái).  
- **Giới hạn kích thước**: Thêm node **IF** kiểm tra `Content‑Length` trước khi download, tránh video quá lớn gây timeout.  
- **Tự động xóa file cũ**: Định kỳ (cron) chạy workflow **Search & Delete** trên Drive để giữ dung lượng sạch sẽ.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình**: nhận URL, tải video, lưu trữ trên Google Drive và gửi link ngay cho người dùng – **không cần code, không tốn thời gian**. Hãy **import**, **cấu hình** nhanh chóng và **bật hoạt động** ngay hôm nay để nâng cao năng suất và trải nghiệm người dùng! 🚀