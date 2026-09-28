---
title: "🚀 Tự Động Hóa Danh Sách Todo Hàng Ngày Trong Todoist - Giảm 90% Thời Gian Quản Lý Công Việc"
description: "Workflow tự động tạo danh sách todo hàng ngày từ mẫu dự án Todoist, thêm ngày và giờ làm việc tự động, giúp các sếp tiết kiệm 90% thời gian quản lý công việc hàng ngày. Hoạt động liên tục 24/7 mà không cần code."
slug: "tu-dong-hoa-danh-sach-todo-hang-ngay-todoist"
tags: [n8n, automation, todoist, no-code, productivity]
keywords: [n8n workflow todoist, tự động hóa todoist, danh sách todo hàng ngày, quản lý công việc tự động, tiết kiệm thời gian]
---

# 🚀 **Tự Động Hóa Danh Sách Todo Hàng Ngày Trong Todoist - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Hàng Ngày**
Các sếp đã bao giờ phải mất **30-60 phút mỗi sáng** để:
- **Tạo danh sách todo mới** từ mẫu dự án cũ?
- **Thêm ngày và giờ làm việc** cho từng công việc?
- **Quên hoặc bỏ sót** công việc quan trọng vì quá bận?
- **Phải làm thủ công** mỗi ngày, khiến tinh thần mệt mỏi?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy danh sách todo từ dự án mẫu** (đã cấu hình sẵn ngày và giờ làm việc).
✅ **Xóa todo cũ** (nếu có nhãn "daily") và **tạo todo mới** với ngày/giờ chính xác.
✅ **Hoạt động tự động hàng ngày** (5h sáng) mà không cần can thiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** quản lý todo hàng ngày.
- **Chính xác 100%** với ngày/giờ làm việc tự động.
- **Không quên công việc** nhờ hệ thống nhắc nhở tự động.
- **Hoạt động liên tục** 24/7, không cần can thiệp.
- **Cá nhân hóa** với mẫu dự án riêng của doanh nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Todoist** và **API Key** của Todoist (để kết nối với n8n).
   - **Cách lấy API Key Todoist**:
     - Mở Todoist → Cài đặt → API → Tạo API Token.
     - Copy token này để sử dụng trong **credentials** của n8n.
2. **Một dự án mẫu (template)** trong Todoist:
   - Tạo một **list mới** (ví dụ: `Template Daily Tasks`).
   - Trong mô tả của mỗi task, định dạng như sau:
     ```
     days:mon,tues; due:8am
     ```
     - `days:mon,tues` → Task sẽ tự động tạo vào **Thứ 2 và Thứ 4**.
     - `due:8am` → Task sẽ có **giờ làm việc là 8h sáng**.
3. **Nhãn "daily"** cho task hàng ngày (để workflow xóa task cũ và tạo mới).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2149) hoặc copy JSON từ canvas.
- Mở **n8n Editor** → Nhấn `Import` → Dán JSON hoặc tải file JSON.
- **Kiểm tra workflow** đã import hoàn chỉnh.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 phần chính**:
- **Phần 1: Lấy task từ dự án mẫu và tạo todo mới** (dùng 2 node `scheduleTrigger`).
- **Phần 2: Xóa task cũ có nhãn "daily"** (dùng node `if` và `delete`).

##### **A. Cấu Hình Todoist Credentials**
- Mở **Credentials** trong n8n → Tạo mới **Todoist API**.
- Điền:
  - **Name**: `todoistApi` (phải trùng với tên trong workflow).
  - **API Token**: Copy từ Todoist (như hướng dẫn trên).

##### **B. Cấu Hình Node Todoist**
Có **3 node Todoist** trong workflow:
1. **"Get all tasks from template project"**
   - **Project ID**: Tìm ID dự án mẫu trong Todoist (đường link dự án có dạng `https://todoist.com/project/123456789` → `123456789` là ID).
   - **Credentials**: Chọn `todoistApi`.

2. **"Get all tasks from Inbox"**
   - **Project ID**: Chọn `Inbox` của Todoist (ID mặc định là `inbox`).
   - **Credentials**: Chọn `todoistApi`.

3. **"Create new task in Inbox"**
   - **Project ID**: Chọn `Inbox`.
   - **Credentials**: Chọn `todoistApi`.

##### **C. Cấu Hình Node Code (Parse task details)**
- Node này **xử lý mô tả task** để trích xuất `days` và `due time`.
- **Không cần chỉnh sửa** nếu đã import đúng JSON.

##### **D. Cấu Hình Node Filter & If**
- **"Keep tasks that match today"**: Lọc task có ngày phù hợp.
- **"If list not empty"**: Chỉ chạy tiếp nếu có task mới.
- **"if it has daily label"**: Xóa task cũ có nhãn `daily`.

##### **E. Thiết Lập Thời Gian Chạy**
- Workflow có **2 node `scheduleTrigger`**:
  - **Every day at 5:10am**: Dùng để **xóa task cũ**.
  - **Every day at 5am**: Dùng để **tạo task mới**.
- **Không cần chỉnh** nếu muốn chạy theo mặc định.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn `Run` để kiểm tra workflow với dữ liệu mẫu.
  - Kiểm tra Todoist Inbox có task mới không.
- **Bật Active**:
  - Đánh dấu workflow thành `Active` để chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm node `slack` hoặc `telegram` để **nhắc nhở task mới** vào buổi sáng.
   - Ví dụ: Gửi tin nhắn `"Todo mới cho hôm nay: [Danh sách]"` vào Slack.

2. **Lưu Log Hoạt Động**
   - Thêm node `stickyNote` hoặc `googleSheets` để **ghi lại lịch sử task** đã tạo/xóa.
   - Dễ dàng theo dõi và debug nếu có lỗi.

3. **Tạo Báo Cáo Hàng Tuần**
   - Sử dụng node `scheduleTrigger` (thứ 7) + `googleSheets` để **tạo báo cáo tổng hợp** công việc tuần.

4. **Tùy Chỉnh Ngày/Giờ**
   - Nếu muốn chạy vào **giờ khác**, chỉnh node `scheduleTrigger` (ví dụ: 6h sáng thay vì 5h).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc quan trọng hơn. **Không cần code**, không cần kỹ thuật, chỉ cần **cấu hình đúng credentials và dự án mẫu** là xong!

**Hãy áp dụng ngay và trải nghiệm sự khác biệt!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/2149)
👉 [Cài n8n trên VPS để chạy 24/7](https://tino.vn/vps-n8n?affid=388)