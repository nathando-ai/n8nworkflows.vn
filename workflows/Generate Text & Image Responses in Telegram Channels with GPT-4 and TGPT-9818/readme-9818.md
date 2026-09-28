---
title: "🚀 Tự động tạo nội dung Text & Hình ảnh bằng AI trong Telegram Channel với n8n"
description: "Hướng dẫn cấu hình workflow n8n tự động giám sát Telegram Channel, xử lý lệnh và tạo nội dung văn bản hoặc hình ảnh bằng GPT-4 (thông qua TGPT)."
slug: "tu-dong-tao-text-image-telegram-channel-gpt4-n8n"
tags: [n8n, telegram, ai, gpt-4, automation, tgpt]
keywords: [n8n workflow, telegram bot ai, tgpt gpt4, tự động hóa telegram, tạo ảnh bằng ai telegram]
---

# 🚀 Tự động tạo nội dung Text & Hình ảnh bằng AI trong Telegram Channel với n8n

Các sếp có đang quản lý các kênh Telegram và muốn biến chúng thành một trợ lý AI thông minh? Việc phải ngồi thủ công trả lời tin nhắn, tạo nội dung văn bản hay vẽ hình ảnh minh họa cho kênh tốn rất nhiều thời gian.

Với workflow n8n này, các sếp sẽ sở hữu một hệ thống bot tự động 100%: giám sát kênh Telegram liên tục, phân loại yêu cầu dựa trên cú pháp, và tự động gọi AI (GPT-4 / TGPT) để tạo ra văn bản sắc sảo hoặc bức ảnh tuyệt đẹp ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Bot tự động quét tin nhắn mỗi 10 giây, chống trùng lặp và lọc theo khung thời gian thực.
- **Đa phương tiện thông minh:** Vừa có thể viết nội dung chuyên sâu (với lệnh `am#`), vừa có thể vẽ tranh sáng tạo độ phân giải cao 1920x1080 (với lệnh `ami#`).
- **Hoạt động 24/7 không cần giám sát:** Chạy ngầm trên n8n, tự động quản lý offset tin nhắn đã đọc một cách chính xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyến nghị bản Self-hosted để chạy lệnh hệ thống `executeCommand`).
- **Telegram Bot Token:** Tạo bot qua [@BotFather](https://t.me/BotFather) và cấp quyền Admin cho bot trong Channel mục tiêu.
- **Telegram Channel ID:** ID của kênh mà bot sẽ giám sát và gửi phản hồi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow và dán trực tiếp vào n8n Editor của các sếp, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Config` (Set):** Cập nhật các thông số cấu hình cốt lõi như Telegram Bot Token (`your_telegram_token`) và Channel ID (`your_telegram_channel_id`).
- **Node `Get Updates` & `Clear Update List` (HTTP Request):** Đảm bảo cấu hình gọi API Telegram chính xác để lấy tin nhắn mới và dọn dẹp danh sách cập nhật.
- **Node `Execute - Text` & `Execute - Image` (Execute Command):** Các node này sử dụng lệnh hệ thống để cài đặt và chạy TGPT. Hãy đảm bảo môi trường VPS của các sếp cho phép thực thi các lệnh này.
- **Node `Send Telegram Text Response` & `Send Telegram Image Response` (Telegram):** 
  - Chọn hoặc tạo mới **Telegram API Credentials** sử dụng Bot Token từ `@BotFather`.
  - Bật chế độ phân tích cú pháp HTML (`Parse Mode: HTML`) để định dạng hiển thị đẹp mắt.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) với một vài tin nhắn mẫu trên Telegram Channel của sếp.
- Kiểm tra kết quả trả về ở dạng Text hoặc Hình ảnh (`/tmp/` thư mục lưu trữ tạm thời).
- Bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Telegram cá nhân để nhận log báo cáo mỗi khi bot hoàn thành việc tạo ảnh nặng.
- **Lưu lịch sử:** Thêm node Google Sheets để ghi lại các câu lệnh (`prompt`) mà người dùng đã tương tác với bot, giúp phân tích nhu cầu nội dung.
- **Tinh chỉnh Prompt:** Thay đổi độ `temperature` trong cấu hình TGPT (ví dụ: `0.3` cho văn bản tập trung, `0.7` cho hình ảnh sáng tạo) để phù hợp hơn với phong cách thương hiệu của sếp.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho những ai muốn tự động hóa việc sáng tạo nội dung trên Telegram Channel mà không tốn một đồng chi phí phần mềm bên thứ ba nào ngoài API. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm việc của các sếp!