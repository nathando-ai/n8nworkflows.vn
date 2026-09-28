---
title: "🚀 Tự động hiển thị số lượng Subscriber YouTube lên đồng hồ thông minh Ulanzi AWTRIX với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu số lượng người đăng ký kênh YouTube hàng giờ và đồng bộ trực tiếp lên đồng hồ Ulanzi AWTRIX Smart Clock."
slug: "hien-thi-youtube-subscriber-len-ulanzi-awtrix-voi-n8n"
tags: [n8n, automation, no-code, youtube, ulanzi, awtrix, iot]
keywords: [n8n workflow, ulanzi awtrix, youtube subscriber count, iot automation, tự động hóa n8n]
---

# 🚀 Tự động hiển thị số lượng Subscriber YouTube lên đồng hồ thông minh Ulanzi AWTRIX với n8n

Các sếp sở hữu kênh YouTube và đang dùng đồng hồ thông minh **Ulanzi AWTRIX Smart Clock** hẳn sẽ rất muốn nhìn thấy số lượng subscriber tăng lên từng giờ ngay trên bàn làm việc mà không cần phải mở máy tính hay điện thoại kiểm tra liên tục. Tuy nhiên, việc thiếu một cầu nối tự động giữa YouTube API và thiết bị IoT khiến các sếp khó theo dõi các mốcmilestone quan trọng theo thời gian thực.

Đừng lo! Workflow n8n siêu gọn nhẹ này chính là giải pháp tự động hóa 100% không cần code, giúp kéo dữ liệu từ YouTube và đẩy thẳng lên đồng hồ Ulanzi AWTRIX của các sếp một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cập nhật tự động theo giờ:** Số liệu subscriber luôn mới nhất mà không tốn công thao tác thủ công.
- **Trải nghiệm trực quan:** Biến đồng hồ bàn thành một dashboard thu nhỏ cực kỳ sống động và chuyên nghiệp.
- **Vận hành bền bỉ 24/7:** n8n âm thầm làm việc ngầm, đảm bảo không bỏ sót bất kỳ mốc tăng trưởng nào của kênh.
- **Tùy biến linh hoạt:** Dễ dàng thay đổi tần suất cập nhật theo ý muốn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đang hoạt động (Cloud hoặc Self-hosted).
- **YouTube Data API Key:** Để gọi dữ liệu kênh YouTube.
- **Ulanzi AWTRIX Smart Clock:** Đã kết nối chung mạng nội bộ và bật HTTP API (thường chạy qua MQTT/AWTRIX Host).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tạo một workflow mới trên n8n, sau đó copy toàn bộ cấu trúc JSON của 3 nodes (`Every Hour`, `Fetch YT Subscriber Count`, `Send to AWTRIX`) và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow chỉ gồm 3 nodes cốt lõi, các sếp cần cấu hình chính xác các điểm sau:
- **Node `Every Hour` (Schedule Trigger):** Node này mặc định chạy mỗi giờ một lần. Các sếp có thể đổi sang phút (`Every Minute`) hoặc tuỳ chỉnh Cron Expression nếu muốn cập nhật nhanh hơn (ví dụ: mỗi 15 phút).
- **Node `Fetch YT Subscriber Count` (HTTP Request):** 
  - Cấu hình gọi đến YouTube API (`channels` endpoint với tham số `part=statistics` và `id=YOUR_CHANNEL_ID`).
  - Điền **YouTube API Key** của các sếp vào phần Header hoặc Query Parameters tương ứng.
- **Node `Send to AWTRIX` (HTTP Request):**
  - Trỏ URL đến địa chỉ IP nội bộ của đồng hồ Ulanzi AWTRIX (ví dụ: `http://<IP-AWTRIX>/api/custom?name=subscribers`).
  - Mapping dữ liệu số lượng subscriber vừa lấy được từ node YouTube vào phần Body của request theo cú pháp API mà AWTRIX yêu cầu (thường bao gồm text hiển thị và icon tùy chọn).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm xem dữ liệu từ YouTube có kéo về thành công và đồng hồ có hiển thị lên hay không.
- Sau khi test ngon lành, gạt công tắc **Active** ở góc trên cùng bên phải để workflow chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm icon sinh động:** Tận dụng thông số icon của AWTRIX để gắn thêm hình logo YouTube hoặc hình nút Play xinh xắn cạnh con số subscriber.
- **Hiển thị thêm số liệu view:** Mở rộng workflow bằng cách gọi thêm tổng số lượt xem (Total Views) và luân phiên hiển thị cùng số lượng subscriber.
- **Gửi thông báo cột mốc (Milestone):** Thêm một nhánh điều kiện (If Node) để nếu số sub đạt mốc tròn (ví dụ: 10k, 50k, 100k), n8n sẽ bắn thông báo chúc mừng về Telegram hoặc Slack của các sếp!

### 📌 Kết luận
Một workflow cực kỳ đơn giản nhưng mang lại trải nghiệm thị giác tuyệt vời cho góc làm việc của các content creator. Hãy setup ngay hôm nay để chiếc đồng hồ Ulanzi AWTRIX của các sếp trở nên thông minh và hữu ích hơn bao giờ hết!