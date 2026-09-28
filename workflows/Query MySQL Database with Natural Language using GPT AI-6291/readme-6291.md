---
title: "🔍 Tự Động Hỏi Đáp Câu Hỏi Tiếng Việt Với Cơ Sở Dữ Liệu MySQL Bằng GPT AI - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn giúp các sếp chuyển đổi câu hỏi tiếng Việt thành truy vấn SQL thông minh, trả kết quả từ cơ sở dữ liệu MySQL chỉ bằng một tin nhắn. Giảm thiểu 90% thời gian tìm kiếm thủ công, tối ưu hóa công việc phân tích dữ liệu."
slug: "tự-dộng-hỏi-dáp-mysql-bằng-gpt-ai"
tags: [n8n, automation, ai-rag, mysql, openai, no-code]
keywords: [n8n workflow mysql, tự động hóa hỏi đáp cơ sở dữ liệu, gpt-4.1-mini tự động hóa, query sql bằng tiếng việt, ai agent cho mysql]
---

# 🚀 **Hỏi Đáp Cơ Sở Dữ Liệu MySQL Bằng Tiếng Việt - Không Cần Code**

### **Giải pháp cho các sếp bị "chìm" trong biển số liệu**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để viết truy vấn SQL phức tạp, tìm kiếm dữ liệu trong cơ sở dữ liệu MySQL, hoặc phân tích báo cáo thủ công. Thậm chí, nhiều câu hỏi đơn giản như *"Hãy cho tôi biết doanh thu tháng 12/2023 của khách hàng ở TP.HCM"* cũng phải mất nhiều bước:
1. Viết SQL chính xác.
2. Chạy query.
3. Lọc và tổng hợp kết quả.
4. Tránh lỗi syntax hoặc logic.

**Workflow này giải quyết tất cả bằng một tin nhắn tiếng Việt đơn giản!** AI sẽ tự động:
✅ **Chuyển đổi câu hỏi tiếng Việt → SQL chính xác**
✅ **Trả kết quả trực tiếp từ MySQL**
✅ **Ghi nhớ lịch sử 5 câu hỏi trước (nâng cao trải nghiệm)**
✅ **Hoạt động 24/7 trên VPS riêng (không phụ thuộc vào máy tính cá nhân)**

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** cho công việc phân tích dữ liệu thủ công.
- **Giảm thiểu lỗi** do viết SQL sai syntax hoặc logic.
- **Truy vấn linh hoạt** mà không cần biết SQL.
- **Hoạt động liên tục** trên VPS, không phụ thuộc vào thời gian làm việc.
- **Cá nhân hóa** với lịch sử câu hỏi (AI nhớ 5 câu hỏi trước).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với **API Key** (để kết nối với GPT-4.1-mini).
2. **Cơ sở dữ liệu MySQL** (các sếp có thể dùng MySQL trên VPS hoặc máy chủ nội bộ).
3. **Thông tin kết nối MySQL**:
   - Host (ví dụ: `localhost` hoặc IP VPS).
   - Port (thường là `3306`).
   - Tên người dùng và mật khẩu.
   - Tên cơ sở dữ liệu (cần thay thế trong node `SQL DB - List Tables and Schema`).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/6291) (nút "Export Workflow").
- **Nhấn "Import"** trong n8n Editor (trang chủ).
- **Hoặc copy toàn bộ JSON** và dán vào ô "Import Workflow" trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình như sau:

##### **A. Cấu hình OpenAI API Key**
- **Node**: `OpenAI Chat Model` (type: `lmChatOpenAi`).
- **Hành động**:
  1. Nhấn vào node → Tab **"Credentials"**.
  2. Chọn hoặc tạo **credentials mới** với tên `openAiApi`.
  3. Điền **API Key** từ tài khoản OpenAI vào ô `apiKey`.
  4. **Model**: Đã mặc định là `gpt-4.1-mini` (có thể thay đổi nếu cần).

##### **B. Cấu hình kết nối MySQL**
Có **2 node MySQL** cần cấu hình:
1. **Node**: `SQL DB - List Tables and Schema` (type: `mySqlTool`).
   - **Query**: Thay thế `"your_query_name"` bằng **tên cơ sở dữ liệu thực tế** của các sếp (ví dụ: `SELECT * FROM information_schema.tables WHERE table_schema = 'tên_cơ_sở_dữ_liệu'`).
   - **Credentials**:
     - Nhấn vào node → Tab **"Credentials"**.
     - Tạo hoặc chọn **credentials mới** (ví dụ: `mysqlCredentials`).
     - Điền:
       - **Host**: `localhost` hoặc IP VPS.
       - **Port**: `3306`.
       - **Database**: Tên cơ sở dữ liệu (đã thay thế ở trên).
       - **User** và **Password**: Tài khoản MySQL của các sếp.

2. **Node**: `Execute a SQL query in MySQL` (type: `mySqlTool`).
   - **Credentials**: Sử dụng cùng **credentials** như node trên (`mysqlCredentials`).
   - **Query**: Node này sẽ tự động nhận **SQL từ AI Agent**, không cần chỉnh sửa.

##### **C. Cấu hình AI Agent**
- **Node**: `AI Agent` (type: `agent`).
  - **Lưu ý**:
    - Agent sẽ tự động **tạo SQL** từ câu hỏi tiếng Việt.
    - **Session Memory** (node `Simple Memory`) mặc định lưu **5 câu hỏi trước**. Nếu cần thay đổi, các sếp có thể chỉnh số lượng trong tab **"Parameters"** của node `memoryBufferWindow`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** và gửi một **câu hỏi tiếng Việt** vào node `When chat message received` (ví dụ: *"Hãy cho tôi biết doanh thu tháng 12/2023 của khách hàng ở TP.HCM"*).
   - Kiểm tra kết quả trả về từ MySQL.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH SỬ DỤNG HIỆU QUẢ NHẤT]
- **Kết hợp với Slack/Telegram**:
  Thay vì sử dụng node `chatTrigger`, các sếp có thể kết nối với **Slack** hoặc **Telegram** để nhận câu hỏi qua channel. Cách làm:
  1. Thêm node `n8n-nodes-slack.webhook` hoặc `n8n-nodes-telegram.webhook`.
  2. Cấu hình webhook trong Slack/Telegram và gắn vào node `When chat message received`.

- **Lưu log câu hỏi và kết quả**:
  Thêm node `n8n-nodes-base.stickyNote` để ghi lại **lịch sử câu hỏi** và **kết quả SQL** vào một file hoặc Google Sheets. Ví dụ:
  ```json
  {
    "name": "Log Query Results",
    "type": "stickyNote",
    "parameters": {
      "content": "Câu hỏi: {{ $json["question"] }}\nKết quả SQL: {{ $json["sqlQuery"] }}\nKết quả: {{ $json["result"] }}"
    }
  }
  ```

- **Tối ưu hóa AI Agent**:
  - Nếu muốn **trả kết quả chi tiết hơn**, thay đổi model OpenAI từ `gpt-4.1-mini` sang `gpt-4` (tuy nhiên chi phí cao hơn).
  - Thêm **prompt custom** vào node `lmChatOpenAi` để hướng dẫn AI trả lời cụ thể hơn (ví dụ: yêu cầu AI trả kết quả dưới dạng bảng).

- **Báo cáo định kỳ**:
  Thêm node `n8n-nodes-base.schedule` để chạy **báo cáo tự động** hàng ngày/tuần. Ví dụ:
  ```json
  {
    "name": "Daily Report",
    "type": "schedule",
    "parameters": {
      "cron": "0 0 * * *" // Chạy hàng ngày lúc 00:00
    }
  }
  ```
  Sau đó kết nối với node `mySqlTool` để lấy dữ liệu và gửi qua email (node `n8n-nodes-base.email`).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa hoàn toàn** công việc phân tích dữ liệu MySQL mà không cần viết một dòng code. Bằng cách chỉ cần **gửi một tin nhắn tiếng Việt**, AI sẽ tự động:
✔ **Chuyển đổi câu hỏi → SQL chính xác**.
✔ **Trả kết quả từ MySQL**.
✔ **Ghi nhớ lịch sử** để tương tác thông minh hơn.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình OpenAI + MySQL.
3. **Test với câu hỏi đầu tiên** và trải nghiệm sự **tiện lợi tuyệt đối**!

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) để tự động hóa hoàn toàn!