---
title: "🚀 Xây dựng Chatbot AI Phân tích Tài chính tự động với Gemini 2.5 Flash và Discord trong n8n"
description: "Tự động hóa hoàn toàn quy trình phân tích tài chính mã cổ phiếu, tổng hợp báo cáo chuyên sâu bằng Google Gemini và gửi trực tiếp về kênh Discord."
slug: "chatbot-ai-phan-tich-tai-chinh-gemini-discord-n8n"
tags: [n8n, ai-chatbot, gemini, discord, automation, finance]
keywords: [n8n workflow, phân tích tài chính tự động, ai chatbot gemini, discord webhook, n8n langchain agent]
---

# 🚀 Xây dựng Chatbot AI Phân tích Tài chính tự động với Gemini 2.5 Flash và Discord

Các sếp trong lĩnh vực tài chính, đầu tư hay kinh doanh chắc hẳn thường xuyên phải đối mặt với việc tốn hàng giờ đồng hồ để tra cứu mã cổ phiếu, phân tích các chỉ số, đọc báo cáo và tổng hợp thông tin gửi cho đội ngũ hoặc khách hàng. Việc làm thủ công này không chỉ chậm trễ mà còn dễ bỏ lỡ các biến động thị trường.

Bài viết này sẽ hướng dẫn các sếp triển khai một **AI Agent tự động phân tích tài chính** cực kỳ thông minh bằng n8n. Workflow này kết hợp sức mạnh của **Google Gemini** để phân tích dữ liệu chuyên sâu và **Discord Webhook** để bắn báo cáo trực tiếp về nhóm chat ngay khi có yêu cầu!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Nhận câu hỏi qua giao diện chat trực quan hoặc trigger, Agent tự động phân tích mã cổ phiếu (Ticker), khung thời gian (Timeframe) và rủi ro.
- **Báo cáo chuẩn chỉnh**: Sử dụng Structured Output Parser để ép Gemini trả về kết quả theo cấu trúc rõ ràng (Luận điểm đầu tư, Tóm tắt, Động lực tăng trưởng, Rủi ro, Chỉ số, Bước tiếp theo).
- **Cập nhật tức thì**: Gửi báo cáo đẹp mắt, định dạng chuẩn Markdown thẳng vào kênh Discord của đội ngũ.
- **Duy trì ngữ cảnh**: Tích hợp Bộ nhớ trò chuyện (Conversation Memory) giúp các cuộc hội thoại tra cứu liên tục có chiều sâu và mạch lạc hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google AI (Gemini) API Key**: Lấy từ Google AI Studio để kết nối mô hình Gemini.
- **Discord Webhook**: Một kênh Discord đã tạo sẵn Webhook để nhận tin nhắn báo cáo từ bot.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ nguồn.
- Mở n8n Editor, chọn **New Workflow** -> Bấm vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây trong workflow:

- **Node `Connect Gemini`**: 
  - Chọn Credential loại `Google Palm API` (hoặc Gemini API).
  - Tạo mới credential, dán **API Key** lấy từ [Google AI Studio](https://aistudio.google.com/app/apikey) và bấm Save.
  - Chọn model phù hợp (ví dụ: `gemini-1.5-pro` cho độ chính xác cao hoặc `gemini-1.5-flash` / `gemini-2.5-flash` cho tốc độ xử lý nhanh).

- **Node `Discord`**: 
  - Chọn Credential loại `Discord Webhook API`.
  - Lấy Webhook URL từ kênh Discord (vào *Server Settings > Integrations > Webhooks*), dán vào trường Webhook URL trong n8n.

- **Node `agent1` (AI Agent)**: 
  - Mở node này để tinh chỉnh **System Message**. Các sếp có thể thay đổi vai trò (ví dụ: Chuyên gia phân tích tài chính phố Wall), điều chỉnh giọng văn, mức độ rủi ro hoặc yêu cầu trả về các phần Markdown cụ thể.

- **Node `Structured Output Parser`**: 
  - Đảm bảo cấu trúc JSON schema được thiết lập khớp với yêu cầu (mặc định bao gồm `idea` cho luận điểm một dòng và `analysis` cho các phần nội dung chi tiết).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** ở node `Example Chat` hoặc `Chat Trigger` để chạy thử với dữ liệu mẫu (ví dụ: ticker: AAPL, timeframe: 6M).
- Kiểm tra kết quả trả về trên kênh Discord xem định dạng đã đẹp mắt chưa.
- Gạt công tắc sang **Active** để đưa workflow vào trạng thái hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp dữ liệu thời gian thực**: Thêm node `HTTP Request` trước node Agent để gọi API lấy giá cổ phiếu, báo cáo tài chính mới nhất từ các bên thứ ba (như Yahoo Finance, Alpha Vantage) làm phong phú thêm ngữ cảnh cho Gemini.
- **Đa kênh thông báo**: Ngoài Discord, các sếp có thể nhân bản nhánh cuối để bắn đồng thời tin nhắn qua Telegram Bot hoặc lưu trữ dữ liệu vào Google Sheets để làm lịch sử theo dõi.
- **Lập lịch tự động (Cron)**: Thay thế hoặc kết hợp Chat Trigger bằng node Schedule (Cron) để bot tự động chạy phân tích các mã cổ phiếu yêu thích vào mỗi buổi sáng trước giờ thị trường mở cửa.

### 📌 Kết luận
Với workflow n8n này, việc xây dựng một trợ lý AI phân tích tài chính chưa bao giờ dễ dàng đến thế. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc, tiết kiệm thời gian nghiên cứu và mang lại những thông tin đầu tư kịp thời nhất cho đội ngũ của các sếp!