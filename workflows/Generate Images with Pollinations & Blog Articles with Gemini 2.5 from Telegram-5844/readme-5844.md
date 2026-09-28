---
title: "🚀 Tạo Bot Telegram Tự Động Sáng Tạo Nội Dung: Ảnh AI (Pollinations) & Bài Viết Blog (Gemini 2.5)"
description: "Hướng dẫn cài đặt workflow n8n tích hợp Telegram Bot, Pollinations AI và Gemini AI giúp tạo ảnh nghệ thuật và bài viết blog chuyên nghiệp ngay trong chat."
slug: "tao-bot-telegram-ai-tao-anh-va-viet-blog-n8n"
tags: [n8n, automation, telegram-bot, gemini-ai, content-creation, google-sheets]
keywords: [n8n workflow, telegram bot ai, tạo ảnh pollinations, viết blog gemini, tự động hóa n8n]
---

# 🚀 Tạo Bot Telegram Tự Động Sáng Tạo Nội Dung: Ảnh AI & Bài Viết Blog với n8n

Việc sáng tạo nội dung hàng ngày cho mạng xã hội hay website thường ngốn rất nhiều thời gian của các sếp: vừa phải nghĩ ý tưởng, viết bài chuẩn SEO, vừa phải tìm hoặc tạo hình ảnh minh họa phù hợp. Làm thủ công từng bước thế này cực kỳ mệt mỏi và tốn kém nhân lực.

Giải pháp là đây! Workflow n8n siêu cấp này sẽ biến tài khoản Telegram của các sếp thành một trợ lý AI đa năng, hoạt động 24/7. Chỉ cần vài câu lệnh đơn giản, bot sẽ tự động tạo ra những bức ảnh nghệ thuật cực đẹp qua **Pollinations AI** và các bài viết blog hoàn chỉnh, chất lượng cao nhờ sức mạnh của **Google Gemini AI**. Không những thế, mọi hoạt động đều được lưu log tự động vào **Google Sheets** và lưu trữ ảnh an toàn trên **Google Drive**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình sáng tạo:** Người dùng chỉ cần chat với Bot Telegram là có ngay ảnh và bài viết trọn vẹn mà không cần rời khỏi ứng dụng.
- **Đa dạng phong cách viết:** Bot cho phép người dùng lựa chọn phong cách bài viết linh hoạt (Formal, Casual, News).
- **Lưu trữ và quản lý minh bạch:** Tự động ghi nhận log chi tiết vào Google Sheets và sao lưu ảnh chất lượng cao vào Google Drive.
- **Trải nghiệm tương tác mượt mà:** Hiển thị trạng thái "đang gõ" (typing), "đang tải ảnh" (uploading) theo thời gian thực giống hệt như đang chat với người thật.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **Tài khoản Google** để cấu hình Google Sheets OAuth2 và Google Drive OAuth2.
- **Google Gemini API Key** (thông qua LangChain) để AI viết bài.
- **Google Sheet** với các cột chuẩn bị sẵn: `Tanggal`, `Prompt`, `User ID`, `Jenis`, `Hasil`, `Style`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp (hoặc sử dụng tính năng copy/paste JSON trực tiếp vào màn hình workflow trống).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà không lỗi, các sếp cần cấu hình chính xác các điểm sau:
- **Telegram Trigger & Bot Nodes:** Kết nối node `Trigger Telegram Message` và các node gửi tin nhắn (`Send Main Menu to User`, `Send Image Result to Telegram`, v.v.) với **Telegram API Credentials** của các sếp.
- **Gemini Chat Model & Chain:** Cấu hình node `Gemini Chat Model` sử dụng **Google Gemini (PaLM) API Key**. Tùy chỉnh prompt viết bài tại node `Generate Article with Gemini`.
- **Google Sheets & Drive Nodes:** 
  - Tại các node `Log Image Prompt to Google Sheets`, `Log Blog Prompt to Google Sheets`, `Store Selected Article Style`, `Fetch Last User Prompt`, `Log Final Article to Google Sheets`: Hãy chọn đúng tài khoản Google Sheets OAuth2, trỏ đến đúng **Spreadsheet ID** và tên Sheet của các sếp.
  - Tại node `Upload Image to Google Drive`: Chọn tài khoản Google Drive OAuth2 và điền **Folder ID** nơi lưu trữ ảnh sinh ra.
- **Kiểm tra biểu thức (Expressions):** Đảm bảo các tham số `chat_id` lấy động từ context của Telegram message thay vì hardcode.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử nghiệm gửi lệnh `/start` vào bot Telegram để test luồng tương tác.
- Nếu mọi thứ chạy trơn tru, hãy gạt công tắc sang **Active** để bật bot 24/7.

---

## 📊 Cấu trúc Google Sheets (Hệ thống Logging)
Workflow sử dụng Google Sheets làm trung tâm lưu trữ dữ liệu với cấu trúc bảng gồm các cột sau:

| Tên cột | Kiểu dữ liệu | Mô tả chi tiết |
| :--- | :--- | :--- |
| `Tanggal` | `string` | Thời gian gửi yêu cầu (`new Date().toLocaleString()`) |
| `Prompt` | `string` | Câu lệnh gốc của người dùng (mô tả ảnh hoặc tiêu đề blog) |
| `User ID` | `string` | Telegram User ID của người gửi |
| `Jenis` | `string` | Loại nội dung: `"image"` hoặc `"blog"` |
| `Hasil` | `string` | Kết quả trả về: Link ảnh (với image) hoặc toàn bộ nội dung bài viết (với blog) |
| `Style` | `string` | Phong cách viết bài (chỉ áp dụng với prompt blog) |

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng phong cách viết:** Thêm các tùy chọn phong cách mới như *SEO-optimized*, *Storytelling*, hoặc *Product Review* tại node xử lý Style của bài viết.
- **Tích hợp thêm AI Models:** Thay thế hoặc bổ sung các mô hình sinh ảnh khác như Stability AI hoặc DALL-E thông qua HTTP Request node.
- **Gửi thông báo quản trị:** Kết nối thêm một nhánh phụ gửi thông báo về kênh Slack hoặc Telegram riêng của admin mỗi khi có người dùng tạo nội dung mới.
- **Tối ưu tên file trên Drive:** Chỉnh sửa cấu trúc tên file trong node Google Drive để kèm theo `Timestamp`, `User ID` giúp quản lý tệp trực quan hơn.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các nhà sáng tạo nội dung, Marketer, hay Freelancer muốn xây dựng một trợ lý AI thu nhỏ ngay trên Telegram. Hãy triển khai ngay hôm nay để tiết kiệm hàng giờ làm việc thủ công và tự động hóa toàn bộ quy trình content của các sếp!