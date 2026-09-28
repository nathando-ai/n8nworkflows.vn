---
title: "🤖 Tự Động Hóa Follow-up Lead B2B với Gemini AI, Gmail & Google Sheets - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn để gửi email nhắc nhở cá nhân hóa cho khách hàng chưa phản hồi trong 5 ngày, tiết kiệm 10+ giờ/tháng cho bộ phận marketing và sales. Kết hợp AI Gemini, Gmail và Google Sheets để tối ưu hóa quy trình chăm sóc khách hàng."
slug: "tieu-dong-hoa-lead-follow-up-gemini-gmail-google-sheets"
tags: [n8n, automation, no-code, lead-nurturing, gemini-ai, google-sheets, gmail, ai-agent]
keywords: [n8n workflow tự động hóa, tự động hóa lead follow-up, gemini ai trong n8n, google sheets n8n, tự động hóa email nhắc nhở, lead nurturing no-code]
---

# 🚀 **Tự Động Hóa Follow-up Lead B2B với Gemini AI, Gmail & Google Sheets**

### **Giải pháp hoàn hảo cho các sếp marketing/sales:**
Bạn đã bao giờ phải mất **10+ giờ/tuần** để nhắc nhở khách hàng chưa phản hồi email giới thiệu? Hoặc phải lo lắng rằng các lead tiềm năng bị bỏ quên vì không có hệ thống tự động hóa? **Workflow này sẽ thay bạn làm việc đó!**

Với **Gemini AI** (mô hình ngôn ngữ lớn của Google), **Gmail** và **Google Sheets**, workflow này sẽ:
✅ **Tự động phát hiện** khách hàng chưa phản hồi trong **5 ngày**
✅ **Gửi email nhắc nhở cá nhân hóa** dựa trên nội dung query ban đầu của khách hàng
✅ **Cập nhật trạng thái** trong Google Sheets để theo dõi hiệu quả
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không phải mất giờ để nhắc nhở khách hàng thủ công.
- **Tăng tỷ lệ chuyển đổi:** Email nhắc nhở cá nhân hóa tăng cơ hội phản hồi lên **30-50%**.
- **Theo dõi hiệu quả:** Google Sheets tự động cập nhật trạng thái lead, giúp phân tích hiệu suất.
- **Hoạt động liên tục:** Workflow chạy tự động mà không cần can thiệp.
- **Cá nhân hóa cao:** Gemini AI phân tích query ban đầu để tạo email nhắc nhở phù hợp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (đã cấp quyền OAuth 2.0 cho n8n)
✔ **Google Sheets** (đã chia sẻ quyền cho n8n)
✔ **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://aistudio.google.com/))
✔ **Danh sách email giới thiệu** (để workflow tìm và nhắc nhở)

---
:::note[Lưu ý quan trọng]
- Workflow **không tự động gửi email** mà chỉ nhắc nhở trên **thread email gốc**.
- Các sếp cần **cấu hình email ID** để workflow biết nơi tìm email giới thiệu ban đầu.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11283](https://n8n.io/workflows/11283) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file JSON.
- Workflow sẽ hiển thị trên **canvas**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Gmail OAuth 2.0**
- Vào **Credentials** → Thêm **Gmail OAuth 2.0** với tài khoản Gmail cần sử dụng.
- Chọn **Scopes**: `https://www.googleapis.com/auth/gmail.readonly` (đọc) và `https://www.googleapis.com/auth/gmail.send` (gửi).

##### **B. Cấu hình Google Sheets OAuth 2.0**
- Vào **Credentials** → Thêm **Google Sheets OAuth 2.0 API**.
- Chọn **Scopes**: `https://www.googleapis.com/auth/spreadsheets`.

##### **C. Cấu hình Google Gemini API**
- Vào **Credentials** → Thêm **Google Palm API** với **API Key** từ [Google AI Studio](https://aistudio.google.com/).
- **Prompt mặc định** (có thể chỉnh sửa):
  ```
  You are a professional email writer. Based on the original query from the customer in the Google Sheet, write a polite and personalized reminder email to encourage them to respond.
  ```

##### **D. Cấu hình "Get many messages"**
- **Email ID để tìm thread gốc**: Điền vào **Search Term** trong node **"Get many messages"** (ví dụ: `from:sales@example.com`).
- **Thời gian tìm kiếm**: Cài đặt **5 ngày** để workflow chỉ nhắc nhở khách hàng chưa phản hồi.

##### **E. Cấu hình "AI Agent" và "Google Gemini Chat Model"**
- **Prompt**: Sử dụng prompt mặc định hoặc chỉnh sửa để phù hợp với brand của các sếp.
- **Output Parser**: Đảm bảo **Structured Output Parser** trả về dữ liệu email nhắc nhở dưới dạng JSON.

##### **F. Cấu hình "Update row in sheet"**
- Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1:D100`) để cập nhật trạng thái lead.

##### **G. Cấu hình "Wait"**
- Thời gian chờ mặc định là **5 ngày** (có thể điều chỉnh).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Execute workflow"** → Kiểm tra email nhắc nhở được tạo ra.
   - Xem **Google Sheets** có cập nhật trạng thái không.
2. **Bật Active**:
   - Chuyển **Manual Trigger** thành **Scheduled Trigger** (nếu muốn chạy tự động hàng ngày).
   - Hoặc để **Manual Trigger** và kích hoạt thủ công khi cần.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi email nhắc nhở được gửi.

2. **Lưu log hoạt động**:
   - Sử dụng **Google Sheets** để lưu lịch sử email nhắc nhở (ngày gửi, nội dung, trạng thái phản hồi).

3. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng **n8n + Google Sheets** để tạo báo cáo tự động về tỷ lệ phản hồi và lead mới.

4. **Chỉnh sửa prompt AI**:
   - Nếu muốn email nhắc nhở **đặc biệt hơn**, hãy cập nhật prompt trong **Google Gemini Chat Model** với:
     - **Tôn trọng hơn** (ví dụ: "Chúng tôi hiểu bạn bận rộn, nhưng có thể hỗ trợ gì cho bạn?").
     - **Gợi ý giải pháp** (ví dụ: "Dưới đây là 3 cách chúng tôi có thể giúp bạn...").

5. **Tích hợp CRM khác**:
   - Nếu sử dụng **HubSpot, Salesforce** hoặc **Zoho CRM**, có thể thay thế **Google Sheets** bằng API của CRM đó.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp marketing/sales để tập trung vào **quyết định chiến lược** thay vì làm việc thủ công. Với **Gemini AI**, email nhắc nhở không chỉ đơn giản mà còn **cá nhân hóa cao**, tăng tỷ lệ phản hồi đáng kể.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test Run** với 1-2 lead mẫu.
3. **Bật Active** và để nó hoạt động tự động!

👉 **Bạn có thể kết hợp workflow này với [Workflow tự động hóa gửi email giới thiệu](link-tới-workflow-khác) để tạo hệ thống chăm sóc lead hoàn chỉnh!**

---
**Chia sẻ ý kiến hoặc gặp vấn đề?** Đăng ký tại [BuildmyAIflow.agency](https://buildmyaiflow.agency) để được hỗ trợ chi tiết! 🚀