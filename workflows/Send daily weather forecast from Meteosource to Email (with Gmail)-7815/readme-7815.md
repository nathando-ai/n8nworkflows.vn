---
title: "☀️ Tự động gửi bản tin dự báo thời tiết hàng ngày qua Gmail với n8n và Meteosource"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy dữ liệu thời tiết từ Meteosource mỗi sáng và gửi bản tóm tắt qua Gmail, giúp bạn chuẩn bị tốt nhất cho ngày mới."
slug: "tu-dong-gui-du-bao-thoi-tiet-hang-ngay-qua-gmail-n8n"
tags: [n8n, automation, no-code, gmail, weather-api]
keywords: [n8n workflow, dự báo thời tiết tự động, meteosource api, gmail automation, tts, n8n việt nam]
---

# ☀️ Tự động gửi bản tin dự báo thời tiết hàng ngày qua Gmail với n8n và Meteosource

Bạn có thường xuyên quên xem dự báo thời tiết trước khi ra khỏi nhà? Việc kiểm tra thủ công mỗi sáng đôi khi khiến bạn quên mất mang theo ô hay mặc chưa đủ ấm. Với workflow n8n này, các sếp có thể tự động hóa hoàn toàn quy trình nhận bản tin thời tiết vào mỗi buổi sáng trực tiếp qua hòm thư Gmail của mình.

Workflow sẽ tự động kích hoạt vào lúc 7:00 sáng, gọi API từ Meteosource để lấy thông tin thời tiết chính xác tại địa điểm bạn chọn, sau đó tổng hợp thời tiết hôm nay cho tiêu đề thư và ngày mai cho nội dung bên trong, gửi gọn gàng đến email của bạn trước khi ngày mới bắt đầu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Không cần thao tác thủ công, bản tin thời tiết tự động "gõ cửa" email vào đúng 7:00 sáng mỗi ngày.
- **Nắm bắt thời tiết nhanh chóng:** Tiêu đề email hiển thị thời tiết hôm nay, nội dung bên trong dự báo ngày mai giúp chủ động lên kế hoạch.
- **Cá nhân hóa dễ dàng:** Dễ dàng thay đổi địa điểm (`place_id`) và email nhận thư chỉ với vài cú click.
- **Hoạt động bền bỉ:** Tận dụng Schedule Trigger chạy ngầm ổn định trên hệ thống n8n của bạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Hệ thống n8n:** Đã được cài đặt và hoạt động bình thường.
- **Tài khoản Meteosource API:** Để lấy dữ liệu thời tiết (cần chuẩn bị API Key và cấu hình `httpQueryAuth`).
- **Tài khoản Gmail:** Đã kết nối sẵn với n8n qua **Gmail OAuth2** để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp, sau đó copy toàn bộ nội dung JSON và paste trực tiếp vào màn hình n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà theo ý muốn, các sếp cần cấu hình chính xác 4 nodes sau:

- **`Schedule - every day 07:00` (Schedule Trigger):**
  - Mặc định lịch chạy là 7:00 sáng mỗi ngày. Các sếp có thể bấm vào node này để điều chỉnh lại khung giờ nếu muốn nhận sớm hơn hoặc muộn hơn.

- **`Config - place_id and recipient` (Set Node):**
  - Cấu hình các biến cốt lõi cho workflow:
    - `place_id`: Nhập mã định danh địa điểm trên Meteosource của bạn (ví dụ: `london`, `hanoi`, hoặc ID cụ thể của khu vực).
    - `send_to_email`: Nhập địa chỉ email sẽ nhận bản tin thời tiết.

- **`Weather API - Meteosource` (HTTP Request):**
  - Node này thực hiện gọi API đến Meteosource dựa trên `place_id` đã cấu hình ở bước trên.
  - Cần kết nối credential **`httpQueryAuth`** với API Key hợp lệ của bạn.

- **`Email - send weather summary` (Gmail):**
  - Node này chịu trách nhiệm gửi email.
  - Chọn credential **`gmailOAuth2`** của bạn.
  - Thiết lập tiêu đề (Subject) nhận tóm tắt thời tiết hôm nay và nội dung (Body) dự báo thời tiết ngày mai dựa trên kết quả trả về từ Meteosource API.

#### 3. Kích hoạt ⚡️
- Bấm **Test step** hoặc **Execute Workflow** trên từng node để kiểm tra xem dữ liệu thời tiết có được trả về và email có được gửi đi thành công hay không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để bật workflow chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng kênh nhận tin:** Ngoài Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để nhận thông báo thời tiết ngay trên điện thoại cho tiện theo dõi.
- **Gửi cho nhiều người:** Nâng cấp node Config để chứa danh sách nhiều email, kết hợp vòng lặp (Looping) để gửi bản tin cho cả gia đình hoặc team công ty.
- **Trình bày đẹp mắt:** Sử dụng định dạng HTML cho phần Body của email Gmail để bản tin thời tiết sinh động, có icon trực quan hơn.

### 📌 Kết luận
Một workflow nhỏ gọn nhưng cực kỳ hữu ích cho đời sống hằng ngày. Hãy cài đặt ngay để không bao giờ bị "bất ngờ" bởi những cơn mưa bất chợt nữa các sếp nhé!