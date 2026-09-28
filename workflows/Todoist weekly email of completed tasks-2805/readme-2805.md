---
title: "📅 [Tự động hóa] Gửi email hàng tuần công việc hoàn thành từ Todoist"
description: "Workflow n8n tự động tổng hợp và gửi email hàng tuần các công việc hoàn thành từ Todoist, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-email-cong-viec-hoan-thanh-tu-todoist"
tags: [n8n, automation, no-code, todoist, email]
keywords: [n8n workflow, tự động hóa, todoist, email hàng tuần, công việc hoàn thành]
---

# 📅 [Tự động hóa] Gửi email hàng tuần công việc hoàn thành từ Todoist

[Các sếp đang làm việc với Todoist nhưng vẫn phải tốn thời gian hàng tuần tổng hợp công việc hoàn thành để gửi email báo cáo? Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình này chỉ trong 5 phút cài đặt.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30 phút/tháng**: Không cần tổng hợp thủ công công việc hoàn thành
- **Chính xác 100%**: Dữ liệu được lấy trực tiếp từ Todoist API
- **Tự động hóa hoàn toàn**: Chạy tự động mỗi thứ Sáu sau giờ làm việc
- **Tùy chỉnh dễ dàng**: Có thể bỏ qua các dự án không quan trọng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Todoist với API key
- Tài khoản email (Gmail, Outlook,...) để gửi email báo cáo
- Thời gian khoảng 5-10 phút để cài đặt
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/2805)
2. Click vào nút "Copy" để sao chép JSON workflow
3. Trong n8n Editor, click vào menu "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get completed tasks via Todoist API"**:
   - Thiết lập credentials cho Todoist API
   - Đảm bảo API key có quyền truy cập đầy đủ vào các dự án cần theo dõi

2. **Node "Optional: Ignore specific projects"**:
   - Chỉnh sửa mã JavaScript để bỏ qua các dự án không quan trọng
   - Ví dụ: `if (projectId === '123456') continue;` để bỏ qua dự án có ID 123456

3. **Node "Format the email body"**:
   - Tùy chỉnh mẫu email theo nhu cầu của các sếp
   - Có thể thay đổi định dạng, màu sắc, hoặc thêm thông tin bổ sung

4. **Node "Every Friday afternoon"**:
   - Thiết lập thời gian gửi email (mặc định là 16:00 thứ Sáu)
   - Có thể điều chỉnh theo múi giờ của các sếp

5. **Node "Send Email"**:
   - Thiết lập credentials cho email gửi
   - Điền địa chỉ email nhận báo cáo
   - Có thể thêm CC/BCC nếu cần

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để kiểm tra với dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Activate" để kích hoạt workflow
3. Workflow sẽ tự động chạy mỗi thứ Sáu sau giờ làm việc

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo đến Slack/Teams cùng lúc với email
2. **Lưu log hoạt động**: Thêm node lưu log các công việc đã hoàn thành vào Google Sheets
3. **Báo cáo tuần trước**: Thêm node so sánh công việc tuần này với tuần trước
4. **Tùy chỉnh theo team**: Có thể chia workflow thành các phiên bản riêng biệt cho từng team

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá hàng tuần bằng cách tự động hóa việc tổng hợp và gửi email báo cáo công việc hoàn thành từ Todoist. Với chỉ 5 phút cài đặt, các sếp có thể bắt đầu tận hưởng lợi ích của tự động hóa ngay hôm nay!