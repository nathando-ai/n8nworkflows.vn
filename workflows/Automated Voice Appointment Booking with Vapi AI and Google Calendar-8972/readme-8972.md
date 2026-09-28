---
title: "🎙️ Tự Động Hẹn Lịch Phỏng Vấn Bằng Giọng Nói AI Với Vapi + Google Calendar (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn bằng n8n kết nối Vapi AI với Google Calendar để thu thập thông tin khách hàng và đặt lịch hẹn tự động. Giúp tiết kiệm 80% thời gian quản lý lịch, giảm thiểu lỗi thủ công và cải thiện trải nghiệm khách hàng."
slug: "tu-dong-hoan-lich-phong-van-voi-vapi-google-calendar"
tags: [n8n, automation, no-code, vapi-ai, google-calendar, content-creation, multimodal-ai]
keywords: [tự động hóa lịch hẹn, vapi ai, google calendar api, n8n workflow, đặt lịch tự động, giải pháp no-code]
---

# 🚀 **Tự Động Hẹn Lịch Phỏng Vấn Bằng Giọng Nói AI (Vapi) + Google Calendar**

### **Giải pháp cho các sếp:**
Bạn đã bao giờ phải mất **30 phút/ngày** để quản lý lịch hẹn, trả lời email hoặc gọi điện để xác nhận lịch? Hay phải **lo lắng khách hàng bỏ cuộc** vì không tìm được thời gian phù hợp? Workflow này sẽ **tự động hóa toàn bộ quy trình** bằng giọng nói AI (Vapi) kết hợp với Google Calendar, giúp bạn:
✅ **Tiết kiệm 80% thời gian** quản lý lịch.
✅ **Giảm thiểu lỗi thủ công** (không cần nhập lại thông tin).
✅ **Cung cấp trải nghiệm khách hàng chuyên nghiệp** (giọng nói tự động, xác nhận lịch tự động).
✅ **Hoạt động 24/7** mà không cần can thiệp của bạn.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gọi điện hoặc gửi email xác nhận lịch.
- **Chính xác 100%**: Thông tin khách hàng được đồng bộ tự động vào Google Calendar.
- **Cá nhân hóa**: Khách hàng được hỏi về **tên, địa chỉ, loại dịch vụ** và được đề xuất thời gian phù hợp.
- **Hoạt động liên tục**: Hệ thống hoạt động **24/7** mà không cần can thiệp của bạn.
- **Dễ dàng mở rộng**: Có thể kết nối thêm **SMS/Email xác nhận**, **CRM**, hoặc **phân tích dữ liệu**.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n** (Cloud hoặc **Self-hosted** trên VPS).
2. **Tài khoản Google** với **Google Calendar** (để kết nối OAuth).
3. **Tài khoản Vapi AI** (để sử dụng trợ lý giọng nói).
4. **Một số thông tin cấu hình**:
   - **Múi giờ** (ví dụ: `Asia/HoChiMinh`).
   - **Giờ làm việc** (ví dụ: bắt đầu từ 8h, kết thúc 17h).
   - **Thời lượng cuộc họp** (ví dụ: 30 phút).
   - **Thời gian buffer** trước và sau cuộc họp (ví dụ: 15 phút).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/8972) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

:::warning[LƯU Ý]
- **Không chỉnh sửa** các node có ghi `(do not change)` (nếu không muốn workflow bị lỗi).
- **Cần chỉnh sửa** các node có ghi `(EDIT ME)` (được đánh dấu trong workflow).
:::

---

### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

#### **A. Cấu hình Webhook (n8n-nodes-base.webhook)**
1. Mở node **Webhook: Production URL = VAPI Server URL**.
2. **Copy URL Production** và lưu lại (sẽ dùng để kết nối với Vapi).
3. **Không cần thay đổi** các tham số `path` và `httpMethod`.

#### **B. Kết nối Vapi với n8n**
1. **Mở Vapi Assistant** → **Messaging**.
2. **Đặt Server URL** = URL Production từ bước trên.
3. **Bật chỉ `toolCalls`** (không cần các thông báo khác).

#### **C. Tạo 2 Tool Custom trong Vapi**
Các sếp phải tạo **hai công cụ** trong Vapi với tên **không thay đổi**:
- **Tool 1: `checkAvailability`**
  - **Arguments**:
    - `initialSearchDateTime` (định dạng ISO-8601, ví dụ: `2025-09-09T09:00:00+07:00`).
- **Tool 2: `bookAppointment`**
  - **Arguments**:
    - `startDateTime` (ISO-8601).
    - `endDateTime` (ISO-8601).
    - `clientName` (string).
    - `propertyAddress` (string).
    - `serviceType` (string).

:::danger[LƯU Ý QUAN TRỌNG]
- **Tên tool phải chính xác** (`checkAvailability` và `bookAppointment`), nếu khác sẽ **không hoạt động**.
- **Switch node** sẽ tự động phân loại dựa trên tên tool này.
:::

#### **D. Cấu hình Thời gian & Lịch (n8n-nodes-base.set)**
Mở node **1. CONFIGURATION (EDIT ME)** và điền:
- `timeZone`: Ví dụ `Asia/HoChiMinh`.
- `workdayStartHour`: 8 (8h sáng).
- `workdayEndHour`: 17 (5h chiều).
- `meetingDurationMinutes`: 30 (30 phút).
- `bufferBeforeMinutes`: 15 (15 phút trước).
- `bufferAfterMinutes`: 15 (15 phút sau).
- `bookingCadenceMinutes`: 30 (khách hàng được chọn lịch theo khoảng 30 phút).

#### **E. Kết nối Google Calendar**
1. Mở node **2. Get Calendar Events (EDIT ME)** → **Credentials** → Chọn/tao **Google Calendar OAuth**.
2. Chọn **calendar** muốn kiểm tra sẵn có.
3. Mở node **3. Book Appointment in Calendar (EDIT ME)** → **Sử dụng cùng credential và calendar** như trên.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gọi Vapi và yêu cầu đặt lịch (ví dụ: *"Đặt lịch phỏng vấn tại địa chỉ 123 ABC"*).
   - Kiểm tra **Google Calendar** có xuất hiện sự kiện mới không.
2. **Bật Active** workflow.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[NÂNG CAO TRẢI NGHIỆM KHÁCH HÀNG]
1. **Thêm SMS/Email xác nhận**:
   - Kết nối với **Twilio** (SMS) hoặc **SendGrid** (Email) để gửi thông báo khi lịch được đặt.
2. **Hỗ trợ đa ngôn ngữ**:
   - Cài đặt **Vapi với nhiều ngôn ngữ** để phục vụ khách hàng quốc tế.
3. **Phân loại khách hàng (Lead Qualification)**:
   - Thêm logic để **lọc khách hàng tiềm năng** trước khi đặt lịch.
4. **Tóm tắt cuộc gọi**:
   - Sử dụng **LLM** (n8n-nodes-base.llm) để tự động ghi chú cuộc gọi.
5. **Kết nối CRM**:
   - Đồng bộ thông tin khách hàng vào **HubSpot**, **Salesforce** hoặc **Zoho CRM**.
6. **Cho phép hủy/lịch lại**:
   - Thêm logic để khách hàng **hủy hoặc thay đổi lịch** qua giọng nói.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi công việc nhắc nhở lịch, nhập liệu và quản lý cuộc gọi** bằng cách tự động hóa toàn bộ quy trình. **Khách hàng sẽ được trải nghiệm chuyên nghiệp**, trong khi bạn **tiết kiệm thời gian và giảm thiểu lỗi**.

👉 **Bắt đầu ngay hôm nay!**
1. **Cài n8n trên VPS** (để chạy 24/7):
   🔹 [Đăng ký VPS TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
   🔹 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Test với một cuộc gọi mẫu** và **bật Active**.

**Chúc các sếp thành công!** 🚀
---
**Cần hỗ trợ?** Liên hệ với tác giả qua:
📩 [Streetlamp Agency](https://streetlamp.agency)