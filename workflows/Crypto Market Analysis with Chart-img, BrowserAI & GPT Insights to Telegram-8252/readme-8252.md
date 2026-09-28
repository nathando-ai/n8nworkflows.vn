---
title: "🚀 Tự động phân tích thị trường Crypto với AI, Chart-img & Gửi báo cáo Telegram"
description: "Xây dựng hệ thống tự động lấy biểu đồ giá, cào dữ liệu tin tức qua BrowserAI, phân tích đa phương thức bằng AI và gửi báo cáo thị trường crypto lên Telegram."
slug: "tu-dong-phan-tich-thi- trường-crypto-ai-telegram"
tags: [n8n, automation, crypto, ai, telegram, browser-ai]
keywords: [n8n workflow, tự động hóa crypto, phân tích biểu đồ ai, browser ai, chart img, telegram bot]
---

# 🚀 Tự động phân tích thị trường Crypto với AI, Chart-img & Gửi báo cáo Telegram

Các sếp đang đầu tư hoặc theo dõi thị trường crypto chắc chắn hiểu cảm giác mệt mỏi khi phải liên tục mở biểu đồ, đọc tin tức tổng hợp từ nhiều nguồn, rồi tự phỏng đoán xu hướng mỗi ngày. Việc làm thủ công này ngốn rất nhiều thời gian và dễ bỏ lỡ cơ hội.

Giải pháp ở đây là gì? Biến n8n thành một "trợ lý phân tích tài chính" tự động 100%. Workflow này sẽ tự động chụp biểu đồ giá (BTC, ETH, SOL, XRP), cào thông tin tin tức mới nhất, nhờ AI phân tích đa phương thức (Multimodal AI) và gửi bản tin tổng hợp trực tiếp vào Telegram của các sếp vào 8h sáng và 8h tối mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ 2 lần/ngày (8h sáng và 8h tối) mà không cần can thiệp thủ công.
- **Phân tích đa nguồn:** Kết hợp hình ảnh biểu đồ giá thực tế từ [Chart-img](https://chart-img.com/) và dữ liệu web scraping thông minh từ [BrowserAI](https://browser.ai/).
- **AI thông minh:** Sử dụng OpenRouter (GPT/Claude) để đọc hiểu biểu đồ, phân tích xu hướng và tóm tắt ngắn gọn.
- **Báo cáo nhanh chóng:** Nhận thông tin phân tích trực tiếp qua Telegram ngay khi AI hoàn thành nhiệm vụ.
:::

### 🚀 Cảnh báo quan trọng
> **LƯU Ý:** Template này chỉ phục vụ mục đích tham khảo và cá nhân, **không phải là lời khuyên tài chính (financial advice)**. Mọi quyết định đầu tư đều thuộc trách nhiệm của các sếp!

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Chart-img API Key:** Đăng ký tài khoản miễn phí tại [Chart-img](https://chart-img.com/) để lấy API key chụp biểu đồ.
- **BrowserAI API Key:** Đăng ký tài khoản tại [BrowserAI](https://browser.ai/) để cào dữ liệu tin tức crypto.
- **OpenRouter API Key:** Để kết nối các mô hình AI ngôn ngữ và thị giác thông qua OpenRouter.
- **Telegram Bot Token & Chat ID:** Tạo bot qua `@BotFather` và lấy Chat ID để nhận tin nhắn.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn gốc hoặc copy toàn bộ JSON.
- Trong giao diện n8n, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 27 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các phần sau:

- **Lịch chạy (Schedule Trigger):** Node `Schedule Trigger` đang được cấu hình chạy định kỳ. Các sếp có thể điều chỉnh lại múi giờ hoặc tần suất theo ý muốn.
- **Lấy biểu đồ giá (HTTP Request nodes):** 
  - Các node `BTCUSD chart`, `ETHUSD chart`, `SOLUSD chart`, `XRPUSD chart` sử dụng API của Chart-img.
  - Cần cấu hình **Credentials** loại `httpBearerAuth` bằng cách điền Chart-img API Key của các sếp.
- **Xử lý hình ảnh (Code nodes):** 
  - Các node `... image converter` làm nhiệm vụ chuyển đổi ảnh biểu đồ sang định dạng base64 để AI có thể đọc trực tiếp.
- **Cào dữ liệu web (BrowserAI nodes):**
  - Node `Create BrowserAI task`, `Get task results`, `Check if finalized`, `Wait if not finished`: Cần điền API key của BrowserAI. Node này sẽ tạo nhiệm vụ cào dữ liệu, kiểm tra trạng thái (nếu chưa xong sẽ đợi - `Wait if not finished`) và lấy kết quả về.
- **AI Phân tích (LangChain Agents & OpenRouter):**
  - Các node `AI graph analyzer`, `AI crypto summarizer` kết nối với `OpenRouter Chat Model...`.
  - Các sếp cần cấu hình **Credentials** loại `openRouterApi` và chọn model phù hợp (ví dụ: `anthropic/claude-3.5-sonnet` hoặc `openai/gpt-4o`) có hỗ trợ đọc hình ảnh (Vision).
- **Gửi tin nhắn (Telegram node):**
  - Node `Send a text message`: Cần cấu hình **Credentials** `telegramApi` với Bot Token và điền chính xác `Chat ID` của các sếp để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thủ công toàn bộ luồng xem biểu đồ có được chụp, AI có phân tích và Telegram có nhận được tin nhắn hay không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để bật workflow chạy tự động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh nhận tin:** Ngoài Telegram, các sếp có thể nối thêm node WhatsApp, Slack hoặc gửi email tóm tắt báo cáo vào mỗi buổi sáng.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets ở cuối luồng để lưu lại các nhận định của AI theo từng ngày, tiện cho việc theo dõi lịch sử dự đoán của AI.
- **Mở rộng danh mục coin:** Dễ dàng nhân bản các HTTP Request node của Chart-img để theo dõi thêm các đồng coin tiềm năng khác (như ADA, AVAX, NEAR...).

---

### 📌 Kết luận
Với workflow này, các sếp đã sở hữu ngay một hệ thống phân tích thị trường crypto tự động bằng AI cực kỳ chuyên nghiệp mà không tốn một xu chi phí dịch vụ đắt đỏ nào. Chúc các sếp cấu hình thành công và giao dịch hiệu quả!