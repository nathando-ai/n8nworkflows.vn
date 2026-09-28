---
title: "🔄 Tự động đồng bộ dữ liệu khách hàng giữa HubSpot và Linear qua Snowflake hàng ngày"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu khách hàng từ HubSpot sang Linear hàng ngày thông qua Snowflake, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-khach-hang-hubspot-linear-snowflake"
tags: [n8n, automation, no-code, crm, snowflake]
keywords: [n8n workflow, tự động hóa, hubspot, linear, snowflake]
---

# 🔄 Tự động đồng bộ dữ liệu khách hàng giữa HubSpot và Linear qua Snowflake hàng ngày

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải đồng bộ dữ liệu khách hàng giữa các hệ thống CRM và quản lý dự án thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ làm việc hàng ngày nhờ tự động hóa quy trình đồng bộ dữ liệu
- Giảm 90% lỗi nhập liệu thủ công giữa các hệ thống
- Đồng bộ dữ liệu khách hàng liên tục và chính xác theo lịch trình hàng ngày
- Nhận thông báo Slack tức thì về kết quả đồng bộ
- Tự động xử lý cả việc tạo mới và cập nhật thông tin khách hàng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập dữ liệu khách hàng
- Tài khoản Linear với quyền quản lý khách hàng
- Tài khoản Snowflake với quyền truy vấn dữ liệu
- Tài khoản Slack để nhận thông báo
- API keys cho Linear và Snowflake
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14518](https://n8n.io/workflows/14518)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Retrieve HubSpot Data from Snowflake"**:
   - Cấu hình credentials cho Snowflake
   - Chỉnh sửa truy vấn SQL để lấy dữ liệu khách hàng từ HubSpot
   - Đảm bảo truy vấn trả về các trường dữ liệu cần thiết (ID, tên, email, thông tin liên hệ...)

2. **Node "Fetch Customer Data"**:
   - Cấu hình credentials cho Linear API
   - Kiểm tra và cập nhật endpoint API nếu cần (mặc định là `/customers`)

3. **Node "When Scheduled at 2 PM"**:
   - Điều chỉnh thời gian chạy theo lịch trình của doanh nghiệp
   - Có thể thay đổi từ 2 PM sang thời gian phù hợp (ví dụ: 9 AM mỗi ngày)

4. **Node "Post Slack Notification"**:
   - Cấu hình channel Slack để nhận thông báo
   - Tùy chỉnh nội dung thông báo theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test chạy dữ liệu mẫu
2. Kiểm tra kết quả trên các node cuối cùng (Post Create/Update to Linear và Post Slack Notification)
3. Sau khi test thành công, bật chế độ Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Lưu log hoạt động**: Thêm node lưu log hoạt động vào Snowflake để theo dõi lịch sử đồng bộ
2. **Báo cáo định kỳ**: Tạo báo cáo tổng hợp kết quả đồng bộ và gửi qua email hàng tuần
3. **Xử lý lỗi tự động**: Thêm node xử lý lỗi và gửi cảnh báo khi có vấn đề xảy ra
4. **Kết hợp với các hệ thống khác**: Kết nối với hệ thống email marketing để cập nhật thông tin khách hàng sau khi đồng bộ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình đồng bộ dữ liệu khách hàng giữa HubSpot và Linear hàng ngày, tiết kiệm thời gian và giảm lỗi nhập liệu. Với việc cấu hình đơn giản và chạy ổn định, đây là giải pháp hoàn hảo cho các doanh nghiệp muốn tối ưu hóa quy trình làm việc. Hãy áp dụng ngay để trải nghiệm hiệu quả của tự động hóa!