---
title: "🤖 Tự Động Hóa Trả Lời Câu Hỏi ERP Cin7 Bằng Chatbot AI (N8N + OpenAI + Peliqan) - Không Cần Code"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp truy vấn dữ liệu ERP Cin7 (sản phẩm, tồn kho, tài chính...) bằng cách chat với AI, chuyển đổi tự động câu hỏi thành SQL và trả lời chính xác 100%. Giảm thời gian tìm kiếm từ giờ xuống phút."
slug: "tự-dộng-hoa-chatbot-ai-erp-cin7-n8n"
tags: [n8n, automation, no-code, ai-chatbot, erp-cin7, peliqan, openai, text-to-sql]
keywords: [n8n workflow erp, tự động hóa cin7, chatbot ai cho doanh nghiệp, query sql từ câu hỏi tự nhiên, peliqan n8n, openai n8n]
---

# 🚀 **Chatbot AI Trả Lời Câu Hỏi ERP Cin7 - Không Cần Code**

### **Giải pháp cho nỗi đau:**
Các sếp thường mất **từ 30 phút đến 2 giờ** mỗi ngày để tìm kiếm thông tin trong ERP như:
- *"Tồn kho sản phẩm ABC hiện tại là bao nhiêu?"*
- *"Doanh thu tháng 12/2023 của khách hàng XYZ là bao nhiêu?"*
- *"Danh sách sản phẩm hết hạn trong 30 ngày tới là gì?"*

Với **workflow này**, các sếp chỉ cần **chat với AI** (Slack, Telegram, hoặc webhook), AI sẽ tự động:
1. **Chuyển đổi câu hỏi thành SQL** (Text-to-SQL).
2. **Truy vấn dữ liệu từ Cin7 qua Peliqan** (không cần API trực tiếp).
3. **Trả lời kết quả chính xác** trong vài giây.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Từ **2 giờ/tuần** xuống **5 phút/tuần**.
✅ **Trả lời chính xác 100%**: Không sai sót như tìm kiếm thủ công.
✅ **Hoạt động 24/7**: AI trả lời ngay cả khi các sếp nghỉ ngơi.
✅ **Cá nhân hóa**: AI hiểu ngữ cảnh và trả lời chi tiết theo yêu cầu.
✅ **Không cần code**: Sử dụng **n8n + Peliqan + OpenAI** để tự động hóa.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Peliqan** (miễn phí trial):
   - [Đăng ký Peliqan](https://peliqan.io) (sử dụng mã giảm giá **N8NPELIQAN** để giảm 20% đầu tiên).
2. **API Key Cin7**:
   - Lấy từ **Cin7 Omni** hoặc **Cin7 Core** (yêu cầu liên hệ hỗ trợ Cin7).
3. **API Key OpenAI**:
   - Tạo tại [OpenAI Platform](https://platform.openai.com/) (gói miễn phí cho phép ~1.000 request/tháng).
4. **VPS cho n8n** (khuyến nghị):
   - [VPS TinoHost (50k/tháng)](https://tino.vn/vps-n8n?affid=388) (mã giảm **VPSN8N**).
   - [VPS Xeon 4GB (BNIX)](https://my.bnix.one/aff.php?aff=172) (ổn định cho AI).
5. **Credentials trong n8n**:
   - **Peliqan API Key** (tìm tại `Settings > API key` trên Peliqan).
   - **OpenAI API Key** (đăng ký tại OpenAI).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7315](https://n8n.io/workflows/7315).
2. **Mở n8n Editor** (trên VPS hoặc n8n.cloud).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
2. Copy toàn bộ mã JSON từ [n8n.io/workflows/7315](https://n8n.io/workflows/7315) → Dán vào và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **5 node chính**, các sếp cần cấu hình như sau:

#### **🔹 Node 1: When chat message received (chatTrigger)**
- **Chọn loại trigger**:
  - **Webhook** (nếu muốn chat qua URL).
  - **Slack/Telegram** (nếu muốn tích hợp với chatbot).
- **Lưu ý**:
  - Nếu dùng **webhook**, các sếp cần chia sẻ URL trigger này cho người dùng (ví dụ: `https://vps-cua-ban.com/webhook/chat`).

#### **🔹 Node 2: AI Agent (agent)**
- **Cấu hình System Message** (định nghĩa logic cho AI):
  ```plaintext
  You are an AI assistant that can query data from Cin7 ERP via Peliqan.
  Your job is to convert user questions into SQL queries and execute them.
  Example:
  - User: "Show me stock levels for product ABC"
  - You: "SELECT stock_level FROM inventory WHERE product_id = 'ABC';"
  ```
  - **Lưu ý**: Nếu muốn AI hiểu cấu trúc dữ liệu cụ thể của Cin7, các sếp có thể **tải datamodel từ Peliqan** (theo hướng dẫn [đây](https://help.peliqan.io/build-ai-agents-with-n8n-and-peliqan#block-2401aa9b387980cf8b2ff069588dd3dc)) và **thay thế** vào System Message.

#### **🔹 Node 3: OpenAI Chat Model (lmChatOpenAi)**
- **Chọn credentials**: `openAiApi` (đã cấu hình trước khi import).
- **Lưu ý**:
  - Nếu OpenAI API bị rate limit, các sếp cần **cài đặt mô hình miễn phí** (`gpt-3.5-turbo`) hoặc nâng cấp.
  - **Prompt Engineering**: Nếu AI trả lời không chính xác, các sếp có thể **cập nhật System Message** để rõ ràng hơn.

#### **🔹 Node 4: Simple Memory (memoryBufferWindow)**
- **Lưu ý**: Node này giúp AI **hiểu ngữ cảnh** trong nhiều lượt chat liên tiếp (ví dụ: nếu người dùng hỏi "Tôi muốn biết sản phẩm nào?" → "Hãy cho tôi biết sản phẩm ABC").
- **Tham số mặc định**: `windowSize: 3` (lưu 3 lượt chat trước đó).

#### **🔹 Node 5: Execute an SQL query via Peliqan (peliqanTool)**
- **Chọn credentials**: `peliqanApi` (API Key Peliqan).
- **Cấu hình**:
  - **Operation**: `exec` (mặc định).
  - **Resource**: `query` (mặc định).
  - **Data warehouse name**: Chọn **data warehouse** đã sync từ Cin7 trên Peliqan.
- **Lưu ý**:
  - **Cài đặt môi trường**:
    ```bash
    export N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE=True
    ```
    (Thực hiện trên **VPS** của các sếp để Peliqan node hoạt động).
  - Nếu query SQL sai syntax, AI sẽ trả lời **"Lỗi: Query không hợp lệ"**.

---
### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Gửi câu hỏi vào **webhook** hoặc **Slack/Telegram**:
     - *"Hãy cho tôi biết tồn kho sản phẩm ABC là bao nhiêu?"*
   - Kiểm tra kết quả trả về từ AI.
2. **Bật Active workflow**:
   - Nhấn **Active** trên n8n Editor.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM NÂNG CAO]
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để chatbot hoạt động trên kênh team.
   - Ví dụ: Khi có tin nhắn trong Slack, AI trả lời ngay trong cùng kênh.

2. **Lưu log truy vấn**:
   - Thêm **node Google Sheets** hoặc **node Airtable** sau node Peliqan để ghi lại tất cả query SQL và kết quả.
   - Cách làm:
     ```plaintext
     - Node Peliqan → Node Google Sheets (Create Row)
     - Tham số: `query = {{$node["Execute an SQL query via Peliqan"].json["query"]}}`
     - `result = {{$node["Execute an SQL query via Peliqan"].json["result"]}}`
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node n8n-nodes-base.schedule** để chạy AI định kỳ (ví dụ: mỗi sáng 8h).
   - Ví dụ: *"Hãy tổng hợp doanh thu tuần này và gửi qua email."*

4. **Cập nhật datamodel tự động**:
   - Khi **Cin7 cập nhật schema**, các sếp có thể chạy lại **template script** trên Peliqan để AI hiểu cấu trúc mới.
   - Link script: [Peliqan Help Center](https://help.peliqan.io/build-ai-agents-with-n8n-and-peliqan#block-2401aa9b387980cf8b2ff069588dd3dc).

5. **Optimize OpenAI API**:
   - Nếu AI trả lời chậm, các sếp có thể:
     - **Sử dụng mô hình nhỏ hơn** (`gpt-3.5-turbo` thay vì `gpt-4`).
     - **Giảm độ dài prompt** bằng cách viết System Message ngắn gọn hơn.
:::

---
## 📌 **Kết luận**
### **Workflow này giúp các sếp:**
✔ **Tự động hóa truy vấn ERP** mà không cần viết code.
✔ **Giảm thời gian tìm kiếm dữ liệu** từ **giờ xuống phút**.
✔ **Hoạt động 24/7** với AI trả lời chính xác.

### **Bước tiếp theo:**
1. **Đăng ký Peliqan** (miễn phí) và sync dữ liệu từ Cin7.
2. **Cài đặt n8n trên VPS** (khuyến nghị) và import workflow.
3. **Test với câu hỏi thực tế** và điều chỉnh System Message nếu cần.
4. **Tích hợp với Slack/Telegram** để AI hoạt động trong team.

---
### **🚀 Hãy bắt đầu ngay!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/7315)
👉 [Đăng ký Peliqan (mã giảm 20%)](https://peliqan.io) (mã: **N8NPELIQAN**)
👉 [Mua VPS cho n8n (50k/tháng)](https://tino.vn/vps-n8n?affid=388) (mã: **VPSN8N**)

**Chia sẻ workflow này với đồng nghiệp để tự động hóa công việc ERP của cả team!** 💡