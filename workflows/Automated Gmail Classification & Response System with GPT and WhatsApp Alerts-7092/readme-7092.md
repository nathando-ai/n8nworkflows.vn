---
title: "🚀 Hệ Thống Tự Động Phân Loại & Trả Lời Email Gmail Với GPT + Cảnh Báo WhatsApp (N8N)"
description: "Tự động hóa hoàn toàn việc phân loại email vào 5 danh mục chính (ưu tiên cao, hỗ trợ khách hàng, quảng cáo, tài chính, chung) và trả lời tự động bằng AI, đồng thời cảnh báo ngay lập tức qua WhatsApp. Giúp các sếp tiết kiệm 8+ giờ/ngày và giảm thiểu sai sót trong quản lý email."
slug: "tự-dộng-phân-loại-email-gmail-whatsapp-gpt"
tags: [n8n, automation, no-code, gmail, openai, whatsapp, ai, ticket-management]
keywords: [n8n workflow email, tự động hóa email gmail, phân loại email bằng ai, cảnh báo whatsapp tự động, trả lời email tự động bằng gpt]
---

# 🚀 **Hệ Thống Tự Động Phân Loại & Trả Lời Email Gmail Với GPT + Cảnh Báo WhatsApp**

### **Giải pháp hoàn toàn tự động hóa quản lý email cho doanh nghiệp**
Hàng ngày, các sếp phải mất **8-10 giờ** để đọc, phân loại và trả lời hàng trăm email. Nhiều tin nhắn quan trọng bị bỏ qua, trong khi những email không cần thiết lại chiếm chỗ trong hộp thư. **Workflow này tự động hóa toàn bộ quy trình** bằng cách:
- **Phân loại email** vào 5 danh mục chính (ưu tiên cao, hỗ trợ khách hàng, quảng cáo, tài chính, chung) bằng AI.
- **Trả lời tự động** với nội dung cá nhân hóa bằng GPT-4.
- **Cảnh báo ngay lập tức** qua WhatsApp cho các email ưu tiên cao hoặc tài chính.
- **Tự động chuyển tiếp** email tài chính cho bộ phận chuyên môn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/ngày** cho việc đọc và phân loại email thủ công.
- **Trả lời email nhanh chóng** với nội dung tự động sinh bởi AI, giảm thiểu sai sót.
- **Cảnh báo tức thời** cho các email ưu tiên cao hoặc tài chính, không bỏ qua bất kỳ tin nhắn quan trọng nào.
- **Tự động chuyển tiếp** email tài chính cho bộ phận chuyên môn, giảm tải cho các sếp.
- **Hộp thư Gmail luôn được sắp xếp** theo danh mục logic, dễ dàng theo dõi và quản lý.
- **Tăng cường trải nghiệm khách hàng** với phản hồi nhanh chóng và tự động.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth 2.0 cho n8n).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)) và tạo **credentials** trong n8n với tên `openAiApi`.
3. **Số điện thoại WhatsApp Business API** (hoặc sử dụng API WhatsApp của nhà cung cấp như [Twilio](https://www.twilio.com/)).
4. **Tài khoản WhatsApp Business** (đã kích hoạt API và tạo `credentials` trong n8n với tên `whatsAppApi`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/7092](https://n8n.io/workflows/7092) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7092) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng như sau:

##### **A. Cấu hình Gmail**
- **Node: Gmail Trigger**
  - Chọn `credentials`: `gmailOAuth2` (đã tạo trước đó).
  - **Lưu ý:** Cần thiết lập **filter** trong Gmail để workflow chỉ hoạt động với email mới (ví dụ: `in:inbox`).
  - **Test:** Gửi email mẫu đến địa chỉ Gmail đã kết nối để kiểm tra trigger.

- **Node: High Priority Email, Customer Support Email, Promotion Email, Finance/Billing Email, Random (General/Other) Email**
  - Tất cả các node này đều sử dụng `operation: addLabels`.
  - **Lưu ý:** Đảm bảo các **label** đã tồn tại trong Gmail (nếu chưa, tạo trước trong Gmail: `Labels > Create new label`).

##### **B. Cấu hình OpenAI**
- **Node: OpenAI Chat Model, Creating a Draft, Create Email, Finance Department, Summarize Promotions**
  - Chọn `credentials`: `openAiApi`.
  - **Model mặc định:** `gpt-4.1-mini` (có thể thay đổi thành `gpt-4` nếu có nhu cầu).
  - **Lưu ý:**
    - Đối với **node "Email Classifier"**, không cần cấu hình thêm (sử dụng mô hình mặc định của LangChain).
    - Đối với **node "Creating a Draft"**, cấu hình `prompt` để AI sinh nội dung trả lời email (ví dụ: `"Tóm tắt email này và trả lời ngắn gọn với nội dung: [Tên khách hàng], cảm ơn bạn đã liên hệ. Chúng tôi sẽ xử lý yêu cầu của bạn trong vòng 24 giờ."`).

##### **C. Cấu hình WhatsApp**
- **Node: High Priority Alert, Confirmation, Promotional Alert, Finance Alert**
  - Chọn `credentials`: `whatsAppApi`.
  - **Lưu ý:**
    - Đảm bảo **số điện thoại WhatsApp** đã được kích hoạt API và có quyền gửi tin nhắn.
    - **Tham số `message`:** Có thể tùy chỉnh nội dung cảnh báo (ví dụ: `"🚨 Email ưu tiên cao từ [Tên khách hàng] - Vui lòng xem ngay!"`).

##### **D. Cấu hình Draft & Auto Reply**
- **Node: Draft email**
  - Chọn `credentials`: `gmailOAuth2`.
  - **Lưu ý:** Workflow sẽ tự động tạo **bản nháp** email trước khi gửi, giúp các sếp kiểm tra trước khi gửi.
- **Node: Auto Reply**
  - Chọn `credentials`: `gmailOAuth2`.
  - **Lưu ý:** Đảm bảo **email nguồn** đã được phân loại trước (ví dụ: `Customer Support Email`).

##### **E. Chuyển tiếp email tài chính**
- **Node: Send to Finance Department**
  - Chọn `credentials`: `gmailOAuth2`.
  - **Lưu ý:** Cần cấu hình **email đích** (ví dụ: `finance@doanhnghiep.com`) trong `keyParameters > to`.

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với email mẫu:
   - Gửi email mẫu đến Gmail đã kết nối.
   - Kiểm tra:
     - Email có được phân loại đúng không?
     - Draft email có hợp lý không?
     - Cảnh báo WhatsApp có được gửi không?
2. **Bật Active workflow** sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh prompt cho AI**
   - Mở rộng **node "Creating a Draft"** và **"Create Email"** để thêm **tone voice** phù hợp với doanh nghiệp (ví dụ: chuyên nghiệp, thân thiện, hoặc formal).
   - Ví dụ:
     ```json
     "prompt": "Tóm tắt email này và trả lời với tone voice chuyên nghiệp, ngắn gọn và thân thiện. Đảm bảo bao gồm: [Yêu cầu cụ thể của khách hàng]."
     ```

2. **Lưu log hoạt động**
   - Thêm **node StickyNote** để ghi lại lịch sử phân loại email (ví dụ: `Email từ [Tên khách hàng] đã được phân loại vào [Danh mục] lúc [Thời gian]`).

3. **Gửi báo cáo định kỳ**
   - Sử dụng **node Gmail** kết hợp với **node OpenAI** để tự động tổng hợp báo cáo hàng ngày về số lượng email đã xử lý, phân loại, và tình trạng chưa xử lý.

4. **Kết hợp với Slack/Telegram**
   - Thêm **node Slack** hoặc **Telegram** để cảnh báo các email ưu tiên cao trên kênh nhóm.

5. **Tự động xóa email không cần thiết**
   - Thêm **node Gmail** với `operation: delete` cho email được phân loại là `Random (General/Other)` sau một thời gian (ví dụ: 30 ngày).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc quản lý email thủ công, đồng thời **tăng cường hiệu quả** với AI và tự động hóa hoàn toàn. **Bắt đầu ngay** bằng cách import và cấu hình theo hướng dẫn trên!

👉 **Bước đầu tiên:** [Tải workflow từ n8n.io](https://n8n.io/workflows/7092) và cài đặt VPS cho n8n để chạy 24/7.
👉 **Cần hỗ trợ?** Đăng ký khóa học **Tự động hóa doanh nghiệp với n8n** tại [n8n.vn](https://n8n.vn) để học chi tiết!

---
**Chúc các sếp thành công với hệ thống tự động hóa email hoàn hảo!** 🚀