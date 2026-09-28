---
title: "🚀 Theo dõi chủ đề n8n Community với từ khóa và lưu vào Google Sheets"
description: "Tự động theo dõi và lưu các chủ đề liên quan đến từ khóa trên n8n Community vào Google Sheets, nhận thông báo qua Slack/Email khi có cập nhật mới."
slug: "theo-doi-chu-de-n8n-community-voi-tu-khoa-va-luu-vao-google-sheets"
tags: [n8n, automation, no-code, google-sheets, slack]
keywords: [n8n workflow, tự động hóa, theo dõi cộng đồng, google sheets, slack]
---

# 🚀 Theo dõi chủ đề n8n Community với từ khóa và lưu vào Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thủ công các chủ đề trên n8n Community. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi các chủ đề liên quan đến từ khóa trên n8n Community.
- Lưu trữ thông tin chủ đề vào Google Sheets với các trường dữ liệu: id, date, title, url, has_solution.
- Nhận thông báo tức thì qua Slack hoặc Email khi có chủ đề mới được thêm vào Google Sheets.
- Tiết kiệm thời gian và công sức trong việc theo dõi thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets API.
- Tài khoản Slack (tùy chọn, nếu muốn nhận thông báo qua Slack).
- Tài khoản Email (tùy chọn, nếu muốn nhận thông báo qua Email).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n Community Workflow](https://n8n.io/workflows/3152).
2. Click vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Đặt lịch chạy workflow theo nhu cầu của bạn (ví dụ: hàng ngày, hàng tuần).

2. **Node "Get latest topics"**:
   - **Double-click** vào node để mở nó cho chỉnh sửa.
   - Điều chỉnh giá trị của tham số "q" để khớp với từ khóa bạn muốn theo dõi.

3. **Node "Google Sheets"**:
   - **Double-click** vào node để mở nó cho chỉnh sửa.
   - Chọn tài liệu từ danh sách và thêm các cột: "id", "date", "title", "url", "has_solution".

4. **Node "Slack"** (tùy chọn):
   - **Double-click** vào node để mở nó cho chỉnh sửa.
   - Chọn kênh Slack bạn muốn nhận thông báo.

5. **Node "Send Email"** (tùy chọn):
   - **Double-click** vào node để mở nó cho chỉnh sửa.
   - Cấu hình thông tin Email để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm các từ khóa khác để theo dõi nhiều chủ đề hơn.
- Kết hợp với các công cụ khác như Telegram để nhận thông báo.
- Lưu log các chủ đề đã theo dõi để phân tích sau này.

### 📌 Kết luận
Workflow này giúp các sếp tự động theo dõi và lưu trữ các chủ đề liên quan đến từ khóa trên n8n Community vào Google Sheets, nhận thông báo tức thì qua Slack hoặc Email. Hãy áp dụng ngay để tiết kiệm thời gian và công sức!