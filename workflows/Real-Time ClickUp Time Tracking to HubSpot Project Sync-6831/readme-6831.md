---
title: "🚀 Tự Động Hóa Theo Dõi Thời Gian ClickUp Sang HubSpot Thực Tế - Giảm 90% Công Việc Nhập Lại Dữ Liệu"
description: "Workflow này tự động đồng bộ thời gian làm việc từ ClickUp sang HubSpot (đối tượng tùy chỉnh) ngay lập tức, giúp các sếp quản lý dự án theo dõi giờ thực tế và giờ theo kế hoạch cho từng sprint một cách chính xác 100% không cần code."
slug: "tieu-dong-ho-thoi-gian-clickup-sang-hubspot"
tags: [n8n, automation, project-management, clickup, hubspot, no-code]
keywords: [n8n workflow clickup hubspot, tự động hóa quản lý dự án, đồng bộ thời gian làm việc, theo dõi sprint, giảm công việc thủ công]
---

# 🚀 **Tự Động Hóa Theo Dõi Thời Gian ClickUp Sang HubSpot Thực Tế**

### **Giải Phẫu Nỗi Đau Của Các Sếp Quản Lý Dự Án**
Các sếp đang phải **nhập lại thủ công** thời gian làm việc từ ClickUp sang HubSpot hàng ngày? Hay phải **so sánh thủ công** giữa giờ thực tế và giờ theo kế hoạch cho từng sprint? Điều này không chỉ **tốn thời gian** mà còn **mang lại sai sót** khi dữ liệu không đồng bộ. Với **Real-Time ClickUp Time Tracking to HubSpot Project Sync**, các sếp sẽ:
✅ **Tiết kiệm 90% thời gian** nhập liệu thủ công.
✅ **Đảm bảo dữ liệu chính xác** với đồng bộ thực thời.
✅ **Theo dõi hiệu suất dự án** theo sprint một cách tự động.
✅ **Cập nhật tự động** khi nhân viên cập nhật thời gian làm việc trên ClickUp.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần nhập liệu thủ công, giảm thiểu sai sót.
- **Dữ liệu đồng bộ thực thời**: Thời gian làm việc từ ClickUp được cập nhật ngay lập tức vào HubSpot.
- **Theo dõi sprint chi tiết**: Hỗ trợ phân loại giờ làm việc theo sprint (Sprint 1, Sprint 2, Additional Requests).
- **Báo cáo chính xác**: Giúp các sếp so sánh giữa giờ thực tế và giờ theo kế hoạch một cách dễ dàng.
- **Hoạt động 24/7**: Workflow chạy tự động khi có thay đổi thời gian trên ClickUp.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài Khoản ClickUp** với:
   - **Custom Field Dropdown** tên là `Sprint` (để phân loại nhiệm vụ theo sprint).
   - **Custom Field Short Text** tên là `HubSpot Deal ID` (để liên kết với bản ghi HubSpot).
   - **Tính năng Time Tracking** được bật cho các task.

2. **Tài Khoản HubSpot** với:
   - **Custom Object** dành riêng cho quản lý dự án (ví dụ: "Project Tracking").
   - **Custom Properties** trong Custom Object để lưu trữ:
     - `actual_hours_tracked` (tổng giờ thực tế).
     - `actual_sprint_1_hours`, `actual_sprint_2_hours`, `actual_additional_requests_hours` (giờ theo sprint).
     - `total_time_remaining` (giờ còn lại theo kế hoạch).

3. **API Keys & Credentials**:
   - **ClickUp OAuth2 API Key** (tạo từ [ClickUp Developer Portal](https://clickup.com/developer/api)).
   - **HubSpot Private App Token** (tạo từ [HubSpot Private Apps](https://developers.hubspot.com/docs/api/private-apps)).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và mở **n8n Editor**.
2. Nhấp vào **Import Workflow** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/6831)).
3. Chọn **Create Workflow** để tạo mới.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **9 node** quan trọng, các sếp cần chú ý cấu hình như sau:

##### **A. Cấu Hình Credentials**
- **ClickUp OAuth2 API**:
  - Đăng nhập vào [ClickUp Developer Portal](https://clickup.com/developer/api) tạo **OAuth2 App**.
  - Trong node `Time Tracked Update Trigger` và `ClickUp: Get Task Details`, chọn **clickUpOAuth2Api** và điền:
    - `Client ID` và `Client Secret` từ OAuth2 App.
    - `Team ID` (tìm trong URL ClickUp: `https://app.clickup.com/t/{team_id}`).

- **HubSpot Header Auth**:
  - Tạo **Private App** trong HubSpot và lấy **Private App Token**.
  - Trong node `HubSpot: Update Project Hours`, chọn **httpHeaderAuth** và điền:
    - `Authorization: Bearer {private_app_token}`.
    - `Content-Type: application/json`.

##### **B. Cấu Hình Node Quan Trọng**
1. **`Time Tracked Update Trigger`**:
   - Chọn **ClickUp Team** và **Space** cần theo dõi.
   - Chọn **Event Type**: `Time Entry Updated`.

2. **`ClickUp: Get Task Details`**:
   - Điền `Task ID` từ payload của node `Time Tracked Update Trigger`.

3. **`Code: Extract Sprint & Task Data`**:
   - Node này sử dụng **JavaScript** để trích xuất dữ liệu từ task (ví dụ: `Sprint` và `HubSpot Deal ID`).
   - Các sếp có thể chỉnh sửa logic ở đây nếu cần (ví dụ: thay đổi cách tính giờ sprint).

4. **`HubSpot: Update Project Hours`**:
   - Điền **ID của Custom Object** trong HubSpot (ví dụ: `12345678901234567890`).
   - Cập nhật URL trong node `OnProjectFolder` để trỏ đến **Custom Object** của các sếp:
     ```
     https://api.hubapi.com/crm/v3/objects/{object_type}/find?filter={...}
     ```
   - Thay thế `{object_type}` bằng ID của Custom Object (tìm trong **Settings > Objects** trên HubSpot).

5. **`Route by Sprint Type`**:
   - Node này phân loại giờ làm việc theo sprint (Sprint 1, Sprint 2, Additional Requests).
   - Các sếp có thể chỉnh sửa logic ở đây nếu cần thêm sprint mới.

##### **C. Test Run & Kích Hoạt**
1. **Test Run**:
   - Nhấp vào **Execute Workflow** và chọn **Test Execution**.
   - Chọn **Time Tracked Update Trigger** và nhấp **Execute** để kiểm tra.
   - Kiểm tra kết quả trong **HubSpot** để đảm bảo dữ liệu được cập nhật chính xác.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[MỘT SỐ Ý TƯỞNG MỞ RỘNG]
1. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Schedule Node** để gửi báo cáo tổng hợp giờ làm việc theo sprint hàng tuần qua **Email** hoặc **Slack**.

2. **Lưu Log Dữ Liệu**:
   - Thêm **Google Sheets** hoặc **Notion** vào workflow để lưu lịch sử thay đổi thời gian.

3. **Kết Hợp Với Slack/Telegram**:
   - Sử dụng **Slack Webhook** hoặc **Telegram Bot** để thông báo khi có thay đổi thời gian mới.

4. **Tự Động Khôi Phục Dữ Liệu**:
   - Nếu dữ liệu HubSpot chưa đồng bộ, chạy workflow **ClickUp Client Project Data Stream** để đồng bộ toàn bộ dữ liệu ban đầu.

5. **Tùy Chỉnh Sprint Logic**:
   - Trong node **Code**, các sếp có thể thay đổi cách tính giờ sprint (ví dụ: thêm sprint mới hoặc thay đổi logic phân loại).

---
### **📌 Kết Luận**
Workflow **Real-Time ClickUp Time Tracking to HubSpot Project Sync** là **giải pháp hoàn hảo** cho các sếp quản lý dự án muốn **tự động hóa hoàn toàn** việc theo dõi thời gian làm việc và đồng bộ dữ liệu giữa ClickUp và HubSpot. Với việc chỉ cần **cấu hình một lần**, các sếp sẽ **tiết kiệm thời gian, giảm sai sót** và **quản lý dự án hiệu quả hơn**.

**🚀 Hãy áp dụng ngay và tự động hóa công việc của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/6831)** | **📌 [Tải file JSON](https://n8n.io/workflows/6831/download)**