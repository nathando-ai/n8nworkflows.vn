---
title: "🤖 **Tự Động Hẹn Lịch Dịch Vụ HVAC Qua WhatsApp Với GoHighLevel & Gemini AI** - Giải Pháp Chatbot 24/7 Cho Doanh Nghiệp"
description: "Workflow tự động hóa hoàn toàn không cần code giúp khách hàng đặt lịch hẹn dịch vụ HVAC qua WhatsApp, với hỗ trợ AI Gemini xử lý yêu cầu và tích hợp CRM GoHighLevel. Giảm thiểu công việc thủ công, tăng trải nghiệm khách hàng và tối ưu hóa lịch làm việc."
slug: "tieu-dong-hoan-lich-hvac-qua-whatsapp-gohighlevel-gemini"
tags: [n8n, automation, no-code, chatbot-ai, gohighlevel, gemini-ai, whatsapp-business]
keywords: [tự động hóa đặt lịch hvac, chatbot whatsapp tự động, gemini ai cho doanh nghiệp, gohighlevel automation, workflow n8n hỗ trợ khách hàng]
---

# 🚀 **Tự Động Hẹn Lịch Dịch Vụ HVAC Qua WhatsApp Với GoHighLevel & Gemini AI**

## **Giới Thiệu**
Các sếp đang gặp phải vấn đề gì khi quản lý dịch vụ HVAC?
- **Lặp đi lặp lại**: Phải trả lời hàng trăm tin nhắn đặt lịch hàng ngày, mất thời gian và dễ mắc lỗi.
- **Không đồng bộ**: Thông tin khách hàng phân tán giữa WhatsApp và hệ thống CRM, dẫn đến trải nghiệm kém.
- **Không cá nhân hóa**: Trả lời chung chung, không hiểu được nhu cầu cụ thể của khách hàng.
- **Không hoạt động 24/7**: Khi bạn ngủ, khách hàng vẫn có thể gửi yêu cầu.

**Workflow này giải quyết tất cả!** Với sự kết hợp giữa **GoHighLevel** (CRM chuyên nghiệp), **Gemini AI** (mô hình ngôn ngữ lớn của Google), và **n8n** (tự động hóa không code), các sếp có thể:
✅ **Đặt lịch tự động** qua WhatsApp mà không cần can thiệp thủ công.
✅ **Hỗ trợ AI 24/7** xử lý yêu cầu khách hàng, trả lời nhanh chóng và chính xác.
✅ **Tích hợp CRM** để lưu trữ thông tin khách hàng và lịch hẹn một cách đồng bộ.
✅ **Tiết kiệm thời gian** lên đến **80%** trong quản lý đặt lịch.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải trả lời tin nhắn đặt lịch thủ công, tự động hóa 100% quá trình.
- **Trải nghiệm khách hàng cao**: AI Gemini trả lời nhanh chóng, cá nhân hóa và hiểu được nhu cầu.
- **Dữ liệu đồng bộ**: Thông tin khách hàng và lịch hẹn tự động lưu vào GoHighLevel, tránh mất mát.
- **Hoạt động 24/7**: Khách hàng có thể đặt lịch bất kỳ lúc nào, kể cả khi các sếp offline.
- **Giảm lỗi**: AI kiểm tra lịch trống và xác nhận trước khi đặt, tránh xung đột.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản WhatsApp Business API**:
   - Đăng ký API từ [Meta for Developers](https://developers.facebook.com/) và cấu hình webhook cho n8n.
   - **Lưu ý**: Các sếp cần **phone number ID** và **access token** để kết nối với n8n.

2. **Tài khoản GoHighLevel**:
   - Tạo **OAuth 2.0 API Key** trong GoHighLevel (Settings > API).
   - Các sếp cần quyền **Admin** để truy cập dữ liệu CRM và lịch.

3. **Google Gemini API**:
   - Tạo **API Key** từ [Google AI Studio](https://aistudio.google.com/).
   - Chọn mô hình **Gemini Pro** hoặc **Gemini 1.5** để sử dụng trong workflow.

4. **Redis Server** (để lưu trữ lịch sử chat):
   - Cài đặt Redis trên VPS hoặc sử dụng dịch vụ cloud như **Redis Labs**.
   - **Lưu ý**: Các sếp cần **URL Redis** và **password** (nếu có).

5. **Tài khoản n8n**:
   - Cài đặt n8n trên VPS hoặc sử dụng phiên bản cloud (n8n.io).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1**: Tải file JSON từ [n8n.io/workflows/15777](https://n8n.io/workflows/15777) hoặc copy toàn bộ JSON từ đây.
- **Bước 2**: Mở **n8n Editor** và chọn **"Import"** > **"From JSON"**.
- **Bước 3**: Dán JSON và nhấn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **11 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **A. Cấu hình WhatsApp Trigger**
- **Node**: `When WhatsApp Message Received`
  - **Credentials**: Chọn `whatsAppTriggerApi` (đã tạo trước khi import).
  - **Webhook URL**: Đảm bảo URL này trùng khớp với URL đã đăng ký trên Meta for Developers.
  - **Test**: Gửi tin nhắn mẫu đến số WhatsApp đã kết nối để kiểm tra trigger hoạt động.

##### **B. Kiểm tra và cấu hình GoHighLevel**
- **Node**: `Fetch GHL Contacts` và `Update Contact Tool`
  - **Credentials**: Chọn `highLevelOAuth2Api` (API Key từ GoHighLevel).
  - **Test**: Chạy node `Fetch GHL Contacts` để đảm bảo kết nối với CRM thành công.

##### **C. Cấu hình Gemini AI**
- **Node**: `Gemini Chat Model`
  - **Credentials**: Chọn `googlePalmApi` (API Key từ Google AI Studio).
  - **Prompt**: Các sếp có thể tùy chỉnh prompt để phù hợp với dịch vụ HVAC (ví dụ: *"Hãy hỗ trợ khách hàng đặt lịch dịch vụ HVAC và trả lời các câu hỏi về sản phẩm."*).

##### **D. Cấu hình Redis Chat Memory**
- **Node**: `Redis Chat Memory`
  - **Credentials**: Chọn `redis` (URL và password Redis).
  - **Test**: Chạy node này để đảm bảo lưu trữ lịch sử chat hoạt động.

##### **E. Cấu hình Tools cho AI Agent**
- **Node**: `Customer Service Agent` (Agent LangChain)
  - **Tools**:
    - `Fetch Calendar Slots Tool`: Kiểm tra lịch trống trong GoHighLevel.
    - `Book Appointment Tool`: Đặt lịch tự động.
    - `Save User Issue Tool`: Lưu vấn đề của khách hàng.
    - `Update Contact Tool`: Cập nhật thông tin khách hàng.
  - **Credentials**: Đảm bảo tất cả các tool sử dụng `highLevelOAuth2Api`.

##### **F. Cấu hình Node "If Valid Sender Exists"**
- **Node**: `If Valid Sender Exists`
  - **Conditions**: Các sếp cần định nghĩa rõ ràng điều kiện để xác thực người gửi (ví dụ: số điện thoại đã đăng ký trong GoHighLevel).
  - **Test**: Gửi tin nhắn từ số chưa đăng ký để kiểm tra logic reject.

##### **G. Cấu hình Node "Send WhatsApp Message"**
- **Node**: `Send WhatsApp Message`
  - **Credentials**: Chọn `whatsAppApi` (API Key WhatsApp Business).
  - **Test**: Gửi tin nhắn mẫu để đảm bảo kết nối hoạt động.

---

#### **3. Kích hoạt ⚡️**
- **Bước 1**: Chạy **Test Run** với dữ liệu mẫu (ví dụ: tin nhắn *"Tôi muốn đặt lịch sửa chữa máy lạnh vào ngày mai"*).
- **Bước 2**: Kiểm tra:
  - AI có trả lời chính xác không?
  - Lịch hẹn có được tạo trong GoHighLevel không?
  - Tin nhắn phản hồi có được gửi về WhatsApp không?
- **Bước 3**: Nếu tất cả hoạt động đúng, **bật Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram để báo cáo**:
   - Sử dụng node **Slack** hoặc **Telegram** để gửi thông báo khi có yêu cầu đặt lịch mới.
   - Ví dụ: *"Khách hàng [Tên] đã đặt lịch sửa chữa máy lạnh vào ngày 10/10."*

2. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** hoặc **Google Sheets** để lưu trữ lịch sử chat và phản hồi của AI.
   - Có thể phân tích để cải thiện chất lượng hỗ trợ.

3. **Tùy chỉnh AI với prompt chuyên nghiệp**:
   - Thay đổi prompt trong `Gemini Chat Model` để AI hiểu rõ hơn về dịch vụ HVAC của các sếp.
   - Ví dụ: *"Hãy trả lời khách hàng bằng giọng điệu thân thiện và chuyên nghiệp. Nếu khách hàng hỏi về giá, hãy trả lời: 'Giá dịch vụ phụ thuộc vào loại máy và tình trạng hiện tại. Tôi sẽ liên hệ lại để tư vấn chi tiết.'"*

4. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng node **Google Sheets** hoặc **Email** để gửi báo cáo tổng hợp số lượng đặt lịch, loại dịch vụ phổ biến, và thời gian phản hồi trung bình.

5. **Kết hợp với CRM khác**:
   - Nếu các sếp sử dụng **HubSpot** hoặc **Zoho CRM**, có thể thay thế GoHighLevel bằng API của hệ thống đó.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quá trình đặt lịch dịch vụ HVAC qua WhatsApp, giảm thiểu công việc thủ công và nâng cao trải nghiệm khách hàng. Với sự hỗ trợ của **Gemini AI**, các sếp có thể yên tâm rằng khách hàng sẽ được trả lời nhanh chóng và chính xác, ngay cả khi hệ thống hoạt động 24/7.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản** (WhatsApp API, GoHighLevel, Google Gemini, Redis).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và bật hoạt động** để tiết kiệm thời gian và nâng cao hiệu suất dịch vụ!

---
**Cần hỗ trợ thêm?** Liên hệ với tác giả Abhi Vaar qua [Calendly](https://cal.com/abhi.vaar/n8n) để tùy chỉnh workflow phù hợp với nhu cầu cụ thể của doanh nghiệp!