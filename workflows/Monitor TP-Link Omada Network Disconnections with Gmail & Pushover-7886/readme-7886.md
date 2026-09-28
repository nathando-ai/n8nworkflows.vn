---
title: "🚀 Giám sát sự cố mất kết nối mạng TP-Link Omada qua Gmail và Pushover với n8n"
description: "Hướng dẫn tự động hóa quy trình giám sát thiết bị mạng TP-Link Omada Controller, lưu log Google Sheets và cảnh báo qua Pushover khi mất kết nối."
slug: "giam-sat-tp-link-omada-gmail-pushover-n8n"
tags: [n8n, automation, devops, tp-link, omada, monitoring, pushover]
keywords: [n8n workflow, tự động hóa, tp-link omada, giám sát mạng, gmail trigger, pushover notification]
---

# 🚀 Tự động giám sát sự cố mất kết nối TP-Link Omada với Gmail & Pushover

Các sếp quản trị hệ thống mạng chắc hẳn đã quá ngán ngẩm cảnh phải thủ công kiểm tra email cảnh báo từ Omada Controller mỗi khi có thiết bị "rớt mạng". Việc bỏ lỡ các cảnh báo quan trọng có thể dẫn đến thời gian downtime kéo dài, ảnh hưởng trực tiếp đến trải nghiệm người dùng hoặc hoạt động kinh doanh.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: bắt email cảnh báo từ Omada, bóc tách thông tin, lưu trữ vào Google Sheets, định kỳ kiểm tra thời gian mất kết nối và đẩy thông báo tức thì qua **Pushover** khi phát hiện thiết bị "ngủm" quá 30 phút. 100% tự động, không cần tốn công canh trực!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sự cố nhanh chóng**: Tự động thông báo qua điện thoại khi thiết bị ngắt kết nối trên 30 phút.
- **Lưu trữ lịch sử trực quan**: Toàn bộ cảnh báo được ghi nhận tự động vào Google Sheets để tiện tra cứu và thống kê.
- **Không bỏ sót cảnh báo**: Xử lý hoàn toàn tự động dựa trên email cảnh báo từ Omada Controller.
- **Dọn dẹp thông minh**: Tự động làm sạch dữ liệu cũ trong Google Sheets định kỳ mỗi 2 ngày để bảng tính luôn gọn gàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Gmail** (đã kết nối với Omada Controller để nhận email cảnh báo).
- Tài khoản **Google Sheets** (để tạo file log dữ liệu).
- Tài khoản **Pushover** (để nhận thông báo đẩy trên điện thoại).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn gốc, sau đó paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow hoạt động trơn tru:

- **Receives Alert (Gmail Trigger)**: Kết nối tài khoản Gmail của các sếp và cấu hình bộ lọc để bắt chính xác các email cảnh báo từ Omada Controller.
- **Process Email and Extract (Code)**: Node này dùng JavaScript để bóc tách các trường dữ liệu như thời gian, tên thiết bị, địa chỉ MAC, mức độ nghiêm trọng (severity) và trạng thái.
- **Append Row in Sheet & Get Row(s) in Sheet & Update Alert & Clear sheet (Google Sheets)**: 
  - Kết nối tài khoản Google Sheets thông qua OAuth2.
  - Trỏ tới file Google Sheet chuẩn bị sẵn để lưu log thiết bị ngắt kết nối.
  - Cấu hình ID file và Sheet Name tương ứng cho các thao tác `Append`, `Update` và `Clear`.
- **Check Every 5 minutes & Clear Rows Every 2 days (Schedule Trigger)**: 
  - Node định kỳ chạy mỗi 5 phút để quét xem thiết bị nào đã mất kết nối quá 30 phút.
  - Node định kỳ dọn dẹp dữ liệu cũ mỗi 2 ngày.
- **Check Device and Notify (Code)**: Chứa logic lọc các thiết bị có thời gian ngắt kết nối vượt ngưỡng 30 phút.
- **Alert User (Pushover)**: Kết nối tài khoản Pushover bằng API Token/User Key để đẩy thông báo về điện thoại của các sếp (có thể thay thế bằng Telegram, Slack tùy ý).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm với dữ liệu giả lập hoặc email thực tế.
- Sau khi kiểm tra mọi thứ chạy mượt mà, gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo**: Ngoài Pushover, các sếp có thể gắn thêm node Telegram Bot hoặc Slack để bắn tin nhắn vào group nội bộ của team IT.
- **Tùy chỉnh thời gian**: Thay đổi mốc thời gian 30 phút trong code node *Check Device and Notify* nếu muốn cảnh báo sớm hơn hoặc muộn hơn tùy theo SLA của hệ thống.
- **Báo cáo định kỳ**: Kết hợp thêm một Schedule Trigger chạy cuối tuần để tổng hợp số lượng sự cố mạng gửi vào email hoặc chatwork cho quản lý.

### 📌 Kết luận
Với workflow này, hệ thống mạng TP-Link Omada của doanh nghiệp sẽ luôn được giám sát chặt chẽ 24/7 mà không tốn một phút nhân lực canh trực thủ công nào. Hãy triển khai ngay để tối ưu hóa vận hành IT cho tổ chức của các sếp nhé!