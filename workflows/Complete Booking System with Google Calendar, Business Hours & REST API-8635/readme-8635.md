---
title: "📅 Hệ Thống Đặt Hẹn Toàn Tự Động với Google Calendar, Giờ Mở Cửa & API REST - N8n"
description: "Workflow này tự động hóa toàn bộ quy trình đặt hẹn từ xác thực thông tin khách hàng đến kiểm tra lịch trống, thời gian làm việc và ngày lễ, đồng thời tạo sự kiện trên Google Calendar. Giúp doanh nghiệp tiết kiệm 80% thời gian quản lý đặt hẹn thủ công."
slug: "he-thong-dat-hen-toan-tu-dong-google-calendar"
tags: [n8n, automation, google-calendar, api-rest, booking-system, no-code]
keywords: [n8n workflow đặt hẹn, tự động hóa đặt hẹn Google Calendar, API REST đặt hẹn, hệ thống đặt hẹn tự động, kiểm tra lịch trống, giờ làm việc doanh nghiệp]
---

# 🚀 **Hệ Thống Đặt Hẹn Toàn Tự Động với Google Calendar, Giờ Mở Cửa & API REST**

## **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, việc quản lý đặt hẹn thủ công không chỉ tốn thời gian mà còn dễ gây lỗi như:
- **Thông tin khách hàng không chính xác** (tên, email, số điện thoại sai định dạng).
- **Khách hàng đặt hẹn vào thời gian không phù hợp** (ngày lễ, giờ nghỉ trưa, ngoài giờ làm việc).
- **Trùng lịch** (khách hàng đặt cùng thời gian với sự kiện khác).
- **Không đồng bộ hóa** (lịch đặt hẹn không tự động cập nhật trên Google Calendar).

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Xác thực tự động** thông tin khách hàng (tên, email, số điện thoại).
✅ **Kiểm tra thời gian hợp lệ** (ngày lễ, giờ làm việc, tránh trùng lịch).
✅ **Tạo sự kiện trên Google Calendar** ngay khi đặt hẹn thành công.
✅ **Cung cấp API REST** để frontend dễ dàng tích hợp (React, Vue, Flutter...).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** quản lý đặt hẹn thủ công.
- **Tránh lỗi trùng lịch** và ngày lễ tự động.
- **Cung cấp API REST** để frontend tích hợp dễ dàng.
- **Lịch đặt hẹn tự động đồng bộ** trên Google Calendar.
- **Cá nhân hóa thông báo** cho khách hàng (email, tin nhắn).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để kết nối với Google Calendar).
2. **API Key Google Calendar OAuth2** (cài đặt theo [hướng dẫn n8n](https://docs.n8n.io/integrations/builtin/credentials/google/)).
3. **Hai lịch Google Calendar**:
   - **Lịch công việc chính** (vd: `suarify-booking-calendar`).
   - **Lịch ngày lễ công cộng** (vd: `malaysia-public-holidays`).
4. **Thời gian làm việc** (cấu hình trong node `ConfigTimeSlots`).
5. **Domain hoặc endpoint webhook** (để frontend gọi API).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8635](https://n8n.io/workflows/8635) hoặc copy JSON từ canvas.
- **Nhập vào n8n Editor**:
  - Mở n8n Studio → **Import Workflow** → Dán JSON → **Import**.
  - **Hoặc** tạo workflow mới → **Paste JSON** từ file.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **2 endpoint chính**:
- **`/make-booking`** (đặt hẹn mới).
- **`/check-booking-date`** (kiểm tra thời gian trống cho ngày cụ thể).

##### **A. Cấu Hình Google Calendar**
1. **Tạo Credentials Google Calendar**:
   - Trong n8n Studio → **Credentials** → **Add Credential** → Chọn **Google Calendar OAuth2**.
   - Đăng nhập Google → Cho phép quyền truy cập → Lưu.
   - **Ghi nhớ tên credential** (vd: `googleCalendarOAuth2Api`) để sử dụng trong nodes.

2. **Cấu hình lịch trong nodes**:
   - Mở node **`Create Calendar Event`**, **`Check Calendar Availability`**, **`Check Public Holiday Calendar`**.
   - Điền **Calendar ID** của lịch công việc và lịch ngày lễ (vd: `suarify-booking-calendar@group.calendar.google.com`).

##### **B. Cấu Hình Thời Gian Làm Việc**
1. Mở node **`ConfigTimeSlots`** (type: **Set**).
2. Cập nhật tham số `businessHours` theo định dạng:
   ```json
   {
     "open": "09:00",
     "close": "18:00",
     "lunchBreak": {
       "start": "12:00",
       "end": "13:00"
     },
     "dinnerBreak": {
       "start": "17:00",
       "end": "17:30"
     }
   }
   ```
   - **Giờ mở cửa**: Thời gian công ty bắt đầu làm việc.
   - **Giờ nghỉ trưa/dinner**: Thời gian không cho phép đặt hẹn.

##### **C. Xác Thực Webhook**
1. **Endpoint `/make-booking`** (đặt hẹn mới):
   - **HTTP Method**: `POST`.
   - **Body Example**:
     ```json
     {
       "name": "John Doe",
       "email": "john@example.com",
       "phone": "+60123456789",
       "date": "2025-09-17",
       "time": "14:30",
       "source": "Booking System"
     }
     ```
   - **Trả về**:
     ```json
     {
       "success": true,
       "message": "Booking confirmed!",
       "bookingDetails": { ... },
       "eventLink": "https://calendar.google.com/..."
     }
     ```

2. **Endpoint `/check-booking-date`** (kiểm tra thời gian trống):
   - **HTTP Method**: `POST`.
   - **Body Example**:
     ```json
     { "date": "2025-09-18" }
     ```
   - **Trả về**:
     ```json
     {
       "success": true,
       "availableSlots": [
         { "time": "15:30", "available": true },
         { "time": "17:30", "available": true }
       ]
     }
     ```

##### **D. Test Run**
- **Gửi request mẫu** bằng Postman hoặc cURL:
  ```bash
  curl -X POST 'https://your-n8n-domain/webhook-test/suarify-make-booking'
  -H 'Content-Type: application/json'
  -d '{
    "name":"John Doe",
    "email":"john@example.com",
    "phone":"+60123456789",
    "date":"2025-09-17",
    "time":"14:30"
  }'
  ```
- **Kiểm tra response** và sửa lỗi nếu có.

##### **E. Bật Workflow**
- Sau khi cấu hình xong, **bật chế độ Active** trong n8n Studio.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Gửi thông báo tự động** cho khách hàng:
   - Thêm node **Email** (vd: SendGrid) hoặc **Slack/Telegram** để gửi xác nhận đặt hẹn.
   - Ví dụ: Khi đặt hẹn thành công, gửi tin nhắn Slack:
     ```json
     {
       "text": "📅 Booking confirmed!\nName: {{ $node["Prepare Success Response"].json["name"] }}\nTime: {{ $node["Prepare Success Response"].json["time"] }}"
     }
     ```

2. **Lưu lịch sử đặt hẹn**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại tất cả lịch đặt hẹn.
   - Ví dụ: Sau khi tạo sự kiện, copy `eventId` vào sheet.

3. **Cập nhật thời gian làm việc động**:
   - Sử dụng node **Code** để lấy giờ làm việc từ một file JSON hoặc API bên ngoài.

4. **Chặn ngày lễ quốc gia**:
   - Nếu công ty có ngày nghỉ đặc biệt, thêm lịch riêng vào Google Calendar và kiểm tra trong node **`Check Public Holiday Calendar`**.

5. **Tích hợp với CRM**:
   - Sau khi đặt hẹn thành công, thêm thông tin khách hàng vào **HubSpot**, **Zoho CRM** hoặc **Salesforce**.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa hệ thống đặt hẹn, từ xác thực thông tin đến kiểm tra lịch và tạo sự kiện trên Google Calendar. **Không cần code**, chỉ cần cấu hình vài bước là có thể tiết kiệm thời gian và tránh lỗi cho doanh nghiệp.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Google Calendar** và thời gian làm việc.
3. **Test với request mẫu** và bật Active.
4. **Tích hợp với frontend** để khách hàng có thể đặt hẹn dễ dàng.

👉 **Xem demo hoạt động**: [Trải nghiệm trực tiếp](https://dragonjump.github.io/suarify-booking/)

---
**Chia sẻ và đánh giá nếu bài hướng dẫn hữu ích!** 🚀