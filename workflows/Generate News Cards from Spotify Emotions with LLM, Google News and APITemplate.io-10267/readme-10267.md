---
title: "🚀 Tự động hóa tạo Thẻ Tin Tức từ Cảm Xúc Nhạc Spotify với AI, Google News & APITemplate.io"
description: "Biến gu âm nhạc thành bản tin trực quan! Workflow n8n tự động đọc bài hát gần đây trên Spotify, dùng AI phân tích cảm xúc, quét Google News, tạo ảnh thẻ tin tức bằng APITemplate.io và đăng lên Slack."
slug: "tao-the-tin-tuc-tu-cam-xuc-spotify-n8n"
tags: [n8n, automation, ai-summarization, spotify, slack, apitemplate]
keywords: [n8n workflow, spotify automation, AI phân tích cảm xúc, APITemplate, slack integration, tự động hóa tin tức]
use_relative_path: true
---

# 🚀 Biến Cảm Xúc Nghe Nhạc Trên Spotify Thành Thẻ Tin Tức Tự Động Gửi Lên Slack

Các sếp có bao giờ tự hỏi tâm trạng nghe nhạc của mình hôm nay sẽ khớp với những tin tức gì trên thế giới chưa? Thay vì tốn thời gian thủ công tìm kiếm tin tức hay tạo hình ảnh chia sẻ, workflow này sẽ lo từ A-Z: phân tích cảm xúc bài hát gần đây trên Spotify bằng AI (OpenRouter), quét các bản tin nóng trên Google News phù hợp với tâm trạng đó, tự động thiết kế ảnh thẻ tin tức (News Card) cực kỳ chuyên nghiệp qua APITemplate.io và gửi ngay vào kênh Slack của team.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) do workflow có sử dụng các node LangChain/AI agent.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cá nhân hóa độc đáo:** Biến lịch sử nghe nhạc cá nhân thành nguồn cảm hứng để cập nhật tin tức hàng ngày.
- **Tự động hóa 100%:** Từ việc đọc nhạc, phân tích cảm xúc, kéo RSS tin tức đến thiết kế hình ảnh và gửi thông báo.
- **Tương tác nhóm đỉnh cao:** Cung cấp nội dung trực quan, sinh động ngay trên Slack giúp team cùng giải trí và nắm bắt thông tin.
- **Hoạt động liên tục:** Chạy tự động theo lịch trình (Cron) thiết lập sẵn mà không cần con người nhúng tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản Spotify** (để lấy OAuth2 credentials truy cập lịch sử nghe nhạc).
- **Tài khoản OpenRouter** (lấy API Key cho LLM phân tích cảm xúc).
- **Tài khoản APITemplate.io** (lấy API Key và Template ID để tạo hình ảnh).
- **Workspace Slack** (để tạo OAuth2 kết nối bot đăng bài lên kênh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình (hoặc import file JSON tải từ nguồn gốc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống không báo lỗi, các sếp nhớ cấu hình kỹ các node trọng điểm sau:
- **Fetch Spotify Recently Played**: Chọn kết nối **Spotify OAuth2** credentials do các sếp tự tạo trong phần Settings của n8n để cho phép workflow đọc lịch sử bài hát.
- **LLM: Infer Emotion from Track**: Gán **OpenRouter API** credentials cho node model chat và cấu hình prompt để AI trả về đúng định dạng cảm xúc mong muốn.
- **Build Google News RSS Query**: Node kiểu **Set** này chuyển đổi từ khóa cảm xúc thành query RSS của Google News. Các sếp có thể tùy chỉnh ngôn ngữ/quốc gia (ví dụ: đổi `hl=en-US` thành `hl=vi-VN` nếu muốn tìm tin tức tiếng Việt).
- **Generate News Card (APITemplate)**: Kết nối với **APITemplate.io** credentials và nhớ thay thế ID template mặc định bằng **Template ID** riêng của các sếp đã tạo trên trang APITemplate.io.
- **Post to Slack (Title + Link + Card URL)**: Chọn kết nối **Slack OAuth2** credentials và chọn channel muốn bot đăng tin.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử công đoạn thủ công với node **Start on Schedule (Cron)** để kiểm tra dữ liệu trả về qua từng bước.
- Sau khi thấy kết quả hiển thị ngon lành trên Slack, các sếp gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi Slack, các sếp có thể nối thêm node Telegram hoặc Discord để chia sẻ "tâm trạng tin tức" đa nền tảng.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable ngay sau bước lấy tin tức để lưu lại lịch sử bài hát và bản tin tương ứng phục vụ phân tích xu hướng cá nhân.
- **Tùy chỉnh Template hình ảnh:** Thiết kế các mẫu thẻ tin tức (News Card) thật bắt mắt trên APITemplate.io với màu sắc thay đổi theo từng loại cảm xúc (ví dụ: Vui = Màu vàng sáng, Buồn = Màu xanh trầm).

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc kết hợp AI, dữ liệu thời gian thực và tự động hóa No-code để tạo ra những sản phẩm sáng tạo mang đậm dấu ấn cá nhân. Hãy cài đặt ngay hôm nay để làm cho kênh Slack của team thêm phần sinh động và thú vị các sếp nhé!