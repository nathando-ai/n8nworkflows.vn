---
title: "📅 Tự Động Hóa Đặt, Quản Lý & Kiểm Tra Lịch Hẹn Với Vapi + Google Calendar (N8N)"
description: "Workflow hoàn toàn tự động hóa quản lý lịch hẹn từ đặt lịch, kiểm tra sẵn sàng, đến hủy/chỉnh sửa lịch với Google Calendar và Vapi Voice Assistant. Giúp doanh nghiệp tiết kiệm 80% thời gian hành chính và giảm thiểu lỗi nhân sự."
slug: "tieu-dong-hoa-dat-quan-ly-lich-hen-vapi-google-calendar"
tags: [n8n, automation, no-code, vapi, google-calendar, ai-chatbot]
keywords: [n8n workflow lịch hẹn, tự động hóa đặt lịch, Vapi + Google Calendar, quản lý lịch hẹn tự động, tự động hóa dịch vụ]
---

# 🚀 **Tự Động Hóa Đặt, Quản Lý & Kiểm Tra Lịch Hẹn Với Vapi + Google Calendar**

## **Giới Thiệu**
Các sếp đang mệt mỏi vì phải quản lý lịch hẹn thủ công qua email, điện thoại, hoặc các công cụ khác? Hay phải lo lắng khi khách hàng đặt lịch trùng với lịch sẵn sàng của nhân viên? **Workflow này sẽ giải quyết tất cả!**

Với **n8n**, các sếp có thể **tự động hóa toàn bộ quy trình quản lý lịch hẹn** từ việc **kiểm tra sẵn sàng thời gian**, **đặt lịch mới**, đến **hủy/chỉnh sửa lịch** chỉ trong vài phút. Không cần viết code, không cần kỹ sư IT, chỉ cần **n8n + Google Calendar + Vapi Voice Assistant** là xong!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian hành chính** – Không cần gọi điện, gửi email xác nhận lịch nữa.
✅ **Tránh trùng lịch tự động** – Kiểm tra sẵn sàng thời gian trước khi đặt lịch.
✅ **Cá nhân hóa trải nghiệm khách hàng** – Vapi Voice Assistant hỗ trợ đặt lịch bằng giọng nói.
✅ **Hủy/chỉnh sửa lịch một cú nhấp chuột** – Khách hàng có thể tự quản lý lịch qua Vapi.
✅ **Báo cáo tự động** – Theo dõi lịch hẹn trong Google Calendar và n8n Dashboard.
✅ **Hoạt động 24/7** – Không cần nhân viên trực đêm để quản lý lịch.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Vapi.ai** (để kết nối với Vapi Voice Assistant)
✔ **Google Calendar** (để lưu trữ và quản lý lịch hẹn)
✔ **n8n Self-hosted** (để chạy workflow 24/7)
✔ **API Key của Google Calendar** (để n8n có quyền truy cập)
✔ **Credentials cho Vapi** (để nhận và gửi dữ liệu đặt lịch)

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow này có **27 node** và được chia thành **3 công cụ chính**:
1. **Check Availability** (Kiểm tra sẵn sàng thời gian)
2. **Book Appointment** (Đặt lịch mới)
3. **Manage Appointment** (Hủy/chỉnh sửa lịch)

#### **Hướng dẫn import:**
1. **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/12831) hoặc copy toàn bộ JSON.
2. Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc upload file.
3. **Kích hoạt workflow** sau khi import xong.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Google Calendar**
- **Node:** `Create Calendar Event`, `Get Calendar Events`, `Update Calendar Event`, `Delete Calendar Event`
- **Cách cấu hình:**
  - Đi đến **Credentials** → Thêm **Google Calendar**.
  - Nhập **Client ID** và **Client Secret** từ [Google Cloud Console](https://console.cloud.google.com/).
  - Chọn **Google Calendar** cần quản lý.
  - **Lưu ý:** Cần cấp quyền **"Read & Write"** cho n8n.

#### **🔹 Cấu hình Vapi Voice Assistant**
- **Node:** `Book Appointment Webhook`, `Check Availability Webhook`, `Manage Appointment Webhook`
- **Cách cấu hình:**
  - Trong **Vapi Dashboard**, tạo **3 Custom Tool** tương ứng với 3 webhook trên.
  - **Book Appointment:** Gửi dữ liệu đặt lịch (name, phone, service, date, time, duration, notes).
  - **Check Availability:** Gửi ngày/thời gian để kiểm tra sẵn sàng.
  - **Manage Appointment:** Gửi yêu cầu hủy/chỉnh sửa (action="cancel" hoặc action="update").
  - **Lưu ý:** Cần định nghĩa **schema** cho mỗi tool trong Vapi.

#### **🔹 Cấu hình Webhook trong n8n**
- **Node:** `Book Appointment Webhook`, `Check Availability Webhook`, `Manage Appointment Webhook`
- **Cách cấu hình:**
  - Mở từng node webhook → Đặt **HTTP Method = POST**.
  - **Path:**
    - `book-appointment` (đặt lịch)
    - `availability` (kiểm tra sẵn sàng)
    - `manage-appointment` (quản lý lịch)
  - **Lưu ý:** Các webhook này sẽ nhận dữ liệu từ Vapi và xử lý tự động.

#### **🔹 Cấu hình Node `Set` (Trích xuất dữ liệu)**
- **Node:** `Extract Booking Data`, `Extract Availability Request`, `Extract Appointment Management Data`
- **Cách cấu hình:**
  - Mở node → Chọn **JSON Path** để trích xuất dữ liệu từ payload.
  - Ví dụ:
    - `$.name` (tên khách hàng)
    - `$.date` (ngày đặt lịch)
    - `$.time` (thời gian đặt lịch)
    - `$.action` (hủy/chỉnh sửa)

#### **🔹 Cấu hình Node `If` (Kiểm tra điều kiện)**
- **Node:** `Validate Required Fields`, `Check Time Slot Availability`
- **Cách cấu hình:**
  - **Validate Required Fields:** Kiểm tra xem tất cả trường bắt buộc (`name`, `phone`, `date`, `time`) có được điền không.
  - **Check Time Slot Availability:** So sánh thời gian đặt lịch với lịch sẵn sàng trong Google Calendar.
  - **Lưu ý:** Nếu thiếu trường bắt buộc → trả về **lỗi xác thực**.

#### **🔹 Cấu hình Node `Google Calendar` (Tạo/Update/Xóa lịch)**
- **Node:** `Create Calendar Event`, `Update Calendar Event`, `Delete Calendar Event`
- **Cách cấu hình:**
  - **Create Calendar Event:**
    - **Summary:** "Lịch hẹn với [Tên Khách Hàng]"
    - **Start Time:** `{{ $json.date }}T{{ $json.time }}:00+07:00`
    - **End Time:** `{{ $json.date }}T{{ $json.time }}:{{ $json.duration }}:00+07:00`
    - **Location:** (Nếu có)
  - **Update Calendar Event:**
    - Sử dụng **ID sự kiện** từ Google Calendar để cập nhật.
  - **Delete Calendar Event:**
    - Sử dụng **ID sự kiện** để xóa lịch.

#### **🔹 Cấu hình Node `Code` (Định dạng phản hồi)**
- **Node:** `Format Booking Success Response`, `Format Validation Error Response`, `Format Available Time Response`, `Format Unavailable Time Response`
- **Cách cấu hình:**
  - Mở node → Chọn **JavaScript** → Sử dụng **template engine** để định dạng phản hồi theo chuẩn Vapi.
  - Ví dụ phản hồi thành công:
    ```javascript
    return {
      response: {
        text: `Lịch hẹn đã được đặt thành công!\nNgày: {{ $json.date }}\nGiờ: {{ $json.time }}\nDịch vụ: {{ $json.service }}`
      }
    };
    ```
  - **Lưu ý:** Phải tuân thủ **schema phản hồi** của Vapi.

#### **🔹 Cấu hình Node `Switch` (Lựa chọn hành động)**
- **Node:** `Route by Action Type`
- **Cách cấu hình:**
  - Chọn **`$json.action`** làm điều kiện phân nhánh.
  - Các trường hợp:
    - `book` → Đặt lịch mới.
    - `cancel` → Hủy lịch.
    - `update` → Chỉnh sửa lịch.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi yêu cầu đặt lịch qua **Vapi** → Kiểm tra phản hồi.
   - Kiểm tra **Google Calendar** để xác nhận lịch được tạo.
2. **Bật Active workflow** sau khi kiểm tra thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Kết hợp với Slack/Telegram để báo cáo**
- Sử dụng **node Slack/Telegram** để gửi thông báo khi có lịch mới/hủy/chỉnh sửa.
- **Cách làm:**
  - Thêm **node Slack** sau `Create Calendar Event` và `Delete Calendar Event`.
  - Tạo **webhook Slack** và cấu hình trong n8n.

### **2. Lưu log tất cả hoạt động**
- Sử dụng **node Database (PostgreSQL/MySQL)** để lưu lịch sử đặt lịch.
- **Cách làm:**
  - Thêm **node Database** sau `Create Calendar Event`.
  - Lưu trường: `name`, `phone`, `date`, `time`, `status`, `created_at`.

### **3. Gửi báo cáo định kỳ**
- Sử dụng **node Schedule** để chạy workflow hàng ngày/tuần.
- **Cách làm:**
  - Thêm **node Schedule** → Chọn thời gian chạy (ví dụ: 8h sáng).
  - Gửi báo cáo tổng hợp qua **email** hoặc **Slack**.

### **4. Cải thiện trải nghiệm khách hàng**
- **Hỗ trợ đặt lịch qua SMS** (nếu Vapi có API SMS).
- **Gửi nhắc nhở trước lịch** (sử dụng **node Email** hoặc **node Telegram**).

---

## 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc quản lý lịch hẹn thủ công. Với **n8n + Google Calendar + Vapi**, các sếp có thể:
✔ **Đặt lịch tự động** mà không lo trùng lịch.
✔ **Hủy/chỉnh sửa lịch** chỉ bằng giọng nói.
✔ **Quản lý toàn bộ lịch hẹn** từ một dashboard duy nhất.

**Hãy áp dụng ngay và tiết kiệm 80% thời gian hành chính!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/12831)**
**📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**