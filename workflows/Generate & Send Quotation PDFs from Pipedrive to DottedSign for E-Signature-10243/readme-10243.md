---
title: "🚀 Tự động tạo báo giá PDF từ Pipedrive và gửi ký điện tử qua DottedSign với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình bán hàng: tạo báo giá PDF chuyên nghiệp từ Pipedrive, lưu trữ file và gửi yêu cầu ký điện tử qua DottedSign."
slug: "tu-dong-tao-bao-gia-pipedrive-dottedsign-n8n"
tags: [n8n, automation, pipedrive, dottedsign, crm, e-signature]
keywords: [n8n workflow, tự động hóa pipedrive, dottedsign e-signature, tạo báo giá tự động, gotenberg pdf]
---

# 🚀 Tự động tạo báo giá PDF từ Pipedrive và gửi ký điện tử qua DottedSign

Chào các sếp! Trong quy trình bán hàng B2B, việc tạo báo giá thủ công, xuất PDF, lưu vào CRM rồi lại gửi qua email cho khách ký duyệt thường ngốn rất nhiều thời gian của đội ngũ sales. Chợt nhận ra deal chuyển sang giai đoạn "Quotation" nhưng sales vẫn hì hục làm file Excel hay Word rồi convert thủ công? Quá mất thời gian!

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ giúp tự động hóa 100% quy trình này: Khi một deal trong Pipedrive chuyển sang giai đoạn báo giá, hệ thống sẽ tự động tổng hợp thông tin, thiết kế file báo giá PDF chuẩn chỉnh, lưu lại trên Pipedrive và đồng thời đẩy thẳng sang **DottedSign** để khách hàng ký điện tử ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần copy-paste hay làm PDF thủ công, tiết kiệm hàng giờ mỗi ngày cho sales.
- **Chuyên nghiệp & Chuẩn hóa:** Báo giá được render từ HTML template đồng bộ, đẹp mắt với đầy đủ thông tin sản phẩm, khách hàng.
- **Lưu trữ minh bạch:** File PDF báo giá tự động đính kèm vào phần "Files" của deal tương ứng trên Pipedrive.
- **Ký duyệt tức thì:** Gửi trực tiếp yêu cầu ký kết qua DottedSign, đẩy nhanh tốc độ chốt sale.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **Pipedrive** (có quyền Admin để lấy API Key / tích hợp Webhook).
- Một tài khoản phát triển **DottedSign** để lấy thông tin API credentials (`client_id`, `client_secret`).
- Một instance **Gotenberg** đang hoạt động (dùng để chuyển đổi HTML sang PDF). Các sếp có thể tự host Gotenberg qua Docker rất dễ dàng.
:::

### Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy trực tiếp và paste vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các điểm mấu chốt sau:
- **Pipedrive Trigger & If Stage is 'Quotation'**: Trong node `If`, hãy thay đổi ID giai đoạn mặc định (`7`) thành ID thực tế của pipeline stage trong Pipedrive mà các sếp muốn dùng làm mốc kích hoạt báo giá.
- **Gotenberg to PDF (HTTP Request)**: Thay thế URL placeholder bằng endpoint của instance Gotenberg mà các sếp đang chạy (Ví dụ: `http://your-gotenberg-server:3000/forms/chromium/convert/html`).
- **Get DottedSign Access Token**: Điền `client_id` và `client_secret` của tài khoản DottedSign vào phần body của request.
- **DottedSign-CreateTask**: Tùy chỉnh tọa độ khung chữ ký (`page` và `coord`) trong `field_settings` cho khớp với vị trí ô ký trên mẫu HTML báo giá của các sếp.
- **Generate Quotation HTML**: Chỉnh sửa nội dung HTML, thêm logo công ty, điều khoản thanh toán, và các biến dữ liệu `{{ ... }}` lấy từ Pipedrive cho phù hợp với nhận diện thương hiệu công ty mình.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) với một deal mẫu trên Pipedrive để kiểm tra toàn bộ luồng dữ liệu từ việc gom data, tạo PDF cho tới khi đẩy sang DottedSign.
- Nếu mọi thứ xanh mướt (success), các sếp chỉ cần gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### Mẹo & gợi ý nâng cao
- **Thêm thông báo Slack/Telegram:** Thêm một node Slack hoặc Telegram vào cuối workflow để bắn thông báo ngay vào nhóm sales khi khách hàng đã mở hoặc ký xong báo giá.
- **Lưu Log Google Sheets:** Lưu lại lịch sử các báo giá đã phát hành kèm link DottedSign vào Google Sheets để ban quản lý dễ dàng thống kê doanh số dự kiến.
- **Tùy biến Template HTML:** Có thể tích hợp thêm các trường dữ liệu tùy chỉnh (Custom Fields) của Pipedrive vào báo giá thông qua các node `Get Pipedrive Custom Fields` và `Split Out Custom Fields` có sẵn trong workflow.

### Kết luận
Workflow này là mảnh ghép hoàn hảo để tối ưu hóa khâu chốt deal và ký kết hợp đồng cho các doanh nghiệp sử dụng Pipedrive CRM. Triển khai ngay hôm nay để giải phóng đội ngũ sales khỏi những tác vụ thủ công nhàm chán các sếp nhé!