---
title: "🔍 Chuyển Văn Bản Sang Query SQL Tự Động + Vẽ Biểu Đồ: Tự Động Hóa Thông Minh Cho Data Analyst"
description: "Workflow này tự động chuyển câu hỏi tiếng Việt thành SQL Query chính xác, phân tích dữ liệu và vẽ biểu đồ trực quan - giúp các sếp tiết kiệm 100 giờ/năm trong phân tích báo cáo và dự báo thị trường."
slug: "chuyen-van-ban-sang-sql-query-tu-dong"
tags: [n8n, automation, no-code, ai, sql, data-analysis, langchain, postgres, deepseek]
keywords: [n8n workflow tự động hóa SQL, chuyển văn bản thành query, phân tích dữ liệu tự động, vẽ biểu đồ từ SQL, AI cho data analyst, LangChain n8n]
---

# 🚀 **Tự Động Hóa "Nói Với Dữ Liệu": Chuyển Văn Bản Sang Query SQL + Vẽ Biểu Đồ Trực Quan**

### **Nỗi Đau Của Các Sếp Trong Phân Tích Dữ Liệu**
Hàng ngày, các sếp và data analyst phải:
- **Gõ thủ công hàng chục query SQL** để trả lời câu hỏi từ CEO, marketing hay finance.
- **Mất thời gian vô ích** trong việc debug syntax, điều chỉnh logic, và tìm kiếm dữ liệu.
- **Không thể tự động hóa báo cáo định kỳ** vì mỗi câu hỏi lại khác nhau.
- **Bị giới hạn bởi kiến thức SQL** của mình, dẫn đến kết quả không chính xác.

**Workflow này giải quyết tất cả!** Dùng AI (DeepSeek + LangChain) để:
✅ **Chuyển câu hỏi tiếng Việt → Query SQL chính xác 100%**
✅ **Trích xuất dữ liệu từ PostgreSQL tự động**
✅ **Vẽ biểu đồ trực quan từ kết quả phân tích**
✅ **Lưu lịch sử và cho phép truy vấn lại bất kỳ lúc nào**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 **không bị gián đoạn**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) với cấu hình tối thiểu:
- **CPU:** 2 nhân (x86_64)
- **RAM:** 4GB+
- **Đĩa:** 20GB SSD
- **API Key:** OpenAI/DeepSeek (miễn phí cho 10k token/ngày)

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo ổn định cho LangChain)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 50-70% thời gian** trong phân tích dữ liệu so với cách thủ công.
- **Query SQL chính xác** ngay từ lần đầu, giảm thiểu lỗi syntax và logic.
- **Báo cáo tự động hóa** với biểu đồ động (line chart, bar chart) từ dữ liệu PostgreSQL.
- **Truy vấn lại dữ liệu** bất kỳ lúc nào bằng cách nhập câu hỏi mới.
- **Không cần biết SQL** - chỉ cần nói với AI là nó làm.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Dữ liệu cơ sở dữ liệu PostgreSQL**
- **Tài khoản PostgreSQL** (Host, Port, Username, Password, Database Name).
- **Schema đã tồn tại** (workflow sẽ tự động trích xuất danh sách bảng và cột).

### **2. API Key cho AI**
- **DeepSeek API Key** (hoặc OpenAI API Key nếu thay thế node `lmChatOpenAi`):
  - Đăng ký tại: [https://deepseek.com](https://deepseek.com) (miễn phí cho 10k token/ngày).
  - **Mô hình AI sử dụng:** `deepseek-chat` (tương đương GPT-4 nhưng hiệu suất cao hơn).

### **3. File Schema (tự động tạo)**
- Workflow sẽ **tự động lưu schema** của database vào file JSON trong folder `./data/schema.json`.
- **Không cần chuẩn bị sẵn** - workflow sẽ tạo ra khi chạy lần đầu.

### **4. Node LangChain (n8n-nodes-langchain)**
- Cài đặt **n8n-nodes-langchain** (nếu chưa có):
  ```bash
  n8n install @n8n/n8n-nodes-langchain
  ```

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/3497](https://n8n.io/workflows/3497) (chọn **Export JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. **Không cần chỉnh sửa** nếu đã có tất cả credentials.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/3497](https://n8n.io/workflows/3497) (chọn **Raw JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.
3. **Không cần chỉnh sửa** nếu đã có tất cả credentials.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **A. Cấu hình PostgreSQL**
- **Node "List all tables in a database"** và **"Schema Extractor"** cần:
  - **Host:** `your-postgres-host.com`
  - **Port:** `5432` (mặc định)
  - **Database:** `your-database-name`
  - **Username/Password:** Điền từ tài khoản PostgreSQL của các sếp.
  - **SSL Mode:** `require` (nếu database yêu cầu).

- **Node "Final SQL result"** cũng cần cùng cấu hình trên.

#### **B. Cấu hình AI (DeepSeek/OpenAI)**
- **Node "deepseek-chat"** (hoặc `lmChatOpenAi`):
  - **API Key:** Điền từ API Key DeepSeek/OpenAI.
  - **Model:** `deepseek-chat` (hoặc `gpt-4` nếu dùng OpenAI).
  - **Temperature:** `0.7` (giá trị mặc định, có thể điều chỉnh).

#### **C. Cấu hình File Schema**
- **Node "Load the schema from the local file"** và **"Save file locally"**:
  - **File Path:** `./data/schema.json` (workflow sẽ tự tạo folder này).
  - **File Mode:** `write` (lưu schema) và `read` (đọc schema).

#### **D. Cấu hình Node "Chat Trigger"**
- **Trigger Type:** Chọn **Manual Trigger** (nếu muốn kích hoạt thủ công).
- **Hoặc:** Kết nối với **Webhook** (ví dụ: từ Slack/Telegram) để tự động hóa.

#### **E. Cấu hình Node "Agent" (AI Logic)**
- **Node "AI Agent"** và **"plot agent"**:
  - **Memory Buffer:** Chọn **Window Buffer Memory** (đã cấu hình sẵn).
  - **Output Parser:** Chọn **Structured Output Parser** (để trả về JSON chuẩn).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Nhấn **Run Workflow** và nhập câu hỏi ví dụ:
     - *"Hãy cho tôi biết doanh thu trung bình theo tháng trong năm 2023."*
     - *"Vẽ biểu đồ so sánh doanh thu giữa sản phẩm A và B trong quý 1-2."*
   - Kiểm tra kết quả trong **Final SQL result** và **plot agent**.

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển **Active** sang **ON**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối Với Slack/Telegram**
- Thêm **node Webhook** sau **Chat Trigger** để nhận câu hỏi từ Slack/Telegram.
- **Cách làm**:
  - Tạo **Incoming Webhook** trên Slack/Telegram.
  - Cấu hình node **Webhook** trong n8n với URL của Slack/Telegram.

### **2. Lưu Lịch Sử Truy Vấn**
- Thêm **node Database** (PostgreSQL) để lưu lịch sử câu hỏi và kết quả.
- **Cấu trúc bảng lưu trữ**:
  ```sql
  CREATE TABLE query_history (
    id SERIAL PRIMARY KEY,
    question TEXT,
    sql_query TEXT,
    result JSONB,
    created_at TIMESTAMP DEFAULT NOW()
  );
  ```

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **node Schedule** (n8n-nodes-base.schedule) để chạy workflow hàng ngày/tuần.
- **Ví dụ**: Tự động gửi báo cáo doanh thu hàng tháng qua email.

### **4. Tối Ưu Hóa Query SQL**
- **Node "Structured Output Parser"** có thể được điều chỉnh để trả về **JSON chuẩn** cho việc phân tích thêm.
- **Mô tả JSON mẫu**:
  ```json
  {
    "query": "SELECT AVG(revenue) FROM sales WHERE month = '2023-01'",
    "result": [{"avg_revenue": 1500000}],
    "chart_type": "line"
  }
  ```

### **5. Sử Dụng Mô Hình AI Khác**
- Thay thế **DeepSeek** bằng **Mistral AI** hoặc **Gemini** (nếu có API Key).
- **Cách thay đổi**:
  - Thay node `deepseek-chat` thành `lmChatMistral` (nếu có node hỗ trợ).

---

## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm 100+ Giờ/Năm!**
Workflow này không chỉ **giải phóng thời gian** cho các sếp khỏi công việc lặp lại mà còn **tăng cường chính xác** trong phân tích dữ liệu. Bằng cách kết hợp **AI (DeepSeek), LangChain, và PostgreSQL**, nó biến các câu hỏi tiếng Việt thành **báo cáo trực quan** chỉ trong vài giây.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình PostgreSQL + API Key.
3. **Test với câu hỏi đầu tiên** và trải nghiệm sự thay đổi!

**Nếu có vấn đề**, các sếp có thể:
- **Comment dưới bài viết** để được hỗ trợ.
- **Tạo issue trên GitHub n8n** (nếu cần sửa đổi workflow).

---
**🚀 Chúc các sếp thành công với tự động hóa thông minh!** 🚀