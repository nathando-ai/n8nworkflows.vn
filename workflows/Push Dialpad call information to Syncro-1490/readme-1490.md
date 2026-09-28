---
title: "📞 Tự Động Hóa Thông Tin Gọi Dialpad → Syncro: Giảm 90% Công Việc Nhập Lại Dữ Liệu"
description: "Workflow này tự động lấy thông tin cuộc gọi từ Dialpad và đẩy lên Syncro, giúp các sếp tiết kiệm thời gian, tránh sai sót và đồng bộ hóa dữ liệu liên tục 24/7."
slug: "tieu-dong-hoa-thong-tin-goi-dialpad-syncro"
tags: [n8n, automation, dialpad, syncro, google-sheets, api-integration]
keywords: [n8n workflow dialpad syncro, tự động hóa cuộc gọi điện thoại, đồng bộ hóa dữ liệu, giảm công việc thủ công, api dialpad]
---

# 🚀 **Tự Động Hóa Thông Tin Gọi Dialpad → Syncro: Giảm 90% Công Việc Nhập Lại Dữ Liệu**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải **nhập thủ công** thông tin cuộc gọi từ Dialpad (hay các hệ thống CRM khác) vào Syncro để theo dõi, phân tích và quản lý khách hàng. Điều này gây ra:
✅ **Tốn thời gian** (tối thiểu 30 phút/ngày cho một đội ngũ nhỏ).
✅ **Sai sót cao** (do nhập sai tên, số điện thoại, hoặc thông tin cuộc gọi).
✅ **Không đồng bộ thời gian thực**, dẫn đến dữ liệu cũ hoặc không chính xác khi phân tích.

**Workflow này giải quyết tất cả!** Nó **tự động lấy thông tin cuộc gọi từ Dialpad và đẩy lên Syncro**, đồng thời lưu trữ bản sao trên Google Sheets để theo dõi và báo cáo.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30-50 giờ/Tháng** cho việc nhập liệu thủ công.
- **Đồng bộ dữ liệu thời gian thực**, không còn lo sai sót.
- **Lưu trữ lịch sử cuộc gọi** trên Google Sheets để phân tích sau này.
- **Hoạt động 24/7**, không phụ thuộc vào nhân viên.
- **Kết hợp với Syncro**, giúp quản lý khách hàng hiệu quả hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Dialpad** (API Key hoặc Credentials để truy cập thông tin cuộc gọi).
2. **Tài khoản Syncro** (API Key hoặc Credentials để tạo/tập tin ticket).
3. **Google Sheets** (một bảng để lưu trữ lịch sử cuộc gọi).
4. **n8n Self-hosted** (để workflow chạy 24/7, không phụ thuộc vào phiên bản miễn phí).
5. **Mã API Header Auth** (để xác thực với Dialpad và Syncro).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/1490](https://n8n.io/workflows/1490) (hoặc copy JSON từ link này).
- **Bước 2:** Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Bước 3:** Chọn **"Create Workflow"** và đặt tên (ví dụ: **"Dialpad → Syncro"**).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **22 node**, nhưng chỉ cần chú ý đến **các node quan trọng sau**:

##### **A. Webhook (Nhận Dữ Liệu Từ Dialpad)**
- **Node:** `Webhook` (path: `moezdialpad`, HTTP Method: `POST`)
- **Lưu ý:**
  - Cần **bật Webhook** và lưu URL để Dialpad gửi dữ liệu đến.
  - **Không cần cấu hình gì thêm** nếu sử dụng cấu hình mặc định.

##### **B. API Dialpad (Lấy Thông Tin Cuộc Gọi)**
- **Node:** `GetCustomer`, `Contacts`, `Customers`
  - **Cấu hình:**
    - **URL API Dialpad** (tham khảo [Dialpad API Docs](https://developer.dialpad.com/)).
    - **Headers Auth:** Điền `Authorization: Bearer {API_KEY_DIALPAD}`.
    - **Query Parameters:** Thêm `filter` để lấy cuộc gọi mới nhất (ví dụ: `filter=createdAt>now-1d`).

##### **C. Logic Xử Lý Dữ Liệu (IF Conditions)**
- **Node:** `IFMoreThanOne`, `IFContacts`, `IFCustomers`, `IF`
  - **Lưu ý:**
    - Nếu cuộc gọi **trùng lặp**, workflow sẽ **bỏ qua** (do `IFMoreThanOne`).
    - Nếu khách hàng **không tồn tại**, workflow sẽ **tạo mới** (do `IFContacts` và `IFCustomers`).

##### **D. Tạo/Tập Tin Ticket Syncro**
- **Node:** `CreateTicket`, `UpdateTicket`, `CreateTicketForCustomer`
  - **Cấu hình:**
    - **URL API Syncro** (tham khảo [Syncro API Docs](https://developer.syncro.com/)).
    - **Headers Auth:** Điền `Authorization: Bearer {API_KEY_SYNCRO}`.
    - **Body Request:** Điền thông tin cuộc gọi (ví dụ: `name`, `phone`, `callDuration`, `notes`).

##### **E. Lưu Trữ Lịch Sử Cuộc Gọi (Google Sheets)**
- **Node:** `Google Sheets`, `Google Sheets1`, `Google Sheets2`
  - **Cấu hình:**
    - **Google API Credentials:** Đăng ký [Google Cloud API](https://developers.google.com/sheets/api/quickstart/python) và cấp quyền cho `https://www.googleapis.com/auth/spreadsheets`.
    - **Sheet Name:** Chọn một bảng Google Sheets mới (ví dụ: **"Dialpad_Calls"**).
    - **Headers:** Điền `Authorization: Bearer {GOOGLE_API_TOKEN}`.

##### **F. Cấu Hình Môi Trường (EnvVariables)**
- **Node:** `EnvVariables`
  - **Lưu ý:**
    - Nếu workflow cần **môi trường biến**, điền vào `n8n.environment` trong **Settings → Workflow → Environment Variables**.

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** **Test Run** với dữ liệu mẫu từ Dialpad (gửi POST đến Webhook).
- **Bước 2:** Kiểm tra **Google Sheets** xem dữ liệu có được ghi lại không.
- **Bước 3:** Nếu mọi thứ OK, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết Nối Slack/Telegram**
   - Thêm **node `slack`** hoặc **`telegram`** để thông báo khi có cuộc gọi mới.
   - Ví dụ: `{"text": "📞 Cuộc gọi mới từ {{$node["Webhook"].json["phone"]}}: {{$node["Webhook"].json["duration"]}} phút"}`.

2. **Lưu Log Lịch Sử**
   - Thêm **node `googleSheets`** để lưu **log hoạt động** (ví dụ: thời gian xử lý, trạng thái thành công/thất bại).

3. **Gửi Báo Cáo Định Kỳ**
   - Sử dụng **node `set` + `httpRequest`** để gọi API Syncro và gửi **báo cáo tổng hợp** qua email (ví dụ: số cuộc gọi/ngày, khách hàng thường xuyên).

4. **Tự Động Xóa Cuộc Gọi Trùng Lặp**
   - Thêm **node `function`** để kiểm tra và xóa cuộc gọi đã tồn tại trong Syncro trước khi tạo mới.

5. **Kết Hợp với CRM Khác**
   - Nếu sử dụng **HubSpot, Zoho CRM**, có thể thay thế Syncro bằng API của hệ thống đó.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc nhập liệu thủ công, đồng thời **đảm bảo dữ liệu chính xác và đồng bộ**. **Chỉ cần 10 phút cấu hình**, bạn đã có một hệ thống tự động hóa hoàn chỉnh!

**Hành động ngay:**
1. **Cài n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình API.
3. **Test và bật hoạt động**!

👉 **Nếu cần hỗ trợ**, để lại comment bên dưới hoặc liên hệ với tác giả [Jonathan](https://n8n.io/workflows/1490) (hoặc [n8n Community](https://community.n8n.io/)).

---
**#TựĐộngHóa #Dialpad #Syncro #n8n #APIAutomation**