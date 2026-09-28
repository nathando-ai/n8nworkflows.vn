---
title: "🤖 Query Thông Tin Credentials n8n Bằng AI SQL Agent – Tự Động Hóa Khám Phá Workflow Miễn Code"
description: "Workflow này giúp các sếp tự động hóa việc tra cứu, phân tích và quản lý thông tin credentials trong các workflow n8n thông qua AI SQL Agent. Giúp tiết kiệm thời gian lên tới 80% khi tìm hiểu cấu trúc workflow, tránh rủi ro mất mát thông tin nhạy cảm, và tối ưu hóa việc sử dụng tài nguyên."
slug: "query-credentials-n8n-ai-sql-agent"
tags: [n8n, automation, ai-agent, sql-query, no-code, self-hosted]
keywords: [n8n workflow tự động hóa, tra cứu credentials n8n, ai sql agent, quản lý workflow n8n, tiết kiệm thời gian tự động hóa]
---

# 🚀 Query Thông Tin Credentials n8n Bằng AI SQL Agent – Giải Pháp Tự Động Hóa Cho Các Sếp

## **💡 Nỗi Đau Của Các Sếp Khi Quản Lý Workflow n8n**
Làm việc với hàng chục, thậm chí hàng trăm workflow trên n8n, các sếp thường gặp phải những vấn đề sau:
- **Tốn thời gian quá nhiều** để tra cứu thông tin credentials (API keys, token, sheet names...) trong từng workflow.
- **Rủi ro mất mát thông tin** khi không có bản đồ toàn cảnh về cách các credentials được sử dụng.
- **Không biết cách tối ưu hóa** việc sử dụng tài nguyên (ví dụ: workflow nào đang sử dụng OpenAI API nhiều nhất).
- **Không thể tự động hóa việc phân tích** để trả lời câu hỏi như: *"Có bao nhiêu workflow sử dụng Slack và Google Sheets cùng lúc?"*

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách:
✅ **Tự động hóa việc thu thập** thông tin credentials từ tất cả workflows n8n.
✅ **Sử dụng AI SQL Agent** để trả lời các câu hỏi phức tạp về cấu trúc workflow.
✅ **Lưu trữ an toàn** thông tin (không bao giờ lộ ra credential thực tế).
✅ **Hoạt động 24/7** trên VPS tự host, không phụ thuộc vào phiên làm việc.

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công.
- **Tránh rủi ro lộ credentials** nhờ lưu trữ an toàn trong SQLite (tạm thời).
- **Tối ưu hóa tài nguyên** bằng cách biết workflow nào đang sử dụng API đắt tiền nhất.
- **Tra cứu linh hoạt** với AI: *"Hãy cho tôi biết tất cả workflows sử dụng AI nhưng không dùng OpenAI!"*
- **Hoạt động liên tục** trên VPS, không cần phải mở máy.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **n8n API Key**:
   - Tạo từ [n8n Cloud](https://n8n.io/) hoặc [Self-hosted](https://docs.n8n.io/hosting/installation/installation-on-premise/).
   - **Lưu ý**: API key chỉ truy cập được workflows trong scope của nó.
2. **OpenAI API Key** (nếu muốn sử dụng AI chat):
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và thêm vào n8n dưới tên `openAiApi`.
3. **VPS tự host n8n** (khuyến nghị):
   - Để workflow chạy 24/7 ổn định.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
4. **Node LangChain** (nếu chưa có):
   - Cài đặt từ [n8n Marketplace](https://marketplace.n8n.io/) (tìm kiếm `@n8n/n8n-nodes-langchain`).
:::

---

## 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor).
2. Nhấp vào **Import Workflow** và chọn file `2347.json` (tải từ [link gốc](https://n8n.io/workflows/2347)).
   **Hoặc**:
   - Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/2347) và paste vào **Import Workflow**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này được chia thành **2 bước chính**:
- **Bước 1**: Thu thập và lưu thông tin credentials vào SQLite (tạm thời).
- **Bước 2**: Sử dụng AI SQL Agent để tra cứu thông tin.

#### **🔹 Bước 1: Populate Database (Node "Save to Database")**
- **Node "Save to Database"** (type: `code`) sẽ:
  - Query API n8n để lấy tất cả workflows.
  - Trích xuất danh sách credentials từ các node trong workflow.
  - Lưu vào SQLite **tạm thời** (nếu n8n restart, database sẽ mất).
- **Lưu ý**:
  - **Không bao giờ lưu credentials thực tế**, chỉ lưu tên và loại credentials (ví dụ: `slackToken`, `googleSheetsApi`).
  - Nếu muốn lưu dài hạn, các sếp cần **cài đặt SQLite trên VPS** và cấu hình đường dẫn tương ứng trong node `code`.

#### **🔹 Bước 2: Query Database với AI (Node "Workflow Credentials Helper Agent")**
- **Node "Chat Trigger"** (type: `chatTrigger`) sẽ khởi động AI SQL Agent.
- **Node "OpenAI Chat Model"** (type: `lmChatOpenAi`) cần:
  - **Credentials**: Chọn `openAiApi` (đã thêm OpenAI API Key trước đó).
  - **Model**: Chọn `gpt-4` hoặc `gpt-3.5-turbo` (tùy chọn).
- **Node "Workflow Credentials Helper Agent"** (type: `agent`) sẽ:
  - Hiểu yêu cầu của người dùng (ví dụ: *"Workflow nào sử dụng Slack và Google Calendar?"*).
  - Query SQLite để trả lời.
- **Lưu ý**:
  - **Không cần cấu hình gì thêm** nếu đã import workflow chính xác.
  - AI sẽ tự động hiểu các từ khóa như `slack`, `airtable`, `openai`, `googleSheets`, etc.

#### **🔹 Node "n8n" (type: `n8n`)**
- **Credentials**: Chọn `n8nApi` (API Key đã tạo trước đó).
- **Lưu ý**:
  - Nếu API Key không đúng, workflow sẽ **không lấy được dữ liệu workflows**.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **Test Workflow** để chạy bước 1 (populate database).
   - Sau đó, nhấp vào **Test Workflow** của bước 2 (AI chat) và gõ câu hỏi như:
     - *"Hãy cho tôi biết tất cả workflows sử dụng Slack và Google Calendar."*
     - *"Workflow nào có tên chứa 'AI' nhưng không dùng OpenAI?"*
2. **Bật Active**:
   - Sau khi test thành công, nhấp **Active Workflow** để chạy liên tục.

---

## ✍️ Mẹo & Gợi Ý Nâng Cao
:::info[CÁCH SỬ DỤNG HIỆU QUẢ]
1. **Lưu trữ SQLite dài hạn**:
   - Thay vì SQLite tạm thời, các sếp có thể **cài đặt SQLite trên VPS** và cấu hình đường dẫn trong node `code`.
   - Hướng dẫn cài SQLite trên Linux:
     ```bash
     sudo apt update && sudo apt install sqlite3
     ```
   - Trong node `code`, thay `new Database()` bằng:
     ```javascript
     const Database = require('sqlite3').verbose();
     const db = new Database('./credentials.db');
     ```

2. **Kết nối với Slack/Telegram**:
   - Sau khi AI trả lời, các sếp có thể **gửi kết quả tự động** đến Slack/Telegram bằng node `slack` hoặc `telegramBot`.
   - Ví dụ:
     ```json
     {
       "node": "slack",
       "credentials": "slackToken",
       "text": "{{ $json.output.text }}"
     }
     ```

3. **Lưu log hoạt động**:
   - Thêm node `set` sau AI để lưu lịch sử câu hỏi và trả lời vào Google Sheets hoặc Airtable.
   - Cách cấu hình:
     ```json
     {
       "node": "set",
       "propertyName": "log",
       "values": {
         "question": "{{ $json.input.question }}",
         "answer": "{{ $json.output.text }}",
         "timestamp": "{{ $json.$timestamp }}"
       }
     }
     ```

4. **Tối ưu hóa AI**:
   - Cập nhật **prompt** trong node `lmChatOpenAi` để AI trả lời chính xác hơn:
     ```json
     {
       "node": "lmChatOpenAi",
       "prompt": "You are an expert in n8n workflows. Answer questions about credentials used in workflows. Only use data from the SQLite database. If you don't know, say 'I don't have data for that.'"
     }
     ```

5. **Báo cáo định kỳ**:
   - Sử dụng node `set` + `email` để gửi báo cáo tuần/month về:
     - Workflow nào đang sử dụng nhiều API nhất.
     - Credentials nào chưa được sử dụng (để dọn dẹp).
:::

---

## 📌 Kết Luận
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa việc quản lý credentials** trong n8n.
✔ **Tiết kiệm thời gian** lên tới 80% so với cách làm thủ công.
✔ **Tối ưu hóa tài nguyên** bằng cách biết cách sử dụng API hiệu quả.
✔ **Hoạt động 24/7** trên VPS, không phụ thuộc vào phiên làm việc.

**Hành động ngay**:
1. **Import workflow** và cấu hình API Key.
2. **Test với câu hỏi** như *"Workflow nào sử dụng Slack và Google Sheets?"*.
3. **Tự động hóa quản lý** credentials trong doanh nghiệp!

---
**🔗 Link gốc**: [https://n8n.io/workflows/2347](https://n8n.io/workflows/2347)
**📧 Liên hệ tác giả**: [hello@jimle.uk](mailto:hello@jimle.uk) (Jim Leuk – Chuyên gia tự động hóa AI tại UK)