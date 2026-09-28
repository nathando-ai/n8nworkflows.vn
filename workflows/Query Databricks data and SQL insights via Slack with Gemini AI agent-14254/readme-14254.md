---
title: "🤖 Tự Động Hỏi Đáp Dữ Liệu Databricks Trên Slack Với AI Gemini - Giải Pháp Tối Ưu Cho Analyst & DevOps"
description: "Tự động hóa việc phân tích SQL và truy vấn dữ liệu Databricks thông qua Slack với AI Gemini, tiết kiệm thời gian lên đến 80% cho các sếp phân tích dữ liệu và kỹ sư. Workflow này cho phép gửi câu hỏi SQL qua Slack, AI tự động phân tích schema, thực thi truy vấn và trả kết quả ngay lập tức."
slug: "tieu-dong-hoi-dap-databricks-slack-gemini"
tags: [n8n, automation, ai-chatbot, databricks, slack-integration, google-gemini, no-code]
keywords: [tự động hóa databricks slack, ai phân tích sql, gemini ai databricks, tự động hóa phân tích dữ liệu, slack bot sql, n8n workflow databricks]
---

# 🚀 **Tự Động Hỏi Đáp Dữ Liệu Databricks Trên Slack Với AI Gemini: Giải Pháp "Nó Làm Tất Cả" Cho Các Sếp**

### **Nỗi Đau Của Các Sếp Phân Tích Dữ Liệu & Kỹ Sư**
Các sếp phân tích dữ liệu và kỹ sư thường phải mất **giờ đồng hồ** để:
- **Tìm hiểu schema** của bảng Databricks để viết câu lệnh SQL chính xác.
- **Thực thi truy vấn** và phân tích kết quả thủ công.
- **Lặp lại quá trình** nếu câu lệnh sai hoặc dữ liệu không phù hợp.
- **Giao tiếp với team** qua Slack để yêu cầu hỗ trợ, làm chậm quá trình quyết định.

**Kết quả?** Thời gian phản hồi chậm, chi phí nhân sự cao, và khả năng sai sót cao do con người.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Với workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** phân tích SQL: AI tự động hiểu schema và viết truy vấn chính xác.
✅ **Trả lời câu hỏi SQL ngay lập tức** qua Slack: Gửi tin nhắn "Tôi muốn biết doanh thu của quý 2", AI trả lời trong giây lát.
✅ **Chính xác 100%**: Không còn lo lắng về syntax SQL sai hoặc truy vấn không hiệu quả.
✅ **Hoạt động 24/7**: Workflow chạy tự động, không phụ thuộc vào giờ làm việc của ai.
✅ **Cá nhân hóa**: AI nhớ lịch sử câu hỏi qua Redis, trả lời thông minh hơn theo từng lần tương tác.

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản Databricks** với quyền truy cập vào:
   - **Table ID** và **Warehouse ID** của bảng cần phân tích.
   - **Token API** (Bearer Token) để kết nối với Databricks.
📌 **Tài khoản Slack**:
   - **App Slack** được cấu hình với quyền `chat:write` và `commands`.
   - **Credentials Slack API** (đăng ký tại [Slack API](https://api.slack.com/)).
📌 **Google Gemini API**:
   - **API Key** từ [Google AI Studio](https://aistudio.google.com/).
📌 **Redis Server** (miễn phí hoặc tự host):
   - Để lưu trữ lịch sử chat của AI (cần `host`, `port`, `password`).
📌 **VPS cho n8n** (khuyến nghị):
   - Để workflow chạy ổn định 24/7.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- Tải file JSON từ [link gốc](https://n8n.io/workflows/14254).
- Trong n8n Editor, nhấn **Import** và chọn file JSON.
- Hoặc copy toàn bộ JSON và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **11 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: When Slack Message Received (slackTrigger)**
- **Cấu hình**:
  - Chọn **Slack API** trong credentials.
  - Thiết lập **Event Subscription URL** (URL của n8n khi Slack gửi tin nhắn).
  - Chọn **Event Type**: `message.im` (tin nhắn riêng tư) hoặc `message.channel` (tin nhắn nhóm).
  - **Filter**: Chỉ lấy tin nhắn có từ khóa `databricks`, `sql`, hoặc `analyze` (ví dụ: `databricks: show revenue Q2`).

##### **🔹 Node 2 & 3: Fetch Databricks Schema + Parse Table Schema (httpRequest + code)**
- **Cấu hình `Fetch Databricks Schema`**:
  - **Method**: `GET`.
  - **URL**: `https://<databricks-instance>/api/2.0/sql/warehouses/{warehouseId}/tables/{tableId}/schema`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer <YOUR_DATABRICKS_TOKEN>",
      "Content-Type": "application/json"
    }
    ```
  - **Node `Parse Table Schema` (Code)**:
    - Sử dụng JavaScript để extra schema thành JSON dễ đọc:
      ```javascript
      const schema = JSON.parse($input.all().json);
      return {
        json: {
          tableName: schema.tableName,
          columns: schema.columns.map(col => ({
            name: col.name,
            type: col.type,
            nullable: col.nullable
          }))
        }
      };
      ```

##### **🔹 Node 4: Set Databricks Config (set)**
- **Cấu hình**:
  - Điền **warehouseId** và **tableId** từ Databricks vào biến `$databricksConfig`.
  - Ví dụ:
    ```json
    {
      "warehouseId": "1234567890abcdef",
      "tableId": "table/1234567890abcdef",
      "schema": $input.all().json // Schema từ node trước
    }
    ```

##### **🔹 Node 5: SQL Data Analyst Agent (agent)**
- **Cấu hình AI Agent**:
  - **System Prompt** (cần chỉnh sửa để phù hợp với schema của các sếp):
    ```plaintext
    Bạn là một chuyên gia SQL phân tích dữ liệu Databricks. Hãy trả lời câu hỏi bằng cách:
    1. Viết câu lệnh SQL chính xác dựa trên schema của bảng {tableName}.
    2. Thực thi truy vấn và trả kết quả.
    3. Nếu câu hỏi không rõ, yêu cầu người dùng cụ thể hóa.
    ```
  - **Tools**:
    - Chọn **`Run Primary SQL Query`** (node sau) để AI có thể thực thi truy vấn.
  - **Memory**:
    - Kết nối với **Redis Chat Memory** (node 8) để AI nhớ lịch sử chat.

##### **🔹 Node 6: Gemini Model (lmChatGoogleGemini)**
- **Cấu hình**:
  - Chọn **Google Palm API** trong credentials.
  - **Model**: `gemini-pro`.
  - **Parameters**:
    ```json
    {
      "temperature": 0.7,
      "max_output_tokens": 1024
    }
    ```

##### **🔹 Node 7: Redis Chat Memory (memoryRedisChat)**
- **Cấu hình**:
  - Điền **host**, **port**, **password** của Redis.
  - **Key Prefix**: `databricks_chat_history`.

##### **🔹 Node 8: Run Primary SQL Query (httpRequestTool)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://<databricks-instance>/api/2.0/sql/statements`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer <YOUR_DATABRICKS_TOKEN>",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "statement": $input.all().json.sqlQuery,
      "warehouse_id": $databricksConfig.warehouseId
    }
    ```

##### **🔹 Node 9: If Output Valid (if)**
- **Cấu hình**:
  - **Condition**: Kiểm tra `$.error` trong output của SQL query.
  - Nếu **có lỗi**, chuyển sang **Post Error to Slack** (node 11).
  - Nếu **không lỗi**, chuyển sang **Post to Slack Channel** (node 4).

##### **🔹 Node 10 & 11: Post to Slack Channel / Post Error to Slack**
- **Cấu hình**:
  - Chọn **Slack API** trong credentials.
  - **Channel**: Điền tên channel (ví dụ: `#data-analytics`).
  - **Message Format**:
    - **Thành công**:
      ```json
      {
        "text": "Kết quả truy vấn:\n```$json.output```",
        "blocks": [
          {
            "type": "section",
            "text": { "type": "mrkdwn", "text": "Kết quả:*\n```$json.output```" }
          }
        ]
      }
      ```
    - **Lỗi**:
      ```json
      {
        "text": "Lỗi SQL:\n```$json.error```",
        "blocks": [
          {
            "type": "section",
            "text": { "type": "mrkdwn", "text": "❌ Lỗi:*\n```$json.error```" }
          }
        ]
      }
      ```

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tăng tính cá nhân hóa**:
   - Thêm **stickyNote** để ghi chú schema đặc biệt của bảng (ví dụ: `nullable` columns).
   - Ví dụ:
     ```json
     {
       "note": "Cột 'customer_id' không thể null, sử dụng WHERE clause khi cần."
     }
     ```

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để tự động gửi báo cáo tổng hợp qua Slack hàng ngày.

3. **Kết hợp với Google Sheets**:
   - Thêm node **Google Sheets** để lưu lịch sử câu hỏi và kết quả vào bảng Excel.

4. **Optimize AI Response**:
   - Chỉnh **system prompt** để AI trả lời ngắn gọn hơn (ví dụ: `Trả lời trong 3 câu`).
   - Thêm **tool** để AI có thể gọi API ngoài Databricks (ví dụ: API của Salesforce).

5. **Monitor Logs**:
   - Sử dụng **n8n Dashboard** để theo dõi workflow và logs của AI.

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, **tăng tốc độ phân tích dữ liệu**, và **giảm sai sót** nhờ AI Gemini. Các sếp chỉ cần:
1. **Cấu hình credentials** (Databricks, Slack, Gemini, Redis).
2. **Chỉnh sửa system prompt** phù hợp với schema của mình.
3. **Bật workflow** và bắt đầu tương tác qua Slack!

**Hành động ngay**: Import workflow, cấu hình và thử nghiệm với câu hỏi đầu tiên như:
> *"Databricks: Hãy cho tôi biết doanh thu của quý 2 theo khu vực."*

**Cần hỗ trợ?** Liên hệ với tác giả Abhi Vaar qua [Calendly](https://cal.com/abhi.vaar/15min) để tùy chỉnh workflow cho doanh nghiệp của các sếp!

---
:::tip[LƯU Ý CUỐI CÙNG]
- **Không cần code**: Workflow hoàn toàn tự động hóa, chỉ cần cấu hình.
- **Miễn phí**: N8n Community Edition hỗ trợ tất cả node này.
- **Scalable**: Dễ dàng mở rộng cho nhiều bảng Databricks.
:::

---
**Bắt đầu tự động hóa ngay hôm nay!** 🚀