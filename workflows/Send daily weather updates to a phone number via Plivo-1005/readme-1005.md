---
title: "☀️ Tự động gửi tin nhắn dự báo thời tiết hàng ngày qua điện thoại với n8n và Plivo"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy thông tin thời tiết từ OpenWeatherMap và gửi SMS cập nhật mỗi ngày qua dịch vụ Plivo một cách nhanh chóng."
slug: "tu-dong-gui-du-bao-thoi-tiết-hang-ngay-qua-plivo-n8n"
tags: [n8n, automation, no-code, plivo, openweathermap, weather-update, sms]
keywords: [n8n workflow, dự báo thời tiết tự động, gửi sms plivo, openweathermap n8n, cron trigger]
---

# ☀️ Tự động gửi tin nhắn dự báo thời tiết hàng ngày qua điện thoại với n8n và Plivo

Các sếp có bao giờ quên mang ô (dù) khi đi làm vì không xem dự báo thời tiết trước? Hay các sếp muốn xây dựng một dịch vụ nhỏ tự động gửi thông tin thời tiết buổi sáng cho khách hàng, người thân mà không phải làm thủ công mỗi ngày? 

Việc cập nhật thông tin thời tiết định kỳ tưởng chừng nhỏ nhặt nhưng nếu làm thủ công sẽ rất dễ quên. Với workflow n8n này, các sếp sẽ tự động hóa toàn bộ quy trình: Tự động kích hoạt vào một khung giờ cố định, lấy dữ liệu thời tiết mới nhất và bắn tin nhắn SMS trực tiếp đến số điện thoại qua tổng đài Plivo mà không cần chạm tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động thời gian:** Lên lịch chạy tự động mỗi sáng sớm (hoặc bất kỳ khung giờ nào các sếp muốn) nhờ node Cron.
- **Thông tin chính xác:** Lấy dữ liệu thời tiết thời gian thực từ OpenWeatherMap (nhiệt độ, độ ẩm, tình trạng mây mưa...).
- **Tiếp cận trực tiếp:** Gửi tin nhắn SMS nhanh chóng, tiện lợi đến điện thoại thông qua dịch vụ viễn thông Plivo.
- **Hoạt động 24/7:** Chạy ngầm liên tục trên server tự động, không lo gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản OpenWeatherMap:** Để lấy API Key truy cập dữ liệu thời tiết.
- **Tài khoản Plivo:** Có Auth ID, Auth Token và số điện thoại gửi/nhận tin nhắn SMS hợp lệ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trong n8n Editor, sau đó copy toàn bộ mã nguồn JSON của workflow này (từ nguồn n8n template #1005) và dán trực tiếp vào giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này siêu gọn nhẹ với chỉ 3 nodes chính, các sếp cần cấu hình chính xác các điểm sau:

- **Node Cron:** 
  - Cấu hình lại lịch chạy (Schedule) theo ý muốn của các sếp (ví dụ: Chạy lúc 7:00 sáng mỗi ngày).
- **Node OpenWeatherMap:**
  - Kết nối `openWeatherMapApi` bằng API Key cá nhân của các sếp.
  - Điền thông tin địa điểm (Thành phố, Quốc gia) mà các sếp muốn nhận dự báo thời tiết.
- **Node Plivo:**
  - Kết nối `plivoApi` sử dụng **Auth ID** và **Auth Token** từ tài khoản Plivo của các sếp.
  - Cấu hình số điện thoại gửi (`src`), số điện thoại nhận (`dst`) và nội dung tin nhắn (`text`) được map từ dữ liệu thời tiết trả về của node OpenWeatherMap.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử xem tin nhắn có bắn về điện thoại thành công hay không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Kết hợp thêm node Telegram Bot hoặc Slack để gửi bản tin thời tiết lên nhóm chat công ty/gia đình bên cạnh việc gửi SMS.
- **Cảnh báo thông minh:** Thêm các điều kiện (If Node) để nếu thời tiết có mưa, hệ thống sẽ gửi tin nhắn đặc biệt: *"Hôm nay trời mưa, nhớ mang ô nhé!"*.
- **Lưu lịch sử:** Lưu lại nhật ký các lần gửi tin nhắn vào Google Sheets để theo dõi trạng thái hoạt động của hệ thống.

### 📌 Kết luận
Một workflow siêu gọn nhẹ nhưng cực kỳ thiết thực cho cuộc sống hằng ngày hoặc tích hợp vào các ứng dụng chăm sóc khách hàng. Hãy "lên đồ" và cài đặt ngay hôm nay để không bao giờ bỏ lỡ bản tin thời tiết mỗi sáng nhé các sếp!