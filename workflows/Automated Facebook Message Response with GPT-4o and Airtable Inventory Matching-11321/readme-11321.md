---
title: "🤖 **Tự Động Hóa Trả Lời Tin Nhắn Facebook Bằng GPT-4o + Kiểm Tra Hàng Tồn Khối Airtable (N8n)**"
description: "Workflow tự động hóa trả lời tin nhắn Facebook ngay lập tức bằng AI GPT-4o, kiểm tra hàng tồn kho trên Airtable và gửi phản hồi tự động. Giúp doanh nghiệp giảm thời gian hỗ trợ khách hàng từ 100% thủ công xuống còn 0%, đồng thời tăng trải nghiệm người dùng và giảm tải cho đội ngũ support."
slug: "tự-dộng-hoa-facebook-message-gpt-4o-airtable"
tags: [n8n, automation, ai-chatbot, facebook-messenger, airtable, gpt-4o, no-code]
keywords: [n8n workflow facebook, tự động hóa tin nhắn facebook, gpt-4o n8n, kiểm tra hàng tồn kho tự động, chatbot hỗ trợ khách hàng, airtable n8n]
---

# 🚀 **Tự Động Hóa Trả Lời Tin Nhắn Facebook Bằng AI GPT-4o + Kiểm Tra Hàng Tồn Khối Airtable**

## **📌 Nỗi Đau Của Doanh Nghiệp Khi Hỗ Trợ Khách Hàng Trên Facebook**
Hiện nay, hầu hết các doanh nghiệp phải **đọc và trả lời hàng trăm tin nhắn Facebook hàng ngày** để hỗ trợ khách hàng về:
- **Hàng tồn kho** (còn hàng không? hàng nào có sẵn?).
- **Thông tin sản phẩm** (giá, đặc điểm, cách sử dụng).
- **Đơn hàng** (trạng thái, thời gian giao).

**Kết quả?**
✅ **Thời gian phản hồi chậm** → Khách hàng mất niềm tin.
✅ **Sai sót trong thông tin** → Hàng tồn kho không chính xác.
✅ **Đội ngũ support bị quá tải** → Giảm hiệu suất làm việc.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quá trình** bằng AI GPT-4o + Airtable, giúp doanh nghiệp:
✔ **Trả lời tin nhắn ngay lập tức** (không cần con người).
✔ **Kiểm tra hàng tồn kho chính xác** từ Airtable.
✔ **Gửi phản hồi tự động** (có hàng/không có hàng).
✔ **Log tin nhắn lỗi** vào Google Sheets để phân tích sau.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** cho đội ngũ support.
- **Trả lời khách hàng trong giây lát** (không chờ đợi).
- **Giảm sai sót** do con người (AI kiểm tra chính xác hàng tồn kho).
- **Hỗ trợ 24/7** (không cần nhân viên làm đêm).
- **Dữ liệu khách hàng được theo dõi** (Google Sheets).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Sử Dụng**]
Để workflow hoạt động, các sếp cần chuẩn bị:
✅ **Tài khoản Facebook Business** (đã cấp quyền API).
✅ **Token API Airtable** (để truy cập bảng hàng tồn kho).
✅ **API Key Azure OpenAI** (để sử dụng GPT-4o).
✅ **Tài khoản Google Sheets** (để log tin nhắn lỗi).
✅ **Bảng Airtable** (đã cấu trúc dữ liệu sản phẩm: `name`, `stock`, `description`).
✅ **N8n Self-hosted** (để chạy workflow 24/7).
:::

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/11321](https://n8n.io/workflows/11321) (chọn **Export as JSON**).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
3. **Chọn workspace** (nếu có nhiều workspace) → Nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/11321](https://n8n.io/workflows/11321).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn **Paste JSON** → Dán mã.
3. **Chọn workspace** → Nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **17 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ là:

#### **🔹 Node 1: Trigger – Fetch New Facebook Messages (Every Hour)**
- **Cấu hình:**
  - **Schedule:** `Every hour` (hoặc tùy chỉnh theo nhu cầu).
  - **Credentials:** Chọn `facebookGraphApi` (đã cấu hình trước).
  - **Test run** để đảm bảo API hoạt động.

#### **🔹 Node 2 & 3: Fetch Facebook Conversation List & Messages**
- **Cấu hình:**
  - **Credentials:** Chọn `facebookGraphApi`.
  - **Fields cần lấy:**
    - `id` (ID cuộc trò chuyện).
    - `messages` (danh sách tin nhắn).
  - **Lưu ý:** Nếu API bị block, kiểm tra lại **token Facebook** và **quyền API** (cần quyền `pages_read_engagement`, `pages_show_list`).

#### **🔹 Node 4 & 5: AI – Extract Product & Customer Intent (GPT-4o)**
- **Cấu hình:**
  - **Credentials:** Chọn `azureOpenAiApi`.
  - **Model:** `gpt-4o` (đã cấu hình trong node `Configure GPT-4o — Message Classification Model`).
  - **Prompt mẫu (cần chỉnh sửa):**
    ```json
    {
      "input": "$json.message.text",
      "instructions": "Extract the product name and customer intent from this message. Return structured JSON with keys: 'product_name', 'customer_intent', 'confidence_score'."
    }
    ```
  - **Test run** với tin nhắn mẫu:
    ```
    "Tôi muốn mua áo thun Nike size M, có hàng không?"
    ```
    → **Kết quả mong đợi:**
    ```json
    {
      "product_name": "Áo thun Nike",
      "customer_intent": "Mua hàng",
      "confidence_score": 0.95
    }
    ```

#### **🔹 Node 6 & 7: Fetch Inventory Records from Airtable**
- **Cấu hình:**
  - **Credentials:** Chọn `airtableTokenApi`.
  - **Base ID & Table Name:** Điền vào `baseId` và `tableName` (tìm trong URL Airtable).
  - **Fields cần lấy:** `name`, `stock`, `description`.
  - **Lưu ý:** Nếu bảng Airtable lớn, **lọc theo `stock > 0`** để tiết kiệm thời gian.

#### **🔹 Node 8 & 9: Merge AI Output With Inventory Dataset**
- **Cấu hình:**
  - **Merge type:** `Array` (để kết hợp danh sách sản phẩm từ Airtable với kết quả AI).
  - **Test run** để kiểm tra dữ liệu hợp nhất.

#### **🔹 Node 10 & 11: AI – Match Requested Product in Inventory (GPT-4o)**
- **Cấu hình:**
  - **Credentials:** Chọn `azureOpenAiApi`.
  - **Model:** `gpt-4o`.
  - **Prompt mẫu (cần chỉnh sửa):**
    ```json
    {
      "input": {
        "customer_query": "$json.product_name",
        "inventory_list": "$json.inventory"
      },
      "instructions": "Check if the product '$customer_query' exists in the inventory list. Return a structured JSON with keys: 'product_found', 'product_details', 'reply_message'."
    }
    ```
  - **Test run** với tin nhắn:
    ```
    "Áo thun Nike size M"
    ```
    → **Kết quả mong đợi:**
    ```json
    {
      "product_found": true,
      "product_details": {
        "name": "Áo thun Nike Size M",
        "stock": 50,
        "description": "Áo thun Nike chất lượng cao, size M"
      },
      "reply_message": "Áo thun Nike Size M có hàng, số lượng còn 50. Bạn muốn mua không?"
    }
    ```

#### **🔹 Node 12: Check If Product Exists (If Condition)**
- **Cấu hình:**
  - **If condition:** `$json.product_found === true`.
  - **Nếu true** → Đi đến node `Send Facebook Reply — Product Found`.
  - **Nếu false** → Đi đến node `Send Facebook Reply — Product Not Found`.

#### **🔹 Node 13 & 14: Send Facebook Reply**
- **Cấu hình:**
  - **Credentials:** Chọn `facebookGraphApi`.
  - **Message template:**
    - **Nếu có hàng:**
      ```
      "Áo thun Nike Size M có hàng, số lượng còn 50. Bạn muốn mua không? 😊"
      ```
    - **Nếu không có hàng:**
      ```
      "Xin lỗi, áo thun Nike Size M hiện không có hàng. Bạn có thể xem các size khác hoặc theo dõi sản phẩm này để được thông báo khi có hàng. 😢"
      ```
  - **Test run** để đảm bảo tin nhắn được gửi đúng.

#### **🔹 Node 15: Log Invalid Records to Google Sheet**
- **Cấu hình:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name:** Điền tên sheet (ví dụ: `Facebook_Invalid_Messages`).
  - **Fields cần log:**
    - `message_id`
    - `message_text`
    - `timestamp`
    - `reason` (ví dụ: "Invalid structure", "No product found")
  - **Lưu ý:** Sheet này sẽ **tự động cập nhật** khi có tin nhắn lỗi.

#### **🔹 Node 16: Validate Record Structure (If Condition)**
- **Cấu hình:**
  - **If condition:** `$json.message.id && $json.message.text`.
  - **Nếu false** → Đi đến node `Log Invalid Records to Google Sheet`.
  - **Nếu true** → Tiếp tục xử lý.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test run** với tin nhắn mẫu (ví dụ: "Áo thun Nike size M").
2. **Kiểm tra:**
   - AI có nhận diện sản phẩm không?
   - Airtable có trả về hàng tồn kho chính xác không?
   - Tin nhắn tự động có được gửi không?
3. **Nếu hoạt động bình thường** → Nhấn **Active** để workflow chạy tự động hàng giờ.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tăng Tính Mạnh Cho AI**
- **Chỉnh sửa prompt** để AI hiểu rõ hơn:
  ```json
  {
    "instructions": "You are a customer support AI. Extract the product name and intent from the message. Handle typos, slang, and unclear text. Return structured JSON with high accuracy."
  }
  ```
- **Sử dụng LangChain Agent** để AI tự động cải tiến prompt.

### **2. Gửi Báo Cáo Hàng Ngày**
- **Thêm node Schedule Trigger** để gửi báo cáo hàng tồn kho qua **Slack/Email**:
  ```json
  {
    "operation": "sendEmail",
    "to": "support@example.com",
    "subject": "Báo cáo hàng tồn kho tự động",
    "body": "Danh sách sản phẩm còn hàng dưới 10 đơn vị:\n$json.inventory_low_stock"
  }
  ```

### **3. Kết Nối Với CRM (Zoho/HubSpot)**
- **Thêm node Zoho/HubSpot** để cập nhật thông tin khách hàng khi họ mua hàng.
- **Ví dụ:**
  ```json
  {
    "operation": "createContact",
    "firstName": "$json.customer_name",
    "email": "$json.customer_email",
    "notes": "Khách hàng đã mua sản phẩm: $json.product_name"
  }
  ```

### **4. Log Tin Nhắn Lỗi Vào Database**
- Thay vì Google Sheets, **sử dụng PostgreSQL/MySQL** để lưu log tin nhắn lỗi:
  ```json
  {
    "operation": "insert",
    "table": "facebook_invalid_messages",
    "data": {
      "message_id": "$json.message.id",
      "message_text": "$json.message.text",
      "timestamp": "$json.timestamp",
      "reason": "$json.reason"
    }
  }
  ```

### **5. Cập Nhật Hàng Tồn Kho Tự Động**
- **Thêm node Airtable** để tự động cập nhật số lượng hàng khi có đơn hàng mới:
  ```json
  {
    "operation": "update",
    "recordId": "$json.product_id",
    "fields": {
      "stock": "$json.new_stock"
    }
  }
  ```

---

## **📌 Kết Luận**
Workflow này **giải quyết hoàn toàn vấn đề hỗ trợ khách hàng trên Facebook** bằng cách:
✅ **Tự động hóa trả lời** trong giây lát.
✅ **Kiểm tra hàng tồn kho chính xác** từ Airtable.
✅ **Log tin nhắn lỗi** để phân tích sau.
✅ **Hoạt động 24/7** mà không cần con người.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình API** (Facebook, Airtable, Azure OpenAI).
3. **Test run** với tin nhắn mẫu.
4. **Active workflow** và **giảm tải cho đội ngũ support** của mình!

**🚀 Cần hỗ trợ thêm?** Đăng ký **khóa học tự động hóa n8n** tại [n8n.vn](https://n8n.vn) để học cách xây dựng workflow chuyên nghiệp!