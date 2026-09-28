---
title: "🤖 **Tự Động Hóa Gmail với AI OpenAI, Google Sheets & Telegram: Phân Loại & Trả Lời Tự Động Email**"
description: "Workflow này tự động phân loại email vào danh mục (ưu tiên cao, hỗ trợ khách hàng, quảng cáo, tài chính) bằng AI OpenAI, tạo phản hồi tự động, và gửi thông báo Telegram thời gian thực. Giúp các sếp tiết kiệm 10+ giờ/ngày quản lý email thủ công."
slug: "tieu-dong-hoa-gmail-voi-ai-openai-telegram"
tags: [n8n, automation, no-code, gmail-automation, ai-openai, google-sheets, telegram-notification]
keywords: [tự động hóa email, phân loại email bằng AI, trả lời tự động gmail, workflow n8n, openai gmail, telegram alert]
---

# 🚀 **Tự Động Hóa Gmail với AI: Phân Loại & Trả Lời Tự Động Email (Với OpenAI, Google Sheets & Telegram)**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Hàng ngày, các sếp phải mất **10-15 giờ** để:
- **Phân loại email** vào các danh mục khác nhau (ưu tiên cao, hỗ trợ khách hàng, quảng cáo, tài chính).
- **Trả lời email** một cách nhất quán, nhưng lại phải viết lại nội dung mỗi lần.
- **Quên theo dõi email quan trọng** trong inbox ồn ào.
- **Phải mở nhiều tab** để tra cứu thông tin trong Google Sheets khi trả lời.

**Workflow này giải quyết tất cả!**
Sử dụng **AI OpenAI** để phân loại email tự động, **tạo phản hồi chuẩn** dựa trên nội dung, và **gửi thông báo Telegram** cho đội ngũ theo dõi. **Không cần viết code, chỉ cần cấu hình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/ngày** quản lý email thủ công.
✅ **Phân loại email chính xác** (ưu tiên cao, hỗ trợ, tài chính, quảng cáo) bằng AI.
✅ **Trả lời email tự động** với nội dung cá nhân hóa, dựa trên dữ liệu trong Google Sheets.
✅ **Thông báo Telegram thời gian thực** cho đội ngũ theo dõi.
✅ **Giữ inbox sạch sẽ** bằng cách tự động xóa email đã xử lý.
✅ **Dễ dàng mở rộng** cho nhiều bộ phận (HR, Marketing, Finance).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (đã cấp quyền OAuth2 cho n8n).
✔ **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
✔ **Google Sheets** (để lưu dữ liệu hỗ trợ trả lời email).
✔ **Bot Telegram** (tùy chọn, để nhận thông báo).
✔ **Danh sách nhãn (labels) trong Gmail**:
   - `High Priority`
   - `Customer Support`
   - `Promotion`
   - `Finance/Billing`

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/11265](https://n8n.io/workflows/11265) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor → Nhấn **Create new workflow**.
2. Chọn **Import from JSON** → Dán JSON từ file vào.
3. Nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **34 node**, nhưng chỉ cần chú ý đến các node quan trọng sau:

#### **🔹 Node Gmail Trigger (Gmail Trigger1)**
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).
  - **Filter**: Chỉ lấy email **UNREAD** (để tránh xử lý lại).
  - **Enable**: Bật để workflow bắt đầu khi có email mới.

#### **🔹 Node Phân Loại Email (Email Classifier Agent)**
- **Prompt AI**:
  ```plaintext
  Phân loại email này vào một trong 4 danh mục sau:
  1. High Priority (ưu tiên cao)
  2. Customer Support (hỗ trợ khách hàng)
  3. Promotion (quảng cáo)
  4. Finance/Billing (tài chính/hoá đơn)

  Nếu email liên quan đến tài chính, trả về "Finance/Billing".
  Nếu email là quảng cáo, trả về "Promotion".
  Nếu email là yêu cầu hỗ trợ, trả về "Customer Support".
  Nếu email rất quan trọng (ví dụ: deadline, khẩn cấp), trả về "High Priority".
  ```
- **Lưu ý**:
  - Cần **cập nhật prompt** nếu có yêu cầu phân loại đặc biệt.
  - Kết quả phân loại sẽ quyết định **nhánh xử lý tiếp theo**.

#### **🔹 Node Trả Lời Tự Động (Auto Reply1, Creating Email1)**
- **Cấu hình OpenAI**:
  - **Model**: Chọn `gpt-4` hoặc `gpt-3.5-turbo` (tùy budget).
  - **Prompt mẫu**:
    ```plaintext
    Tôi là trợ lý hỗ trợ khách hàng của công ty XYZ.
    Email này là: {{ $json.email.body }}
    Hãy trả lời email này một cách **chuyên nghiệp, thân thiện và ngắn gọn**.
    Nếu email liên quan đến hỗ trợ, hãy tra cứu trong Google Sheets (Sheet: "Customer_Support_Guides") trước khi trả lời.
    ```
- **Google Sheets Tool (FTAI Info)**:
  - **Sheet Name**: Đặt tên là `Customer_Support_Guides` (hoặc tùy chỉnh).
  - **Cột cần tra cứu**: Ví dụ: `Question` và `Answer`.

#### **🔹 Node Gửi Thông Báo Telegram (Notify 1-4)**
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi` (đã đăng ký bot Telegram).
  - **Message**: Tùy chỉnh nội dung thông báo (ví dụ: `🚨 Email mới từ {{ $json.email.from }} - Danh mục: {{ $json.classification }}`).

#### **🔹 Node Xóa Email Sau Xử Lý (Mark as Read + Remove From Inbox)**
- **Lưu ý**:
  - Workflow sẽ **xóa email** sau khi xử lý xong (để giữ inbox sạch).
  - Nếu muốn **giữ email**, bỏ node `Delete a message`.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với email mẫu:
   - Sử dụng **Demo Emails** (node `Send Demo Emails`) để thử phân loại.
   - Kiểm tra phản hồi AI và thông báo Telegram.
2. **Bật Active**:
   - Đảm bảo **Gmail Trigger** đang hoạt động.
   - Kiểm tra **credentials** của tất cả node (Gmail, OpenAI, Telegram).

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa Prompt AI**
- **Ví dụ cho danh mục "High Priority"**:
  ```plaintext
  Nếu email có từ khóa: "deadline", "khẩn cấp", "hết hạn", "urgent", "cấp bách" → phân loại "High Priority".
  ```
- **Ví dụ cho danh mục "Finance"**:
  ```plaintext
  Nếu email có từ khóa: "hoá đơn", "than toán", "tài chính", "đơn hàng", "thanh toán" → phân loại "Finance/Billing".
  ```

### **2. Kết Hợp Với Slack (Thay Thế Telegram)**
- Thay node `telegram` bằng `slack` để gửi thông báo vào Slack channel.
- **Cấu hình**:
  - **Credentials**: `slackApi` (đã đăng ký webhook Slack).
  - **Message**: `📧 Email mới từ {{ $json.email.from }} - {{ $json.classification }}`.

### **3. Lưu Log Xử Lý Email**
- Thêm node **Google Sheets** để ghi lại lịch sử xử lý:
  - **Sheet Name**: `Email_Log`.
  - **Cột**: `Date`, `From`, `Subject`, `Classification`, `Reply Status`.

### **4. Gửi Báo Cáo Hàng Ngày**
- Sử dụng **node `googleSheets`** để tạo báo cáo tổng hợp:
  - **Báo cáo**: Số email đã xử lý theo danh mục.
  - **Gửi qua Email**: Dùng node `gmail` để gửi báo cáo tự động vào buổi sáng.

### **5. Cập Nhật Dữ Liệu Hỗ Trợ (Google Sheets)**
- **Cập nhật thường xuyên** sheet `Customer_Support_Guides` để phản hồi AI luôn mới nhất.
- **Ví dụ dữ liệu**:
  | Question | Answer |
  |----------|--------|
  | "Làm sao hủy đơn hàng?" | "Xin lỗi quý khách! Đơn hàng #{{order_id}} đã được hủy thành công..." |

---

## 📌 **Kết Luận: Áp Dụng Ngay & Tiết Kiệm Thời Gian!**
Workflow này **giải phóng 100% thời gian** của các sếp khỏi việc quản lý email thủ công. **Không cần code, chỉ cần cấu hình!**

👉 **Bước đầu tiên**: Import workflow và **test với Demo Emails**.
👉 **Bước tiếp theo**: Cập nhật **prompt AI** và **dữ liệu hỗ trợ** cho phù hợp với doanh nghiệp.
👉 **Kết quả**: **Inbox sạch sẽ, phản hồi tự động, thông báo thời gian thực** – tất cả chỉ với **một workflow n8n!**

---
**🚀 Cần hỗ trợ thêm?** Đăng ký khóa học của tác giả [Sandeep Patharkar](https://www.fasttrackaimastery.com) để học cách tối ưu workflow này! 🎓