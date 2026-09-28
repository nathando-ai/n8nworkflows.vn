---
title: "🗓️ Tự Động Tạo Lịch Trang Bị Lọc Sàng Cho Baserow Với N8n – Hỗ Trợ Tích Hợp Lịch Ngoại Viên"
description: "Workflow này tự động tạo **lịch cá nhân hóa** trong Baserow dựa trên ngày tháng và bảng lọc, sau đó chia sẻ dưới dạng file `.ics` để tích hợp với Outlook, Google Calendar hoặc các ứng dụng lịch khác. Giúp quản lý công việc, khách hàng hoặc kho hàng hiệu quả hơn mà không cần viết code."
slug: "tay-dong-tao-lich-trang-bi-loc-sang-baserow-n8n"
tags: [n8n, automation, baserow, calendar, no-code, calendar-integration]
keywords: [n8n workflow baserow, tự động hóa lịch cá nhân, tích hợp baserow với google calendar, tự động tạo lịch theo ngày tháng, baserow api automation]
---

# 🚀 **Tự Động Tạo Lịch Cá Nhân Hóa Trong Baserow Với N8n – Khắc Phục Nỗi Đau Quản Lý Thông Tin Phức Tạp**

Bạn có bao giờ phải **lọc và quản lý hàng trăm công việc, khách hàng hoặc đơn hàng** trong Baserow mà lại phải **tìm kiếm thủ công** trên lịch để biết thông tin liên quan? Hoặc muốn **chia sẻ lịch cá nhân** cho từng nhân viên, khách hàng hoặc nhà cung cấp mà không muốn làm thủ công mỗi ngày?

Workflow này **giải quyết vấn đề đó bằng cách tự động tạo lịch trang bị lọc sàng** trong Baserow, sau đó **chia sẻ dưới dạng file `.ics`** để tích hợp với **Outlook, Google Calendar, Apple Calendar** hoặc bất kỳ ứng dụng lịch nào khác. **Không cần viết một dòng code nào!**

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tạo lịch thủ công cho từng nhân viên/khách hàng.
- **Tích hợp hoàn hảo**: Lịch được tạo ra có thể **đồng bộ tự động** với Google Calendar, Outlook, hoặc ứng dụng lịch khác.
- **Cá nhân hóa hoàn toàn**: Mỗi người dùng chỉ xem **thông tin liên quan** đến họ (ví dụ: công việc của nhân viên, đơn hàng của khách hàng).
- **Hoạt động liên tục 24/7**: Chỉ cần kích hoạt workflow một lần, hệ thống sẽ tự động cập nhật khi có thay đổi.
- **Dễ dàng chia sẻ**: File `.ics` có thể **gửi qua email, Slack, hoặc Telegram** cho người dùng.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Baserow** (Cloud hoặc Self-hosted).
2. **Một cơ sở dữ liệu Baserow** với **hai bảng dữ liệu** và **các trường sau**:
   - **Bảng 1 (Date Table)**: Có **trường Ngày tháng** (ví dụ: `deadline`, `appointment_date`) và **trường Link đến bảng khác** (ví dụ: `customer_id`, `employee_id`).
   - **Bảng 2 (Filter Table)**: Bảng này **liên kết** với trường Link trong Bảng 1 (ví dụ: bảng `Customers`, `Employees`, `Products`).
3. **Thông tin API Baserow**:
   - **Username** và **password** (để tạo JWT token).
   - **Host API** (mặc định: `https://api.baserow.io`, nhưng có thể thay đổi nếu self-hosted).
4. **Các ID quan trọng** (sẽ được hướng dẫn chi tiết trong phần **cấu hình**):
   - ID của **Database**, **Table**, **Date Field**, **Filter Field**, **Status Field** (nếu có).
   - (Tùy chọn) ID của trường **View Link** và **ICS Field** để lưu trữ liên kết.
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Workflow đã được **tạo sẵn trên n8n.io** (ID: **8485**). Các sếp có thể:
- **Tải xuống file JSON** từ [đây](https://n8n.io/workflows/8485) và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- Nếu **self-hosted**, đảm bảo **host API** trong node `Set Baserow credentials` được cập nhật chính xác.
- **Không cần thay đổi cấu trúc**, chỉ cần **cấu hình các tham số** như hướng dẫn dưới đây.
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

Workflow gồm **10 node** với logic như sau. Các sếp **phải cấu hình** các node sau **trước khi kích hoạt**:

#### **A. Cấu Hình Credentials Baserow**
1. **Node: "Set Baserow credentials" (type: `set`)**
   - **Tham số cần điền**:
     - `baserowUsername`: Tên đăng nhập Baserow.
     - `baserowPassword`: Mật khẩu Baserow.
     - `baserowHost`: Host API (mặc định: `https://api.baserow.io`).
     - **Lưu ý**: Thông tin này sẽ được sử dụng để tạo **JWT token** cho các yêu cầu API sau.

2. **Node: "Create a token" (type: `httpRequest`)**
   - **Đây là node tự động** sau khi cấu hình credentials ở trên.
   - **Không cần chỉnh sửa**, chỉ cần **chạy workflow** để nó tạo token.

#### **B. Cấu Hình ID Của Bảng & Trường**
3. **Node: "Set table and field ids" (type: `set`)**
   - **Tham số cần điền** (đọc kỹ phần **Required tables and fields** dưới đây):
     - `databaseId`: ID của **Database** trong Baserow.
     - `dateTableId`: ID của **bảng chứa ngày tháng** (ví dụ: `Tasks`).
     - `dateFieldId`: ID của **trường ngày tháng** (ví dụ: `deadline`).
     - `filterTableId`: ID của **bảng lọc** (ví dụ: `Customers`).
     - `filterFieldId`: ID của **trường Link đến bảng ngày tháng** (ví dụ: `customer_id`).
     - `statusFieldId` (tùy chọn): ID của **trường màu nền** (nếu muốn màu nền khác nhau cho từng trạng thái).
     - `icsFieldId` (tùy chọn): ID của **trường lưu liên kết `.ics`**.
     - `viewLinkFieldId` (tùy chọn): ID của **trường lưu liên kết lịch**.

   - **Cách lấy ID**:
     - Mở Baserow → Chọn **Database** → Chọn **Table** → ID nằm trong **URL** (ví dụ: `.../database/123/table/456` → `tableId = 456`).
     - ID của **field** cũng nằm trong URL khi chỉnh sửa trường (ví dụ: `.../field/789` → `fieldId = 789`).

#### **C. Cấu Hình Cụ Thể Các Node Quan Trọng**
4. **Node: "Get all records from filter table" (type: `baserow`)**
   - **Không cần chỉnh sửa**, nó sẽ **lấy tất cả dữ liệu** từ bảng lọc (ví dụ: `Customers`).

5. **Node: "Create new calendar view" (type: `httpRequest`)**
   - **Đây là node API** tạo **lịch mới** trong Baserow.
   - **Body của request** sẽ tự động cấu hình:
     - `name`: Tên lịch (ví dụ: `Lịch Công Việc của {Tên Khách Hàng}`).
     - `date_field`: ID của trường ngày tháng.
     - **Không cần chỉnh sửa**, nó sẽ lấy từ **node "Set table and field ids"**.

6. **Node: "Create filter" (type: `httpRequest`)**
   - **Tạo lọc** để chỉ hiển thị **các bản ghi liên quan** đến người dùng.
   - Ví dụ: Nếu bảng lọc là `Customers`, lịch sẽ chỉ hiển thị **các công việc của khách hàng đó**.

7. **Node: "Set background color" (type: `httpRequest`)**
   - **Tùy chọn**: Đặt **màu nền** cho mỗi mục trong lịch.
   - Nếu có **trường `statusFieldId`**, nó sẽ tự động **đổi màu** theo trạng thái (ví dụ: đỏ cho `Overdue`, xanh cho `Completed`).

8. **Node: "Share the view" (type: `httpRequest`)**
   - **Cập nhật lịch** để **chia sẻ dưới dạng `.ics`**.
   - Sau khi chạy, **file `.ics`** sẽ có sẵn để **tải xuống hoặc chia sẻ**.

9. **Node: "Update the url’s" (type: `baserow`)**
   - **Cập nhật bảng lọc** để **lưu liên kết lịch và `.ics`** vào trường tương ứng (`viewLinkFieldId` và `icsFieldId`).
   - **Dùng để xây dựng ứng dụng trên cơ sở dữ liệu** sau này.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Chọn **1 bản ghi** trong bảng lọc (ví dụ: 1 khách hàng).
   - Chạy workflow để **tạo lịch cá nhân** cho khách hàng đó.
   - Kiểm tra **file `.ics`** có được tạo không.

2. **Bật Active**:
   - Sau khi **cấu hình hoàn chỉnh**, chuyển **Manual Trigger** thành **Webhook** (nếu muốn tự động hóa) hoặc **bật Active** để chạy thủ công.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM KHÁC ĐỂ TĂNG CƯỜNG HỆ THỐNG]
1. **Tích Hợp Với Slack/Telegram**:
   - Sau khi tạo lịch, **gửi thông báo** qua Slack/Telegram với liên kết `.ics` bằng node **`slack`** hoặc **`telegram`**.
   - **Cú pháp**:
     ```json
     {
       "text": "📅 Lịch cá nhân của {{$node["Get all records from filter table"].json()["name"]}} đã được tạo!\n🔗 [Tải lịch .ics]({{$node["Share the view"].json()["ical_url"]}})"
     }
     ```

2. **Lưu Log Tất Cả Các Lịch Đã Tạo**:
   - Thêm **node `stickyNote`** để **ghi lại lịch sử** các lịch được tạo.
   - **Cú pháp**:
     ```json
     {
       "title": "Lịch mới tạo",
       "content": `Lịch cho {{$node["Get all records from filter table"].json()["name"]}} đã được tạo vào {{$node["Create new calendar view"].json()["created_at"]}}`
     }
     ```

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `setInterval`** để **gửi báo cáo** về số lượng lịch đã tạo hàng tháng.
   - **Cú pháp**:
     ```json
     {
       "frequency": "1 month",
       "action": "sendEmail",
       "email": "team@example.com",
       "subject": "Báo cáo lịch cá nhân tháng {{$date.getMonth()}}",
       "body": `Tổng số lịch đã tạo: {{$node["Get all records from filter table"].json()["length"]}}`
     }
     ```

4. **Tự Động Tạo Lịch Khi Có Thay Đổi**:
   - Thay **Manual Trigger** bằng **Webhook** từ **Google Sheets** hoặc **Zapier** để **tạo lịch tự động** khi có dữ liệu mới.
   - **Cú pháp Webhook**:
     ```json
     {
       "url": "YOUR_N8N_WEBHOOK_URL",
       "method": "POST",
       "body": {
         "action": "create_calendar_view",
         "customer_id": "{{$node["Google Sheets"].json()["customer_id"]}}"
       }
     }
     ```

5. **Chia Sẻ Lịch Cho Nhiều Người Dùng**:
   - Sử dụng **node `baserow`** để **cập nhật quyền truy cập** cho từng lịch.
   - **Cú pháp**:
     ```json
     {
       "operation": "update",
       "resource": "view_permissions",
       "data": {
         "user_id": "{{$node["Get all records from filter table"].json()["user_id"]}}",
         "view_id": "{{$node["Create new calendar view"].json()["id"]}}",
         "permission": "read"
       }
     }
     ```
:::

---

## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow này **giải phóng bạn khỏi công việc lặp lại** như tạo lịch thủ công, quản lý thông tin phức tạp, và chia sẻ dữ liệu cho nhiều người dùng. **Với chỉ vài bước cấu hình**, bạn đã có một **hệ thống lịch tự động hóa hoàn chỉnh**, tích hợp với **Google Calendar, Outlook** và các ứng dụng khác.

:::success[HÀNH ĐỘNG NGÀY HÔM NAY]
1. **Tải workflow** từ [n8n.io](https://n8n.io/workflows/8485).
2. **Cấu hình Baserow credentials** và **ID của bảng/trường**.
3. **Test run** với 1-2 bản ghi mẫu.
4. **Bật Active** và **chia sẻ lịch** cho đội nhóm!
:::

---
### 🔗 **Tài Liệu Tham Khảo**
- [Baserow API Documentation](https://api.baserow.io/api/redoc/)
- [n8n Baserow Nodes](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.baserow/)
- [Tạo JWT Token cho Baserow](https://docs.baserow.io/docs/api/authentication/)

---
### 🎁 **Ưu Đãi Đặc Biệt Cho Các Sếp**
:::info[HÀNH TRẦN N8N TRÊN VPS]
Để workflow **chạy ổn định 24/7**, các sếp nên **self-host n8n** trên VPS.
👉 **Đăng ký VPS TinoHost** (mã giảm giá **VPSN8N** - giảm tới **39%**):
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)
👉 **VPS Xeon 4GB