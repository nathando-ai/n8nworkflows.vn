---
title: "🤖 Chat với GPT-4o qua Telegram Bot: Tự động hóa AI không cần code"
description: "Hướng dẫn chi tiết cách xây dựng Telegram Bot chat với OpenAI GPT-4o Mini bằng n8n. Kết nối AI vào kênh giao tiếp quen thuộc, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "chat-gpt-telegram-bot-n8n"
tags: [n8n, automation, no-code, openai, telegram, ai-agent]
keywords: [n8n workflow, telegram bot ai, chat gpt telegram, tự động hóa ai, n8n openai]
---

# 🤖 Chat với GPT-4o qua Telegram Bot: Tự động hóa AI không cần code

Trong kỷ nguyên AI, việc tiếp cận các mô hình ngôn ngữ mạnh mẽ như GPT-4o không còn là rào cản với các lập trình viên. Tuy nhiên, đối với đa số doanh nghiệp và cá nhân, việc tích hợp AI vào quy trình làm việc hàng ngày thường gặp phải rào cản kỹ thuật: phải xây dựng API, quản lý server, hay phát triển giao diện web phức tạp.

Giải pháp tối ưu nhất chính là đưa AI vào nơi bạn đã quen thuộc nhất: **Telegram**. Với workflow n8n này, các sếp có thể biến bất kỳ kênh Telegram nào thành một trợ lý AI thông minh, sử dụng sức mạnh của GPT-4o Mini, mà hoàn toàn không cần viết một dòng code nào. Chỉ với 4 nodes đơn giản, các sếp sẽ sở hữu một hệ thống chat AI hoạt động 24/7, phản hồi tức thì và cực kỳ linh hoạt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiếp cận AI mọi lúc, mọi nơi:** Chat với GPT-4o trực tiếp trên điện thoại hoặc máy tính qua Telegram, không cần mở trình duyệt hay ứng dụng riêng.
- **Chi phí tối ưu:** Sử dụng model `gpt-4o-mini` có hiệu suất cao nhưng chi phí API thấp hơn đáng kể so với các model lớn, phù hợp cho việc sử dụng thường xuyên.
- **Không cần kiến thức lập trình:** Toàn bộ quy trình được xử lý bởi n8n, các sếp chỉ cần cấu hình credentials và prompt.
- **Độ tin cậy cao:** Workflow hoạt động liên tục trên server riêng, đảm bảo phản hồi nhanh chóng và ổn định.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy n8n (khuyến khích self-hosted).
2. **Tài khoản Telegram:**
   - Tạo bot mới qua @BotFather để lấy **Bot Token**.
   - Ghi lại **Chat ID** của người dùng hoặc nhóm (nếu muốn giới hạn quyền truy cập).
3. **Tài khoản OpenAI:**
   - Có **API Key** từ OpenAI.
   - Đảm bảo tài khoản có credit để gọi API `gpt-4o-mini`.
4. **Credentials trong n8n:**
   - Tạo credential `telegramApi` (loại Telegram API).
   - Tạo credential `openAiApi` (loại OpenAI API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link workflow gốc: [https://n8n.io/workflows/2114](https://n8n.io/workflows/2114) hoặc tải file JSON và import.
4. Sau khi import, các sếp sẽ thấy 4 nodes chính: `Telegram Trigger`, `AI Agent`, `Telegram`, và `OpenAI Chat Model`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node 1: Telegram Trigger**
- **Mục đích:** Bắt đầu workflow khi nhận được tin nhắn từ Telegram.
- **Cấu hình:**
  - Chọn credential `telegramApi` đã tạo.
  - Trong phần **Options**, các sếp có thể thiết lập **Allowed Chat IDs** để chỉ cho phép một số người dùng cụ thể chat với bot (tăng bảo mật). Nếu bỏ trống, bot sẽ phản hồi cho tất cả ai nhắn tin.
  - Chọn **Trigger on Message** để kích hoạt khi có tin nhắn mới.

**Node 2: AI Agent**
- **Mục đích:** Xử lý logic AI, kết nối giữa input từ Telegram và output từ OpenAI.
- **Cấu hình:**
  - Đảm bảo node này được kết nối với `Telegram Trigger` (input) và `Telegram` (output).
  - Trong phần **System Message** (nếu có), các sếp có thể tùy chỉnh persona của AI (ví dụ: "Bạn là trợ lý ảo thân thiện, trả lời ngắn gọn và chính xác").
  - Node này tự động quản lý lịch sử hội thoại (memory) để AI nhớ ngữ cảnh trước đó.

**Node 3: Telegram**
- **Mục đích:** Gửi phản hồi từ AI trở lại Telegram.
- **Cấu hình:**
  - Chọn credential `telegramApi`.
  - **Chat ID:** Để trống hoặc dùng biến `{{ $json.chat.id }}` để gửi tin nhắn về đúng người đã hỏi.
  - **Text:** Dùng biến `{{ $json.output }}` hoặc `{{ $json.response }}` (tùy thuộc vào output của AI Agent) để hiển thị câu trả lời.
  - **Parse Mode:** Chọn `Markdown` hoặc `MarkdownV2` để định dạng câu trả lời (in đậm, link, code block) đẹp mắt.

**Node 4: OpenAI Chat Model**
- **Mục đích:** Cung cấp sức mạnh AI từ OpenAI.
- **Cấu hình:**
  - Chọn credential `openAiApi`.
  - **Model:** Mặc định là `gpt-4o-mini`. Các sếp có thể đổi sang `gpt-4o` hoặc `gpt-3.5-turbo` nếu muốn, nhưng `gpt-4o-mini` là lựa chọn cân bằng giữa chất lượng và chi phí.
  - **Temperature:** Giữ ở mức 0.7-0.8 để câu trả lời tự nhiên.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn nút **Execute Workflow** trong n8n.
   - Mở Telegram, tìm bot của bạn và gửi tin nhắn "Xin chào".
   - Kiểm tra xem n8n có nhận được trigger và gửi phản hồi không.
2. **Bật Active:**
   - Sau khi test thành công, nhấn nút **Active** ở góc trên bên phải n8n.
   - Workflow sẽ chạy liên tục, sẵn sàng phản hồi mọi tin nhắn từ Telegram.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Memory dài hạn:** Mặc định AI Agent có memory ngắn hạn. Các sếp có thể kết nối thêm node `Simple Memory` hoặc `Vector Store` để AI nhớ thông tin lâu dài về người dùng.
- **Tích hợp dữ liệu doanh nghiệp:** Thêm node `Google Sheets` hoặc `Notion` vào trước AI Agent để AI có thể tra cứu dữ liệu nội bộ (ví dụ: bảng giá, FAQ) trước khi trả lời.
- **Gửi báo cáo định kỳ:** Tạo thêm một workflow riêng với `Cron` trigger để AI tổng hợp dữ liệu và gửi báo cáo hàng ngày qua Telegram.
- **Đa ngôn ngữ:** Trong System Message, hướng dẫn AI trả lời bằng tiếng Việt để tăng trải nghiệm người dùng.

### 📌 Kết luận
Việc tích hợp AI vào Telegram thông qua n8n là một bước tiến lớn trong việc dân chủ hóa công nghệ AI. Với workflow này, các sếp không chỉ tiết kiệm thời gian phát triển mà còn có được một trợ lý AI mạnh mẽ, sẵn sàng hỗ trợ 24/7. Hãy bắt đầu ngay hôm nay, import workflow, cấu hình credentials và trải nghiệm sức mạnh của GPT-4o Mini chỉ với vài cú click chuột!