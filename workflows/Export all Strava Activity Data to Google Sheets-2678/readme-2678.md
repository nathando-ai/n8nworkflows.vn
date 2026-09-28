---
title: "🚀 Tự động đồng bộ toàn bộ dữ liệu hoạt động Strava lên Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow tự động trích xuất toàn bộ dữ liệu chạy bộ, đạp xe từ Strava và lưu trữ an toàn vào Google Sheets mà không bị trùng lặp."
slug: "tu-dong-dong-bo-strava-len-google-sheets-n8n"
tags: [n8n, automation, strava, google-sheets, no-code, fitness-tracking]
keywords: [n8n workflow, export strava to google sheets, tự động hóa strava, đồng bộ dữ liệu tập luyện, n8n strava integration]
---

# 🚀 Tự động đồng bộ toàn bộ dữ liệu hoạt động Strava lên Google Sheets

Các sếp là tín đồ của chạy bộ, đạp xe hay bơi lội và đang dùng **Strava** để ghi lại hành trình luyện tập? Chắc hẳn các sếp đã từng cảm thấy bực mình khi muốn phân tích sâu hơn về quãng đường,pace, hay calo tiêu thụ bằng Excel/Google Sheets nhưng Strava lại không cung cấp công cụ export dữ liệu linh hoạt, thời gian thực. Việc copy/paste thủ công từng buổi tập thì quá mất thời gian và nhanh nản!

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh: Tự động quét, lọc trùng lặp và đồng bộ toàn bộ dữ liệu hoạt động từ **Strava** trực tiếp vào **Google Sheets** một cách mượt mà, tự động 100%.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần đụng tay, dữ liệu buổi tập mới sẽ tự động bay lên Google Sheets theo lịch hẹn.
- **Không lo trùng lặp dữ liệu:** Workflow thông minh tự động đối chiếu giữa dữ liệu cũ trên Google Sheets và Strava, chỉ thêm các hoạt động mới phát sinh.
- **Dễ dàng phân tích:** Thỏa sức vẽ biểu đồ phong độ, tính tổng quãng đường tháng/năm bằng các hàm và công cụ của Google Sheets.
- **Hoạt động bền bỉ 24/7:** Chạy ngầm ổn định trên server riêng mà không sợ bị ngắt quãng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản Strava:** Tài khoản cá nhân để lấy API/OAuth2 Credentials.
- **Google Account:** Chuẩn bị sẵn một Google Sheet với các cột tiêu đề tương ứng (Ngày, Tên hoạt động, Khoảng cách, Thời gian, Pace...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Schedule Trigger:** Cấu hình thời gian chạy tự động (ví dụ: Chạy mỗi ngày 1 lần vào lúc sáng sớm, hoặc chạy hàng tuần tùy nhu cầu).
- **Strava:** Cần kết nối tài khoản Strava của các sếp thông qua OAuth2. Thiết lập tham số `operation` là `getAll` để lấy toàn bộ danh sách hoạt động.
- **activities (Google Sheets):** Node này dùng để đọc dữ liệu đã lưu trữ trước đó trên Google Sheets. Các sếp cần chọn đúng tài khoản Google Sheets Credentials, chọn đúng File và Sheet chứa dữ liệu lịch sử tập luyện.
- **Remove Duplicates & Code:** Các node logic này đóng vai trò "bảo vệ", so sánh danh sách từ Strava với danh sách đã có trên Google Sheets (`saved_last`, `last_strava`, `sort_results`) để lọc ra chính xác các hoạt động hoàn toàn mới.
- **Google Sheets (Append):** Node thực hiện nhiệm vụ ghi các hoạt động mới tìm được vào cuối bảng Google Sheets của các sếp. Nhớ map đúng các trường dữ liệu (Fields) từ Strava sang các cột trong Sheet nhé!

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công lần đầu, kiểm tra xem dữ liệu có đổ về Google Sheets chuẩn chỉnh chưa.
- Sau khi test xanh mướt, hãy bật công tắc **Active** ở góc trên bên phải để n8n tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Bắn thông báo Telegram/Slack:** Nối thêm node Telegram ngay sau bước append thành công để mỗi khi chạy xong, bot sẽ gửi tin nhắn báo cáo: *"Hôm nay vừa chạy được 10km, đã đồng bộ vào Sheets!"*
- **Tạo dashboard tự động:** Kết hợp Google Sheets với Looker Studio (Google Data Studio) để tạo biểu đồ theo dõi phong độ chạy bộ cực kỳ chuyên nghiệp.

### 📌 Kết luận
Chỉ với vài phút thiết lập cùng workflow n8n này, các sếp đã giải quyết triệt để bài toán quản lý dữ liệu thể thao cá nhân. Không còn cảnh thủ công nhập liệu, giờ đây việc tập luyện và theo dõi tiến độ đã trở nên thông minh hơn bao giờ hết. Chúc các sếp "lên đồ" thành công!