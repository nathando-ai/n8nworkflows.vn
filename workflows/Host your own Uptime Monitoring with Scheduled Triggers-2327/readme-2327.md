---
title: "🚀 Tự xây dựng hệ thống giám sát Uptime website tự động với n8n và Google Sheets"
description: "Hướng dẫn cài đặt hệ thống giám sát website (Uptime Monitoring) tự động bằng n8n, kiểm tra trạng thái HTTP, gửi cảnh báo qua Slack/Gmail và ghi log vào Google Sheets."
slug: "tu-xay-dung-he-thong-giam-sat-uptime-website-voi-n8n"
tags: [n8n, automation, devops, monitoring, google-sheets, slack]
keywords: [n8n workflow, uptime monitoring, giám sát website tự động, kiem tra uptime n8n, devops automation]
---

# 🚀 Tự xây dựng hệ thống giám sát Uptime website tự động với n8n

Việc các website, ứng dụng hoặc dịch vụ của doanh nghiệp bị sập (downtime) mà không hay biết sẽ gây tổn thất lớn về doanh thu và uy tín. Các giải pháp giám sát trả phí đôi khi quá đắt đỏ hoặc phức tạp so với nhu cầu cơ bản. 

Bài viết này sẽ hướng dẫn các sếp tự xây dựng một hệ thống **giám sát Uptime website hoàn toàn miễn phí** ngay trên nền tảng n8n kết hợp với Google Sheets và Slack/Gmail, hoạt động tự động 24/7 mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động kiểm tra định kỳ**: Hệ thống tự động ping danh sách website theo lịch trình cài đặt sẵn.
- **Cảnh báo tức thì**: Lập tức gửi thông báo qua Slack hoặc Gmail khi phát hiện website "sập" (DOWN) hoặc có thay đổi trạng thái.
- **Lưu lịch sử chi tiết (Logging)**: Tự động ghi lại mọi sự kiện uptime/downtime và cập nhật trạng thái mới nhất vào Google Sheets.
- **Tối ưu chi phí**: Tận dụng hạ tầng n8n sẵn có, không tốn phí dịch vụ monitoring bên thứ ba.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** (để tạo Google Sheets lưu danh sách website và log).
- **Tài khoản Slack** (tuỳ chọn, để nhận cảnh báo qua chat).
- **Tài khoản Gmail** (tuỳ chọn, để nhận cảnh báo qua email).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này (từ nguồn n8n template #2327) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng 10 nodes chính, trong đó các sếp cần lưu ý cấu hình kỹ các phần sau:

- **Google Sheets (Get Sites, Log Uptime Event, Update Site Status)**: 
  - Cần kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Chuẩn bị một Google Sheet với các cột bắt buộc:
    * **Property**: Địa chỉ URL của website cần giám sát (ví dụ: `https://example.com`).
    * **Status**: Trạng thái hiện tại (ghi giá trị ban đầu là `UP` hoặc `DOWN`).
- **Schedule Trigger**: 
  - Thiết lập chu kỳ chạy (ví dụ: kiểm tra mỗi 5 phút hoặc 15 phút tùy theo nhu cầu thực tế).
- **Perform Site Test (HTTP Request)**: 
  - Node này sẽ thực hiện gửi request GET đến các URL lấy từ Google Sheets và kiểm tra HTTP Status Code.
- **Status Router (Switch) & Calculate Status (Set)**: 
  - Xử lý logic phân loại trạng thái (nếu trang web phản hồi lỗi hoặc không truy cập được sẽ chuyển sang nhánh DOWN).
- **Send Chat Alert (Slack) & Send Email Alert (Gmail)**: 
  - Kết nối tài khoản Slack/Gmail để nhận thông báo khẩn cấp khi hệ thống ghi nhận sự cố.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) với 1-2 URL mẫu trong Google Sheets để đảm bảo luồng chạy suôn sẻ.
- Kiểm tra xem Google Sheets có ghi nhận log và đổi trạng thái chính xác không.
- Bật công tắc **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram Bot**: Thay vì chỉ dùng Slack/Gmail, các sếp có thể thay thế bằng node Telegram để nhận tin nhắn cảnh báo trực tiếp vào điện thoại cực kỳ nhanh chóng.
- **Báo cáo định kỳ**: Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp tỷ lệ Uptime của các website gửi về email báo cáo tổng kết.
- **Theo dõi mã lỗi chi tiết**: Mở rộng node HTTP Request để bắt thêm các mã lỗi cụ thể như `500 Internal Server Error` hoặc `404 Not Found` nhằm phân loại sự cố tốt hơn.

### 📌 Kết luận
Hệ thống giám sát Uptime tự động này là một "must-have" cho bất kỳ ai quản lý nhiều website hoặc hệ thống hạ tầng nhỏ. Chỉ với vài phút cài đặt trên n8n, các sếp đã có ngay một "vệ sĩ" túc trực 24/7 bảo vệ website của mình. Triển khai ngay thôi các sếp ơi!