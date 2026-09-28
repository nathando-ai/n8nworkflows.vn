---
title: "🚀 Tự động đồng bộ dữ liệu từ HubSpot sang Klaviyo và ghi log hoạt động lên Slack & Google Sheets"
description: "Hướng dẫn chi tiết cách tự động đồng bộ danh sách liên hệ từ HubSpot sang Klaviyo, gửi thông báo lên Slack và lưu log hoạt động lên Google Sheets bằng n8n"
slug: "tu-dong-dong-bo-hubspot-sang-klaviyo-voi-n8n"
tags: [n8n, automation, no-code, crm, email-marketing]
keywords: [n8n workflow, tự động hóa, HubSpot, Klaviyo, Slack, Google Sheets]
---

# 🚀 Tự động đồng bộ dữ liệu từ HubSpot sang Klaviyo và ghi log hoạt động lên Slack & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ danh sách liên hệ mới từ HubSpot sang Klaviyo ngay khi tạo
- Gửi thông báo đồng bộ thành công lên Slack để theo dõi
- Lưu log chi tiết các hoạt động đồng bộ lên Google Sheets
- Tiết kiệm thời gian và giảm thiểu lỗi thủ công
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập API
- Tài khoản Klaviyo với API key và danh sách đã tạo
- Tài khoản Slack để nhận thông báo (tùy chọn)
- Tài khoản Google để lưu log hoạt động
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/15940)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vừa sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive HubSpot Contact"**:
   - Đảm bảo đã cấu hình webhook trong HubSpot:
     - Vào Settings > Integrations > Private Apps
     - Tạo webhook mới với event "Contact Created"
     - Dán URL từ node này vào webhook URL

2. **Node "Configure Mapping and Settings"**:
   - Thêm HubSpot API key:
     - Tạo Private App trong HubSpot với quyền đọc Contacts
     - Copy access token và dán vào trường "HubSpot API Key"
   - Thêm Klaviyo API key:
     - Tạo Private API Key trong Klaviyo với quyền đầy đủ
     - Dán vào trường "Klaviyo API Key"
   - Cấu hình Klaviyo List IDs:
     - Lấy List ID từ Klaviyo (Lists > Segments)
     - Dán vào các trường tương ứng (Lead, MQL, SQL, Customer)

3. **Node "Notify Sync Complete"**:
   - Kết nối tài khoản Slack
   - Chọn channel để nhận thông báo
   - Nếu không dùng Slack, right-click và Disable node này

4. **Node "Log Sync to Sheets"**:
   - Tạo Google Sheet mới với tên "Klaviyo Sync Log"
   - Tạo các cột: Timestamp, Name, Email, Company, HubSpot Stage, Klaviyo List, Status
   - Kết nối tài khoản Google và chọn sheet vừa tạo

#### 3. Kích hoạt ⚡️
1. Test workflow bằng cách tạo liên hệ mới trong HubSpot
2. Kiểm tra:
   - Liên hệ có xuất hiện trong Klaviyo
   - Thông báo có đến Slack
   - Log có được ghi vào Google Sheets
3. Nếu tất cả đều hoạt động, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm các trường dữ liệu bổ sung từ HubSpot vào quá trình đồng bộ
2. Tạo branch để cập nhật profile Klaviyo khi liên hệ thay đổi stage trong HubSpot
3. Kết nối với Clearbit hoặc Apollo để bổ sung thông tin công ty
4. Thiết lập báo cáo định kỳ từ Google Sheets để theo dõi hiệu suất đồng bộ

### 📌 Kết luận
Workflow này giúp tự động hóa hoàn toàn quá trình đồng bộ dữ liệu từ HubSpot sang Klaviyo, giảm thiểu công việc thủ công và tăng độ chính xác. Các sếp có thể tùy chỉnh theo nhu cầu cụ thể của doanh nghiệp để tối ưu hóa quy trình marketing.