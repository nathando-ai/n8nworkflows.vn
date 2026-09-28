---
title: "🚀 Tự động hóa điều khiển thiết bị IoT qua Webhook và MQTT với n8n"
description: "Hướng dẫn xây dựng hệ thống điều khiển phần cứng IoT (ESP32) từ xa dễ dàng thông qua Webhook và MQTT Broker bằng n8n workflow tự động 100%."
slug: "dieu-khien-thiet-bi-iot-mqtt-webhook-n8n"
tags: [n8n, automation, iot, mqtt, webhook, esp32, no-code]
keywords: [n8n iot control, mqtt webhook n8n, dieu khien iot bang n8n, esp32 mqtt n8n, automation iot no-code]
---

# 🚀 Tự động hóa điều khiển thiết bị IoT qua Webhook và MQTT với n8n

Việc kết nối các hệ thống web với phần cứng IoT (như ESP32, Arduino, Raspberry Pi) thường đòi hỏi phải thiết lập các server trung gian phức tạp, lập trình socket hoặc cấu hình các giao thức mạng rườm rà. Nếu các sếp đang tìm kiếm một giải pháp nhanh gọn để biến các cú click chuột trên web thành lệnh điều khiển thiết bị vật lý mà không cần viết quá nhiều code, thì workflow n8n này chính là mảnh ghép hoàn hảo.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và giữ kết nối MQTT liên tục với các thiết bị IoT, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Điều khiển thời gian thực (Real-time):** Nhận tín hiệu từ Web khi người dùng bấm nút "On" hoặc "Off" và truyền ngay lập tức xuống thiết bị phần cứng.
- **Tách biệt giao diện và phần cứng:** Sử dụng Webhook làm cầu nối an toàn giữa giao diện điều khiển (web page) và MQTT Broker.
- **Tối ưu hóa tài nguyên:** Không cần duy trì một server backend cồng kềnh, n8n đóng vai trò là "bộ não" điều phối thông minh.
- **Mở rộng dễ dàng:** Dễ dàng bổ sung thêm các node logic, ghi log lịch sử bật/tắt vào Google Sheets hoặc gửi thông báo Telegram khi thiết bị thay đổi trạng thái.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (ưu tiên bản Self-hosted để kết nối MQTT ổn định).
- **MQTT Broker:** Thông tin kết nối MQTT Broker (Hostname/IP, Port, Username, Password nếu có).
- **Thiết bị IoT (Ví dụ: ESP32):** Đã được lập trình để kết nối vào MQTT Broker và lắng nghe (subscribe) vào topic `pin-control` nhằm điều khiển chân GPIO (bật/tắt đèn LED, relay,...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor (hoặc import file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 node chính hoạt động nhịp nhàng với nhau:

- **Node `IOT control Webhook` (Webhook):**
  - Node này đóng vai trò lắng nghe tín hiệu từ trang web điều khiển IoT của các sếp (ví dụ khi người dùng click nút "On" hoặc "Off").
  - Lưu ý cấu hình HTTP Method (thường là POST hoặc GET tùy thuộc vào cách thiết kế web page) và chú ý đường dẫn endpoint `pin-control` được cung cấp.
- **Node `Set data for MQTT message payload` (Set):**
  - Node này chịu trách nhiệm chuẩn bị dữ liệu (chuẩn hóa payload) nhận được từ webhook để chuyển đổi thành định dạng mà MQTT Broker yêu cầu.
  - Các sếp cần trích xuất giá trị (ví dụ: trạng thái `state: on` hoặc `state: off`) truyền từ webhook để đưa vào payload gửi đi.
- **Node `MQTT Publish Topic Node` (MQTT):**
  - Node quan trọng nhất để đẩy lệnh xuống phần cứng.
  - Các sếp cần cấu hình **Credentials** cho MQTT (nhập địa chỉ Broker, Port, thông tin đăng nhập).
  - Cấu hình Topic name là `pin-control` và truyền Payload đã được xử lý từ node Set trước đó. Khi node này chạy, nó sẽ bắn message xuống topic và ESP32 đang lắng nghe topic này sẽ lập tức thực thi bật/tắt GPIO tương ứng.

#### 3. Kích hoạt ⚡️
- Sử dụng tính năng **Execute Node** hoặc **Test workflow** trên webhook bằng cách gửi một request giả lập (dùng Postman hoặc curl) để kiểm tra xem thiết bị phần cứng có nhận được lệnh hay không.
- Sau khi test thành công, các sếp nhớ gạt công tắc **Active** góc trên bên phải để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Ghi log lịch sử:** Nối thêm một node Google Sheets hoặc Notion sau bước MQTT Publish để lưu lại lịch sử mỗi lần ai đó bật/tắt thiết bị (kèm theo timestamp).
- **Cảnh báo qua Telegram/Slack:** Nếu thiết bị IoT bị mất kết nối MQTT (hoặc gửi tín hiệu báo lỗi), có thể dùng n8n để nhận phản hồi và bắn tin nhắn cảnh báo ngay lập tức vào nhóm chat của đội kỹ thuật.
- **Lập lịch tự động (Cron):** Kết hợp thêm node **Schedule Trigger** trước node Set để tự động bật/tắt thiết bị IoT theo khung giờ định sẵn hàng ngày (ví dụ: tự động bật đèn lúc 18:00 và tắt lúc 23:00).

### 📌 Kết luận
Việc kết hợp n8n với MQTT và Webhook mở ra một hướng đi cực kỳ mạnh mẽ, giúp các kỹ sư hay dân "maker" tự động hóa các dự án IoT, Smart Home một cách nhanh chóng mà không phải tốn hàng tuần code backend phức tạp. Chúc các sếp "lên đồ" thành công!