---
title: "🗓️ Tự Động Tạo Sự Kiện Google Calendar Từ Dữ Liệu Google Sheets - Không Cần Code!"
description: "Học cách tự động hóa việc tạo sự kiện Google Calendar từ Google Sheets chỉ trong 3 node đơn giản, tiết kiệm thời gian và tránh sai sót thủ công. Phù hợp cho các sếp quản lý lịch trình, dự án hoặc sự kiện thường xuyên."
slug: "tu-dong-tao-su-kien-google-calendar-tu-google-sheets"
tags: [n8n, automation, google-calendar, google-sheets, no-code, workflow-tự-dộng]
keywords: [tự động hóa google calendar, google sheets tự động tạo sự kiện, n8n workflow calendar, tự động hóa quản lý lịch, tự động hóa sự kiện]
---

# 🚀 **Tự Động Tạo Sự Kiện Google Calendar Từ Google Sheets - Không Cần Code!**

### **🔥 Giải quyết vấn đề gì?**
Các sếp đã bao giờ phải **nhập thủ công** các sự kiện từ Google Sheets vào Google Calendar? Hay phải **lo lắng về sai sót** khi sao chép dữ liệu giữa hai nền tảng? Với workflow này, **n8n sẽ tự động hóa toàn bộ quy trình** chỉ trong **3 node**, giúp bạn:
- **Tiết kiệm thời gian** lên đến **30 phút/ngày** cho việc quản lý lịch.
- **Tránh sai sót** do nhập liệu thủ công.
- **Cập nhật tự động** khi có sự kiện mới trong Google Sheets.
- **Tùy chỉnh** màu sắc, trạng thái (Busy/Available) cho sự kiện.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa hoàn toàn** việc tạo sự kiện từ Google Sheets → Google Calendar.
✅ **Chỉnh sửa và cập nhật** sự kiện một cách nhanh chóng mà không cần mở cả hai ứng dụng.
✅ **Tùy chỉnh màu sắc và trạng thái** cho sự kiện (Busy/Available) để quản lý lịch hiệu quả.
✅ **Không cần viết code** - chỉ cần cấu hình 3 node đơn giản.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần:
1. **Tài khoản Google** (đã kết nối với Google Sheets và Google Calendar).
2. **Google Sheet** chứa dữ liệu sự kiện với các cột:
   - **Tên sự kiện (Summary)**
   - **Mô tả (Description)**
   - **Ngày giờ bắt đầu (Start Date/Time)**
   - **Ngày giờ kết thúc (End Date/Time)**
   - *(Tùy chọn)* **Địa điểm (Location)** và **Màu sắc (Background Color)**.
3. **API Key của n8n** (nếu tự host) hoặc tài khoản n8n Cloud.
4. **N8n Editor** (cài đặt hoặc truy cập [n8n.io](https://n8n.io/)).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste** JSON vào n8n Editor:
- **Tải workflow gốc** từ [đây](https://n8n.io/workflows/3300) (nút "Download").
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/3300) và paste vào **"Import"** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **3 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Node 1: New Event Entry Listener (Google Sheets Trigger)**
- **Loại node:** `googleSheetsTrigger`
- **Cấu hình:**
  - **Google Sheets Credential:** Chọn tài khoản Google đã kết nối với Google Sheets.
  - **Sheet Name:** Điền tên **trang tính** chứa dữ liệu sự kiện.
  - **Range:** Điền **địa chỉ ô** (ví dụ: `Sheet1!A1:E1000`).
  - **Trigger Type:** Chọn **"New Row"** (để kích hoạt khi có hàng mới).
  - **Watch for Changes:** Bật **ON** để theo dõi thay đổi.

##### **🔹 Node 2: Event Date Formatter (Code Node)**
- **Loại node:** `code`
- **Mục đích:** Đảm bảo **định dạng ngày giờ** phù hợp với Google Calendar.
- **Mã JavaScript mặc định:**
  ```javascript
  // Format date to match Google Calendar's expected format
  const date = new Date($input.all()[0].date);
  const formattedDate = date.toISOString();

  return {
    json: {
      ...$input.all()[0],
      date: formattedDate
    }
  };
  ```
- **Lưu ý:**
  - Nếu dữ liệu ngày giờ trong Google Sheets **không phải ISO format**, các sếp cần **sửa mã** để chuyển đổi đúng.
  - Ví dụ: Nếu ngày giờ trong Sheets là `DD/MM/YYYY HH:MM`, cần chuyển thành `YYYY-MM-DDTHH:MM:SSZ`.

##### **🔹 Node 3: Google Calendar Event Creator**
- **Loại node:** `googleCalendar`
- **Cấu hình:**
  - **Google Calendar Credential:** Chọn tài khoản Google Calendar.
  - **Calendar Name:** Chọn **lịch** muốn tạo sự kiện (ví dụ: "Lịch công việc").
  - **Event Details:**
    - **Summary:** `$node["New Event Entry Listener"].json["summary"]` (tên sự kiện từ Sheets).
    - **Description:** `$node["New Event Entry Listener"].json["description"]` (mô tả).
    - **Start Date/Time:** `$node["Event Date Formatter"].json["date"]` (định dạng ISO).
    - **End Date/Time:** `$node["New Event Entry Listener"].json["end_date"]` (hoặc tính toán từ `start_date + duration`).
    - **Location:** `$node["New Event Entry Listener"].json["location"]` (nếu có).
    - **Status:** Chọn **"Busy"** hoặc **"Available"** (tùy chọn).
    - **Background Color:** Chọn màu (ví dụ: **Đỏ** cho sự kiện quan trọng).

---

#### **3. Kích hoạt ⚡️**
- **Test Run:** Nhấn **"Run Workflow"** với **dữ liệu mẫu** từ Google Sheets để kiểm tra.
- **Bật Active:** Sau khi kiểm tra thành công, **bật "Active"** để workflow chạy tự động khi có sự kiện mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM NÂNG CAO]
1. **Lưu log sự kiện:** Thêm **node `stickyNote`** để ghi lại lịch sử sự kiện đã tạo.
2. **Gửi thông báo Slack/Email:** Kết nối với **Slack** hoặc **Gmail** để thông báo khi có sự kiện mới.
3. **Tự động xóa sự kiện cũ:** Sử dụng **node `googleCalendar` với action "Delete"** để xóa sự kiện đã hoàn thành.
4. **Tùy chỉnh thời gian chạy:** Sử dụng **node `set`** để điều chỉnh giờ bắt đầu/kết thúc tự động.
5. **Kết hợp với Google Forms:** Nếu sự kiện được nhập từ **Google Form**, sử dụng **node `googleSheetsTrigger`** để lấy dữ liệu từ Form → Sheets → Calendar.
:::

---

### 📌 **Kết luận**
Với workflow này, các sếp **không cần viết code** mà vẫn tự động hóa việc tạo sự kiện từ Google Sheets sang Google Calendar. **Tiết kiệm thời gian, tránh sai sót và quản lý lịch hiệu quả** chỉ trong **3 node đơn giản**!

👉 **Bắt đầu ngay:** [Tải workflow](https://n8n.io/workflows/3300) và **cài đặt n8n trên VPS** để chạy 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Hãy thử ngay và chia sẻ kết quả với chúng tôi!** 🚀