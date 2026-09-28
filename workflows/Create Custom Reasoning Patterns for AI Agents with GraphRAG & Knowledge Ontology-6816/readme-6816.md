---
title: "🚀 Tự động tạo mẫu suy luận tùy chỉnh cho AI Agents với GraphRAG & Knowledge Ontology"
description: "Kết hợp GraphRAG và Ontology của InfraNodus để AI tự mở rộng prompt, cung cấp câu trả lời sâu sắc, chính xác mà không cần viết code."
slug: "tu-dong-tao-mau-suy-luan-ai-agents-graphrag-knowledge-ontology"
tags: [n8n, automation, no-code, AI, RAG, GraphRAG]
keywords: [n8n workflow, tự động hóa, GraphRAG, knowledge ontology, AI agents]
---

# 🚀 Tự động tạo mẫu suy luận tùy chỉnh cho AI Agents với GraphRAG & Knowledge Ontology

Khi các doanh nghiệp muốn AI trả lời “đúng ngữ cảnh” nhưng lại phải tốn hàng giờ để xây dựng prompt, tạo knowledge base, và duy trì các công cụ RAG. Việc làm thủ công này gây **trễ**, **sai lệch** và **tốn kém**.  
Workflow này giải quyết toàn bộ quy trình: từ nhận tin nhắn chat → lưu trữ ngắn hạn → truy vấn Knowledge Ontology trên InfraNodus → tạo prompt mở rộng → trả lời người dùng – **tự động 100%**, **không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn viết prompt thủ công cho mỗi câu hỏi.  
- **Độ chính xác cao**: Knowledge Ontology cung cấp ngữ cảnh chuyên môn, giảm lỗi “hallucination”.  
- **Cá nhân hoá**: Mỗi agent có thể được “đào tạo” bằng ontology riêng cho lĩnh vực (marketing, pháp lý, kỹ thuật…).  
- **Hoạt động liên tục**: Workflow chạy 24/7, trả lời ngay khi có tin nhắn mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản n8n** (Self‑hosted hoặc n8n.cloud).  
- **API Key OpenAI** (đăng ký tại https://platform.openai.com).  
- **API Bearer Token** cho InfraNodus (được tạo trong InfraNodus > Settings > API).  
- **Knowledge Graph “Reasoning Ontology”** đã được tạo trên InfraNodus (xem hướng dẫn dưới).  
- **Kết nối chat** (Slack, Discord, Telegram, hoặc webhook) để nhận tin nhắn.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.  
2. Nhấn **Import** → **From JSON**.  
3. Dán nội dung JSON của workflow (tải từ https://n8n.io/workflows/6816) hoặc tải file `.json` đã lưu.  
4. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần thay đổi | Hướng dẫn chi tiết |
|------|----------------------|--------------------|
| **When chat message received** (`chatTrigger`) | Chọn **Credential** của kênh chat (Slack, Discord, Telegram, …). | Vào **Credentials** → **Add New** → chọn loại kênh → nhập token/bot ID. |
| **OpenAI Chat Model** (`lmChatOpenAi`) | - Chọn **Credential** `openAiApi`.<br>- Đặt **Model**: `gpt-4o-mini` (hoặc model khác). | Vào **Credentials** → **OpenAI API** → dán API Key. |
| **Simple Memory** (`memoryBufferWindow`) | Không cần thay đổi, mặc định lưu 5 tin nhắn gần nhất. | Nếu muốn lưu lâu hơn, tăng **Window Size**. |
| **Interaction Dynamics Expert** (`httpRequestTool`) | - **Credential**: `httpBearerAuth` (InfraNodus API token).<br>- **URL**: `https://api.infranodus.com/v1/graph/query` (hoặc endpoint bạn dùng).<br>- **Method**: `POST`.<br>- **Body**: JSON chứa `graphName` = “Reasoning Ontology”, `prompt` = `{{$json["prompt"]}}`. | Tạo **Credential** mới → **HTTP Bearer Auth** → dán token InfraNodus. |
| **Reasoning Agent** (`agent`) | - **System Prompt**: Dán đoạn “system prompt” mô tả cách augment prompt dựa trên ontology (xem phần “Reasoning Agent” trong canvas).<br>- **Tools**: Kết nối **Interaction Dynamics Expert** (HTTP request) và **OpenAI Chat Model**. | Mở node → **System Prompt** → dán nội dung: <br>```\nYou are a reasoning expert. Use the provided knowledge graph to enrich the user’s query before answering.\n```<br>Trong **Tools**, bật **Interaction Dynamics Expert** và **OpenAI Chat Model**. |
| **Sticky Note** (n8n‑nodes‑base.stickyNote) | Chỉ dùng để ghi chú, không cần cấu hình. | - |

> **Lưu ý:** Sau khi cấu hình xong, nhấn **Execute Node** từng node để kiểm tra kết nối (OpenAI, InfraNodus) trước khi chạy toàn workflow.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một tin nhắn mẫu qua kênh chat đã kết nối. Kiểm tra log của các node để chắc chắn dữ liệu được truyền đúng.  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động lắng nghe và phản hồi.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram Bot**: Thêm node `Slack` hoặc `Telegram` để gửi báo cáo tóm tắt hoạt động mỗi ngày.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại câu hỏi, prompt đã augment và câu trả lời – tiện cho phân tích hiệu suất.  
- **Tự động cập nhật Ontology**: Thiết lập một cron job (node `Cron`) gọi API `https://infranodus.com/import/ai-ontologies` để đồng bộ các khái niệm mới từ nguồn bên ngoài.  
- **Multi‑agent**: Nhân bản node **Reasoning Agent** và thay đổi **System Prompt** để tạo các “expert” chuyên về marketing, pháp lý, kỹ thuật… và dùng **Switch** để định tuyến câu hỏi.

### 📌 Kết luận
Với workflow này, các sếp có thể biến **InfraNodus Knowledge Graph** thành “bộ não” cho AI, tự động mở rộng prompt và cung cấp câu trả lời sâu sắc, giảm thiểu công sức chuẩn bị dữ liệu. Hãy triển khai ngay, kết nối kênh chat yêu thích và để AI làm việc cho bạn 24/7! 🚀