---
title: "🐟 Hệ thống tự động cho ăn cá thông minh dựa trên thời tiết từ BMKG và cảnh báo Telegram"
description: "Hướng dẫn tự động hóa quá trình cho ăn cá dựa trên dự báo thời tiết từ BMKG và gửi cảnh báo qua Telegram. Giảm thiểu lãng phí thức ăn và tối ưu hóa quá trình nuôi cá."
slug: "he-thong-tu-dong-cho-an-ca-thong-minh-bmkg-telegram"
tags: [n8n, automation, no-code, nuôi cá, thời tiết, BMKG, Telegram]
keywords: [n8n workflow, tự động hóa, nuôi cá, thời tiết, BMKG, Telegram]
---

# 🐟 Hệ thống tự động cho ăn cá thông minh dựa trên thời tiết từ BMKG và cảnh báo Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của người nuôi cá khi phải theo dõi thời tiết và điều chỉnh lượng thức ăn thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quá trình theo dõi thời tiết và điều chỉnh lượng thức ăn.
- Chính xác: Dựa trên dữ liệu thời tiết chính xác từ BMKG.
- Cá nhân hóa: Điều chỉnh lượng thức ăn dựa trên dự báo mưa.
- Hoạt động liên tục: Chạy tự động theo lịch trình đã đặt.
- Cảnh báo tức thời: Nhận thông báo qua Telegram khi hệ thống hoạt động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và một bot Telegram đã tạo.
- Thiết bị ESP8266 kết nối với mạng WiFi.
- Tài khoản n8n đã cài đặt và chạy.
- Thông tin vị trí (tọa độ) của ao nuôi cá.
- Mã khu vực BMKG (ADM4) cho vị trí của bạn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/8667](https://n8n.io/workflows/8667).
2. Sao chép toàn bộ JSON của workflow.
3. Trong n8n Editor, nhấp vào menu → Import from File.
4. Dán JSON vào và nhấp vào Import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Cron: 05:30 & 16:30 WIB**: Node này đặt lịch chạy workflow vào lúc 05:30 và 16:30 mỗi ngày. Các sếp có thể thay đổi thời gian này theo nhu cầu.
- **Config**: Node này chứa các thông số cấu hình như tên ao, tọa độ, mã khu vực BMKG, ngưỡng mưa và phần trăm giảm lượng thức ăn.
  ```json
  {
    "locationName": "Main Pond",
    "lat": "-6.2000",
    "lon": "106.8166",
    "adm4": "31.71.03.1001",
    "thresholdProb": "60",
    "reducePercent": "-20"
  }
  ```
- **Telegram: Send Report**: Node này gửi báo cáo qua Telegram. Các sếp cần cấu hình credentials và Chat ID.
  - Để lấy Chat ID, các sếp có thể chuyển tiếp một tin nhắn bất kỳ đến @userinfobot và sao chép Chat ID hiển thị.
- **ESP8266 Fish Feeder Control**: Node này gửi lệnh điều khiển đến thiết bị ESP8266. Các sếp cần cấu hình URL của ESP8266.
  ```json
  {
    "esp8266WebhookUrl": "http://192.168.1.100/webhook"
  }
  ```

#### 3. Kích hoạt ⚡️
- **Test run dữ liệu mẫu**: Các sếp có thể thực hiện test run bằng cách nhấp vào nút "Execute Node" trên node đầu tiên (Cron) để kiểm tra workflow.
- **Bật Active workflow**: Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, các sếp có thể bật chế độ Active để workflow chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Các sếp có thể thêm node Slack để nhận cảnh báo thay vì Telegram.
- **Lưu log**: Các sếp có thể thêm node lưu log để theo dõi lịch sử hoạt động của workflow.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo hàng ngày hoặc hàng tuần qua email hoặc Telegram.
- **Cảnh báo khi thiết bị ngoại tuyến**: Các sếp có thể thêm node kiểm tra trạng thái của ESP8266 và gửi cảnh báo nếu thiết bị ngoại tuyến.

### 📌 Kết luận
Hệ thống tự động cho ăn cá thông minh dựa trên thời tiết từ BMKG và cảnh báo Telegram giúp các sếp tiết kiệm thời gian, chính xác và tối ưu hóa quá trình nuôi cá. Hãy áp dụng ngay để nâng cao hiệu quả nuôi cá của bạn!