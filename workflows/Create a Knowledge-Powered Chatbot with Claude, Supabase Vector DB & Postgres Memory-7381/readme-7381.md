---
title: "🤖 Tạo Chatbot Cực Khỏe Powered by AI với Claude, Supabase Vector DB & Bộ Nhớ PostgreSQL - Tự Động Hóa Trợ Lý 24/7"
description: "Workflow này giúp các sếp xây dựng một chatbot thông minh, tự động trả lời câu hỏi từ cơ sở tri thức cá nhân hóa trên Supabase, nhớ lịch sử hội thoại qua PostgreSQL, và sử dụng Claude 4 Sonnet để trả lời chính xác nhất. Giảm thiểu 80% thời gian hỗ trợ khách hàng thủ công!"
slug: "tạo-chatbot-ai-claude-supabase-postgres"
tags: [n8n, automation, no-code, chatbot-ai, multimodal-ai, supabase, postgres, claude-ai]
keywords: [n8n workflow chatbot, tự động hóa hỗ trợ khách hàng, Claude AI chatbot, Supabase vector database, PostgreSQL memory, AI agent automation]
---

# 🚀 **Chatbot Cực Khỏe Powered by AI: Tự Động Hóa Trợ Lý Hỗ Trợ Khách Hàng 24/7**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp đang phải:
- **Phải trả lời cùng một câu hỏi hàng trăm lần** mỗi ngày (ví dụ: "Chính sách hoàn tiền", "Cách sử dụng sản phẩm", "Thời gian giao hàng").
- **Mất thời gian theo dõi lịch sử hội thoại** của khách hàng để trả lời chính xác.
- **Không thể cập nhật tri thức mới** một cách nhanh chóng khi có thay đổi sản phẩm hoặc chính sách.
- **Đang lo lắng về chất lượng hỗ trợ** khi nhân viên nghỉ phép hoặc bận rộn.

**Giải pháp?** Một **chatbot AI thông minh** tự động trả lời từ cơ sở tri thức cá nhân hóa, nhớ lịch sử hội thoại, và sử dụng **Claude 4 Sonnet** (mô hình AI tiên tiến nhất của Anthropic) để trả lời **chính xác, tự nhiên, và cá nhân hóa** như một nhân viên thực sự.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và **tối ưu chi phí**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) với cấu hình tối thiểu:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ cho workflow này chạy mượt mà)

*Lưu ý:* Nếu dùng **n8n Cloud**, chi phí API (Claude, OpenAI, Supabase) sẽ cao hơn.
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian hỗ trợ khách hàng** – Chatbot tự động trả lời 90% câu hỏi thường gặp.
✅ **Trả lời chính xác, tự nhiên** – Sử dụng **Claude 4 Sonnet** (mô hình AI tiên tiến nhất hiện nay).
✅ **Nhớ lịch sử hội thoại** – Không cần khách hàng phải lặp lại thông tin (nhờ **PostgreSQL Memory**).
✅ **Cập nhật tri thức dễ dàng** – Chỉ cần thêm/đổi dữ liệu trong **Supabase Vector DB**.
✅ **Hoạt động 24/7** – Không cần nhân viên trực đêm.
✅ **Cá nhân hóa trải nghiệm** – Chatbot có thể nhớ tên khách hàng và lịch sử tương tác.
✅ **Dễ dàng mở rộng** – Kết nối với **Slack, Website, Discord, Teams** hoặc **API của doanh nghiệp**.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:

### **1. Tài Khoản & API Keys**
| **Dịch vụ**          | **API Key/Credential** | **Lưu ý** |
|----------------------|----------------------|-----------|
| **Anthropic (Claude)** | `anthropicApi` (API Key) | [Tạo API Key tại đây](https://console.anthropic.com/) |
| **OpenAI (Embeddings)** | `openAiApi` (API Key) | [Tạo API Key tại đây](https://platform.openai.com/account/api-keys) |
| **Supabase**         | `supabaseApi` (URL + Key) | [Tạo Project tại đây](https://supabase.com/) |
| **PostgreSQL**       | **Built-in n8n** (không cần API) | n8n tự động tạo bảng lưu lịch sử hội thoại |

### **2. Cơ Sở Tri Thức (Knowledge Base)**
- **Supabase Vector DB** chứa dữ liệu văn bản (tài liệu, FAQ, hướng dẫn sử dụng).
- **Cách tạo:** Theo dõi [bài hướng dẫn của Cole Medin](https://www.youtube.com/watch?v=...) (xem phần **Hướng Dẫn Chi Tiết** bên dưới).

### **3. N8n Workflow**
- **Phiên bản n8n:** 1.40+ (đã tích hợp nodes LangChain).
- **Nền tảng:** Self-hosted (khuyến nghị) hoặc n8n Cloud.

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7381](https://n8n.io/workflows/7381).
2. **Nhấn "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo workflow mới.
2. **Nhấn "Import"** → **"Paste JSON"**.
3. **Dán JSON** từ [n8n.io/workflows/7381](https://n8n.io/workflows/7381) (mở tab "Code" trên trang workflow).
4. **Nhấn "Import"**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **6 nodes chính**, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: When chat message received (chatTrigger)**
- **Chức năng:** Nhận tin nhắn từ **webhook** (Slack, Website, Discord, Teams...).
- **Cấu hình:**
  - **Trigger Type:** `Webhook` (nếu muốn kết nối với bên ngoài).
  - **URL Webhook:** Cần **cấu hình ở bên thứ ba** (ví dụ: Slack, Website).
  - **Credentials:** Không cần (sử dụng mặc định).

#### **🔹 Node 2: AI Agent (agent)**
- **Chức năng:** Xử lý logic chatbot, quyết định khi nào gọi đến **Claude**, **Supabase**, hoặc **PostgreSQL**.
- **Cấu hình:**
  - **Prompt:** Cần **tùy chỉnh** theo mục đích chatbot (ví dụ:
    ```plaintext
    Bạn là trợ lý ảo của [Tên Doanh Nghiệp]. Hãy trả lời các câu hỏi của khách hàng về sản phẩm/dịch vụ của chúng tôi. Nếu không biết câu trả lời, hãy nói "Tôi sẽ kiểm tra và trả lời lại ngay".
    ```
  - **Tools:** Chọn tất cả các node khác (`Anthropic Chat Model`, `Supabase Vector Store`, `Postgres Chat Memory`).

#### **🔹 Node 3: Anthropic Chat Model (lmChatAnthropic)**
- **Chức năng:** Gọi API **Claude 4 Sonnet** để trả lời.
- **Cấu hình:**
  - **Credentials:** Chọn `anthropicApi` (đã tạo trước).
  - **Model:** `claude-sonnet-4-20250514` (mô hình mới nhất).
  - **Temperature:** Giữ mặc định (`0.7`) để trả lời tự nhiên.

#### **🔹 Node 4: Supabase Vector Store (vectorStoreSupabase)**
- **Chức năng:** Tìm kiếm **tri thức liên quan** từ cơ sở dữ liệu Supabase.
- **Cấu hình:**
  - **Credentials:** Chọn `supabaseApi` (URL + Key Supabase).
  - **Table Name:** Tên bảng chứa dữ liệu (ví dụ: `growth_ai_documents`).
  - **Mode:** `retrieve-as-tool` (cho phép AI tự động gọi khi cần).
  - **Tool Description:** "Database" (có thể đổi thành tên cụ thể).

#### **🔹 Node 5: Embeddings OpenAI (embeddingsOpenAi)**
- **Chức năng:** Chuyển đổi văn bản thành **embeddings** (dữ liệu số) để Supabase tìm kiếm.
- **Cấu hình:**
  - **Credentials:** Chọn `openAiApi` (API Key OpenAI).
  - **Model:** `text-embedding-ada-002` (mặc định).

#### **🔹 Node 6: Postgres Chat Memory (memoryPostgresChat)**
- **Chức năng:** Lưu **lịch sử hội thoại** để AI nhớ context.
- **Cấu hình:**
  - **Credentials:** Sử dụng `postgres` mặc định của n8n.
  - **Table Name:** `n8n_chat_memory` (n8n tự động tạo).
  - **Context Window Length:** `20` (có thể điều chỉnh).

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn vào **webhook** (ví dụ: `https://tên-vps-của-bạn.n8n.cloud/webhook/your-webhook-id`).
   - Kiểm tra phản hồi của Claude có logic không?
2. **Bật Active:**
   - Nhấn **Active** trên nút ở góc trên bên phải.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối với Slack/Teams/Website**
- **Slack:**
  - Tạo **Incoming Webhook** tại Slack → Chọn URL webhook của n8n.
  - Cấu hình **Slack App** để chatbot trả lời trong channel.
- **Website:**
  - Sử dụng **n8n Webhook Trigger** + **HTML/JavaScript** để hiển thị chatbot.
  - Ví dụ: [Hướng dẫn embed chatbot vào website](https://docs.n8n.io/integrations/builtins/webhook-trigger/).

### **2. Lưu Log & Báo Cáo Hàng Ngày**
- **Node StickyNote:** Thêm node `n8n-nodes-base.stickyNote` để ghi log lỗi.
- **Node Email/Slack:** Gửi báo cáo lỗi hàng ngày qua email/Slack.
  ```plaintext
  "Error occurred at [time]: [error message]. User ID: [user_id]."
  ```

### **3. Cập Nhật Tri Thức Mới**
- **Thêm dữ liệu vào Supabase:**
  - Sử dụng **Supabase Dashboard** hoặc **PostgreSQL CLI** để thêm mới.
  - Sau đó, **rebuild embeddings** (nếu cần).
- **Cập Nhật Prompt:**
  - Nếu chatbot trả lời không phù hợp, chỉnh sửa **prompt** trong node `AI Agent`.

### **4. Mở Rộng Hỗ Trợ API**
- **Gọi API bên ngoài:**
  - Thêm node `HTTP Request` để gọi API (ví dụ: tra cứu giá sản phẩm).
- **Kết nối với Airtable/Google Sheets:**
  - Sử dụng node `Airtable` hoặc `Google Sheets` để cập nhật dữ liệu.

---

## 📌 **Kết Luận: Chatbot AI Cực Khỏe Đã Sẵn Sàng!**

### **Bước Đầu Tiên: Lên Đồ Ngay!**
Các sếp đã có:
✔ **Workflow hoàn chỉnh** với Claude, Supabase, và PostgreSQL.
✔ **Hướng dẫn chi tiết** để cấu hình từng node.
✔ **Mẹo nâng cao** để tối ưu hiệu suất.

**Bây giờ chỉ cần:**
1. **Cài n8n trên VPS** (tiết kiệm chi phí).
2. **Tạo Supabase Vector DB** (theo dõi [Cole Medin](https://www.youtube.com/watch?v=...)).
3. **Import workflow** và **cấu hình API keys**.
4. **Test và bật Active!**

**Kết quả?** Một **trợ lý AI thông minh** tự động trả lời khách hàng **24/7**, tiết kiệm **80% thời gian hỗ trợ**, và **cải thiện trải nghiệm khách hàng** một cách đáng kể.

---
**🚀 Hãy bắt đầu ngay và tự động hóa hỗ trợ khách hàng của mình!** 🚀