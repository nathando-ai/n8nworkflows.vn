---
title: "📁 Tự động tạo cấu trúc thư mục Google Drive từ Template - Workflow n8n"
description: "Tự động hóa việc tạo thư mục Google Drive theo template với n8n. Tiết kiệm thời gian và đảm bảo tính nhất quán cho các dự án của bạn."
slug: "tu-dong-tao-thu-muc-google-drive-tu-template"
tags: [n8n, automation, no-code, google-drive, apps-script]
keywords: [n8n workflow, tự động hóa thư mục, google drive template, apps script]
---

# 📁 Tự động tạo cấu trúc thư mục Google Drive từ Template - Workflow n8n

[Các sếp] có bao giờ phải tạo hàng chục thư mục Google Drive với cấu trúc giống nhau cho các dự án khác nhau không? Việc này tốn thời gian và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tạo thư mục mới chỉ trong vài giây thay vì vài phút
- Đảm bảo tính nhất quán: Luôn có cấu trúc thư mục giống nhau cho mọi dự án
- Giảm lỗi: Loại bỏ các lỗi do tay người trong quá trình tạo thư mục
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công sau khi thiết lập
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập đầy đủ
- Template thư mục đã chuẩn bị với các placeholder `{{NAME}}`
- Google Apps Script đã được triển khai (xem phần hướng dẫn dưới đây)
- Credentials Google Drive đã được cấu hình trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/11663](https://n8n.io/workflows/11663)
3. Hoặc copy nội dung JSON từ link trên và dán vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Folder Request Form"**:
   - Cấu hình form để thu thập thông tin cần thiết (tên thư mục, thông tin khác nếu cần)
   - Có thể thêm các trường dữ liệu khác nếu cần

2. **Node "Create Main Folder"**:
   - Cấu hình credentials Google Drive
   - Đảm bảo có quyền truy cập đầy đủ vào thư mục đích

3. **Node "Duplicate Template"**:
   - Cập nhật các tham số sau:
     - `DESTINATION_PARENT_FOLDER_ID`: ID của thư mục cha nơi thư mục mới sẽ được tạo
     - `YOUR_APPS_SCRIPT_URL`: URL của Google Apps Script đã triển khai
     - `YOUR_TEMPLATE_FOLDER_ID`: ID của template thư mục

4. **Node "Wait for Drive"**:
   - Điều chỉnh thời gian chờ nếu cần thiết (mặc định là 1 giây)

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả trên Google Drive
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm thông báo**: Kết nối với Slack hoặc Email để thông báo khi thư mục mới được tạo
2. **Tích hợp CRM**: Cập nhật liên kết thư mục vào hệ thống CRM của bạn
3. **Tự động hóa thêm**: Kết nối với các dịch vụ khác như Trello, Asana để tạo task tự động
4. **Bảo mật nâng cao**: Thiết lập quyền truy cập chi tiết cho từng thư mục mới

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý thư mục Google Drive. Với việc tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào công việc thực sự quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi mà nó mang lại!