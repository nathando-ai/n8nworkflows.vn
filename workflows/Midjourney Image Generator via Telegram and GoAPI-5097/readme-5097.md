---
title: "🚀 Tự động tạo ảnh AI Midjourney qua Telegram và GoAPI bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Telegram Bot với GoAPI để tạo ảnh nghệ thuật Midjourney, tự động upscale và gửi thông báo trực tiếp cực nhanh chóng."
slug: "tao-anh-midjourney-qua-telegram-va-goapi-bang-n8n"
tags: [n8n, automation, ai, midjourney, telegram, goapi]
keywords: [n8n workflow, tạo ảnh midjourney, telegram bot ai, goapi midjourney, tự động hóa n8n]
---

# 🚀 Tự động tạo ảnh AI Midjourney qua Telegram và GoAPI bằng n8n

Việc truy cập Midjourney thông thường đòi hỏi các sếp phải sử dụng Discord, đôi khi gây bất tiện và khó tích hợp vào các quy trình làm việc cá nhân hoặc kinh doanh. Thay vào đó, tại sao không mang thẳng sức mạnh của Midjourney vào một khung chat Telegram quen thuộc? 

Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n hoàn chỉnh, kết hợp **Telegram Bot**, **GoAPI (Midjourney API)** và **Discord** để tự động nhận prompt, tạo ảnh, chờ xử lý, gửi tùy chọn upscale (phóng to ảnh) và trả kết quả ngay trong Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo ảnh mọi lúc mọi nơi:** Chỉ cần gửi tin nhắn chứa prompt vào Telegram Bot là có ngay ảnh AI chất lượng cao từ Midjourney.
- **Tương tác thông minh:** Workflow tự động gửi lưới 4 ảnh, cho phép người dùng chọn số thứ tự (index) để upscale bức ảnh ưng ý nhất.
- **Tự động hóa hoàn toàn:** Xử lý bất đồng bộ thông qua các node `Wait`, `IF` và `HTTP Request` mà không cần can thiệp thủ công.
- **Lưu trữ nhật ký linh hoạt:** Hỗ trợ ghi log hoạt động lên kênh Discord cá nhân hoặc nhóm để dễ dàng quản lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Telegram Bot Token:** Tạo qua BotFather trên Telegram.
- **GoAPI Account:** Đăng ký tài khoản tại [GoAPI](https://goapi.ai/) và lấy API Key để gọi Midjourney API.
- **Discord Bot (Tùy chọn):** Nếu các sếp muốn dùng node ghi log qua Discord.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n (hoặc copy toàn bộ JSON), sau đó dán trực tiếp vào n8n Editor của các sếp bằng phím tắt `Ctrl + V` (hoặc `Cmd + V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các credentials và thông số sau:

- **Telegram Trigger**, **Notify Generation**, **Notify Upscaling**, **Main Log**, **Get Index to Upscale**: 
  - Tạo và kết nối **Telegram API Credentials** sử dụng Bot Token đã chuẩn bị.
- **Generate Image**, **Get Generation Task**, **Upscale**, **Get Upscale Task** (Nodes `httpRequest`):
  - Cấu hình **HTTP Header Auth** bằng cách thêm API Key lấy từ trang quản trị GoAPI của các sếp.
- **Discord - Generation Log** (Tùy chọn):
  - Nếu không muốn nhận log qua Discord, các sếp có thể **xóa** node này hoặc kết nối nó với một Discord Bot hợp lệ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử nhắn một prompt bất kỳ tới Telegram Bot để kiểm tra luồng chạy mẫu.
- Sau khi kiểm tra thành công, gạt công tắc sang **Active** để đưa bot vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets/Airtable:** Lưu lại lịch sử các câu lệnh (prompt) và link ảnh đã tạo để làm thư viện nội dung cho team Marketing.
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi qua Telegram cá nhân, các sếp có thể chuyển tiếp kết quả ảnh vào nhóm chat công việc hoặc kênh Slack.
- **Xử lý lỗi (Error Trigger):** Thêm một Error Workflow để nhận thông báo ngay lập tức nếu GoAPI hết hạn mức (credits) hoặc gặp sự cố kết nối.

### 📌 Kết luận
Với workflow n8n tích hợp Midjourney qua GoAPI và Telegram này, các sếp đã sở hữu một "xưởng vẽ AI" thu nhỏ ngay trong tầm tay mà không cần mở giao diện Discord phức tạp. Hãy triển khai ngay và trải nghiệm sự tiện lợi của tự động hóa!