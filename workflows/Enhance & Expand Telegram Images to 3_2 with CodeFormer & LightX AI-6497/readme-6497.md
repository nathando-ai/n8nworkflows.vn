---
title: "🚀 Tự động upscale và mở rộng ảnh Telegram sang tỷ lệ 3:2 với CodeFormer & LightX AI"
description: "Hướng dẫn chi tiết workflow n8n giúp tự động tiếp nhận ảnh từ Telegram, upscale bằng CodeFormer và mở rộng tỷ lệ sang 3:2 thông qua LightX AI một cách chuyên nghiệp."
slug: "tu-dong-upscale-mo-rong-anh-telegram-codeformer-lightx-ai"
tags: [n8n, automation, no-code, telegram, ai-image, lightx, codeformer]
keywords: [n8n workflow, tự động hóa ảnh telegram, codeformer n8n, lightx ai, upscale ảnh ai, mở rộng ảnh 3:2]
---

# 🚀 Tự động upscale và mở rộng ảnh Telegram sang tỷ lệ 3:2 với CodeFormer & LightX AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải xử lý thủ công từng bức ảnh gửi qua Telegram: vừa phải làm nét (upscale), vừa phải crop hoặc mở rộng khung hình sang tỷ lệ chuẩn 3:2 để đăng mạng xã hội? Công việc lặp đi lặp lại này ngốn rất nhiều thời gian quý báu của đội ngũ sáng tạo nội dung.

Đừng lo, workflow n8n này sẽ giải quyết trọn gói bài toán trên! Chỉ với một thao tác gửi ảnh đơn giản qua Telegram Bot, hệ thống sẽ tự động hóa 100% các bước: lưu trữ đám mây (AWS S3), xử lý AI tăng chất lượng với CodeFormer, tính toán padding thông minh, mở rộng tỷ lệ khung hình chuẩn 3:2 qua LightX AI, và trả lại kết quả sắc nét trực tiếp cho người dùng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, chỉ cần gửi ảnh vào Telegram Bot là có ngay ảnh chuẩn.
- **Chất lượng đỉnh cao**: Kết hợp sức mạnh của CodeFormer (làm nét mặt, upscale) và LightX AI (mở rộng khung hình 3:2 thông minh).
- **Trải nghiệm mượt mà**: Tự động quản lý trạng thái xử lý thông qua vòng lặp chờ (Wait & Check Status) và gửi lại kết quả ngay lập tức khi hoàn thành.
- **Tiết kiệm thời gian**: Giảm thiểu 90% thời gian xử lý ảnh thủ công cho các nhà sáng tạo nội dung và quản trị viên cộng đồng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
- **Telegram Bot Token** (tạo qua BotFather).
- **Tài khoản AWS S3** (hoặc dịch vụ lưu trữ tương thích S3) để lưu trữ ảnh gốc và ảnh sau khi xử lý.
- **Tài khoản Replicate API** (dùng cho mô hình AI CodeFormer upscale ảnh).
- **Tài khoản LightX AI API** (dùng cho tính năng mở rộng khung hình ảnh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow (từ nguồn n8n template #6497) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:
- **Telegram Trigger1**: Kết nối với Telegram Bot Credentials của sếp để lắng nghe sự kiện người dùng gửi ảnh.
- **Upload Original Photo to S1 / Upload Final Photo to S1**: Điền thông tin cấu hình AWS S3 (Bucket Name, Region, Access Key, Secret Key) để hệ thống lưu trữ file ảnh trung gian và file kết quả.
- **AI Upscale Image via Replicate**: Nhập Replicate API Key và kiểm tra endpoint của mô hình CodeFormer.
- **Request Upload Link from LightX / Request AI Expansion from LightX**: Cấu hình HTTP Request kèm API Key của LightX AI để thực hiện tiến trình mở rộng khung hình.
- **Send Final URL to User via Telegram**: Trỏ lại đúng Telegram Bot và cấu hình tin nhắn phản hồi chứa đường dẫn ảnh hoàn thiện.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một bức ảnh bất kỳ vào Telegram Bot để kiểm tra log hoạt động.
- Nếu mọi thứ chạy xanh mướt (success), các sếp hãy bật công tắc **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo**: Kết nối thêm node Telegram/Slack để gửi cảnh báo về kênh nội bộ mỗi khi có khách hàng sử dụng dịch vụ xử lý ảnh.
- **Lưu trữ lịch sử**: Thêm node Google Sheets hoặc Airtable để lưu lại thông tin người dùng và link ảnh đã xử lý nhằm phục vụ việc thống kê.
- **Tùy biến tỷ lệ**: Có thể điều chỉnh logic tính toán padding trong các node Code (như *Calculate Padding for 3:2 Ratio*) nếu muốn mở rộng ra các tỷ lệ khác như 16:9 hoặc 1:1.

### 📌 Kết luận
Workflow tích hợp AI này là giải pháp tuyệt vời giúp tự động hóa khâu xử lý ảnh nặng nhọc, mang lại trải nghiệm tương tác cực kỳ chuyên nghiệp ngay trên nền tảng Telegram. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!