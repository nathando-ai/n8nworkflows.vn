---
title: "🤖 **Tự Động Hóa Chatbot Trợ Lý Khách Hàng AI trên Facebook Messenger với Google Gemini (N8N)**"
description: "Xây dựng một chatbot AI thông minh tự động trả lời tin nhắn khách hàng trên Facebook Messenger bằng Google Gemini, với tính năng nhớ lịch sử hội thoại và phản hồi nhanh chóng - hoàn toàn không cần code. Giúp doanh nghiệp tiết kiệm thời gian hỗ trợ 24/7 và cải thiện trải nghiệm khách hàng."
slug: "tay-dong-hoa-chatbot-ai-facebook-messenger-google-gemini"
tags: [n8n, automation, ai-chatbot, facebook-messenger, google-gemini, no-code]
keywords: [n8n workflow facebook messenger, tự động hóa chatbot AI, google gemini n8n, hỗ trợ khách hàng tự động, giải pháp chatbot không code]
---

# 🚀 **Chatbot Trợ Lý Khách Hàng AI trên Facebook Messenger với Google Gemini**

### **Giải pháp tự động hóa hỗ trợ khách hàng 24/7 mà không cần code**
Hiện nay, đội ngũ hỗ trợ khách hàng của các sếp thường phải dành nhiều giờ mỗi ngày để trả lời các câu hỏi lặp đi lặp lại trên Facebook Messenger. Với **workflow này**, các sếp có thể xây dựng một **chatbot AI thông minh** tự động trả lời tin nhắn, nhớ lịch sử hội thoại, và phản hồi nhanh chóng - giúp tiết kiệm **tối thiểu 80% thời gian** cho bộ phận hỗ trợ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Hỗ trợ khách hàng 24/7** mà không cần nhân viên trực ca.
- **Trả lời nhanh chóng** với Google Gemini, AI mạnh mẽ nhất hiện nay.
- **Nhớ lịch sử hội thoại** (10 tin nhắn gần nhất) để phản hồi logic và cá nhân hóa.
- **Tiết kiệm thời gian** tối thiểu **80%** cho bộ phận hỗ trợ.
- **Cải thiện trải nghiệm khách hàng** với phản hồi tự động nhưng vẫn chuyên nghiệp.
- **Không cần code** - chỉ cần cấu hình vài bước đơn giản.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n** (self-hosted hoặc cloud).
2. **Facebook Developer Account** và **Facebook Page** muốn tích hợp chatbot.
3. **Facebook Page Access Token** (để xác thực webhook).
4. **Google Gemini API Key** (để sử dụng AI).
5. **URL công khai** (n8n phải được truy cập từ bên ngoài để Facebook gửi tin nhắn).

:::info[CHUẨN BỊ]
- **Facebook Page Access Token**:
  - Tạo tại [Facebook Developers](https://developers.facebook.com/) → **Settings** → **Page Access Tokens**.
  - Chọn quyền `pages_messaging` và `pages_read_engagement`.
- **Google Gemini API Key**:
  - Đăng ký tại [Google AI Studio](https://aistudio.google/) và lấy API key.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/13080](https://n8n.io/workflows/13080).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

#### **🔹 Node "Set Context" (Thiết lập bối cảnh)**
- **Cần thay đổi**:
  - Thay `YOUR_PAGE_ACCESS_TOKEN_HERE` bằng **Facebook Page Access Token** của mình.
  - Kiểm tra các biến `user_id`, `page_id`, `message`, `token` để đảm bảo trích xuất dữ liệu chính xác.

#### **🔹 Node "Facebook Webhook" (Webhook Facebook)**
- **Cấu hình**:
  - Đảm bảo **URL webhook** công khai và đúng định dạng:
    ```
    https://<tên-domain>/webhook/<nguyenthieutoan-facebook-page-1234>
    ```
  - Trong **Facebook Developer Dashboard**, cập nhật **Webhook URL** để nhận tin nhắn từ Messenger.

#### **🔹 Node "Gemini Flash" (Google Gemini AI)**
- **Cấu hình**:
  - Đăng ký **Google Gemini API Key** trong **n8n Credentials**.
  - Chọn **credentials**: `googlePalmApi` (đã được cấu hình sẵn trong workflow).

#### **🔹 Node "Process Merged Message" (Xử lý tin nhắn hợp nhất)**
- **Tùy chỉnh AI**:
  - Các sếp có thể **sửa đổi system prompt** để thay đổi tính cách của chatbot (ví dụ: thân thiện, chuyên nghiệp, hài hước).
  - Ví dụ:
    ```plaintext
    Bạn là một trợ lý hỗ trợ khách hàng chuyên nghiệp. Trả lời ngắn gọn và chính xác.
    ```

#### **🔹 Node "Cut if reply more than 2000 characters" (Cắt tin nhắn quá dài)**
- **Lưu ý**:
  - Facebook Messenger có giới hạn **2000 ký tự** cho mỗi tin nhắn.
  - Workflow tự động **cắt và giữ lại 1900 ký tự** để tránh lỗi.

#### **🔹 Node "Send Text" (Gửi tin nhắn)**
- **Kiểm tra**:
  - Đảm bảo **URL API** của Facebook Messenger đúng và có quyền truy cập.

### **3. Kích hoạt ⚡️**
1. **Test run** với một tin nhắn mẫu:
   - Gửi tin nhắn từ **Facebook Messenger** đến Page của mình.
   - Kiểm tra phản hồi của chatbot.
2. **Bật Active workflow** trong n8n.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với Slack/Telegram**:
  - Sử dụng node **HTTP Request** để gửi báo cáo hoạt động chatbot lên Slack/Telegram.
- **Lưu log hội thoại**:
  - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử tin nhắn.
- **Gửi báo cáo định kỳ**:
  - Sử dụng **n8n Scheduler** để gửi báo cáo tổng hợp về số lượng tin nhắn, chủ đề phổ biến.
- **Tăng cường tính cá nhân hóa**:
  - Sử dụng **Google Gemini** để phân tích cảm xúc và trả lời phù hợp.
:::

---

## 📌 **Kết luận**
Với **workflow này**, các sếp đã có một **chatbot AI hỗ trợ khách hàng** hoàn toàn tự động, không cần code, và hoạt động 24/7. Đặc biệt, nó **nhớ lịch sử hội thoại**, giúp phản hồi logic và chuyên nghiệp hơn.

**Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất hỗ trợ khách hàng!**

---
### **🔗 Tài liệu tham khảo**
- [Tutorial chi tiết từ tác giả](https://n8n.io/workflows/13080)
- [Cách lấy Facebook Page Access Token](https://developers.facebook.com/docs/pages/messages/get-started-webhooks/)
- [Google Gemini API Documentation](https://ai.google.dev/gemini-api/docs)

---
### **⚠️ Lưu ý quan trọng**
- **Không sử dụng cho mục đích spam** hoặc vi phạm chính sách của Facebook.
- **Test cẩn thận** trước khi triển khai trên Page thực tế.
- **Nếu cần nâng cấp**, xem các workflow nâng cao như:
  - [Smart message batching](https://n8n.io/workflows/9192) (tránh spam)
  - [Smart human takeover](https://n8n.io/workflows/11920) (hỗ trợ chuyển giao cho nhân viên)