---
title: "🚀 **Tự Động Hóa Quá Trình Nuôi Dưỡng Khách Hàng & Lấy Đánh Giá Tự Động Cho Gumroad (Notion + Email) - Khai Phóng 100% Không Code!**"
description: "Workflow này tự động chuyển đổi khách hàng mua hàng thành khách hàng trung thành, thu thập đánh giá tích cực và cập nhật thông tin vào Notion chỉ trong vài giây. Giúp các sếp tiết kiệm 10+ giờ/tháng và xây dựng mối quan hệ khách hàng chuyên nghiệp."
slug: "tieu-dong-hoa-nuoi-duong-khach-hang-gumroad-notion-email"
tags: [n8n, automation, gumroad, notion, email-marketing, no-code, testimonial-automation]
keywords: [n8n workflow gumroad, tự động hóa nuôi dưỡng khách hàng, lấy đánh giá tự động, notion + email automation, workflow cho creator]
---

# 🚀 **Tự Động Hóa Quá Trình Nuôi Dưỡng Khách Hàng & Lấy Đánh Giá Tự Động Cho Gumroad (Notion + Email)**

---

## **💡 Bạn đã bao giờ mệt mỏi vì phải:**
- **Gọi điện hoặc gửi email thủ công** để cảm ơn khách hàng sau khi mua hàng?
- **Quên theo dõi khách hàng** sau 3-7 ngày, khiến họ cảm thấy bị bỏ rơi?
- **Phải nhắc nhở khách hàng** để họ để lại đánh giá, nhưng lại không có thời gian?
- **Cập nhật thông tin khách hàng** vào Notion một cách rườm rà?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Chuyển đổi khách hàng mua hàng thành khách hàng trung thành** với chuỗi email cá nhân hóa.
✅ **Thu thập đánh giá tích cực** từ khách hàng một cách tự động.
✅ **Cập nhật tất cả thông tin** vào Notion để theo dõi và phân tích.
✅ **Gửi thông báo lỗi** nếu workflow bị gián đoạn.

---

### **🎯 Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng** cho việc nuôi dưỡng khách hàng và lấy đánh giá.
- **Tăng tỷ lệ chuyển đổi** với chuỗi email tự động hóa.
- **Cập nhật dữ liệu chính xác** vào Notion, không cần làm thủ công.
- **Tăng độ tin cậy** với khách hàng bằng cách nhắc nhở họ để lại đánh giá.
- **Hoạt động 24/7** mà không cần can thiệp của bạn.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gumroad** (để nhận webhook khi khách hàng mua hàng).
2. **Tài khoản Notion** (để lưu trữ thông tin khách hàng và đánh giá).
3. **Tài khoản Email** (Gmail, SendGrid, hoặc SMTP khác) để gửi email tự động.
4. **API Key của Notion** (để workflow có thể tạo và cập nhật database).
5. **Domain hoặc địa chỉ email** để xác thực gửi email (tránh bị đánh dấu là spam).
6. **Webhook URL của Gumroad** (để n8n nhận được thông báo khi có đơn hàng mới).
:::

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/8020) (hoặc copy JSON từ link trên).
2. **Mở n8n Editor** trên máy chủ của bạn.
3. **Nhấp vào "Import"** và chọn file JSON đã tải.
4. **Chọn "Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [đây](https://n8n.io/workflows/8020).
2. **Mở n8n Editor** và nhấp vào **"Import"** → **"Paste JSON"**.
3. **Chọn "Import"** để hoàn tất.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: Gumroad Sale (Webhook)**
- **Cấu hình:**
  - Đăng ký **webhook** trên Gumroad với URL:
    ```
    https://[your-n8n-domain]/webhook/gumroad-sale
    ```
  - Chọn **event**: `Order Created`.
  - **Tham số cần truyền:**
    - `order_id`
    - `customer_email`
    - `product_title`
    - `amount_paid`

#### **🔹 Node 2 & 10: Map Sale → Client & Map Testimonial (Function)**
- **Cấu hình:**
  - **Node "Map Sale → Client"** (Function):
    - **Code JavaScript** (sử dụng template dưới đây):
      ```javascript
      return {
        client: {
          email: $input.all()[0].json.customer_email,
          name: $input.all()[0].json.customer_name || "Khách hàng mới",
          product_purchased: $input.all()[0].json.product_title,
          purchase_date: $input.all()[0].json.created_at,
          purchase_amount: $input.all()[0].json.amount_paid,
          status: "Mua hàng"
        }
      };
      ```
  - **Node "Map Testimonial"** (Function):
    - **Code JavaScript** (sử dụng template dưới đây):
      ```javascript
      return {
        testimonial: {
          client_email: $input.all()[0].json.email,
          client_name: $input.all()[0].json.name,
          product_name: $input.all()[0].json.product_purchased,
          testimonial_text: $input.all()[0].json.testimonial_text,
          rating: $input.all()[0].json.rating,
          status: "Đã nhận đánh giá"
        }
      };
      ```

#### **🔹 Node 3 & 11: Notion — Create Client & Create Testimonial**
- **Cấu hình:**
  - **Database Notion:**
    - Tạo **2 database** riêng biệt:
      1. **"Khách Hàng"** (để lưu thông tin khách hàng).
      2. **"Đánh Giá"** (để lưu thông tin đánh giá).
  - **Tham số cần điền:**
    - **Database ID** (tìm trong URL của Notion khi mở database).
    - **Properties** (cấu trúc dữ liệu):
      - **Khách Hàng:**
        - `Email` (Text)
        - `Tên` (Text)
        - `Sản Phẩm Mua` (Text)
        - `Ngày Mua` (Date)
        - `Số Tiền` (Number)
        - `Trạng Thái` (Select: "Mua hàng" / "Đã nuôi dưỡng")
      - **Đánh Giá:**
        - `Email Khách Hàng` (Text)
        - `Tên Khách Hàng` (Text)
        - `Sản Phẩm` (Text)
        - `Nội Dung Đánh Giá` (Rich Text)
        - `Đánh Giá (Sao)` (Number)
        - `Trạng Thái` (Select: "Chưa nhận" / "Đã nhận")
  - **Example payload cho Notion:**
    ```json
    {
      "properties": {
        "Email": { "rich_text": [{ "text": "khachhang@example.com" }] },
        "Tên": { "rich_text": [{ "text": "Tên Khách Hàng" }] },
        "Sản Phẩm Mua": { "rich_text": [{ "text": "Sản Phẩm X" }] },
        "Ngày Mua": { "date": "2024-05-20" },
        "Số Tiền": { "number": 49900 },
        "Trạng Thái": { "select": { "name": "Mua hàng" } }
      }
    }
    ```

#### **🔹 Node 4, 6, 8, 12: Email — Delivery (Immediate), Tips (Day 3), Testimonial Ask (Day 7), Owner Notify**
- **Cấu hình:**
  - **Tài khoản Email:**
    - Sử dụng **Gmail** (đăng ký OAuth) hoặc **SendGrid/SMTP** khác.
  - **Nội dung email:**
    - **Email 1 (Gửi ngay sau mua hàng):**
      ```html
      <h2>Cảm ơn bạn đã mua sản phẩm!</h2>
      <p>Chúng tôi rất vui khi bạn đã chọn {{product_purchased}}.</p>
      <p>Chúng tôi sẽ liên lạc với bạn trong 3 ngày để chia sẻ một số mẹo hữu ích.</p>
      <p>Trân trọng,<br>Đội ngũ [Tên Công Ty]</p>
      ```
    - **Email 2 (Ngày 3):**
      ```html
      <h2>Mẹo hữu ích cho bạn!</h2>
      <p>Đây là một số mẹo để tối ưu hóa trải nghiệm với {{product_purchased}}:</p>
      <ul>
        <li>Mẹo 1: ...</li>
        <li>Mẹo 2: ...</li>
      </ul>
      <p>Nếu bạn có bất kỳ câu hỏi nào, đừng ngần ngại liên hệ với chúng tôi!</p>
      ```
    - **Email 3 (Ngày 7 - Yêu cầu đánh giá):**
      ```html
      <h2>Chia sẻ trải nghiệm của bạn!</h2>
      <p>Bạn đã sử dụng {{product_purchased}} như thế nào? Chúng tôi rất muốn biết ý kiến của bạn!</p>
      <p>Bạn có thể để lại đánh giá tại: <a href="[LINK ĐẶN GIÁ]">Đăng giá</a></p>
      <p>Cảm ơn bạn đã ủng hộ!</p>
      ```
    - **Email 4 (Thông báo cho chủ sở hữu):**
      ```html
      <h2>Bạn đã nhận được một đánh giá mới!</h2>
      <p>Khách hàng {{client_name}} ({{client_email}}) đã để lại đánh giá:</p>
      <blockquote>{{testimonial_text}}</blockquote>
      <p>Đánh giá: {{rating}}/5 sao</p>
      ```

#### **🔹 Node 5 & 7: Wait — 3 days & Wait — 7 days**
- **Cấu hình:**
  - Thời gian chờ **3 ngày** và **7 ngày** sẽ tự động tính từ khi khách hàng mua hàng.
  - **Không cần chỉnh sửa** nếu đã cấu hình đúng thời gian trong node.

#### **🔹 Node 9: Build Testimonial Link**
- **Cấu hình:**
  - **Function JavaScript** (sử dụng template dưới đây):
    ```javascript
    const testimonialLink = `https://your-gumroad-link.com/testimonial?email=${$input.all()[0].json.email}&product=${encodeURIComponent($input.all()[0].json.product_purchased)}`;
    return { testimonial_link: testimonialLink };
    ```
  - **Thay `your-gumroad-link.com`** bằng URL của trang web hoặc Gumroad của bạn.

#### **🔹 Node 13: Respond — Thank You**
- **Cấu hình:**
  - **Trả lời webhook** từ Gumroad khi khách hàng để lại đánh giá.
  - **Nội dung trả lời:**
    ```json
    {
      "status": "success",
      "message": "Cảm ơn bạn đã để lại đánh giá!"
    }
    ```

#### **🔹 Node 14 & 15: On Error & Email — Error Alert**
- **Cấu hình:**
  - **Email lỗi** sẽ được gửi khi workflow gặp sự cố.
  - **Nội dung email lỗi:**
    ```html
    <h2>Lỗi trong workflow!</h2>
    <p>Workflow tự động hóa đã gặp lỗi:</p>
    <p><strong>Lỗi:</strong> {{error.message}}</p>
    <p><strong>Bước gặp lỗi:</strong> {{error.node.name}}</p>
    <p><strong>Dữ liệu đầu vào:</strong> {{error.input}}</p>
    <p>Vui lòng kiểm tra và khắc phục!</p>
    ```

---

### **✍️ Mẹo & gợi ý nâng cao**
:::info[**TIẾP CẬN HƠN VỚI WORKFLOW**]
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có đơn hàng mới hoặc đánh giá.
   - **Cách làm:**
     - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
     - Gửi thông báo như:
       ```json
       {
         "text": `🚀 Đơn hàng mới từ ${client_name} (${client_email})!`,
         "attachments": [{
           "title": "Chi tiết đơn hàng",
           "fields": [
             { "title": "Sản phẩm", "value": product_purchased, "short": true },
             { "title": "Số tiền", "value": purchase_amount, "short": true }
           ]
         }]
       }
       ```

2. **Lưu log hoạt động:**
   - Thêm node **Google Sheets** hoặc **Notion** để lưu tất cả hoạt động của workflow.
   - **Cách làm:**
     - Thêm node `n8n-nodes-base.googleSheets` và cấu hình để ghi log:
       ```json
       {
         "sheetName": "Log Workflow",
         "values": [
           [
             new Date().toISOString(),
             $input.all()[0].json.client.email,
             $input.all()[0].json.action,
             $input.all()[0].json.status
           ]
         ]
       }
       ```

3. **Gửi báo cáo định kỳ:**
   - Tạo một workflow riêng để gửi **báo cáo tuần/month** về số lượng khách hàng nuôi dưỡng và đánh giá.
   - **Cách làm:**
     - Sử dụng node `n8n-nodes-base.notion` để lấy dữ liệu từ database.
     - Thêm node `n8n-nodes-base.emailSend` để gửi báo cáo dưới dạng PDF hoặc Excel.

4. **Tối ưu email với AI:**
   - Sử dụng **node `n8n-nodes-base.llm`** (nếu có) để tự động hóa việc viết email cá nhân hóa.
   - **Ví dụ:**
     ```javascript
     // Node Function trước khi gửi email
     return {
       email_content: `Chào ${client_name},\n\nTôi là [Tên Công Ty] và rất vui khi bạn đã mua ${product_purchased}. Đây là một số mẹo để bạn tối ưu trải nghiệm:\n\n- Mẹo 1: [AI tự động sinh nội dung]\n- Mẹo 2: [AI tự động sinh nội dung]\n\nTrân