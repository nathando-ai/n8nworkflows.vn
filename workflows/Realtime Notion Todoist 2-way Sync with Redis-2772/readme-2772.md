---
title: "🔄 **Tự Động Hóa Đồng Bộ 2 Chiều Todoist & Notion Thực Tế với Redis - Giải Pháp Tối Ưu Cho Nhóm Sales/HR/Marketing**"
description: "Workflow này tự động đồng bộ hóa 2 chiều giữa Todoist và Notion, đảm bảo mọi thay đổi trên một nền tảng sẽ tức thì phản ánh trên nền tảng kia, giảm thiểu sai sót và tiết kiệm thời gian lên đến 10 giờ/tuần cho các sếp. Sử dụng Redis để tránh vòng lặp và tối ưu hiệu suất."
slug: "tieu-dong-bo-2-chieu-todoist-notion-redis"
tags: [n8n, automation, no-code, todoist, notion, redis, sales, hr, marketing, productivity]
keywords: [n8n workflow todoist notion, tự động hóa đồng bộ 2 chiều, tự động hóa quản lý công việc, đồng bộ hóa todoist và notion, redis cho n8n, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Đồng Bộ 2 Chiều Todoist & Notion Thực Tế với Redis**

## **Giới Thiệu**
Bạn đã bao giờ mệt mỏi vì phải thủ công đồng bộ hóa công việc giữa **Todoist** và **Notion**? Hay phải lo lắng rằng một thay đổi trên Todoist sẽ không được cập nhật kịp thời trên Notion, và ngược lại? **Workflow này giải quyết vấn đề này hoàn toàn tự động hóa**, đồng bộ hóa **2 chiều** giữa hai nền tảng với tốc độ thực thời, đồng thời sử dụng **Redis** để tránh vòng lặp và tối ưu hiệu suất.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đồng bộ hóa thủ công hàng ngày, tiết kiệm **10+ giờ/tuần**.
- **Chính xác 100%**: Thay đổi trên Todoist sẽ tức thì phản ánh trên Notion và ngược lại.
- **Tránh xung đột**: Sử dụng **Redis** để tránh vòng lặp và đồng bộ hóa trùng lặp.
- **Cá nhân hóa công việc**: Đồng bộ hóa **status**, **due date**, **priority**, và **description** tự động.
- **Báo cáo tự động**: Gửi email tổng hợp tất cả thay đổi trong ngày.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Todoist**:
   - Một **project Todoist** đã tồn tại với các **section** tương ứng với **status** trong Notion (Backlog, In progress, Done, Obsolete).
   - [Tạo project Todoist](https://todoist.com/help/articles/200186605-Projects) nếu chưa có.

2. **Tài khoản Notion**:
   - Một **database Notion** với cấu trúc sau (đảm bảo tên trường chính xác):
     - **Text**: "Name"
     - **Status**: "Status" (có các tùy chọn: Backlog, In progress, Done, Obsolete)
     - **Select**: "Priority" (có các tùy chọn: do first, urgent, important)
     - **Date**: "Due"
     - **Checkbox**: "Focus"
     - **Text**: "Todoist ID" (để lưu ID Todoist tương ứng).
   - [Tải template Notion](https://steadfast-banjo-d1f.notion.site/17682b476c848086b002de766879aa71) để bắt đầu.

3. **Redis**:
   - Tạo một **Redis Cloud miễn phí** ([Redis Cloud](https://redis.io/try-free/)) hoặc tự host Redis trên VPS.

4. **Credentials cho n8n**:
   - **Notion API**: [Cài đặt tại đây](https://docs.n8n.io/integrations/builtin/credentials/notion/).
   - **Todoist API**: [Cài đặt tại đây](https://docs.n8n.io/integrations/builtin/credentials/todoist/).
   - **Redis**: [Cài đặt tại đây](https://docs.n8n.io/integrations/builtin/credentials/redis/).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** của workflow từ [n8n.io/workflows/2772](https://n8n.io/workflows/2772).
- Trong **n8n Editor**, nhấn **Import** và chọn file JSON đã tải.
- Hoặc **copy/paste** nội dung JSON vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** với **174 nodes**, nhưng chỉ cần chú ý đến các bước sau:

##### **A. Cấu hình Credentials**
- **Notion API**: Điền **Integration Token** từ Notion.
- **Todoist API**: Điền **API Token** từ Todoist (tạo tại [Todoist Developer](https://todoist.com/app/settings/developer)).
- **Redis**: Điền **URL Redis** và **Password** (nếu có).

##### **B. Cấu hình Globals Nodes**
Workflow có **3 node "Globals"** cần cấu hình bằng JSON từ **Sync Setup Helper Workflow**.
**Hướng dẫn chi tiết:**
1. **Chạy workflow "Sync Setup Helper"** (tên: `Notion-Todoist Sync Setup Helper`).
2. Mở **URL Production** của node `Notion-Todoist Sync Setup Helper` (trong tab "Triggers").
3. Điền thông tin:
   - **Notion Database ID** (copy từ URL Notion database).
   - **Todoist Project ID** (copy từ URL Todoist project).
4. Sau khi hoàn thành form, **copy JSON** từ node `Return config JSON` và dán vào **3 node "Globals"** trong workflow chính.

##### **C. Cấu hình Webhook Todoist**
1. Trong **Todoist Developer App**:
   - Tạo một **new app** với tên `"Notion-Todoist Sync"`.
   - Cấu hình **OAuth Redirect URL** bằng URL từ node `OAuth redirect` trong workflow (mở tab "Triggers" để lấy).
   - Sau khi đồng ý quyền, **cấu hình Webhook** với URL từ node `Todoist Webhook` (Todoist to Notion Diff sync).
   - Chọn các event:
     - `item:added`
     - `item:updated`
     - `item:completed`
     - `item:uncompleted`
     - `item:deleted`
2. **Activate webhook** và lưu lại.

##### **D. Cấu hình Webhook Notion**
Có **2 cách**:
**Option A: Notion Automation (phí)**
- Tạo **automation** trong Notion với trigger `"Any property edited"` và action `"Send webhook"`.
- URL Webhook: Copy từ node `Notion Webhook` trong workflow.

**Option B: Notion Webhook Emulator (miễn phí)**
- Sử dụng [workflow Notion Webhook Emulator](https://n8n.io/workflows/2284) và kết nối với URL từ node `Notion Webhook`.

##### **E. Cấu hình Email Báo Cáo**
- Thay đổi node `Gmail` để gửi báo cáo đến email của mình (hoặc sử dụng **SMTP** khác).

##### **F. Cấu hình Schedule (Tùy chọn)**
- Nếu muốn chạy **full sync hàng ngày**, cấu hình node `Schedule Trigger` để chạy vào giờ không làm việc (ví dụ: 23:00).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Thêm một task vào Todoist và kiểm tra Notion có đồng bộ không.
   - Thêm một task vào Notion và kiểm tra Todoist có đồng bộ không.
2. **Bật Active workflow**:
   - Chọn workflow và nhấn **Active** ở góc trên bên phải.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tách workflow thành 3 phần**:
   - **Notion-Todoist Full Sync** (đồng bộ toàn bộ dữ liệu).
   - **Notion-Todoist Diff Sync** (đồng bộ thay đổi thực thời).
   - **Todoist-Notion Diff Sync** (đồng bộ thay đổi Todoist sang Notion).
   - **Hướng dẫn**: Cắt & dán 3 phần workflow lớn (được đánh dấu bằng màu xanh lam) vào 3 workflow riêng biệt.

2. **Sử dụng Todoist Webhook Router (nâng cao)**:
   - Nếu sync nhiều project Todoist, tạo **workflow con** cho mỗi project và sử dụng node `Execute Workflow Trigger` để phân phối webhook.

3. **Lưu log thay đổi**:
   - Thêm node `Set` sau node `Gmail` để lưu **ID task** và **thời gian thay đổi** vào Notion hoặc Redis để theo dõi lịch sử.

4. **Báo cáo định kỳ**:
   - Sử dụng node `Schedule Trigger` kết hợp với `Gmail` để gửi báo cáo hàng tuần hoặc hàng tháng.

5. **Tránh xung đột với Redis**:
   - Redis được sử dụng để **lock task** khi đồng bộ hóa, tránh việc đồng bộ hóa trùng lặp. Thời gian lock mặc định là **15 giây**.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần đồng bộ hóa Todoist và Notion **một cách tự động, chính xác và tiết kiệm thời gian**. Bằng cách **tách workflow thành 3 phần** và **cấu hình Redis**, các sếp có thể yên tâm rằng mọi thay đổi sẽ được đồng bộ hóa **không sai sót**, đồng thời **tiết kiệm hàng giờ công việc hàng tuần**.

**Hành động ngay hôm nay!**
1. **Clone workflow** và cấu hình theo hướng dẫn.
2. **Chạy Sync Setup Helper** để lấy JSON cho Globals.
3. **Cấu hình Webhook Todoist và Notion**.
4. **Bật workflow** và bắt đầu tự động hóa!

👉 **Nếu cần hỗ trợ thêm**, các sếp có thể liên hệ với **Mario (Software Architect)** qua [đây](https://n8n.io/workflows/2772) để đặt lịch tư vấn cá nhân hóa workflow!