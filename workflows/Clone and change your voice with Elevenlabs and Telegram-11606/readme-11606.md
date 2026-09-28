---
title: "🚀 Clone và Thay Đổi Giọng Nói với ElevenLabs & Telegram"
description: "Tự động sao chép giọng nói hoặc chuyển đổi giọng nói qua bot Telegram, lưu trữ trên Google Drive, hoàn toàn không cần code."
slug: "clone-thay-doi-giong-nho-voi-elevenlabs-telegram"
tags: [n8n, automation, no-code, voice, ai, telegram, elevenlabs, google-drive]
keywords: [n8n workflow, tự động hóa, clone giọng nói, ElevenLabs, Telegram bot, Google Drive, AI voice]
---

# 🚀 Clone và Thay Đổi Giọng Nói với ElevenLabs & Telegram

Bạn đang gặp khó khăn khi muốn tạo ra những bản ghi âm giọng nói độc đáo, hoặc muốn chuyển đổi giọng nói của mình thành một giọng khác mà không cần phải học cách lập trình?  
Workflow này sẽ giúp bạn **sao chép giọng nói** của chính mình hoặc **chuyển đổi** giọng nói thành một giọng đã được lưu trữ trên ElevenLabs chỉ bằng một tin nhắn giọng nói gửi tới bot Telegram. Kết quả được lưu trữ ngay trên Google Drive, bạn có thể truy cập bất cứ lúc nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết code, chỉ gửi tin nhắn giọng nói.  
- **Chính xác & linh hoạt**: ElevenLabs cung cấp chất lượng giọng nói tự nhiên, có thể clone ngay lập tức.  
- **Tự động lưu trữ**: Tất cả file âm thanh được upload lên Google Drive, dễ dàng chia sẻ và quản lý.  
- **Hoạt động liên tục**: Bot Telegram hoạt động 24/7, bạn chỉ cần gửi tin nhắn bất cứ lúc nào.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Telegram Bot**: Tạo bot qua BotFather, lấy `token` và cấu hình node `Telegram Trigger`.  
- **Telegram User ID**: Đăng ký node `Sanitaze` và thay thế `XXXX` bằng ID của bạn.  
- **ElevenLabs API Key**: Đăng ký tại [ElevenLabs](https://try.elevenlabs.io/ahkbf00hocnu) và cấu hình `httpHeaderAuth` với `Name: xi-api-key`, `Value: YOUR_API_KEY`.  
- **Google Drive OAuth2**: Cấu hình credentials `googleDriveOAuth2Api` và chọn thư mục lưu trữ.  
- **(Tùy chọn) Voice ID**: Nếu muốn chuyển đổi giọng nói, nhập `voice_id` đã clone vào node `Generate cloned audio`.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
- Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/11606) hoặc sao chép toàn bộ JSON vào clipboard.  
- Mở n8n Editor → `Import` → `Import from clipboard` → dán JSON → `Import`.  

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|--------------------|---------|
| Telegram Trigger | `Telegram Trigger` | Credentials: `telegramApi` (bot token) | Đảm bảo bot đã được kích hoạt và có quyền nhận tin nhắn. |
| Switch | `Switch` | Kiểm tra `message.type` (voice) | Đảm bảo chỉ xử lý tin nhắn giọng nói. |
| Sanitaze | `Sanitaze` | Thay `XXXX` bằng Telegram User ID của bạn | Giúp giới hạn quyền truy cập. |
| Get audio | `Get audio` | Credentials: `telegramApi` | Lấy file âm thanh từ tin nhắn. |
| Create Cloned Voice | `Create Cloned Voice` | Credentials: `httpHeaderAuth` (xi-api-key) | Gửi file lên ElevenLabs để clone giọng. |
| Generate cloned audio | `Generate cloned audio` | Credentials: `httpHeaderAuth` (xi-api-key) | Gửi file và `voice_id` đã clone để chuyển đổi. |
| Upload file | `Upload file` | Credentials: `googleDriveOAuth2Api` | Lưu file âm thanh đã chuyển đổi lên Google Drive. |

> **Lưu ý**: Node `Sanitaze` có thể được bỏ qua nếu bạn không cần giới hạn quyền. Tuy nhiên, để bảo mật, hãy giữ nó.

### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một tin nhắn giọng nói tới bot Telegram của bạn.  
2. Kiểm tra log trong n8n để xem workflow đã chạy thành công chưa.  
3. Nếu mọi thứ ổn, bật `Active` cho workflow.  

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notifications**: Thêm node `Telegram` hoặc `Slack` để gửi thông báo khi file đã được upload.  
- **Lưu log**: Sử dụng node `Google Drive` để lưu file log JSON, giúp theo dõi lịch sử clone.  
- **Báo cáo định kỳ**: Kết hợp với node `Cron` để gửi báo cáo tổng hợp giọng nói đã clone mỗi tuần.  
- **Tích hợp với Zapier**: Khi file được lưu trên Google Drive, trigger Zapier để tự động chia sẻ trên mạng xã hội.  

## 📌 Kết luận
Workflow này cho phép các sếp nhanh chóng **clone giọng nói** hoặc **chuyển đổi giọng nói** mà không cần bất kỳ kỹ năng lập trình nào. Chỉ cần một bot Telegram, một tài khoản ElevenLabs và Google Drive, bạn đã có một công cụ AI voice assistant hoàn chỉnh. Hãy thử ngay hôm nay và trải nghiệm sức mạnh của AI trong công việc!

---