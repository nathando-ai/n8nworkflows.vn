---
title: "🚀 Tự động gửi tin nhắn LinkedIn cá nhân hóa cho người xem hồ sơ với ConnectSafely.ai và Google Sheets"
description: "Hướng dẫn tự động hóa gửi tin nhắn LinkedIn cá nhân hóa cho người xem hồ sơ của bạn bằng n8n, tiết kiệm thời gian và tăng hiệu quả kết nối mạng"
slug: "tu-dong-gui-tin-nhan-linkedin-ca-nhan-hoa"
tags: [n8n, automation, no-code, linkedin, google-sheets]
keywords: [n8n workflow, tự động hóa, linkedin, tin nhắn cá nhân hóa, google sheets]
---

# 🚀 Tự động gửi tin nhắn LinkedIn cá nhân hóa cho người xem hồ sơ với ConnectSafely.ai và Google Sheets

[Các sếp] có biết không? Việc phải theo dõi và gửi tin nhắn cá nhân hóa cho hàng trăm người xem hồ sơ LinkedIn hàng ngày là một công việc cực kỳ tốn thời gian và dễ gây mệt mỏi. Bạn phải liên tục kiểm tra danh sách người xem, lọc những người đã liên hệ, chuẩn bị nội dung phù hợp và gửi từng tin nhắn một. Điều này không chỉ tốn thời gian mà còn dễ gây lỗi và làm giảm hiệu quả kết nối mạng của bạn.

Với workflow này, các sếp có thể tự động hóa hoàn toàn quá trình này với n8n. Workflow sẽ tự động:
- Lấy danh sách người xem hồ sơ LinkedIn trong 7 ngày qua
- Kiểm tra xem đã liên hệ với họ chưa
- Gửi tin nhắn cá nhân hóa hoặc yêu cầu kết nối tùy theo trạng thái kết nối
- Ghi lại tất cả hoạt động vào Google Sheets để theo dõi

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quá trình gửi tin nhắn và yêu cầu kết nối
- **Tăng hiệu quả kết nối**: Gửi tin nhắn cá nhân hóa phù hợp với từng người
- **Theo dõi dễ dàng**: Ghi lại tất cả hoạt động vào Google Sheets
- **Hoạt động liên tục**: Chạy 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ConnectSafely.ai và API key
- Tài khoản Google và Google Sheets đã tạo sẵn
- Thông tin xác thực HTTP Bearer Auth cho ConnectSafely.ai
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12311](https://n8n.io/workflows/12311)
2. Click vào nút "Import" trên trang workflow
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch Profile Visitors"**:
   - Cấu hình credentials HTTP Bearer Auth với API key của ConnectSafely.ai
   - Đảm bảo API key có quyền truy cập vào danh sách người xem hồ sơ

2. **Node "Check if Already Contacted" và "Log DM Sent to Sheet"**:
   - Cập nhật ID của Google Sheet trong các node này
   - Đảm bảo Google Sheet có các cột: `Name`, `Linkedin URL`, `Status`

3. **Node "Generate DM for Connected User" và "Generate Message for New Connection"**:
   - Chỉnh sửa nội dung tin nhắn trong các node này để phù hợp với phong cách và mục tiêu kết nối của bạn

4. **Node "Weekly Schedule Trigger"**:
   - Điều chỉnh lịch trình để phù hợp với nhu cầu của bạn (mặc định là mỗi tuần một lần)

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có người mới xem hồ sơ
- Thêm node để gửi báo cáo hàng tuần về hoạt động kết nối
- Tùy chỉnh nội dung tin nhắn dựa trên ngành nghề hoặc vị trí công việc của người xem hồ sơ
- Sử dụng nhiều hơn các tính năng của ConnectSafely.ai để tối ưu hóa quá trình kết nối

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình gửi tin nhắn LinkedIn cá nhân hóa, tiết kiệm thời gian và tăng hiệu quả kết nối mạng. Bằng cách tích hợp với ConnectSafely.ai và Google Sheets, workflow đảm bảo rằng bạn luôn duy trì danh sách liên hệ tươi mới và hiệu quả. Hãy áp dụng ngay để nâng cao hiệu suất kết nối mạng của mình!