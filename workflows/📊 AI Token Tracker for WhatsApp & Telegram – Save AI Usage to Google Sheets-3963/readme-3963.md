---
title: "📊 AI Token Tracker: Theo dõi chi phí AI & Chatbot đa kênh (WhatsApp/Telegram) vào Google Sheets"
description: "Workflow n8n giúp các sếp theo dõi chính xác lượng token AI tiêu thụ, quản lý chi phí LLM và log toàn bộ hội thoại từ WhatsApp & Telegram vào Google Sheets một cách tự động."
slug: "ai-token-tracker-whatsapp-telegram-google-sheets"
tags: [n8n, ai-automation, cost-tracking, whatsapp-bot, telegram-bot, google-sheets]
keywords: [n8n workflow, theo dõi chi phí AI, log chatbot, whatsapp automation, telegram bot, google sheets integration]
---

# 📊 AI Token Tracker: Theo dõi chi phí AI & Chatbot đa kênh (WhatsApp/Telegram) vào Google Sheets

Trong kỷ nguyên AI, việc triển khai các chatbot thông minh là xu hướng tất yếu. Tuy nhiên, nỗi đau lớn nhất của các doanh nghiệp và nhà phát triển không còn là "làm sao để bot hoạt động", mà là **"Chi phí AI đang chạy đi đâu?"** và **"Bot đã trả lời chính xác chưa?"**.

Việc kiểm tra log thủ công trên các nền tảng LLM (như OpenAI, OpenRouter) hoặc kiểm tra từng tin nhắn trên WhatsApp/Telegram là cực kỳ tốn thời gian và dễ bỏ sót. Workflow **AI Token Tracker** do Amanda Benks phát triển chính là giải pháp "chốt hạ" cho vấn đề này. Nó không chỉ là một chatbot, mà là một **hệ thống giám sát tài chính và vận hành (FinOps/Ops)** hoàn chỉnh, tự động ghi lại mọi tương tác, lượng token tiêu thụ và lỗi phát sinh vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý lượng lớn tin nhắn từ WhatsApp/Telegram và gọi API AI, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Kiểm soát chi phí AI tuyệt đối:** Ghi nhận chính xác số token input/output cho mỗi cuộc hội thoại, giúp dự báo và cắt giảm chi phí LLM không cần thiết.
- **Log toàn diện đa kênh:** Hỗ trợ đồng thời **WhatsApp** (qua Evolution API) và **Telegram**, gộp chung dữ liệu vào một bảng Google Sheets duy nhất.
- **Xử lý đa phương tiện:** Tự động chuyển đổi tin nhắn giọng nói (Audio) thành văn bản trước khi đưa vào AI, đảm bảo không bỏ sót dữ liệu.
- **Cơ chế báo lỗi thông minh:** Khi có lỗi xảy ra (API down, lỗi logic), workflow tự động log vào sheet "Errors" và gửi cảnh báo qua Telegram, giúp đội kỹ thuật phản ứng nhanh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi import, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Tài khoản n8n:** Đã cài đặt và chạy (Self-hosted hoặc Cloud).
2. **Google Sheets:** Tạo một Google Sheet mới với 2 tab (Sheet):
   - Tab 1: `Log` (Các cột gợi ý: Timestamp, Channel, User ID, Message, AI Response, Tokens Used, Cost).
   - Tab 2: `Errors` (Các cột gợi ý: Timestamp, Error Message, Context).
3. **Tài khoản AI (LLM):**
   - API Key của **OpenRouter** (hoặc OpenAI) cho node `Chat Model`.
   - API Key của **OpenAI** (nếu dùng riêng cho Audio Transcription).
4. **Kênh liên lạc:**
   - **Telegram:** Tạo Bot qua BotFather, lấy Bot Token.
   - **WhatsApp:** Cài đặt và chạy **Evolution API** (hoặc dùng API khác tương thích) và lấy Webhook URL/Token.
5. **Tùy chọn (Tools):**
   - **Airtable:** Nếu muốn AI tra cứu danh bạ khách hàng.
   - **Gmail:** Nếu muốn AI gửi email.
   - **Google Calendar:** Nếu muốn AI tạo lịch hẹn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/3963` HOẶC
3. Copy toàn bộ JSON của workflow và dán vào n8n (Import from Clipboard).
4. Lưu workflow với tên dễ nhớ, ví dụ: `AI Token Tracker - WhatsApp/Telegram`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này khá phức tạp với 25 nodes, các sếp cần tập trung cấu hình các nhóm node chính sau:

**A. Cấu hình Kênh vào (Triggers & Webhooks)**
- **Node `Telegram` (telegramTrigger):**
  - Chọn Credentials Telegram đã tạo.
  - Đảm bảo Bot đã được thêm vào nhóm hoặc chat cá nhân cần theo dõi.
- **Node `Evolution API` (webhook):**
  - Đây là điểm vào cho WhatsApp. Các sếp cần cấu hình Evolution API để gửi webhook về n8n.
  - Kiểm tra URL webhook trong n8n và copy nó vào cấu hình của Evolution API.
  - *Lưu ý:* Node `Input Source` (switch) sẽ phân loại tin nhắn đến từ Telegram hay WhatsApp dựa trên dữ liệu đầu vào.

**B. Xử lý Dữ liệu & AI**
- **Node `Audio or Text Separation` (if):**
  - Node này kiểm tra xem tin nhắn có chứa file audio không.
  - Nếu có, nó sẽ đi qua `GET Media` -> `Convert to File` -> `Audio Transcription` (dùng OpenAI Whisper) để chuyển giọng nói thành chữ.
  - Các sếp cần điền **OpenAI API Key** vào node `Audio Transcription`.
- **Node `Chat Model` (lmChatOpenRouter):**
  - Đây là "bộ não" chính. Chọn Credentials OpenRouter.
  - Chọn Model phù hợp (ví dụ: `openai/gpt-4o-mini` để tiết kiệm chi phí, hoặc `anthropic/claude-3-sonnet` để chất lượng cao).
  - *Mẹo:* OpenRouter cho phép xem chi phí token rất rõ ràng, rất phù hợp cho workflow này.
- **Node `AI Agent` (agent):**
  - Cấu hình Prompt hệ thống (System Prompt) để định hình cách bot trả lời.
  - Gắn các Tools nếu cần:
    - `Get Contacts` (Airtable): Cần điền Base ID và Table ID.
    - `Send Email` (Gmail): Chọn Credentials Gmail.
    - `Create Event` (Google Calendar): Chọn Credentials Calendar.
  - *Lưu ý:* Nếu không dùng các tool này, các sếp có thể bỏ qua hoặc tắt các nhánh liên quan để giảm độ phức tạp.

**C. Ghi log & Báo cáo (Phần quan trọng nhất)**
- **Node `Log` (googleSheets):**
  - Chọn Credentials Google Sheets.
  - Chọn đúng Sheet ID và Tab `Log`.
  - Kiểm tra ánh xạ cột (Mapping) để đảm bảo các trường như `Tokens Used`, `Cost`, `Message` được ghi đúng vị trí.
  - *Mẹo:* Workflow có các node `Clean Up` và `Clean_Up` (code) để định dạng lại dữ liệu trước khi ghi vào Sheet. Các sếp nên giữ nguyên logic này để dữ liệu sạch sẽ.
- **Node `Errors` (googleSheets):**
  - Chọn Tab `Errors`.
  - Đảm bảo khi có lỗi, thông tin lỗi được ghi lại đầy đủ để debug.

**D. Phản hồi người dùng**
- **Node `Response` (telegram):** Gửi tin nhắn trả lời cho user Telegram.
- **Node `WhatsApp` (httpRequest):** Gửi tin nhắn trả lời qua Evolution API.
- **Node `Error Response` (telegram):** Gửi thông báo lỗi cho user (tùy chọn, có thể tắt nếu không muốn user thấy lỗi kỹ thuật).

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Gửi một tin nhắn text đơn giản từ Telegram.
   - Gửi một tin nhắn voice từ WhatsApp.
   - Kiểm tra xem dữ liệu có xuất hiện trong Google Sheets (tab Log) không.
   - Kiểm tra xem cột `Tokens Used` có giá trị không.
2. **Bật Active:**
   - Sau khi test thành công, bật nút **Active** trên workflow.
   - Workflow sẽ bắt đầu chạy nền 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa Báo cáo Chi phí:** Thêm một workflow n8n khác chạy hàng ngày (Cron) để đọc sheet `Log`, tính tổng chi phí AI trong ngày và gửi báo cáo qua Email hoặc Telegram cho sếp.
- **Phân loại theo Khách hàng:** Nếu dùng Airtable, hãy thêm trường `Customer Tier` (VIP, Thường). Workflow có thể ưu tiên dùng Model AI đắt tiền hơn cho khách VIP và Model rẻ hơn cho khách thường để tối ưu chi phí.
- **Cảnh báo Ngưỡng Chi phí:** Thêm một node `If` sau khi ghi log. Nếu tổng chi phí trong ngày vượt quá mức cho phép (ví dụ: 10 USD), hãy gửi cảnh báo khẩn cấp cho đội kỹ thuật.
- **Lưu trữ Lâu dài:** Google Sheets có giới hạn dung lượng. Sau 3-6 tháng, hãy thêm node để xuất dữ liệu cũ sang BigQuery hoặc database khác để giữ sheet nhẹ và nhanh.

### 📌 Kết luận
Workflow **AI Token Tracker** không chỉ là một công cụ chatbot, mà là một **hệ thống quản trị chi phí AI (FinOps)** thực chiến. Với khả năng tích hợp đa kênh (WhatsApp/Telegram), xử lý đa phương tiện (Audio/Text) và ghi log chi tiết vào Google Sheets, đây là giải pháp hoàn hảo cho các doanh nghiệp muốn kiểm soát chặt chẽ ngân sách AI và đảm bảo chất lượng dịch vụ chatbot.

Các sếp hãy import ngay, cấu hình credentials và bắt đầu theo dõi từng đồng chi phí AI của mình! 🚀