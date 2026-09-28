---
title: "🚀 Đăng bài RSS tự động lên WordPress & Mạng Xã hội"
description: "Tự động lấy bài viết từ RSS, tạo bài viết WordPress, chia sẻ lên Discord, LinkedIn, Telegram, Facebook, WhatsApp và gửi thông báo qua email."
slug: "dang-bai-rss-tu-dong-len-wordpress-va-mang-xa-hoi"
tags: [n8n, automation, no-code, wordpress, social-media, rss, ai]
keywords: [n8n workflow, tự động hóa, đăng bài RSS, WordPress, mạng xã hội, AI]
---

# 🚀 Đăng bài RSS tự động lên WordPress & Mạng Xã hội

Bạn đang phải mất hàng giờ mỗi ngày để copy‑paste bài viết từ nguồn RSS, upload ảnh, đăng lên WordPress và chia sẻ trên các kênh mạng xã hội?  
Workflow này sẽ giải quyết mọi nỗi đau đó bằng cách tự động hoá 100% quy trình, giảm thiểu sai sót và tăng tính nhất quán trong nội dung.  

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ → vài phút.  
- **Độ chính xác cao**: Không còn sai sót khi copy‑paste thủ công.  
- **Tự động cập nhật**: Mỗi khi có bài mới trong RSS, workflow sẽ chạy ngay.  
- **Tích hợp đa kênh**: Đăng bài đồng thời lên WordPress, Discord, LinkedIn, Telegram, Facebook, WhatsApp và gửi thông báo qua email.  
- **Khả năng mở rộng**: Thêm kênh mới hoặc chỉnh sửa nội dung bằng AI chỉ cần thay đổi một vài node.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ / API | Mô tả | Cách lấy |
|---|---|---|
| **WordPress** | API REST để tạo bài viết và upload media | Tạo Application Password trong WordPress (đăng nhập > Users > Profile) |
| **Discord** | Bot token, Channel ID | Tạo bot trên Discord Developer Portal, thêm vào server |
| **LinkedIn** | OAuth 2.0 credentials (Client ID, Secret, Redirect URL) | Đăng ký ứng dụng LinkedIn Developer |
| **Telegram** | Bot token, Chat ID | Tạo bot qua BotFather, lấy chat ID |
| **Facebook Graph API** | Page Access Token | Tạo app Facebook, lấy token cho page |
| **WhatsApp (Rapiwa)** | API Key, Phone Number | Đăng ký tài khoản Rapiwa |
| **OpenAI** | API Key | Đăng ký tại OpenAI |
| **Gmail** | OAuth 2.0 credentials | Tạo project Google Cloud, bật Gmail API |
| **RSS Feed** | URL feed | Cung cấp URL trong node `RSS Read Domani` |
| **Image Hosting** | URL để upload ảnh (được WordPress cung cấp) | Được trả về từ node `upload media to wp` |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc:  
   `https://n8n.io/workflows/11677`  
2. Mở n8n Editor → `Import` → `Upload file` → chọn file JSON.  
3. Hoặc copy toàn bộ JSON và dán vào tab `Import` → `Paste JSON`.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Thông tin cần cấu hình | Ghi chú |
|---|---|---|---|
| `Schedule Trigger` | `Schedule Trigger` | Thời gian chạy (ví dụ: 0 0 * * *) | Đặt theo tần suất cần cập nhật |
| `RSS Read Domani` | `RSS Read Domani` | URL RSS, Thời gian refresh | Đảm bảo feed trả về XML hợp lệ |
| `Set` (Add RSS link) | `Add RSS link` | Thêm trường `rssLink` | Sử dụng trong nội dung bài viết |
| `OpenAI` | `OpenAI` | Prompt, Model (gpt‑3.5‑turbo) | Tùy chỉnh prompt để tóm tắt hoặc chỉnh sửa nội dung |
| `AI Agent` | `AI Agent` | Định nghĩa các hành động, dữ liệu đầu vào | Sử dụng để xử lý logic phức tạp |
| `Create WordPress Post` | `Create WordPress Post` | WordPress credentials, Post title, Content, Status | Đặt `Status` là `publish` |
| `Edit Image` | `Edit Image` | Đường dẫn ảnh, kích thước, crop | Đảm bảo ảnh phù hợp với WordPress |
| `upload media to wp` | `upload media to wp` | WordPress credentials, Media file | Trả về `mediaId` |
| `upload image to meta data` | `upload image to meta data` | WordPress credentials, `mediaId` | Đặt metadata cho ảnh |
| `set featured image` | `set featured image` | WordPress credentials, `postId`, `mediaId` | Đặt ảnh đại diện |
| `Post on Discord Channel` | `Post on Discord Channel` | Discord credentials, Channel ID, Message | Đưa link bài viết |
| `Post on LinkedIn Profile` & `Post on LinkedN page` | `LinkedIn` | LinkedIn credentials, Content | Đăng bài lên profile và page |
| `Post on telegram Channel` | `telegram` | Telegram credentials, Chat ID, Message | Chia sẻ link |
| `Post on Facebook page` | `facebookGraphApi` | Facebook credentials, Page ID, Message | Đăng bài |
| `Rapiwa (sent whatsapp Notification)` | `Rapiwa` | Rapiwa API Key, Phone Number, Message | Gửi thông báo |
| `Send a Notification1` | `gmail` | Gmail credentials, To, Subject, Body | Email thông báo |
| `Send a Notification` | `discord` | Discord credentials, Channel ID, Message | Thông báo thêm |
| `If (check link)` | `if` | Điều kiện kiểm tra URL đã tồn tại | Tránh đăng bài trùng lặp |
| `Do nothing` | `noOp` | - | Dùng làm placeholder |

> **Lưu ý**: Mỗi node có thể cần **Credentials** riêng. Vào `Credentials` → `Create New` → chọn loại (WordPress, Discord, LinkedIn, …) và điền thông tin.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow thủ công (`Execute Workflow`) với dữ liệu mẫu. Kiểm tra log, đảm bảo không có lỗi.  
2. **Bật Active**: Sau khi test thành công, bật `Active` để workflow tự động chạy theo lịch.  
3. **Giám sát**: Kiểm tra `Execution History` thường xuyên, xem log chi tiết nếu có lỗi.

## ✍️ Mẹo & gợi ý nâng cao

- **Tùy chỉnh nội dung bằng AI**: Thêm node `OpenAI` để tóm tắt, dịch hoặc tạo tiêu đề hấp dẫn trước khi gửi lên WordPress.  
- **Lưu trữ log**: Sử dụng node `HTTP Request` gửi log tới Google Sheets hoặc Airtable để theo dõi lịch sử đăng bài.  
- **Chia sẻ đa kênh đồng thời**: Thêm node `Telegram` hoặc `Discord` mới để gửi tin nhắn tới nhóm khách hàng.  
- **Thông báo định kỳ**: Thêm node `Schedule Trigger` mới để gửi báo cáo hàng ngày qua email.  
- **Quản lý ảnh**: Sử dụng node `Edit Image` để tự động resize, watermark trước khi upload.  

## 📌 Kết luận

Workflow “Publish RSS Articles to WordPress and Social Media Platforms” là giải pháp hoàn hảo cho các doanh nghiệp muốn tiết kiệm thời gian, giảm lỗi và đồng thời tăng phạm vi tiếp cận khách hàng.  
Hãy triển khai ngay, tận dụng sức mạnh của n8n và AI để đưa nội dung của bạn lên mọi nền tảng một cách nhanh chóng và hiệu quả!