---
title: "🚀 Trợ lý hội thoại PostgreSQL với Claude & DeepSeek (Multi‑KPI, Bảo mật)"
description: "Kết nối AI Claude và DeepSeek để truy vấn, tạo, cập nhật dữ liệu PostgreSQL qua chat, hỗ trợ đa KPI và bảo mật cao."
slug: "postgresql-conversational-agent-claude-deepseek"
tags: [n8n, automation, no-code, AI, PostgreSQL, IT‑Ops]
keywords: [n8n workflow, tự động hóa, PostgreSQL, AI agent, Claude, DeepSeek]
---

# 🚀 Trợ lý hội thoại PostgreSQL với Claude & DeepSeek (Multi‑KPI, Bảo mật)

Doanh nghiệp ngày càng phụ thuộc vào dữ liệu để đưa ra quyết định nhanh chóng. Tuy nhiên, việc truy vấn, tạo, cập nhật bảng PostgreSQL thường đòi hỏi kiến thức SQL và thời gian thao tác thủ công, gây **tắc nghẽn** và **rủi ro sai sót**.  

Workflow này biến **câu hỏi bằng ngôn ngữ tự nhiên** thành các lệnh SQL thông minh, nhờ AI Claude (Anthropic) và DeepSeek, đồng thời thực hiện các thao tác CRUD trên PostgreSQL một cách **tự động 100 %**, không cần viết code. Bạn chỉ cần chat, AI sẽ:

* Đọc schema, danh sách bảng.
* Thực hiện truy vấn, tạo, cập nhật bản ghi.
* Ghi nhớ ngữ cảnh ngắn hạn để hỗ trợ các câu hỏi liên tiếp.
* Bảo mật dữ liệu qua MCP (Multi‑Channel Protocol) và các credential riêng.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Truy vấn và thao tác DB chỉ bằng một câu chat.  
- **Độ chính xác cao**: AI sinh SQL dựa trên schema thực tế, giảm lỗi cú pháp.  
- **Cá nhân hoá**: Nhớ ngữ cảnh ngắn hạn, hỗ trợ các yêu cầu liên tiếp mà không cần lặp lại thông tin.  
- **Hoạt động liên tục**: MCP cho phép tích hợp với các hệ thống nội bộ mà không mở rộng cổng công cộng.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **PostgreSQL**: URL, database, username, password (hoặc SSL cert).  
- **Anthropic API Key**: Để sử dụng Claude (lmChatAnthropic).  
- **DeepSeek API Key** (nếu muốn dùng mô hình DeepSeek trong `Think` tool).  
- **MCP Server Credential**: Token/Secret để kích hoạt `PostgreSQL MCP Server`.  
- **n8n**: Phiên bản >= 1.0, đã cài các node LangChain (`@n8n/n8n-nodes-langchain`).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `postgresql-conversational-agent.json` (hoặc copy toàn bộ JSON từ trang gốc).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là danh sách các node quan trọng và hướng dẫn cấu hình chi tiết:

| Node | Loại | Mô tả ngắn | Cấu hình cần chỉnh |
|------|------|------------|--------------------|
| **GetTableSchema** | `postgresTool` | Lấy mô tả chi tiết của một bảng. | Chọn **PostgreSQL Credential**, nhập **Table Name** (được truyền từ `Think`). |
| **ListTables** | `postgresTool` | Liệt kê toàn bộ bảng trong DB. | Chọn **PostgreSQL Credential**. |
| **When Executed by Another Workflow** | `executeWorkflowTrigger` | Đầu vào khi workflow này được gọi từ workflow khác. | Không cần thay đổi, chỉ để nhận `input` từ workflow cha. |
| **CreateTableRecords** | `toolWorkflow` | Gọi workflow phụ để tạo nhiều bản ghi cùng lúc. | Đảm bảo **Workflow ID** trỏ tới workflow “Create Multiple Records”. |
| **ReadTableRecord** | `postgres` | Đọc một bản ghi duy nhất theo `id`. | Chọn **PostgreSQL Credential**, viết **Query**: `SELECT * FROM {{ $json.table }} WHERE id = {{$json.id}};` |
| **Operation** | `switch` | Phân nhánh dựa trên loại thao tác (read, create, update, delete). | Thiết lập **Values**: `read`, `create`, `update`, `delete`. |
| **UpdateTableRecord** | `postgres` | Cập nhật một bản ghi. | Chọn **PostgreSQL Credential**, viết **Query**: `UPDATE {{ $json.table }} SET ... WHERE id = {{$json.id}} RETURNING *;` |
| **UpdateTableRecords** | `toolWorkflow` | Gọi workflow phụ để cập nhật nhiều bản ghi. | Đặt **Workflow ID** đúng với workflow “Batch Update”. |
| **CreateTableRecord** | `postgres` | Tạo một bản ghi mới. | Chọn **PostgreSQL Credential**, viết **Query**: `INSERT INTO {{ $json.table }} (col1, col2, …) VALUES ({{ $json.val1 }}, {{ $json.val2 }}, …) RETURNING *;` |
| **PostgreSQL MCP Server** | `mcpTrigger` | Lắng nghe các yêu cầu MCP từ client. | Cấu hình **Port**, **Token**, và **Allowed IPs** (nếu cần). |
| **When chat message received** | `chatTrigger` | Nhận tin nhắn từ giao diện chat (Web, Slack, Telegram…). | Chọn **Chat Provider** (WebSocket, Slack, …) và **Credential** tương ứng. |
| **AI Agent** | `agent` | Core AI, kết hợp Claude + DeepSeek để sinh SQL. | - **LLM**: chọn **Anthropic Chat Model**.<br>- **Tools**: thêm `GetTableSchema`, `ListTables`, `CreateTableRecord`, `ReadTableRecord`, `UpdateTableRecord`, `ReadTableRows`.<br>- **Memory**: gắn `Simple Memory`. |
| **Simple Memory** | `memoryBufferWindow` | Lưu trữ ngữ cảnh 5 tin nhắn gần nhất. | Đặt **Window Size** = 5. |
| **MCP Client** | `mcpClientTool` | Gửi yêu cầu tới `PostgreSQL MCP Server`. | Điền **Server URL**, **Token** và **Timeout**. |
| **Anthropic Chat Model** | `lmChatAnthropic` | Mô hình Claude (v2/v3) để sinh SQL. | Dán **Anthropic API Key**, chọn **Model** (ví dụ `claude-3-5-sonnet-20240620`). |
| **Think** | `toolThink` | Xử lý logic “suy nghĩ” trước khi gọi tool. | Đặt **Prompt**: “Dựa trên schema, viết câu lệnh SQL cho yêu cầu: {{ $json.question }}”. |
| **get table details** | `toolWorkflow` | Workflow phụ trả về chi tiết bảng (cột, kiểu). | Đảm bảo **Workflow ID** trỏ tới workflow “Table Details”. |
| **ReadTableRows** | `toolWorkflow` | Lấy nhiều hàng từ bảng (paging). | Đặt **Workflow ID** đúng, truyền **limit** và **offset**. |

> **Lưu ý:**  
> - Mỗi node `postgres`/`postgresTool` phải **chọn cùng một credential PostgreSQL** để tránh lỗi kết nối.  
> - `Anthropic Chat Model` và `Think` cần **API Key** hợp lệ; nếu key hết hạn, workflow sẽ trả về lỗi 401.  
> - Khi sử dụng MCP, **cổng 8080** (hoặc cổng bạn cấu hình) phải mở trên firewall VPS.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một tin nhắn mẫu như “Liệt kê 10 bản ghi mới nhất của bảng `orders`”.  
2. Kiểm tra log của các node `AI Agent`, `Think`, và `ReadTableRows`.  
3. Khi mọi thứ hoạt động ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `When chat message received` để nhận và trả lời tin nhắn trực tiếp trong kênh nhóm.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại mỗi lần truy vấn (ngày‑giờ, câu hỏi, SQL sinh ra, kết quả).  
- **Báo cáo KPI định kỳ**: Tạo workflow phụ chạy mỗi ngày, dùng `ReadTableRows` để tổng hợp số lượng truy vấn, thời gian phản hồi, và gửi báo cáo qua email.  
- **Bảo mật nâng cao**: Kích hoạt **TLS** cho PostgreSQL và **IP whitelist** cho MCP Server.  

### 📌 Kết luận
Với workflow **PostgreSQL Conversational Agent**, các sếp có thể biến mọi câu hỏi dữ liệu thành hành động thực tế chỉ trong vài giây, giảm tải công việc thủ công, tăng độ chính xác và bảo mật. Hãy **import ngay**, cấu hình các credential, và để AI làm việc cho bạn! 🚀