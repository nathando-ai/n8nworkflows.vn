---
title: "🚀 Tạo Playlist Spotify Tự Động từ Telegram bằng AI Agent & OpenRouter"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo playlist Spotify thông qua Telegram bot với sự trợ giúp của AI Agent và OpenRouter, xử lý đầy đủ định mức API."
slug: "tao-playlist-spotify-tu-dong-tu-telegram-openrouter-n8n"
tags: [n8n, automation, no-code, spotify, telegram, ai-agent, openrouter]
keywords: [n8n workflow, tao spotify playlist tu dong, telegram bot ai, openrouter gpt, tich hop spotify n8n]
---

# 🚀 Tạo Playlist Spotify Tự Động từ Telegram bằng AI Agent & OpenRouter

Các sếp có bao giờ cảm thấy mất thời gian khi phải ngồi tìm từng bài hát để thêm vào playlist trên Spotify mỗi khi có cảm hứng nghe một dòng nhạc mới? Việc tạo thủ công hàng chục bài hát vừa tẻ nhạt, vừa tốn thời gian. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó! Chỉ với một tin nhắn cực kỳ đơn giản qua **Telegram**, AI Agent sẽ đóng vai một DJ chuyên nghiệp, lên danh sách từ 30-50 bài hát phù hợp nhất, tự động tạo playlist mới trên tài khoản Spotify của các sếp và thêm toàn bộ các bài hát đó vào mà không cần chạm tay vào bất kỳ thao tác thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Chỉ cần gửi yêu cầu qua chat Telegram (VD: *"Create a chill house playlist"*), nhận ngay link playlist hoàn chỉnh sau chưa đầy 60 giây.
- **AI Curated thông minh**: AI đóng vai trò DJ chuyên nghiệp, đề xuất danh sách 30-50 bài hát chuẩn xác theo đúng gu âm nhạc yêu cầu.
- **Tuân thủ Rate Limit**: Workflow được thiết kế thông minh với độ trễ (delay) hợp lý giữa các lần gọi API, tránh việc bị Spotify chặn do gửi request quá nhanh.
- **Trải nghiệm mượt mà**: Gửi thông báo trạng thái "đang xử lý" ngay khi nhận yêu cầu và gửi trả link playlist trực tiếp vào Telegram cho người dùng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua `@BotFather`).
- **Tài khoản Spotify** (Cần tài khoản Developer hoặc kết nối qua OAuth2 của n8n để quản lý playlist).
- **OpenRouter API Key** (Sử dụng các mô hình ngôn ngữ lớn như OpenAI GPT để gợi ý bài hát).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow hoặc import trực tiếp file JSON vào giao diện n8n Editor để hiển thị toàn bộ 12 nodes bao gồm: *Telegram Trigger, AI Agent, OpenRouter Chat Model, Structured Output Parser, Split Out Array, Loop Over Items, Search tracks by keyword, Create a playlist, Add an Item to a playlist, Send a text message, If, Wait 1 Sec*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Telegram Trigger & Send a text message**: Kết nối tài khoản Telegram thông qua `telegramApi` credentials bằng cách nhập Bot Token từ BotFather.
- **OpenRouter Chat Model**: Chọn credentials `openRouterApi` và cấu hình model (ví dụ mặc định sử dụng `openai/gpt-5-nano` hoặc các model mạnh mẽ khác tuỳ ý các sếp).
- **AI Agent & Structured Output Parser**: Đảm bảo cấu hình prompt cho AI hiểu rõ cách phân rã danh sách bài hát theo cấu trúc đầu ra mong muốn để các node phía sau dễ dàng xử lý.
- **Search tracks by keyword, Create a playlist, Add an Item to a playlist**: Kết nối tài khoản Spotify của các sếp bằng `spotifyOAuth2Api` để cấp quyền tạo playlist và thêm bài hát.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step / Execute Workflow** để gửi một tin nhắn thử nghiệm qua Telegram bot.
- Kiểm tra xem playlist có được tạo thành công trên tài khoản Spotify hay không.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow sẵn sàng hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo**: Thêm node Slack hoặc Discord để thông báo cho team mỗi khi có một playlist mới được tạo trên hệ thống.
- **Lưu trữ lịch sử**: Kết nối thêm node Google Sheets để lưu lại các yêu cầu playlist của người dùng nhằm phân tích xu hướng âm nhạc.
- **Tuỳ biến thể loại**: Tinh chỉnh system prompt trong AI Agent để giới hạn các thể loại âm nhạc độc quyền hoặc thêm các thẻ hashtag tuỳ chỉnh.

### 📌 Kết luận
Với workflow tự động hóa này, việc tạo và quản lý playlist Spotify chưa bao giờ dễ dàng đến thế. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tối ưu hóa thời gian và trải nghiệm những công nghệ AI tiên tiến nhất!