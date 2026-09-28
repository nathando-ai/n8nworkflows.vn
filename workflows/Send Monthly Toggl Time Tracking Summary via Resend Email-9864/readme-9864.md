---
title: "📅 [Tự động hóa] Gửi báo cáo theo dõi thời gian hàng tháng từ Toggl qua email Resend"
description: "Hướng dẫn tự động hóa gửi báo cáo thời gian làm việc hàng tháng từ Toggl đến email thông qua Resend, tiết kiệm thời gian và nâng cao hiệu quả quản lý dự án"
slug: "tu-dong-hoa-gui-bao-cao-thoi-gian-toggl-qua-email-resend"
tags: [n8n, automation, no-code, toggl, resend, email-marketing]
keywords: [n8n workflow, tự động hóa báo cáo, toggl time tracking, resend email, quản lý thời gian]
---

# 📅 [Tự động hóa] Gửi báo cáo theo dõi thời gian hàng tháng từ Toggl qua email Resend

[Các sếp đang gặp khó khăn khi phải tổng hợp báo cáo thời gian làm việc hàng tháng từ Toggl thủ công. Việc này tốn thời gian, dễ xảy ra lỗi và không thể tự động hóa. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ lấy dữ liệu đến gửi báo cáo qua email Resend, tiết kiệm thời gian đáng kể và đảm bảo tính chính xác cao.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tháng cho việc tổng hợp báo cáo thủ công
- Đảm bảo báo cáo luôn được gửi đúng hạn hàng tháng
- Có dữ liệu chi tiết về thời gian làm việc theo dự án và khách hàng
- Tự động hóa hoàn toàn quy trình báo cáo, giảm thiểu lỗi con người
- Có bản báo cáo có thể tùy chỉnh theo nhu cầu cụ thể của từng dự án
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Toggl với thông tin: Login, Password, TOGGL_WORKSPACE_ID
- Tài khoản Resend.com với RESEND_API_KEY
- Địa chỉ email gửi (FROM) và nhận (TO)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9864](https://n8n.io/workflows/9864)
2. Nhấn nút "Import" trên giao diện n8n Editor
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Toggle Projects"**:
   - Thêm credentials "togglApi" với thông tin đăng nhập Toggl
   - Điền TOGGL_WORKSPACE_ID vào URL request

2. **Node "Get Toggle Summary"**:
   - Thêm credentials "togglApi" với thông tin đăng nhập Toggl
   - Đảm bảo URL request chứa đúng TOGGL_WORKSPACE_ID
   - Kiểm tra ngày tháng trong query parameters để lấy dữ liệu tháng trước

3. **Node "Send email via Resend"**:
   - Thêm credentials "resendApi" với RESEND_API_KEY
   - Cấu hình địa chỉ email gửi (FROM) và nhận (TO)
   - Kiểm tra template email trong body request

4. **Node "Schedule Trigger"**:
   - Thiết lập thời gian gửi báo cáo hàng tháng (thường là ngày đầu tiên của tháng)
   - Kiểm tra timezone để đảm bảo thời gian đúng

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết quả
2. Kích hoạt workflow bằng cách nhấn nút "Active" trên giao diện n8n

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo Slack/Telegram khi báo cáo được gửi thành công
- Lưu bản sao báo cáo vào Google Drive hoặc Dropbox
- Tùy chỉnh template email với logo công ty và thông tin liên hệ
- Thêm báo cáo tuần/quý bằng cách thay đổi tham số thời gian trong node "Get Toggle Summary"
- Tích hợp với các công cụ báo cáo khác như Google Data Studio

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình báo cáo thời gian làm việc hàng tháng từ Toggl, tiết kiệm thời gian đáng kể và đảm bảo tính chính xác cao. Với việc tích hợp với Resend, các sếp có thể gửi báo cáo đến bất kỳ địa chỉ email nào một cách dễ dàng và chuyên nghiệp. Hãy áp dụng ngay để nâng cao hiệu quả quản lý thời gian và dự án của bạn!