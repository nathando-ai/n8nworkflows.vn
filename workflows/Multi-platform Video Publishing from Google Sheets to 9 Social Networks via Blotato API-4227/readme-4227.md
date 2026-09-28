---
title: "🚀 Tự động đăng video lên 9 mạng xã hội từ Google Sheets với Blotato API qua n8n"
description: "Hướng dẫn xây dựng hệ thống tự động hóa xuất bản video và hình ảnh từ Google Sheets lên 9 nền tảng mạng xã hội sử dụng Blotato API và n8n."
slug: "tu-dong-dang-video-9-mang-xa-hoi-google-sheets-blotato"
tags: [n8n, automation, no-code, social-media, marketing, ai]
keywords: [n8n workflow, tự động hóa mạng xã hội, Blotato API, Google Sheets to social media, auto publish video n8n]
---

# 🚀 Tự động đăng video lên 9 mạng xã hội từ Google Sheets với Blotato API

Các sếp làm sáng tạo nội dung hay marketing chắc chắn hiểu cảm giác mệt mỏi thế nào khi phải ngồi thủ công đăng từng chiếc video lên TikTok, Reels, YouTube Shorts, Facebook, LinkedIn, Twitter, Pinterest, Threads và Bluesky. Việc này không chỉ ngốn hàng giờ đồng hồ mỗi ngày mà còn dễ dẫn đến sai sót, quên lịch đăng bài.

Giải pháp là đây! Workflow n8n siêu cấp này sẽ giúp các sếp tự động hóa 100% quy trình: Đọc dữ liệu từ **Google Sheets**, xử lý thông minh qua **OpenAI**, và tự động phân phối video/hình ảnh lên **9 mạng xã hội lớn** thông qua **Blotato API**. Không cần code phức tạp, chỉ cần thiết lập một lần và hệ thống sẽ tự chạy 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh copy-paste, tải lên từng nền tảng thủ công.
- **Đa kênh đồng bộ:** Đăng một phát lên liền 9 mạng xã hội: Instagram, Facebook, LinkedIn, TikTok, Pinterest, YouTube, Threads, Twitter và Bluesky.
- **Tối ưu nội dung thông minh:** Kết hợp OpenAI để tinh chỉnh tiêu đề, caption phù hợp với từng nền tảng.
- **Hoạt động tự động 24/7:** Lên lịch sẵn trên Google Sheets, workflow tự động kích hoạt theo thời gian biểu (Schedule Trigger).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets & Drive:** Bảng tính chứa danh sách video/caption và Google Drive lưu trữ file video.
- **Blotato API Key:** Tài khoản và API key từ nền tảng Blotato để kết nối trung gian đăng bài lên mạng xã hội.
- **OpenAI API Key:** Dùng cho node OpenAI để tối ưu hóa nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này từ nguồn gốc (hoặc tải file JSON), sau đó vào giao diện n8n Editor, chọn **Add workflow** -> Dấu ba chấm (...) -> **Import from File / JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình kỹ các node trọng điểm sau:

- **Schedule Trigger:** Thiết lập mốc thời gian (giờ, ngày trong tuần) để workflow tự động quét Google Sheets và đăng bài.
- **Google Sheets Node:** Kết nối tài khoản Google của các sếp, trỏ đến đúng file Sheet chứa lịch đăng bài, tên bảng (Sheet Name) và cấu trúc cột (Link video, Caption, Trạng thái...).
- **Setup Social Accounts & Get Google Drive ID (Set Nodes):** Cấu hình các biến số chung, ID tài khoản mạng xã hội liên kết trên Blotato, và cách tách lấy file ID từ Google Drive.
- **OpenAI Node:** Điền thông tin OpenAI Credential và tinh chỉnh Prompt (nếu cần) để AI viết/tối ưu caption cho hấp dẫn hơn trước khi gửi sang Blotato.
- **Upload to Blotato & Các node Publish ([Instagram], [Facebook], [Linkedin], [Tiktok], [Pinterest], [Youtube], [Threads], [Twitter], [Bluesky]):** 
  - Cấu hình **HTTP Request** nodes để gọi Blotato API.
  - Điền Blotato API Key vào phần Header Authentication.
  - Kiểm tra Endpoint URL của từng mạng xã hội để đảm bảo video/hình ảnh được bắn đúng đích.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với 1 dòng dữ liệu mẫu trên Google Sheets để kiểm tra log lỗi.
- Nếu mọi thứ xanh mướt (success), các sếp bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước thông báo (Slack / Telegram):** Gắn thêm node Telegram hoặc Slack ở cuối luồng để bot bắn tin nhắn báo cáo về điện thoại ngay khi video được đăng thành công lên các nền tảng.
- **Quản lý trạng thái (Status Logging):** Sau khi publish thành công, viết thêm một lệnh cập nhật ngược lại Google Sheets (đổi cột Trạng thái từ "Chờ đăng" thành "Đã đăng") để tránh việc đăng trùng lặp.
- **Xử lý lỗi (Error Handling):** Sử dụng tính năng Error Trigger của n8n để nhận cảnh báo ngay lập tức qua email nếu API của Blotato hoặc mạng xã hội gặp sự cố.

### 📌 Kết luận
Việc quản lý và phân phối nội dung video đa kênh chưa bao giờ dễ dàng đến thế với sự kết hợp giữa Google Sheets, AI và Blotato API trên n8n. Hãy thiết lập ngay hôm nay để giải phóng sức lao động và bùng nổ traffic cho thương hiệu của các sếp!