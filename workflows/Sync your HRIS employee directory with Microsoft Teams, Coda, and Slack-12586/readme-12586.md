---
title: "🚀 Tự động đồng bộ danh sách nhân viên từ HRIS sang Microsoft Teams, Coda và Slack"
description: "Hướng dẫn tự động hóa đồng bộ danh sách nhân viên giữa HRIS và các công cụ nội bộ như Coda, Teams và Slack hàng ngày, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-danh-sach-nhan-vien-hris-teams-coda-slack"
tags: [n8n, automation, no-code, HR, Microsoft Teams, Coda, Slack]
keywords: [n8n workflow, tự động hóa HR, đồng bộ nhân viên, Coda API, Teams notification]
---

# 🚀 Tự động đồng bộ danh sách nhân viên giữa HRIS và các công cụ nội bộ

[Các sếp] có biết rằng việc cập nhật danh sách nhân viên thủ công giữa các hệ thống HRIS và các công cụ nội bộ như Coda, Microsoft Teams và Slack là một công việc tẻ nhạt, dễ gây lỗi và tiêu tốn nhiều thời gian? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này trong vòng 24 giờ, đảm bảo dữ liệu luôn đồng bộ và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động cập nhật danh sách nhân viên hàng ngày mà không cần can thiệp thủ công
- **Giảm lỗi**: Loại bỏ các lỗi nhập liệu do làm thủ công
- **Dữ liệu đồng bộ**: Đảm bảo thông tin nhân viên luôn nhất quán trên tất cả các hệ thống
- **Thông báo tức thời**: Nhận thông báo ngay khi có nhân viên mới hoặc thay đổi trạng thái
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HRIS với API truy cập danh sách nhân viên
- Tài khoản Coda với quyền tạo/sửa bảng "Employees"
- Tài khoản Microsoft Teams với quyền gửi tin nhắn
- (Tùy chọn) Tài khoản Slack với quyền gửi tin nhắn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12586](https://n8n.io/workflows/12586)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoàn tất import và mở workflow

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch HR Employees"**:
   - Cấu hình URL API của HRIS
   - Thêm headers và authentication cần thiết
   - Đảm bảo API trả về dữ liệu JSON đúng định dạng

2. **Node "Create/Update Employee in Coda"**:
   - Tạo tài liệu Coda mới hoặc sử dụng tài liệu hiện có
   - Đảm bảo bảng "Employees" đã được tạo
   - Cập nhật Doc ID và API Key trong credentials

3. **Node "Teams Notify"**:
   - Tạo OAuth credential trong n8n cho Microsoft Teams
   - Cung cấp Team ID và Channel ID
   - Kiểm tra quyền gửi tin nhắn

4. **Node "Slack Notify - New Employee"**:
   - Tạo OAuth credential trong n8n cho Slack
   - Cập nhật tên channel nếu cần

5. **Node "Map Employee Fields"**:
   - Kiểm tra và điều chỉnh mapping giữa các trường HRIS và các hệ thống đích
   - Đặc biệt chú ý đến trường "active" để phân biệt nhân viên đang làm việc

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu
2. Kiểm tra kết quả trên Coda, Teams và Slack
3. Bật chế độ Active workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm email thông báo**: Kết nối với node Email để gửi báo cáo hàng ngày
2. **Lưu log hoạt động**: Thêm node Database để lưu lịch sử các thay đổi
3. **Xử lý lỗi nâng cao**: Thêm node Error Handling để xử lý các trường hợp ngoại lệ
4. **Tích hợp với Google Sheets**: Thêm node Google Sheets để lưu bản sao lưu

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình đồng bộ danh sách nhân viên hàng ngày, giảm thiểu lỗi và tiết kiệm thời gian đáng kể. Bằng cách triển khai workflow này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong khi dữ liệu nhân viên luôn được cập nhật và đồng bộ trên tất cả các hệ thống nội bộ.