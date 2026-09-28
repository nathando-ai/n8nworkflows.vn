---
title: "📧 [Tự Động Hiểu Nhanh Email: Parse Email Body Message - Không Cần Code!]"
description: "Workflow này tự động phân tích nội dung email, tách biệt chủ đề, người gửi và nội dung chính để các sếp tiết kiệm thời gian xử lý hàng trăm tin nhắn hàng ngày. Giúp giảm thiểu sai sót và tối ưu hóa quy trình làm việc."
slug: "parse-email-body-message-n8n"
tags: [n8n, automation, email-parsing, no-code, business-productivity]
keywords: [n8n workflow email, tự động hóa email, parse email body, phân tích email tự động, tiết kiệm thời gian email]
---

# 🚀 **Tự Động Hiểu Nhanh Email: Parse Email Body Message - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Xử Lý Email**
Hàng ngày, các sếp phải mở hàng trăm email, đọc từng dòng để tìm thông tin quan trọng: **ai gửi**, **nội dung chính là gì**, và **chủ đề cụ thể**. Quá trình này tốn thời gian, dễ gây nhầm lẫn, và đôi khi thông tin quan trọng bị bỏ qua. **Workflow này giải quyết vấn đề đó bằng cách tự động phân tích và tách biệt nội dung email thành các phần logic**, giúp các sếp tập trung vào những điều thực sự quan trọng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đọc từng email thủ công, workflow tự động phân tích và tách nội dung.
- **Chính xác cao**: Tránh sai sót khi xử lý thông tin từ email.
- **Tối ưu hóa quy trình**: Dễ dàng tích hợp với các công cụ khác (Slack, Google Sheets, CRM...) để tự động hóa thêm.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào máy tính cá nhân.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Không cần API Key hoặc tài khoản đặc biệt**: Workflow này chỉ hoạt động trên **n8n Editor** (self-hosted hoặc n8n.cloud).
- **N8n phiên bản mới nhất** (để đảm bảo tính tương thích với các node).
- **Dữ liệu mẫu** (nếu muốn test trước khi chạy thực tế).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1: Import từ file JSON**
  1. Tải workflow từ [n8n.io/workflows/1453](https://n8n.io/workflows/1453) (chọn **Download JSON**).
  2. Mở **n8n Editor** (trang chủ của n8n).
  3. Nhấn **Import** và chọn file JSON vừa tải.
  4. Workflow sẽ xuất hiện trong danh sách workflows của bạn.

- **Cách 2: Copy/Paste JSON**
  1. Mở **n8n Editor**.
  2. Nhấn **Import** → **Paste JSON**.
  3. Dán nội dung JSON từ [n8n.io/workflows/1453](https://n8n.io/workflows/1453) (chọn **Raw**).
  4. Nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **không cần cấu hình API Key** vì nó chỉ hoạt động trên **n8n Editor** với 3 node cơ bản:
- **Node 1: "On clicking 'execute'" (manualTrigger)**
  - **Lưu ý**: Node này **không tự động kích hoạt** mà cần **nhấn "Execute"** thủ công hoặc kết nối với một **webhook** (nếu muốn tự động hóa).
  - **Mẹo**: Để tự động hóa, các sếp có thể kết nối node này với **n8n-nodes-base.http** (webhook) để nhận email từ một dịch vụ như **Gmail API** hoặc **Zapier**.

- **Node 2: "Email Parser Snippet" (functionItem)**
  - **Nội dung mặc định**:
    ```javascript
    const emailBody = $input.all()[0].json.emailBody;
    const subject = $input.all()[0].json.subject;
    const sender = $input.all()[0].json.sender;

    return {
      parsedEmail: {
        subject: subject,
        sender: sender,
        body: emailBody,
        // Thêm logic phân tích nếu cần (ví dụ: tách chủ đề, nội dung chính)
      }
    };
    ```
  - **Lưu ý**:
    - Các sếp có thể **sửa code này** để phù hợp với yêu cầu cụ thể (ví dụ: tách ra chủ đề, nội dung chính, hoặc thêm logic OCR nếu email có file đính kèm).
    - **Input cần có**:
      - `emailBody`: Nội dung email (dạng text).
      - `subject`: Chủ đề email.
      - `sender`: Người gửi (email hoặc tên).

- **Node 3: "Set values" (set)**
  - **Lưu ý**:
    - Node này **không cần cấu hình thêm** vì nó chỉ **trả về kết quả** từ node `Email Parser Snippet`.
    - **Output** sẽ chứa:
      ```json
      {
        "parsedEmail": {
          "subject": "Chủ đề email",
          "sender": "nguoidung@example.com",
          "body": "Nội dung email..."
        }
      }
      ```
    - **Mẹo nâng cao**:
      - Các sếp có thể **kết nối node này với `n8n-nodes-base.google-sheets`** để tự động ghi dữ liệu vào bảng Google Sheets.
      - Hoặc kết nối với **Slack/Telegram** để thông báo kết quả phân tích.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute** trên node `On clicking 'execute'`.
   - Điền vào **Input Data** (ví dụ):
     ```json
     {
       "emailBody": "Xin chào, tôi là Nguyễn Văn A. Nội dung email này là về dự án mới. Vui lòng xem file đính kèm.",
       "subject": "Dự án mới - Yêu cầu hỗ trợ",
       "sender": "nvA@example.com"
     }
     ```
   - Kiểm tra kết quả ở node `Set values`.

2. **Bật Active Workflow**:
   - Nhấn **Active** trên tab workflow.
   - **Lưu ý**: Nếu muốn tự động hóa, các sếp cần **kết nối với một webhook** (ví dụ: Gmail API) để nhận email tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Gmail API**
   - Sử dụng **n8n-nodes-base.google** để **nhận email tự động** từ Gmail và truyền vào workflow.
   - **Cách làm**:
     - Tạo một **webhook** bằng `n8n-nodes-base.http`.
     - Kết nối với **Gmail API** (sử dụng OAuth 2.0).
     - Khi có email mới, Gmail sẽ gọi webhook → workflow tự động phân tích.

2. **Lưu Log & Báo Cáo**
   - Kết nối node `Set values` với **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để gửi kết quả phân tích.
   - Hoặc lưu vào **Google Sheets** để theo dõi lịch sử.

3. **Phân Tích Nội Dung Tự Động**
   - Sửa code trong `Email Parser Snippet` để **tách chủ đề chính** bằng regex hoặc AI (nếu kết nối với **n8n-nodes-base.llm**).
   - Ví dụ:
     ```javascript
     const subjectRegex = /(dự án|yêu cầu|hỗ trợ|thông báo)/i;
     const mainSubject = subjectRegex.test(subject) ? "Dự án" : "Khác";
     ```

4. **Tự Động Trả Lời Email**
   - Kết nối workflow với **n8n-nodes-base.email** để tự động gửi trả lời dựa trên nội dung phân tích.

---

### 📌 **Kết Luận**
Workflow **Parse Email Body Message** là **giải pháp đơn giản nhưng hiệu quả** để các sếp **tự động hóa việc đọc và phân tích email**, tiết kiệm thời gian và giảm thiểu sai sót. **Không cần code**, chỉ cần **import và chạy** trên n8n.

**Hãy áp dụng ngay để bắt đầu tự động hóa email của mình!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/1453)
👉 [Cài đặt n8n trên VPS để chạy 24/7](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)