---
title: "🚀 Tạo video tự động từ ảnh với Telegram, GPT-4.1 và Seedance-Veo3 trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình biến hình ảnh thành video ngắn qua Telegram bot, kết hợp AI Agent, Google Drive, Google Sheets và Wavespeed API."
slug: "tao-video-tu-dong-tu-anh-telegram-gpt4-seedance-veo3-n8n"
tags: [n8n, automation, ai-agent, telegram, video-generation, openai]
keywords: [n8n workflow, tạo video từ ảnh, telegram bot n8n, seedance veo3 api, ai agent n8n, tự động hóa marketing]
---

# 🚀 Tạo video tự động từ ảnh với Telegram, GPT-4.1 và Seedance-Veo3

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công nhận hình ảnh từ khách hàng hoặc đội ngũ, viết prompt, sau đó đem lên các công cụ tạo video AI, chờ đợi rồi tải về gửi lại không? Quá trình này ngốn rất nhiều thời gian và làm giảm năng suất làm việc.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ do **Automate With Marc** phát triển. Workflow này sẽ tự động hóa 100% quy trình: Nhận ảnh từ Telegram $\rightarrow$ Xử lý bằng AI Agent $\rightarrow$ Gọi Wavespeed API (Seedance/Veo3) để tạo video $\rightarrow$ Trả kết quả trực tiếp về Telegram cho người dùng. Không cần code phức tạp, chỉ cần "lên đồ" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến ảnh tĩnh thành video ngắn (Reels, TikTok) chỉ bằng một tin nhắn qua Telegram Bot.
- **Tối ưu hóa Prompt thông minh:** Sử dụng AI Agent kết hợp GPT-4.1-mini để tự động viết video prompt chuẩn hóa từ hình ảnh và chú thích của người dùng.
- **Lưu trữ khoa học:** Tự động lưu ảnh vào Google Drive và ghi log chi tiết vào Google Sheets để dễ dàng tra cứu.
- **Trải nghiệm liền mạch:** Người dùng chỉ cần gửi ảnh, hệ thống tự xử lý ngầm và gửi lại video hoàn thiện qua khung chat Telegram.
:::

### 📦 Các bước hoạt động chi tiết của Workflow
1. **Telegram Bot Trigger:** Lắng nghe hình ảnh và caption mới gửi đến từ người dùng.
2. **Conditional Logic (If node):** Lọc bỏ các đầu vào không hợp lệ.
3. **AI Agent (LangChain + OpenAI):** Xử lý hình ảnh và tạo ra prompt tương thích cho mô hình Seedance/Veo3.
4. **Google Drive & Google Sheets:** Tự động upload ảnh, lấy share link và ghi lại dữ liệu tương tác.
5. **Wavespeed API (Seedance/Veo3):** Gửi yêu cầu tạo video (Image-to-Video).
6. **Polling & Telegram Output:** Chờ xử lý xong (có node Wait) và trả file video trực tiếp về Telegram cho người dùng.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- **Telegram Bot Token** (tạo qua BotFather).
- **OpenAI API Key** (cho GPT-4.1-mini).
- Tài khoản **Google Drive** và **Google Sheets** (để lưu trữ file và log dữ liệu).
- Tài khoản và **API Key từ Wavespeed** (hoặc nền tảng cung cấp Seedance/Veo3 API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node sau trước khi kích hoạt:
- **Telegram Trigger & Telegram / Telegram2:** Kết nối tài khoản Telegram Bot Credentials của các sếp. Đảm bảo bot có quyền nhận tin nhắn và gửi file video.
- **OpenAI Chat Model:** Cấu hình OpenAI API Key và chọn model `gpt-4.1-mini`.
- **Google Drive & Google Sheets / Google Sheets1:** 
  - Kết nối Google OAuth2 credentials.
  - Thay thế **Google Drive Folder ID** nơi lưu trữ ảnh tải lên từ Telegram.
  - Thay thế **Google Document ID** của file Google Sheets dùng để log dữ liệu.
- **Wavespeed Post & Wavespeed Get (HTTP Request nodes):** 
  - Cấu hình API Key của Wavespeed vào phần Header/Authorization.
  - Kiểm tra lại endpoint gọi API tạo video (ví dụ: `/bytedance/seedance-v1-pro-i2v-480p`).
- **Wait 15 / Wait another 15 Seconds:** Điều chỉnh thời gian chờ phù hợp với tốc độ render video thực tế của API bên thứ ba.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một ảnh và caption bất kỳ trên Telegram để kiểm tra luồng dữ liệu qua từng node.
- Nếu không có lỗi xuất hiện, bật công tắc **Active workflow** để đưa hệ thống vào trạng thái hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram Notification:** Thêm một node thông báo về kênh nội bộ của team mỗi khi có khách hàng/user tạo video thành công.
- **Quản lý giới hạn (Rate Limit):** Thêm bước kiểm tra số lượng request trong Google Sheets để giới hạn số lần tạo video miễn phí cho mỗi user trên Telegram.
- **Lưu trữ video đầu ra:** Mở rộng workflow để tự động lưu video xuất ra từ Wavespeed vào một thư mục riêng trên Google Drive thay vì chỉ trả về Telegram.

### 📌 Kết luận
Workflow tích hợp Telegram, GPT-4.1 và Seedance-Veo3 là một giải pháp tuyệt vời để tự động hóa sản xuất nội dung hình ảnh sang video ngắn. Hãy triển khai ngay hôm nay trên hạ tầng n8n của các sếp để tối ưu hóa hiệu suất công việc và mang lại trải nghiệm tuyệt vời cho người dùng!