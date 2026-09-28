---
title: "🔄 Hướng Dẫn Tự Động Hóa Hệ Thống Chatbot WhatsApp ↔ Telegram Cho 10K+ Khách Hàng (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn miễn phí kết nối WhatsApp và Telegram thành một hệ thống hỗ trợ khách hàng song phương, tạo topic riêng cho mỗi khách hàng, đồng bộ tin nhắn hai chiều và lưu trữ dữ liệu trong Supabase. Tiết kiệm 90% thời gian phản hồi và nâng cao trải nghiệm khách hàng."
slug: "tieu-dong-hoa-chatbot-whatsapp-telegram"
tags: [n8n, automation, no-code, chatbot, customer-support, telegram-bot, whatsapp-api, supabase]
keywords: [n8n workflow chatbot, tự động hóa whatsapp telegram, hệ thống hỗ trợ khách hàng song phương, tạo topic telegram cho khách hàng, đồng bộ tin nhắn whatsapp telegram, supabase database]
---

# 🚀 **Tự Động Hóa Hệ Thống Chatbot WhatsApp ↔ Telegram Cho 10K+ Khách Hàng (Không Cần Code)**

---

## **💥 Nỗi Đau Của Các Sếp Trong Hỗ Trợ Khách Hàng**
Hiện nay, các doanh nghiệp thường phải **quét qua nhiều nền tảng** (WhatsApp, Telegram, Email, Facebook Messenger) để hỗ trợ khách hàng, dẫn đến:
- **Thời gian phản hồi chậm** (trung bình 24-48 giờ).
- **Tin nhắn bị mất liên kết** giữa các kênh, khiến khách hàng phải giải thích lại vấn đề.
- **Không theo dõi được lịch sử tương tác** của từng khách hàng.
- **Không thể tự động hóa** việc chuyển tiếp tin nhắn giữa WhatsApp và Telegram.

**Giải pháp?** Một **hệ thống tự động song phương** kết nối WhatsApp và Telegram, **tạo topic riêng cho mỗi khách hàng**, đồng bộ tin nhắn hai chiều và **lưu trữ dữ liệu trong cơ sở dữ liệu** để quản lý hiệu quả.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động tạo topic Telegram riêng cho mỗi khách hàng** (không cần quản lý thủ công).
✅ **Đồng bộ tin nhắn hai chiều** giữa WhatsApp và Telegram (khách hàng và nhân viên đều có thể gửi tin nhắn).
✅ **Lưu trữ lịch sử tương tác** trong **Supabase** (PostgreSQL) để theo dõi và phân tích.
✅ **Tiết kiệm 90% thời gian phản hồi** so với cách làm thủ công.
✅ **Hoạt động liên tục 24/7** (không cần nhân viên trực đêm).
✅ **Scale lên 10K+ khách hàng** mà không lo bị treo hoặc chậm.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản WhatsApp Cloud API** (Meta Business):
   - **Phone Number ID** và **Access Token** (mua trên [Meta Developer Portal](https://developers.facebook.com/)).
2. **Bot Telegram** với quyền **manage topics** trong **supergroup forum**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather).
   - Thêm bot vào **supergroup Telegram** với chức năng **Forum** (để tạo topic).
3. **Cơ sở dữ liệu Supabase** (hoặc PostgreSQL):
   - Tạo bảng `wa_tg_threads` với các trường:
     ```sql
     CREATE TABLE wa_tg_threads (
       id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
       phone_e164 VARCHAR(20) UNIQUE NOT NULL,
       supergroup_id BIGINT NOT NULL,
       telegram_topic_id BIGINT NOT NULL,
       created_at TIMESTAMP DEFAULT NOW(),
       updated_at TIMESTAMP DEFAULT NOW()
     );
     ```
4. **Supergroup Telegram Forum** (để tạo topic cho từng khách hàng).
5. **n8n Self-Hosted** (khuyến nghị dùng VPS để tránh giới hạn cloud).

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Workflow này bao gồm **2 phần chính**:
- **Workflow 1**: Nhận tin nhắn từ WhatsApp → Tạo topic Telegram mới (nếu chưa có) → Gửi tin nhắn đến Telegram.
- **Workflow 2**: Nhận tin nhắn từ Telegram → Tìm kiếm khách hàng tương ứng → Gửi tin nhắn lại WhatsApp.

#### **Hướng dẫn import:**
1. **Tải file JSON** từ [n8n.io/workflows/8350](https://n8n.io/workflows/8350).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON.
3. **Hoặc copy/paste JSON** vào **Import Workflow** trong n8n.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Cấu hình Telegram Trigger & WhatsApp Trigger**
- **Telegram Trigger**:
  - Điền **Telegram Bot Token** vào `credentials.telegramApi`.
  - Chọn **Supergroup ID** (đặt trước trong `Set Telegram SuperGroupID` node).
- **WhatsApp Trigger**:
  - Điền **Phone Number ID** và **Access Token** vào `credentials.whatsappTriggerApi`.

#### **🔹 Cấu hình Supabase**
- **Credentials**:
  - Điền **URL Supabase** và **API Key** vào `credentials.supabaseApi`.
- **Query trong "Get a row" và "Get existing customer details"**:
  - Đảm bảo bảng `wa_tg_threads` có cấu trúc như trên.
  - Cập nhật **filter conditions** để trùng khớp với `phone_e164` (số điện thoại của khách hàng).

#### **🔹 Cấu hình HTTP Requests (Telegram API)**
- **Thêm Bot Token vào URL**:
  - Trong các node `httpRequest` (ví dụ: `Create a Telegram Topic`), thay thế `$TELEGRAM_BOT_TOKEN` bằng **Bot Token** của bạn.
  - Ví dụ:
    ```json
    "url": "https://api.telegram.org/bot{{$credentials.telegramApi.token}}/createForumTopic"
    ```
- **Supergroup ID**:
  - Đặt **Supergroup ID** trong `Set Telegram SuperGroupID` node (đọc từ Telegram: `@myidbot` → `/getchat -1001234567890`).

#### **🔹 Cấu hình "If" Conditions**
- **Check existing conversation**:
  - Đảm bảo điều kiện trong `Check existing conversation or not` node trùng khớp với logic:
    - Nếu `telegram_topic_id` **không tồn tại** → Tạo topic mới.
    - Nếu tồn tại → Gửi tin nhắn vào topic cũ.

#### **🔹 Set Customer Name & Phone**
- Trong `Set Customer Name`, sử dụng **regex** để trích xuất tên từ tin nhắn WhatsApp (ví dụ: `phone_e164` + tên khách hàng).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Gửi tin nhắn từ WhatsApp đến số điện thoại đã đăng ký.
   - Kiểm tra:
     - Topic Telegram có được tạo không?
     - Tin nhắn có được gửi đến Telegram không?
   - Sau đó, gửi tin nhắn từ Telegram vào topic đó và kiểm tra tin nhắn có được gửi lại WhatsApp không?
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển workflow từ **Draft** sang **Active**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tự Động Xóa Topic Idle**
- Thêm **node `Set`** sau `Create a row` để lưu `last_activity_at`.
- Sử dụng **node `Schedule`** (n8n Premium) hoặc **node `If` + `Set`** để xóa topic nếu không hoạt động trong 7 ngày.

### **2. Gửi Báo Cáo Định Kỳ**
- Sử dụng **node `Schedule`** (n8n Premium) hoặc **node `HTTP Request`** để gửi báo cáo hoạt động (số tin nhắn, khách hàng mới,...) đến Email/Slack.

### **3. Kết Nối Với CRM (Zoho, HubSpot, Salesforce)**
- Thêm **node `HTTP Request`** để gửi dữ liệu khách hàng vào CRM khi có tin nhắn mới.

### **4. Lọc Tin Nhắn VIP**
- Sử dụng **node `If`** để kiểm tra `phone_e164` có trong danh sách VIP không.
- Nếu là VIP, gửi tin nhắn thông báo đến Slack/Email của quản lý.

### **5. Lưu Log Tin Nhắn**
- Thêm **node `Set`** để lưu tin nhắn vào bảng `chat_logs` trong Supabase:
  ```sql
  CREATE TABLE chat_logs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    phone_e164 VARCHAR(20) NOT NULL,
    message TEXT NOT NULL,
    channel VARCHAR(10) NOT NULL, -- 'whatsapp' or 'telegram'
    timestamp TIMESTAMP DEFAULT NOW()
  );
  ```

---

## **📌 Kết Luận**
Workflow này **giải quyết hoàn toàn tự động hóa** việc kết nối WhatsApp và Telegram, **tạo topic riêng cho mỗi khách hàng**, đồng bộ tin nhắn hai chiều và **lưu trữ dữ liệu trong Supabase**. Đây là **giải pháp hoàn hảo** cho các doanh nghiệp muốn:
✔ **Tiết kiệm thời gian phản hồi**.
✔ **Nâng cao trải nghiệm khách hàng**.
✔ **Scale lên 10K+ khách hàng** mà không lo bị treo.

**Hành động ngay!**
1. **Chuẩn bị tài khoản WhatsApp & Telegram** (nếu chưa có).
2. **Tạo bảng `wa_tg_threads` trong Supabase**.
3. **Import workflow** và **cấu hình theo hướng dẫn**.
4. **Test và kích hoạt** để bắt đầu tự động hóa hỗ trợ khách hàng!

---
**💬 Có thắc mắc? Hãy để lại comment bên dưới hoặc liên hệ [info@zenithworks.ai](mailto:info@zenithworks.ai) để được hỗ trợ chi tiết!**