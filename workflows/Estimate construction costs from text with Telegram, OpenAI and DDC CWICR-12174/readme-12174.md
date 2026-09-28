---
title: "🚀 Tự động ước tính chi phí xây dựng từ văn bản với Telegram, OpenAI và DDC CWICR trên n8n"
description: "Hướng dẫn xây dựng trợ lý AI trên Telegram tự động phân tích hạng mục, tìm kiếm dữ liệu chi phí xây dựng từ kho dữ liệu mở DDC CWICR và xuất báo cáo PDF/Excel."
slug: "uoc-tinh-chi-phi-xay-dung-telegram-openai-ddc-cwicr"
tags: [n8n, automation, ai-agent, telegram, openai, qdrant, construction]
keywords: [n8n workflow, ước tính chi phí xây dựng, DDC CWICR, Telegram bot AI, Qdrant vector search, tự động hóa xây dựng]
---

# 🚀 Tự động ước tính chi phí xây dựng từ văn bản với Telegram, OpenAI và DDC CWICR

Các sếp làm trong ngành xây dựng, thầu khoán hay dự toán chắc hẳn đều ngán ngẩm cảnh phải ngồi tra cứu hàng ngàn định mức, đơn giá thủ công từ các tập tài liệu dày cộp mỗi khi bóc tách khối lượng công trình. Việc này vừa tốn thời gian, dễ sai sót, lại khó cá nhân hóa theo từng yêu cầu thay đổi liên tục của khách hàng.

Giải pháp đây rồi! Workflow khủng với **70 nodes** trên n8n này sẽ biến Telegram thành một **Trợ lý AI ước tính chi phí xây dựng thông minh**. Chỉ cần gõ mô tả công việc bằng ngôn ngữ tự nhiên (hỗ trợ tới 9 ngôn ngữ), hệ thống sẽ tự động bóc tách hạng mục, tìm kiếm thông minh trong cơ sở dữ liệu hơn 55,000 định mức của **DDC CWICR** thông qua Vector Search (Qdrant), tính toán chi tiết và xuất ngay báo cáo dạng HTML, Excel hoặc PDF cho các sếp ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow quy mô lớn với các tác vụ AI và Vector Search chạy ổn định 24/7 không lo quá tải, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến chat Telegram thành công cụ bóc tách khối lượng và lập dự toán chuyên nghiệp.
- **Tốc độ chớp nhoáng:** Tra cứu hàng chục ngàn mã định mức trong tích tắc nhờ công nghệ Vector Search (Qdrant) kết hợp AI Rerank.
- **Đa ngôn ngữ & Tiền tệ:** Hỗ trợ 9 ngôn ngữ (DE, EN, RU, ES, FR, PT, ZH, AR, HI) và linh hoạt chuyển đổi đơn vị tiền tệ.
- **Xuất báo cáo đa định dạng:** Tự động tổng hợp và gửi trực tiếp file PDF, Excel (CSV) hoặc HTML qua Telegram cho người dùng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Telegram Bot Token:** Tạo qua `@BotFather`.
- **OpenAI API Key:** Dùng cho các mô hình LLM (GPT-4o, GPT-4o-mini) và Embeddings API (`text-embedding-3`).
- **Qdrant Vector Database:** Đã cài đặt server Qdrant và nạp các collections dữ liệu DDC CWICR (hơn 55,000 work items từ kho lưu trữ GitHub chính thức `datadrivenconstruction/OpenConstructionEstimate-DDC-CWICR`).
- **Các API tùy chọn (nếu muốn đổi model):** Anthropic (Claude), Google Gemini, hoặc OpenRouter.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp (hoặc copy trực tiếp JSON) và Import vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `🔑 TOKEN`:** Cấu hình chính xác `bot_token` (Telegram), `QDRANT_URL` và `QDRANT_API_KEY` để kết nối hệ thống Vector DB.
- **n8n Credentials:** Vào *Settings → Credentials* thêm thông tin tài khoản **OpenAI API** và liên kết với các node mô hình LLM (`OpenAI Model 1`, `OpenAI Model 2`, `3️⃣ Embeddings API`).
- **Tùy chỉnh ngôn ngữ giao diện & cấu hình:** Kiểm tra node `Config` nếu muốn tùy chỉnh object `LANG` (thay đổi nhãn nút bấm, thông báo, đơn vị tiền tệ mặc định).
- **Lựa chọn AI Model:** Workflow hỗ trợ linh hoạt OpenAI, Claude, Gemini, DeepSeek. Các sếp có thể bật/tắt các node LLM tương ứng trên canvas tuỳ theo nhu cầu sử dụng.

#### 3. Kích hoạt ⚡️
- Gửi lệnh `/start` vào bot Telegram để test menu ngôn ngữ và tương tác thử.
- Nhập mô tả công việc xây dựng và kiểm tra kết quả tính toán chi phí trả về.
- Bật công tắc **Active** để đưa bot vào hoạt động chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử dự toán:** Kết nối thêm node Google Sheets hoặc cơ sở dữ liệu PostgreSQL để lưu lại lịch sử các yêu cầu báo giá của khách hàng.
- **Thông báo qua kênh nội bộ:** Tích hợp thêm node Slack hoặc Telegram Channel để gửi thông báo mỗi khi có khách hàng hoàn thành một bảng ước tính chi phí lớn.
- **Gửi Email tự động:** Mở rộng Block 8 để tự động gửi file báo cáo PDF/Excel trực tiếp vào email của khách hàng thay vì chỉ nhận qua Telegram.

### 📌 Kết luận
Workflow ước tính chi phí xây dựng tích hợp AI và Qdrant này là một vũ khí hạng nặng giúp tự động hóa khâu tiền kỳ trong ngành xây dựng. Hãy triển khai ngay lên hệ thống n8n tự túc của các sếp để tối ưu hóa năng suất và mang lại trải nghiệm cực kỳ chuyên nghiệp cho khách hàng!