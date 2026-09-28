---
title: "🚀 Tự động săn Trạm Không Gian Quốc Tế (ISS) bay qua đầu với n8n"
description: "Hướng dẫn cấu hình workflow n8n tự động theo dõi vị trí Trạm ISS, kiểm tra thời tiết thực tế và bắn thông báo qua Discord, Telegram, Gmail."
slug: "tu-dong-theo-doi-tram-iss-bay-qua-dau-n8n"
tags: [n8n, automation, no-code, api, discord, telegram, gmail]
keywords: [n8n workflow, theo doi iss, tu dong hoa n8n, openweathermap api, thong bao telegram discord]
---

# 🚀 Tự động săn Trạm Không Gian Quốc Tế (ISS) bay qua đầu với n8n

Các sếp có bao giờ tò mò muốn biết khi nào Trạm Không Gian Quốc Tế (ISS) bay ngang qua bầu trời nhà mình để ra ngoài ngắm nhìn không? Việc tra cứu lịch thủ công vừa mất thời gian lại dễ bỏ lỡ khoảnh khắc vàng. 

Giải pháp đây rồi! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thú vị, tự động kiểm tra vị trí ISS, đối chiếu điều kiện thời tiết thực tế tại khu vực của các sếp, và bắn tin báo cáo ngay lập tức qua Discord, Telegram hoặc Gmail khi có thể quan sát được. Toàn bộ tự động 100% không cần tốn một giọt mồ hôi code tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 săn trạm ISS, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Theo dõi thời gian thực:** Cập nhật vị trí ISS liên tục mà không bỏ lỡ đợt bay ngang qua nào.
- **Lọc thông minh theo thời tiết:** Chỉ gửi cảnh báo khi trời quang mây tạnh, đảm bảo nhìn thấy ISS bằng mắt thường thay vì báo động công cốc khi trời mưa bão.
- **Đa kênh thông báo:** Nhận thông tin chi tiết qua Discord, Telegram hay Gmail cá nhân kèm theo tên các phi hành gia đang làm việc trên trạm và link Google Earth xem vị trí trực quan.
- **Phù hợp mọi đối tượng:** Từ người yêu thiên văn, phụ huynh muốn truyền cảm hứng khoa học cho con trẻ, đến dân văn phòng cần một góc giải trí ngắn trong ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã hoạt động ổn định.
- **OpenWeatherMap API Key:** Tài khoản miễn phí để kiểm tra mây mưa, thời tiết.
- **Kênh thông báo (chọn ít nhất 1):** 
  - Discord Webhook URL
  - Telegram Bot Token & Chat ID
  - Tài khoản Gmail kết nối với n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy trực tiếp mã JSON và dán vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 16 nodes kết hợp nhịp nhàng từ lịch trình, xử lý tọa độ đến kiểm tra thời tiết. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Schedule Trigger:** Mặc định chạy mỗi 10 phút một lần (vì chu kỳ quỹ đạo ISS quay quanh Trái Đất là ~90 phút, tần suất này đảm bảo không bỏ sót lần bay nào).
- **Calculate Distance and Direction (Node loại Code):** ⚠️ **CỰC KỲ QUAN TRỌNG:** Các sếp cần vào node này để sửa lại tọa độ nhà mình:
  - `USER_LAT`: Vĩ độ (Latitude) nơi các sếp sinh sống.
  - `USER_LON`: Kinh độ (Longitude) nơi các sếp sinh sống.
  - `USER_LOCATION_NAME`: Tên thành phố/địa điểm (ví dụ: "Hanoi, Vietnam").
  - `VISIBILITY_RADIUS_KM`: Bán kính cảnh báo (mặc định 800km).
- **Get Local Weather (Node loại HTTP Request):** Cần gắn thông tin API Key của OpenWeatherMap để hệ thống biết được thời tiết thực tế tại tọa độ trên.
- **Các node thông báo (Send to Discord, Send to Telegram, Send Email via Gmail):** 
  - Điền Webhook, Bot Token, hoặc cấu hình tài khoản Gmail. 
  - Nếu kênh nào không dùng, các sếp có thể tạm thời vô hiệu hóa (Disable) node đó để tránh lỗi phát sinh.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử dữ liệu mẫu và kiểm tra xem luồng dữ liệu có đi qua các nhánh `Is ISS Overhead?` và `Can Observe?` mượt mà không.
- Sau khi test thành công, bật công tắc **Active** góc trên bên phải để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm Google Sheets để lưu lại lịch sử mỗi lần ISS bay qua và quan sát được nhằm làm nhật ký thiên văn cá nhân.
- **Tạo dashboard mini:** Gửi dữ liệu về Airtable hoặc Notion để thống kê số lần quan sát thành công trong tháng.
- **Tùy biến bán kính:** Điều chỉnh `VISIBILITY_RADIUS_KM` rộng hơn nếu các sếp muốn nhận thông tin sớm hơn để chuẩn bị dụng cụ ngắm sao (ống nhòm, máy ảnh).

### 📌 Kết luận
Một workflow vừa mang tính tự động hóa cao, vừa mang lại trải nghiệm giải trí tuyệt vời công nghệ vũ trụ ngay tại bàn làm việc của các sếp. Hãy áp dụng ngay và khoe thành quả "săn" trạm ISS với bạn bè nhé!