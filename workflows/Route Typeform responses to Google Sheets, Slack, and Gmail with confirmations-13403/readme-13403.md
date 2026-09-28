---
title: "🚀 Tự Động Hóa Trả Lời Typeform Sang Google Sheets, Slack & Email Với Xác Nhận (N8n)"
description: "Giải pháp tự động hóa 100% không code để nhận, phân loại và chuyển tiếp phản hồi từ Typeform sang Google Sheets, Slack và gửi email xác nhận tự động. Tiết kiệm thời gian quản lý leads và hỗ trợ khách hàng 24/7."
slug: "tu-dong-hoa-typeform-sang-google-sheets-slack-email"
tags: [n8n, automation, ticket-management, typeform, google-sheets, slack, gmail]
keywords: [n8n workflow typeform, tự động hóa typeform, quản lý leads tự động, phân loại phản hồi, gửi email tự động, slack automation]
---

# 🚀 Tự Động Hóa Trả Lời Typeform Sang Google Sheets, Slack & Email Với Xác Nhận

### **Giải pháp cho các sếp:**
Bạn đã mệt mỏi với việc phải thủ công:
- **Nhận phản hồi từ Typeform** và phải copy-paste vào Google Sheets?
- **Phân loại leads** theo sở thích (sales, support, hoặc khác) và chuyển tiếp cho đội ngũ?
- **Gửi email xác nhận** cho khách hàng sau mỗi phản hồi?

**Workflow này tự động hóa toàn bộ quy trình đó!** Khi khách hàng gửi phản hồi qua Typeform, hệ thống sẽ:
✅ **Lưu tất cả dữ liệu** vào Google Sheets (dễ theo dõi và phân tích).
✅ **Phân loại tự động** phản hồi theo sở thích (sales, support, hoặc khác) và chuyển tiếp đến Slack.
✅ **Gửi email xác nhận** cho khách hàng ngay lập tức.

---
### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy-paste dữ liệu thủ công.
- **Phân loại chính xác**: Phản hồi được chuyển đến đội ngũ phù hợp (sales/support).
- **Trải nghiệm khách hàng tốt**: Email xác nhận tự động tăng độ chuyên nghiệp.
- **Dữ liệu tập trung**: Tất cả phản hồi được lưu vào Google Sheets, dễ theo dõi và phân tích.
- **Hoạt động 24/7**: Không cần can thiệp người dùng.
:::

---
### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Typeform** và **Form ID** (để n8n nghe phản hồi).
2. **Tài khoản Google Sheets** với:
   - **Spreadsheet ID** (để lưu phản hồi).
   - **Sheet tên "Responses"** với cột: `name`, `email`, `interest`, `submitted_at`.
3. **Tài khoản Slack** với:
   - **Channel ID** cho sales (ví dụ: `#sales-leads`).
   - **Channel ID** cho support (ví dụ: `#support-tickets`).
4. **Tài khoản Gmail** (để gửi email xác nhận).
5. **API Keys/Credentials**:
   - **Typeform Webhook Secret** (để n8n xác thực phản hồi).
   - **Google Sheets OAuth2 API Key**.
   - **Gmail OAuth2 API Key**.
   - **Slack Bot Token** (để gửi tin nhắn).
:::

---
### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/13403) (hoặc copy JSON từ trang này).
- **Bước 2**: Mở **n8n Editor** (trên máy chủ tự host hoặc n8n.cloud).
- **Bước 3**: Nhấn **Import** và dán JSON vào hoặc tải file JSON lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích chi tiết các node cần cấu hình:

##### **1. Node "Typeform Trigger" (n8n-nodes-base.typeformTrigger)**
- **Cấu hình**:
  - **Form ID**: Điền ID của form Typeform bạn muốn nghe phản hồi.
  - **Webhook Secret**: Tạo một secret (ví dụ: `my-secret-key`) và điền vào **Webhook Secret** trong node này.
  - **Test**: Nhấn **Execute Node** để kiểm tra kết nối.

##### **2. Node "Set Response Fields" (n8n-nodes-base.set)**
- **Cấu hình**:
  - **Field Mappings**: Đảm bảo các trường (`name`, `email`, `interest`) trong node này **khớp với tên cột trong Typeform**.
  - **Ví dụ**:
    ```json
    {
      "name": "$json.name",
      "email": "$json.email",
      "interest": "$json.interest",
      "submitted_at": "$json.created"
    }
    ```
  - **Lưu ý**: Nếu Typeform có tên trường khác, hãy điều chỉnh theo.

##### **3. Node "Log to Google Sheets" (n8n-nodes-base.googleSheets)**
- **Cấu hình**:
  - **Spreadsheet ID**: Tìm trong URL của Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name**: Đảm bảo sheet tên là **"Responses"**.
  - **Operation**: Chọn **Append** (thêm mới).
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).

##### **4. Node "Send Confirmation Email" (n8n-nodes-base.gmail)**
- **Cấu hình**:
  - **To**: `$json.email` (để gửi email cho người trả lời).
  - **Subject**: "Xác nhận phản hồi của bạn đã được nhận!"
  - **Body**: Thêm nội dung email (ví dụ: `Xin chào $json.name, cảm ơn bạn đã liên hệ với chúng tôi. Chúng tôi sẽ xử lý yêu cầu của bạn sớm.`).
  - **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).

##### **5. Node "Route by Interest" (n8n-nodes-base.switch)**
- **Cấu hình**:
  - **Conditions**: Đặt điều kiện phân loại phản hồi theo `interest`:
    - **Sales**: Nếu `$json.interest` = "sales" → chuyển đến node **Notify Sales Channel**.
    - **Support**: Nếu `$json.interest` = "support" → chuyển đến node **Notify Support Channel**.
    - **Fallback**: Nếu khác → bỏ qua (hoặc thêm logic khác).
  - **Ví dụ**:
    ```json
    {
      "sales": "$json.interest === 'sales'",
      "support": "$json.interest === 'support'",
      "default": "true"
    }
    ```

##### **6. Node "Notify Sales Channel" & "Notify Support Channel" (n8n-nodes-base.slack)**
- **Cấu hình**:
  - **Channel**: Điền **Channel ID** của Slack (ví dụ: `#sales-leads`).
  - **Message**: Thêm tin nhắn (ví dụ: `📩 New sales lead: $json.name`).
  - **Credentials**: Chọn `slack` (đã cấu hình trước).

---
#### 3. Kích hoạt ⚡️
- **Test Run**: Nhấn **Execute Workflow** với dữ liệu mẫu để kiểm tra.
- **Active**: Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động 24/7.

---
### ✍️ Mẹo & gợi ý nâng cao
:::info[CẢNH BÁO & MỆNH CHỮ]
- **Lưu log**: Thêm node **Sticky Note** để ghi chú lỗi hoặc debug.
- **Kết hợp với AI**: Sử dụng node **LLM** (n8n-nodes-base.llm) để phân tích phản hồi tự động.
- **Báo cáo định kỳ**: Tạo một workflow khác để gửi báo cáo tổng hợp từ Google Sheets qua email hàng tuần.
- **Tự động phản hồi**: Sử dụng node **Gmail** để gửi email tự động trả lời khách hàng (ví dụ: "Chúng tôi sẽ liên hệ trong 24h").
- **Duy trì dữ liệu**: Xóa dữ liệu cũ trong Google Sheets bằng node **Google Sheets** với `operation: delete`.
:::

---
### 📌 Kết luận
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công quản lý phản hồi Typeform. Bằng cách tự động:
✔ **Lưu dữ liệu** vào Google Sheets.
✔ **Phân loại và chuyển tiếp** phản hồi đến đội ngũ phù hợp.
✔ **Gửi email xác nhận** cho khách hàng.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa!

👉 **🎁 Đăng ký VPS TinoHost** với mã giảm giá **VPSN8N** (giảm tới 39%) để tự host n8n ổn định:
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)

---
:::note[CHÚ THÍCH]
- Nếu gặp lỗi, hãy kiểm tra **credentials** của các node (Google Sheets, Slack, Gmail).
- Để nâng cao tính bảo mật, sử dụng **OAuth2** thay vì API Key.
- Workflow này phù hợp cho **doanh nghiệp B2B** quản lý leads và hỗ trợ khách hàng.
:::