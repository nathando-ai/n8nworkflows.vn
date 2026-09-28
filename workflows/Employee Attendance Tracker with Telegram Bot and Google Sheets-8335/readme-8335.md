---
title: "🚀 Quản lý Chấm công Nhân viên Tự động hóa qua Telegram Bot và Google Sheets với n8n"
description: "Xây dựng hệ thống chấm công thông minh qua Telegram Bot, tự động đồng bộ dữ liệu vào Google Sheets, xác thực nhân viên và chống trùng lặp hoàn toàn tự động với n8n."
slug: "quan-ly-cham-cong-telegram-google-sheets-n8n"
tags: [n8n, automation, telegram-bot, google-sheets, hr-automation]
keywords: [n8n workflow, chấm công telegram, google sheets automation, quản lý nhân sự n8n, bot telegram chấm công]
---

# 🚀 Quản lý Chấm công Nhân viên Tự động hóa qua Telegram Bot và Google Sheets

Việc quản lý chấm công thủ công qua sổ sách hoặc các phần mềm phức tạp thường gây tốn kém thời gian, dễ xảy ra sai sót và khó kiểm soát dữ liệu real-time. Các sếp có muốn xây dựng một hệ thống điểm danh gọn nhẹ, nhân viên chỉ cần thao tác trực tiếp trên **Telegram** (Check-in, Check-out, xem trạng thái) còn dữ liệu tự động lưu trữ và phân loại rạch ròi trên **Google Sheets** không? 

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình nhân sự này mà không tốn một đồng chi phí phần mềm đắt đỏ nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Check-in/Check-out siêu tốc**: Nhân viên chấm công mọi lúc mọi nơi ngay trên ứng dụng Telegram quen thuộc.
- **Bảo mật & Xác thực tự động**: Hệ thống tự động đối chiếu danh sách nhân viên qua `Sheets Read (employee)`, ngăn chặn tuyệt đối người lạ chấm công hộ.
- **Chống gian lận/trùng lặp**: Tự động kiểm tra lịch sử chấm công trong ngày, chặn các thao tác check-in/check-out nhiều lần bằng node `IF duplicate attendance`.
- **Dữ liệu trực quan**: Toàn bộ lịch sử điểm danh được đồng bộ hóa gọn gàng vào Google Sheets nhờ node `Sheets Append (Attendance)`.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot**: Tạo bot qua **BotFather** trên Telegram để lấy API Token.
- **Google Sheets**: Tài khoản Google Drive/Sheets để lưu trữ cơ sở dữ liệu nhân viên và bảng chấm công.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow `Attendance Telegram App.json` và import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các thành phần sau:
- **Telegram Trigger & các node Telegram**: Tạo Credentials loại `Telegram API` bằng cách dán Token của Bot do BotFather cung cấp. Áp dụng cho các node như `Send Main Menu`, `Send Check In/Out Menu`, `Reply Attendance Status`, v.v.
- **Google Sheets Nodes (`Sheets Read` & `Sheets Append`)**: Kết nối tài khoản Google thông qua `Google Sheets OAuth2 API`. 
  - Sử dụng [Google Sheets Template mẫu](https://docs.google.com/spreadsheets/d/1miqc4zpTecMwk_qNHgM17na2rDsWNpICIblKy44hwnw/edit?usp=sharing) và copy về Drive cá nhân.
  - Cập nhật đúng `Document ID` và tên Sheet tương ứng (`Employee` và `Attendance`) vào các node đọc/ghi dữ liệu trong workflow.
- **Bảng Employee**: Đảm bảo điền đầy đủ thông tin nhân viên (`id_employee`, `full_name`, `username_telegram`) vào sheet trước khi thử nghiệm.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách mở Telegram bot vừa tạo, gõ lệnh `/start` hoặc `/menu`.
- Kiểm tra các luồng Check-in, Check-out và xem trạng thái.
- Nếu mọi thứ hoạt động chính xác, hãy gạt công tắc **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo quản lý**: Kết nối thêm node Telegram hoặc Slack để gửi thông báo về nhóm quản lý mỗi khi có nhân viên check-late (đi muộn) hoặc vắng mặt.
- **Báo cáo tự động**: Thêm một Schedule Trigger chạy vào cuối tuần để tổng hợp số công và gửi báo cáo qua Email hoặc Telegram cho HR.
- **Chấm công định vị**: Có thể mở rộng tích hợp tính năng gửi vị trí (Location) trên Telegram để bắt buộc nhân viên phải chấm công tại văn phòng.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một hệ thống chấm công tự động hóa chuyên nghiệp, tiết kiệm hàng chục giờ quản lý thủ công mỗi tháng. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình nhân sự cho doanh nghiệp của mình nhé!