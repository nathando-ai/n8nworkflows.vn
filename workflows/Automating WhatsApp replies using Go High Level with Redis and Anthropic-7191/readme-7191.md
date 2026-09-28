---
title: "🤖 Tự Động Hóa Trả Lời WhatsApp Với AI + Go High Level, Redis & Claude Sonnet 4 - Giảm Chi Phí 90%"
description: "Workflow này tự động hóa hoàn toàn quá trình trả lời tin nhắn WhatsApp/SMS từ Go High Level bằng AI Claude Sonnet 4, sử dụng Redis để buffer tin nhắn và tránh chi phí inbound. Giúp doanh nghiệp tiết kiệm thời gian, cải thiện trải nghiệm khách hàng và tự động hóa 100% không cần code."
slug: "tieu-dong-hoa-tra-loi-whatsapp-voi-ai-ghl-redis-claude"
tags: [n8n, automation, no-code, ai-chatbot, go-high-level, whatsapp-business, redis, anthropic, claude-sonnet, multimodal-ai]
keywords: [tự động hóa whatsapp go high level, trả lời tin nhắn whatsapp tự động, ai trả lời whatsapp, giảm chi phí inbound whatsapp, workflow n8n ai, redis buffer tin nhắn, claude sonnet 4 tự động hóa]
---

# 🚀 **Tự Động Hóa Trả Lời WhatsApp/SMS Với AI Claude Sonnet 4, Go High Level & Redis**

## **🔥 Giải Pháp Cho Doanh Nghiệp Bị "Đánh Đầu" Bởi Tin Nhắn WhatsApp**
Hàng ngày, doanh nghiệp phải đối mặt với hàng trăm tin nhắn WhatsApp/SMS từ khách hàng, yêu cầu trả lời nhanh chóng và chính xác. Nếu làm thủ công:
- **Tốn thời gian**: Đội ngũ phải ngồi "chăm sóc" liên tục.
- **Chất lượng không đồng nhất**: Trả lời chậm hay sai lệch gây mất niềm tin.
- **Chi phí cao**: Go High Level tính phí cho mỗi tin nhắn inbound (khoảng **10.000-15.000 VND/tin nhắn**).
- **Không cá nhân hóa**: Trả lời chung chung làm mất tính chuyên nghiệp.

**Workflow này giải quyết tất cả!** Sử dụng **AI Claude Sonnet 4** để trả lời tự động, **Redis** để buffer tin nhắn tránh chi phí inbound, và **Go High Level** để gửi trả lời một cách miễn phí (thông qua custom field).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% chi phí inbound**: Không tính phí cho tin nhắn khách hàng gửi vào.
- **Trả lời nhanh chóng & chính xác**: AI Claude Sonnet 4 trả lời dựa trên dữ liệu **ClientInfo** (Excel/Google Drive) để đảm bảo tính chuyên nghiệp.
- **Cá nhân hóa từng tin nhắn**: Hỗ trợ khách hàng một cách thân thiện và chuyên nghiệp.
- **Hoạt động 24/7**: Không cần người dùng trực tiếp, tự động hóa hoàn toàn.
- **Giảm tải cho đội ngũ**: Đội CSKH tập trung vào vấn đề phức tạp hơn thay vì trả lời tin nhắn đơn giản.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Go High Level (GHL)** với:
   - **API Key** của sub-account.
   - **Plugin Wazzap** (để xử lý tin nhắn WhatsApp).
   - **Custom field** tên là `IA_answer` (để lưu trả lời AI).
   - **Automation inbound**: Trigger khi khách hàng trả lời SMS/WhatsApp → gửi payload đến **Webhook n8n**.
   - **Automation outbound**: Trigger khi `IA_answer` được cập nhật → gửi SMS trả lời tự động.

2. **Redis Database** (miễn phí hoặc tự host):
   - Host (ví dụ: `redis-12345.caches.ngrok.io`).
   - Port (thường là `6379`).
   - DB index (ví dụ: `0`).
   - Password (nếu có).

3. **API Key Anthropic (Claude Sonnet 4)**:
   - Đăng ký tại [Anthropic Developer Portal](https://www.anthropic.com/api).
   - Thêm vào n8n dưới **Credentials** → `httpBearerAuth`.

4. **Google Drive (nếu sử dụng ClientInfo từ Excel)**:
   - File Excel có 2 sheet: `tests` và `sites`.
   - API Key Google Drive OAuth 2.0 (cài đặt tại [Google Cloud Console](https://console.cloud.google.com/)).

5. **n8n Self-hosted** (không dùng phiên bản free):
   - Đăng ký VPS tại [TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172) (VPS Xeon 4GB chỉ 50k/tháng).
   - Cài đặt n8n theo [hướng dẫn official](https://docs.n8n.io/hosting/installation/self-hosted/).
---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7191](https://n8n.io/workflows/7191) hoặc copy toàn bộ JSON từ link trên.
- Trong **n8n Editor**, nhấn **Import** → Dán JSON hoặc tải file JSON.
- **Không** nhấn **Active** ngay, phải cấu hình trước!

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Webhook (Node "Webhook")**
- **Path**: `fce352e8-8edf-447c-9b54-c2c2b6649ccc` (không đổi).
- **HTTP Method**: `POST`.
- **Credentials**: Không cần (Webhook nhận payload từ GHL).

#### **B. Cấu Hình Redis (Node "Save message", "Get messages", "Delete messages")**
- **Host**: Địa chỉ Redis (ví dụ: `redis-12345.caches.ngrok.io`).
- **Port**: `6379`.
- **DB Index**: `0` (hoặc số khác nếu đã cấu hình).
- **Password**: Nếu Redis có mật khẩu, điền vào.
- **Key Format**: Sử dụng `contact_id` từ payload GHL (ví dụ: `contact_12345`).

#### **C. Cấu Hình Anthropic (Node "Anthropic Chat Model")**
- **Model**: `claude-sonnet-4-20250514` (đã mặc định).
- **API Key**: Thêm vào **Credentials** → `httpBearerAuth` (tên tương tự như trong node `Update Contact`).

#### **D. Cấu Hình Go High Level API (Node "Update Contact", "GHL Custom fields")**
- **Credentials**: Sử dụng `httpBearerAuth` (điền API Key GHL).
- **Endpoint**:
  - `GET /api/v2/contacts/{contactId}/custom_fields` (lấy danh sách custom fields).
  - `PUT /api/v2/contacts/{contactId}/custom_fields/{fieldId}` (cập nhật `IA_answer`).

#### **E. Cấu Hình ClientInfo (Sub-Workflow) - Nếu Sử Dụng**
- **Tạo workflow riêng** để trích xuất dữ liệu từ Excel (Google Drive).
- **Cấu hình node "Extract Tests" và "Extract Sites"** để đọc sheet `tests` và `sites`.
- **Merge data** trước khi gửi cho AI.

#### **F. Cấu Hình Sanitize Message (Node "Sanitize and Format Message Body")**
- **Mã JavaScript** trong node `code` sẽ:
  - Sửa lỗi quote bị escape (`\"` → `"`).
  - Escape line breaks, tabs, và carriage returns.
  - Trim whitespace.
- **Không cần chỉnh** nếu không hiểu code, nhưng **bắt buộc phải chạy** để tránh lỗi.

#### **G. Cấu Hình Wait (Node "Wait")**
- **Thời gian đợi**: `15000` ms (15 giây) để buffer tin nhắn.
- Nếu khách hàng gửi nhiều tin nhắn liên tiếp, AI sẽ trả lời tất cả cùng một lúc.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với payload mẫu từ GHL:
   - Gửi tin nhắn WhatsApp/SMS từ GHL đến Webhook.
   - Kiểm tra log trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - Kiểm tra **Automation outbound** trong GHL đã được cấu hình đúng không.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa AI Trả Lời**
- **Cập nhật System Prompt** trong node `AI Agent` để phù hợp với ngành nghề:
  ```json
  {
    "role": "system",
    "content": "Bạn là trợ lý hỗ trợ khách hàng của [Tên Doanh Nghiệp]. Trả lời dựa trên dữ liệu từ ClientInfo. Nếu không biết, hãy nói 'Tôi sẽ liên hệ lại với bạn' và ghi nhớ yêu cầu."
  }
  ```
- **Thêm Context** từ tin nhắn trước đó (nếu khách hàng hỏi nhiều câu liên tiếp).

### **2. Lưu Log Tin Nhắn**
- Thêm node **Google Drive** hoặc **Slack** để lưu lịch sử tin nhắn và trả lời.
- Ví dụ:
  ```json
  {
    "name": "Log to Google Drive",
    "type": "googleDrive",
    "operation": "createFile",
    "fileName": "whatsapp_logs_${date}.xlsx",
    "credentials": ["googleDriveOAuth2Api"]
  }
  ```

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **n8n Cron Trigger** để gửi báo cáo tổng hợp tin nhắn và trả lời hàng ngày qua Email/Slack.

### **4. Xử Lý Tin Nhắn Audio**
- Nếu khách hàng gửi tin nhắn audio (không thể đọc được), workflow sẽ tự động trả lời:
  ```json
  {
    "content": "Xin lỗi, tôi không thể đọc tin nhắn audio. Hãy gửi lại tin nhắn văn bản để tôi hỗ trợ!"
  }
  ```

### **5. Cập Nhật Dữ Liệu ClientInfo**
- Nếu dữ liệu trong Excel thay đổi, **cập nhật sub-workflow** để AI có thông tin mới nhất.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho doanh nghiệp sử dụng Go High Level muốn:
✅ **Tự động hóa trả lời WhatsApp/SMS 100% không cần code**.
✅ **Giảm chi phí inbound xuống gần 0** (chỉ trả phí cho tin nhắn outbound).
✅ **Cải thiện trải nghiệm khách hàng** với trả lời nhanh chóng và chính xác.
✅ **Tiết kiệm thời gian** cho đội ngũ CSKH.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (đăng ký tại [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172)).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Kích hoạt** và theo dõi kết quả!

**Nếu có vấn đề**, để lại comment bên dưới hoặc liên hệ tôi qua [Facebook](https://facebook.com/tencuaban) để hỗ trợ!

---
**💡 Chúc các sếp thành công với tự động hóa WhatsApp!** 🚀