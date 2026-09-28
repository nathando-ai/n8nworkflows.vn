---
title: "🚀 Tăng cường Chatbot AI bằng Bộ nhớ dài hạn và Định tuyến công cụ động"
description: "Workflow n8n tự động hóa cho chatbot AI có khả năng lưu trữ và truy xuất ký ức dài hạn qua Google Docs, đồng thời định tuyến công cụ để gửi thông báo qua Gmail/Telegram, mang lại trải nghiệm trò chuyện cá nhân hóa và thông minh."
slug: "empower-ai-chatbot-long-term-memory-dynamic-tool-routing"
tags: [n8n, automation, no-code, AI, chatbot, google-docs, gmail, telegram]
keywords: [n8n workflow, tự động hóa chatbot, AI agent, long term memory, google docs integration, gmail telegram notification]
---

# 🚀 Tăng cường Chatbot AI bằng Bộ nhớ dài hạn và Định tuyến công cụ động

Trong thời đại AI, một chatbot chỉ “thông minh” khi nó có thể nhớ lại các cuộc trò chuyện trước đó, sở thích của người dùng và các thông tin quan trọng để đưa ra phản hồi cá nhân hóa. Tuy nhiên, việc lưu trữ và truy xuất bộ nhớ này thường đòi hỏi mã code phức tạp hoặc các dịch vụ bên ngoài tốn kém. Workflow n8n dưới đây giải quyết vấn đề đó bằng cách kết hợp **Google Docs** làm kho lưu trữ dài hạn, **OpenAI GPT‑4o‑mini** làm bộ não xử lý ngôn ngữ, và một **công cụ router động** để tự động chọn hành động (lưu ký ức, truy xuất ký ức, gửi thông báo qua Gmail/Telegram) dựa trên chỉ thị của AI agent.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động lưu/truy xuất ký ức mà không cần can thiệp thủ công.
- **Cá nhân hóa cao**: Bot nhớ sở thích, lịch sử giao dịch và cung cấp phản hồi liên quan.
- **Thông báo đa kênh**: Gửi tóm tắt ký ức hoặc báo cáo thống kê qua Gmail và Telegram ngay lập tức.
- **Mở rộng dễ dàng**: Thêm công cụ mới (Slack, Notion, Airtable…) chỉ cần kéo thả vào router.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **OpenAI API Key** (credential `openAiApi`) để truy cập model gpt-4o-mini.
- **Google Docs OAuth2** (credential `googleDocsOAuth2Api`) – cần có quyền truy cập tạo, đọc và cập nhật tài liệu Google Docs.
- **Gmail OAuth2** (credential `gmailOAuth2`) – để gửi email thống kê hoặc thông báo.
- **Telegram Bot Token** (credential `telegramApi`) – để gửi tin nhắn tới cá nhân hoặc nhóm.
- Một **Google Doc** sẽ làm “bộ nhớ dài hạn”. Lưu lại ID của tài liệu này (có thể lấy từ URL: `https://docs.google.com/document/d/<DOC_ID>/edit`).
:::

### 🚀 Cách import & Lưu ý khi “lên đồ”

#### 1. Import Workflow 📥
- Trong n8n Editor, nhấn **Import** → chọn **From File** hoặc dán trực tiếp JSON của workflow.
- Đặt tên workflow (ví dụ: `AI Chatbot – Long Term Memory`) và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, cần cấu hình các node sau để workflow hoạt động đúng:

| Node (tên chính xác) | Loại | Cần cấu hình | Hướng dẫn chi tiết |
|----------------------|------|--------------|--------------------|
| **When Executed by Another Workflow** | `executeWorkflowTrigger` | Không cần thay đổi – node này nhận tín hiệu từ workflow con (toolWorkflow) khi agent gọi công cụ. |
| **Save Long Term Memories** | `googleDocs` (operation: **update**) | **Document ID** – điền ID của Google Doc sẽ lưu ký ức. <br> **Content** – map từ trường `{{ $json["memory"] }}` (nội dung cần lưu). |
| **Retrieve Long Term Memories** (hai node có tên tương tự) | `googleDocs` (operation: **get**) | **Document ID** – cùng ID như trên. <br> **Field to Return** – chọn `documentBody` để lấy toàn bộ nội dung ký ức. |
| **OpenAI Chat Model** (ba node: `OpenAI Chat Model2`, `OpenAI Chat Model3`, `🤖OpenAI Chat Model`) | `lmChatOpenAi` | **Model** – đã được pre‑set là `gpt-4o-mini`. <br> **Credentials** – chọn `openAiApi`. |
| **🧠 AI Agent w/Long Term Memory** | `agent` | **System Message** – chỉnh sửa để phù hợp với tono và mục đích chatbot (ví dụ: “Bạn là trợ lý thông minh, luôn tham khảo ký ức dài hạn trước khi trả lời.”). <br> **Tools** – đảm bảo 4 tool workflow (🧠Save Memories, 🔎Retrieve Memories, 📤Send Memories to Telegram, 📫Send Memories to Gmail) đã được kết nối đúng. |
| **Memory Tool Router** | `switch` | **Value** – node này nhận chuỗi từ agent (tool name). Thêm 4 case: `Save Memories`, `Retrieve Memories`, `Send Memories to Telegram`, `Send Memories to Gmail`. Mỗi case nối tới node toolWorkflow tương ứng. |
| **Prepare Telegram Message** & **Prepare Gmail Message** | `chainLlm` | **Prompt** – viết hướng dẫn để LLM tóm tắt ký ức thành tin nhắn ngắn gọn (Telegram) hoặc email chuyên nghiệp (Gmail). Ví dụ: “Tóm tắt các ký ức sau thành một tin nhắn Telegram không quá 200 ký tự: {{ $json[\"memories\"] }}”. |
| **Send Success Message to Telegram** | `telegram` | **Chat ID** – ID nhóm hoặc người nhận. <br> **Text** – map từ output của node `Prepare Telegram Message`. |
| **Email Workflow Stats** | `gmail` | **To** – địa chỉ email người nhận. <br> **Subject** – ví dụ: “[AI Chatbot] Báo cáo hoạt động hôm nay”. <br> **Body** – map từ output của node `Prepare Gmail Message` hoặc thêm thống kê số lượng ký ức đã lưu. |
| **🧠Save Memories**, **🔎Retrieve Memories**, **📤Send Memories to Telegram**, **📫Send Memories to Gmail** | `toolWorkflow` | Đây là các workflow con (sub‑workflow) cần được **import trước** hoặc **tạo mới** trong cùng folder. Mỗi sub‑workflow chỉ chứa một node chính (Google Docs update/get, Telegram send, Gmail send) và được gọi qua `executeWorkflowTrigger` trong workflow chính. Đảm bảo chúng đã **Active** và credentials tương ứng được thiết lập. |

> **Lưu ý quan trọng**: Sau khi thay đổi Document ID hoặc credentials, hãy nhấn **Save** trên mỗi node rồi thực hiện **Test Workflow** để xác nhận dữ liệu được ghi/đọc đúng trước khi bật Active.

#### 3. Kích hoạt ⚡️
- Chọn **Execute Workflow** để chạy một lần test với dữ liệu mẫu (bạn có thể gửi tin nhắn tới node `Ⓜ️ When chat message received` qua giao diện Chat Trigger hoặc sử dụng công cụ “Execute Workflow” trong panel).
- Kiểm tra:
  - Nội dung được lưu vào Google Doc (node **Save Long Term Memories**).
  - Khi hỏi lại, agent truy xuất ký ức và trả lời dựa trên thông tin đó (node **Retrieve Long Term Memories**).
  - Lệnh “Lưu ký ức này và gửi qua Telegram” → agent gọi tool **📤Send Memories to Telegram**, nhận được tin nhắn trên Telegram.
  - Lệnh “Gửi tóm tắt ký ức qua email” → agent gọi tool **📫Send Memories to Gmail**, nhận được email.
- Nếu mọi thứ đều ổn, bật nút **Active** ở góc trên bên phải workflow để nó bắt đầu lắng nghe sự kiện chat 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram Bot** để nhận báo cáo thực thời gian về số lượng ký ức mới mỗi ngày (node `telegram` hoặc `slack` sau `Email Workflow Stats`).
- **Lưu log chi tiết** vào một bảng Google Sheets hoặc Airtable để audit các hoạt động của agent (thêm node `googleSheets` sau mỗi toolWorkflow).
- **Định kỳ gửi báo cáo tóm tắt** (cron trigger) sử dụng node `cron` → `googleDocs get` → `email` hoặc `telegram`.
- **Tích hợp bộ nhớ vector** (Pinecone, Weaviate) để tìm kiếm ký ức ngữ nghĩa thay vì chỉ dựa trên tài liệu văn bản thô.
- **Tùy chỉnh prompt của Agent** theo từng lĩnh vực (chăm sóc khách hàng, bán hàng, hỗ trợ kỹ thuật) để tăng độ liên quan của phản hồi.
- **Sử dụng n8n Encryption** để lưu trữ API keys một cách an toàn khi triển khai trên môi trường production.

### 📌 Kết luận
Workflow n8n này biến chatbot AI từ một “trò chuyện một chiều” thành một **trợ lý thông minh có bộ nhớ dài hạn**, khả năng học hỏi từ từng tương tác và tự động thực hiện hành động qua nhiều công cụ khác nhau. Với chỉ vài bước cấu hình credential và Google Doc ID, các sếp có thể ngay lập tức triển khai một giải pháp AI mạnh mẽ, tiết kiệm thời gian và mang lại trải nghiệm người dùng vượt trội. Hãy import, thử nghiệm và để chatbot của bạn “nhớ” mọi thứ quan trọng ngay hôm nay!