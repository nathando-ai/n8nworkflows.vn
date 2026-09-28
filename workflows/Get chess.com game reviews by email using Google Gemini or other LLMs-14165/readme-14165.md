---
title: "🚀 Tự động nhận bản phân tích cờ vua từ Chess.com qua email bằng AI Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy ván đấu mới nhất trên Chess.com, phân tích bằng Google Gemini và gửi báo cáo chi tiết qua Gmail mỗi ngày."
slug: "tu-dong-nhan-phan-tich-co-vua-chess-com-qua-email-ai-gemini"
tags: [n8n, automation, chess, ai, google-gemini, gmail, productivity]
keywords: [n8n workflow, chess.com automation, google gemini ai, tu dong phan tich co vua, n8n ai coach]
---

# 🚀 Tự động nhận bản phân tích cờ vua từ Chess.com qua email bằng AI Gemini

Các sếp có đang chơi cờ vua trên Chess.com và muốn cải thiện trình độ nhưng lại lười phân tích lại từng ván đấu (game review)? Việc mở từng ván cờ, xem lại nước đi và tự tìm điểm mù tốn rất nhiều thời gian, chưa kể chúng ta thường hay "quên lối về" sau những ván thua đậm. 

Đừng lo, workflow n8n cực xịn xò này do **Ucartz Online** phát triển sẽ tự động hóa 100% quy trình: lấy ván đấu mới nhất của các sếp trên Chess.com, đưa cho AI (Google Gemini) mổ xẻ, chấm điểm, chỉ ra nước đi sai lầm và gửi ngay một bản báo cáo huấn luyện (coaching report) cực kỳ chi tiết qua email mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần mất công phân tích thủ công sau mỗi trận đấu.
- **AI Huấn luyện viên riêng:** Google Gemini sẽ chỉ ra chính xác các khoảnh khắc quyết định (critical moments), sai lầm và bài học kinh nghiệm.
- **Báo cáo trực quan qua Email:** Nhận ngay báo cáo định dạng HTML đẹp mắt, rõ ràng với quân cờ, kết quả, khai cuộc và lời khuyên hữu ích.
- **Hoạt động tự động:** Chạy ngầm mỗi ngày nhờ lịch trình (Schedule Trigger) hoặc test thủ công bất cứ lúc nào các sếp muốn.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Chess.com:** Chỉ cần nhớ Username (không cần API Key vì Chess.com dùng API công khai).
- **Google Gemini API Key:** Để kết nối với node LLM (hoặc có thể thay thế bằng OpenAI, Claude...).
- **Gmail Account:** Cấp quyền cho n8n qua OAuth2 để gửi email báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow và dán trực tiếp vào giao diện n8n Editor (hoặc import file JSON tải từ nguồn gốc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Trong workflow có 11 nodes, các sếp chú ý cấu hình kỹ các điểm sau:
- **`Config - Username - Email` (Node Set):** Mở node này và điền chính xác:
  - `username`: Tên tài khoản Chess.com của các sếp (không phân biệt chữ hoa/thường).
  - `email`: Địa chỉ nhận báo cáo phân tích.
- **`LLM — Google Gemini` (Node lmChatGoogleGemini):** Kết nối credentials `googlePalmApi` với API key của Google Gemini. (Các sếp hoàn toàn có thể đổi sang node OpenAI GPT-4o hoặc Claude nếu muốn phân tích sâu hơn choElo cao).
- **`Email the Report` (Node Gmail):** Kết nối tài khoản Gmail cá nhân thông qua OAuth2 để n8n có quyền gửi email thay cho các sếp.

#### 3. Kích hoạt ⚡️
- Bấm nút **▶️ Manual Test Run** để chạy thử nghiệm xem email có về hòm thư hay không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để node `⏰ Daily Schedule Trigger` tự động làm việc mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Gmail, các sếp có thể nối thêm node **Telegram** hoặc **Slack** ngay sau bước AI để nhận thông báo nhanh trên điện thoại.
- **Lưu trữ dữ liệu:** Thêm node **Notion** hoặc **Google Sheets** để lưu lại lịch sử các ván đấu và lời khuyên của AI nhằm theo dõi tiến trình thăng hạng Elo.
- **Đổi AI thông minh hơn:** Nếu các sếp đạt Elo trên 1000+, hãy thử đổi sang OpenAI GPT-4o hoặc Claude 3.5 Sonnet để nhận các nhận xét sắc bén và chiến thuật sâu sắc hơn.

### 📌 Kết luận
Một workflow cực kỳ thú vị và thiết thực cho những ai đam mê cờ vua và muốn nâng cao kỹ năng qua từng ngày. Hãy "lên đồ" ngay trên n8n để có một HLV AI riêng miễn phí nhé các sếp!