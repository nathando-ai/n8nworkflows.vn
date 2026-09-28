---
title: "🚀 Tự động tạo ảnh bằng OpenAI DALL-E qua Telegram và lưu log vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng chatbot Telegram tự động nhận câu lệnh mô tả, tạo hình ảnh chất lượng cao bằng OpenAI DALL-E và tự động lưu thông tin vào Google Sheets."
slug: "tao-anh-openai-dalle-qua-telegram-google-sheets-n8n"
tags: [n8n, automation, no-code, openai, dalle, telegram, google-sheets]
keywords: [n8n workflow, telegram bot ai, tạo ảnh dalle, google sheets logger, tự động hóa n8n]
---

# 🚀 Tạo ảnh bằng OpenAI DALL-E qua Telegram và lưu log vào Google Sheets

Các sếp có bao giờ cảm thấy tốn thời gian khi mỗi lần cần tạo ý tưởng thiết kế, hình ảnh minh họa lại phải truy cập vào trang web của OpenAI, gõ prompt, tải về rồi thủ công lưu lại lịch sử không? Việc này vừa ngắt quãng mạch sáng tạo vừa khó quản lý dữ liệu.

Giải pháp ở đây là gì? Hãy để workflow n8n này thay các sếp làm tất cả! Chỉ với một tin nhắn gửi qua **Telegram**, AI sẽ tự động vẽ tranh bằng **OpenAI DALL-E**, gửi trả ảnh ngay lập tức cho các sếp và đồng thời **lưu lại log (prompt + link ảnh)** một cách ngăn nắp vào **Google Sheets**. Hoàn toàn tự động, 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo ảnh mọi lúc mọi nơi:** Biến chiếc điện thoại thành xưởng vẽ cá nhân thông qua ứng dụng Telegram quen thuộc.
- **Phản hồi tức thì:** Nhận hình ảnh sắc nét từ DALL-E chỉ trong vài giây sau khi gửi tin nhắn.
- **Quản lý dữ liệu chuyên nghiệp:** Tự động lưu trữ toàn bộ lịch sử prompt và liên kết hình ảnh vào Google Sheets để tra cứu, kiểm tra bất cứ lúc nào.
- **Vận hành không gián đoạn:** Bot hoạt động 24/7, tự động xử lý hàng loạt yêu cầu mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot Token:** Tạo một bot mới thông qua `@BotFather` trên Telegram.
- **OpenAI API Key:** Tài khoản OpenAI có quyền gọi API DALL-E.
- **Google Account:** Một Google Sheet được thiết kế sẵn các cột để lưu dữ liệu (Prompt, Link ảnh, Thời gian...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này dán trực tiếp vào n8n Editor, hoặc import file JSON theo hướng dẫn của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính, các sếp cần cấu hình chuẩn xác các thông số sau:

- **Telegram Trigger:** 
  - Tạo Credentials kết nối với Telegram Bot thông qua Token nhận được từ `@BotFather`.
  - Node này sẽ lắng nghe mọi tin nhắn văn bản gửi tới bot của các sếp.
- **OpenAI (Node tạo ảnh):**
  - Chọn Credentials loại `openAiApi` và điền API Key của các sếp.
  - Tại tham số `Resource`, chọn `Image`.
  - Tại ô `Prompt`, đảm bảo biểu thức đang trỏ chính xác đến nội dung tin nhắn người dùng: `={{ $json.message.text }}`.
- **Google Sheets (Node lưu log):**
  - Kết nối tài khoản Google qua OAuth2.
  - Chọn file Google Sheet và Sheet Name nơi các sếp muốn lưu dữ liệu.
  - Cấu hình thao tác `Operation` là `Append` để thêm dòng mới chứa prompt và link ảnh trả về từ OpenAI.
- **Telegram (Node trả kết quả):**
  - Chọn Credentials Telegram tương tự node Trigger.
  - Cấu hình `Operation` thành `Send Photo` để gửi hình ảnh trực tiếp ngược lại khung chat Telegram cho người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tin nhắn mô tả hình ảnh bất kỳ tới Bot Telegram của các sếp để test xem ảnh có được trả về và ghi vào Google Sheets thành công không.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình này hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Thông báo qua Slack/Telegram Group:** Gửi thông báo kèm hình ảnh vừa tạo vào nhóm chung của công ty mỗi khi có thành viên tạo ảnh mới.
- **Kiểm duyệt nội dung prompt:** Thêm một node AI phụ (như GPT-4o-mini) để dịch, tối ưu hóa hoặc kiểm duyệt nội dung prompt của người dùng trước khi gửi sang DALL-E.
- **Tự động lưu file lên Google Drive:** Thay vì chỉ lưu link, có thể tải trực tiếp file ảnh về Google Drive để lưu trữ lâu dài.

### 📌 Kết luận
Chỉ với vài bước cấu hình đơn giản trên n8n, các sếp đã sở hữu ngay một trợ lý AI tạo ảnh chuyên nghiệp tích hợp trực tiếp vào Telegram. Không còn thao tác thủ công, tiết kiệm thời gian và tối ưu hiệu suất công việc. Áp dụng ngay thôi các sếp ơi!