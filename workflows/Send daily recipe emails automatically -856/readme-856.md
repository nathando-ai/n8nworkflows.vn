---
title: "🍳 Tự động gửi email công thức nấu ăn mỗi ngày với n8n"
description: "Xây dựng hệ thống tự động hóa gửi email công thức nấu ăn hằng ngày từ API đến hòm thư người dùng một cách đơn giản và chuyên nghiệp với n8n."
slug: "tu-dong-gui-email-cong-thuc-nau-an-moi-ngay-voi-n8n"
tags: [n8n, automation, no-code, email-marketing, cron, smtp]
keywords: [n8n workflow, tự động hóa gửi email, gửi email công thức nấu ăn, cron job n8n, automation marketing]
---

# 🍳 Tự động gửi email công thức nấu ăn mỗi ngày với n8n

Các sếp đang vận hành một trang web ẩm thực, blog chia sẻ mẹo nấu ăn hoặc các bản tin (newsletter) nội dung vị giác? Việc phải chọn lọc và gửi thủ công hàng loạt công thức món ăn mới mỗi ngày đến hàng ngàn người đăng ký thực sự là một cơn ác mộng tốn thời gian, dễ nhầm lẫn và thiếu tính nhất quán.

Giải pháp ở đây là gì? Hãy để chiếc workflow n8n **"Send daily recipe emails automatically"** này gánh vác toàn bộ quy trình từ A-Z! Hệ thống sẽ tự động kích hoạt theo lịch trình, gọi dữ liệu món ăn từ API, xử lý định dạng HTML và tự động gửi email đều đặn mỗi ngày mà các sếp không cần tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chạy đúng hẹn mỗi ngày nhờ bộ đếm thời gian thông minh mà không cần can thiệp thủ công.
- **Trải nghiệm chuyên nghiệp:** Tự động tạo nội dung email bằng mã HTML bắt mắt, trình bày công thức nấu ăn rõ ràng, hấp dẫn người đọc.
- **Tiết kiệm nguồn lực:** Thay vì tốn hàng giờ mỗi ngày để soạn email, hệ thống tự động tổng hợp và gửi đi trong chớp mắt.
- **Mở rộng dễ dàng:** Dễ dàng thay đổi nguồn dữ liệu công thức (API, Database) hoặc mở rộng tệp khách hàng nhận tin.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động ổn định.
- **SMTP Credentials:** Thông tin tài khoản gửi email (Gmail, SendGrid, Amazon SES, hoặc máy chủ SMTP riêng của doanh nghiệp).
- **API Nguồn Công Thức:** Một endpoint API (hoặc dịch vụ bên thứ ba) cung cấp dữ liệu công thức nấu ăn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, vào giao diện n8n chọn **Add Workflow** -> **Import from File** (hoặc dán trực tiếp mã JSON) để đưa toàn bộ 9 nodes lên màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Node `Cron`**: Thiết lập lịch chạy mong muốn (ví dụ: 7:00 sáng mỗi ngày) để hệ thống tự động kích hoạt tiến trình gửi email.
- **Node `Search Criteria` & `Set Query Values` (Set & Function)**: Cấu hình các tham số tìm kiếm hoặc truy vấn món ăn theo ngày hoặc danh mục phù hợp với API nguồn của các sếp.
- **Node `Retrieve Recipe Counts` & `Retrieve Recipes` (HTTP Request)**: Điền chính xác Endpoint API lấy dữ liệu tổng số lượng và chi tiết công thức nấu ăn.
- **Node `Create Email Body in HTML` (Function)**: Tùy chỉnh đoạn mã code JavaScript bên trong để định dạng giao diện email HTML (thêm màu sắc, bố cục hình ảnh, nút bấm xem chi tiết món ăn).
- **Node `Send Recipes` (EmailSend - SMTP)**: Kết nối tài khoản SMTP của các sếp. Nhập thông tin người gửi (From), người nhận (To), tiêu đề email và chọn nguồn nội dung HTML được truyền từ node phía trước.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu, kiểm tra kỹ hòm thư xem email đã hiển thị đúng định dạng HTML hay chưa.
- Sau khi mọi thứ đã hoàn hảo, gạt công tắc sang chế độ **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node thông báo vào kênh Telegram nội bộ mỗi khi hệ thống gửi email thành công hoặc gặp lỗi kết nối API.
- **Lưu lịch sử vào Google Sheets:** Thêm bước ghi lại danh sách các công thức đã gửi vào Google Sheets để tránh việc gửi trùng lặp món ăn cho người dùng trong tuần.
- **Cá nhân hóa nội dung:** Kết hợp thêm dữ liệu người dùng để gọi tên trực tiếp (Ví dụ: *"Chào Linh, công thức món ngon hôm nay dành riêng cho bạn..."*).

### 📌 Kết luận
Một workflow cực kỳ gọn nhẹ nhưng mang lại giá trị chuyển đổi cao cho các nhà sáng tạo nội dung ẩm thực hoặc đội ngũ làm email marketing. Hãy "lên đồ" và cài đặt ngay hôm nay để tự động hóa hoàn toàn chiến dịch gửi email của các sếp nhé!