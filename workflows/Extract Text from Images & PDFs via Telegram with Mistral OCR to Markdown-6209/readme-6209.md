---
title: "🚀 Trích xuất văn bản từ Ảnh & PDF qua Telegram với Mistral OCR và n8n"
description: "Hướng dẫn xây dựng Bot Telegram tự động nhận ảnh và file PDF, dùng Mistral OCR đọc chữ cực chuẩn và trả về file Markdown gọn gàng qua n8n."
slug: "trich-xuat-van-ban-anh-pdf-telegram-mistral-ocr"
tags: [n8n, automation, no-code, telegram, ai, ocr]
keywords: [n8n workflow, mistral ocr, telegram bot ocr, trích xuất văn bản pdf, tự động hóa n8n]
---

# 🚀 Trích xuất văn bản từ Ảnh & PDF qua Telegram với Mistral OCR

Các sếp có bao giờ cảm thấy mệt mỏi khi phải gõ lại văn bản từ hình ảnh chụp tài liệu, hóa đơn, hoặc copy chữ từ các file PDF scan lỗi font? Việc xử lý thủ công này cực kỳ tốn thời gian và dễ sai sót. 

Giải pháp ở đây là tự động hóa 100%! Workflow n8n này sẽ biến chiếc Bot Telegram của các sếp thành một "siêu máy quét" tích hợp **Mistral OCR** đa phương thức (Multimodal AI). Người dùng chỉ cần gửi ảnh (`PNG`, `JPEG`) hoặc file `PDF` vào chat, bot sẽ tự động đọc hiểu, bóc tách toàn bộ văn bản và gửi trả lại một file định dạng **Markdown (`.md`)** sạch sẽ, sẵn sàng để sử dụng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý mượt mà các file dung lượng lớn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **OCR cực đỉnh bằng AI**: Tận dụng sức mạnh của Mistral OCR để nhận diện văn bản chính xác từ cả ảnh chụp vội lẫn file PDF phức tạp.
- **Tự động hóa qua Telegram**: Không cần cài app phức tạp, tương tác trực tiếp ngay trên Telegram quen thuộc.
- **Đầu ra chuẩn Markdown**: Nhận file `.md` ngay trong khung chat, dễ dàng lưu trữ, chỉnh sửa hoặc đưa vào Notion, Obsidian.
- **Bảo mật với Whitelist**: Tùy chọn bật danh sách trắng (`Whitelist`) để giới hạn chỉ những tài khoản Telegram được cấp phép mới dùng được bot.
- **Quản lý Webhook thông minh**: Tự động cấu hình Webhook cho cả môi trường Development và Production.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
1. **n8n Instance**: Đã chạy ổn định (khuyến nghị bản Self-hosted trên VPS).
2. **Telegram Bot Token**: Tạo bot thông qua `@BotFather` trên Telegram.
3. **Mistral AI API Key**: Tài khoản và API key từ Mistral AI để gọi dịch vụ Mistral OCR.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng 3 chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste Workflow**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 32 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình chính xác các điểm sau:

- **Node `Telegram Webhook Configuration` (Set)**:
  - Dán **Bot API Token** vào trường `Bot_API_Key`.
  - Lấy URL từ node **`Incoming Request`**: Copy *Test URL* dán vào `Webhook_Dev_URL` và *Production URL* dán vào `Webhook_Prod_URL`.
  - Chỉnh cờ `Production_Mode` thành `true` nếu chạy thật trên server.

- **Node `Settings` (Set)**:
  - `Bot_Whitelist_Active`: Đặt là `true` nếu muốn giới hạn người dùng, hoặc `false` nếu cho phép toàn bộ mọi người.
  - `Allowed_Chat_IDs`: Nếu bật Whitelist, điền danh sách Telegram User ID cách nhau bởi dấu phẩy (Ví dụ: `"123456789, 987654321"`).
  - `File_Downloader_Prod_URL`: Điền URL Production của n8n (lấy từ node `Incoming Request`). *Lưu ý:* Nếu n8n chạy port khác chuẩn (như `5678`), nhớ thêm port vào URL (Ví dụ: `https://yourdomain.com:5678`).

- **Node `Mistral OCR` (HTTP Request)**:
  - Chọn hoặc tạo mới **Credentials** cho `Mistral Cloud API` bằng API Key đã chuẩn bị.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một bức ảnh hoặc file PDF chứa chữ tới Bot Telegram của các sếp để test nhanh.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để bot hoạt động 24/7.
- *Lưu ý quan trọng:* Tính năng tải file thông qua link tự trỏ (Self-request) yêu cầu workflow bắt buộc phải ở trạng thái **Active**.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho doanh nghiệp hoặc cá nhân, các sếp có thể mở rộng thêm:
- **Lưu trữ tự động**: Thêm node Google Drive hoặc Notion để tự động lưu file Markdown `.md` vừa trích xuất vào thư mục lưu trữ riêng.
- **Thông báo Slack/Telegram nhóm**: Gửi cảnh báo hoặc bản tóm tắt sang một kênh Telegram/Slack nội bộ mỗi khi có tài liệu được số hóa thành công.
- **Xử lý hậu kỳ bằng LLM**: Kết nối thêm một node AI (OpenAI/Anthropic) ngay sau OCR để tự động tóm tắt nội dung chính hoặc trích xuất thông tin quan trọng từ văn bản nhận được.

### 📌 Kết luận
Một workflow cực kỳ "đáng đồng tiền bát gạo" giúp tự động hóa toàn bộ quy trình số hóa tài liệu giấy và hình ảnh thành văn bản Markdown chỉ trong một nốt nhạc. Chúc các sếp cài đặt thành công và xây dựng được trợ lý OCR siêu việt cho riêng mình!