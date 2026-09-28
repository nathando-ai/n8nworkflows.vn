---
title: "🚀 Trích xuất văn bản từ hình ảnh tự động với Telegram Bot và OCR trong n8n"
description: "Hướng dẫn xây dựng trợ lý AI trên Telegram giúp tự động đọc ảnh, trích xuất text và xử lý thông tin bằng Google Gemini AI một cách nhanh chóng."
slug: "trich-xuat-van-ban-tu-hinh-anh-telegram-bot-ocr-n8n"
tags: [n8n, automation, telegram, ocr, ai-agent, google-gemini, multimodal]
keywords: [n8n workflow, trích xuất text từ ảnh, telegram bot ocr, google gemini n8n, ai agent n8n]
---

# 🚀 Trích xuất văn bản từ hình ảnh tự động với Telegram Bot và OCR trong n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải ngồi gõ lại văn bản từ hình ảnh, chụp màn hình tài liệu hay hóa đơn gửi qua Telegram chưa? Việc này không chỉ tốn thời gian mà còn dễ gây sai sót trong quá trình nhập liệu thủ công. 

Thay vì tốn nhân lực cho những việc lặp đi lặp lại đó, workflow n8n tuyệt vời này sẽ giúp các sếp xây dựng ngay một **Telegram Bot thông minh**. Bot sẽ tự động nhận ảnh các sếp gửi lên, tiến hành OCR trích xuất văn bản, kết hợp cùng sức mạnh của AI Agent và Google Gemini để xử lý, tóm tắt hoặc trả lời theo đúng yêu cầu một cách hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần gửi ảnh vào chat với Bot Telegram, kết quả sẽ trả về ngay lập tức mà không cần thao tác phức tạp.
- **Xử lý đa phương thức (Multimodal):** Kết hợp OCR và Google Gemini AI giúp hiểu sâu nội dung văn bản trong ảnh thay vì chỉ đọc chữ thô.
- **Tiết kiệm thời gian tối đa:** Giảm thiểu 90% thời gian nhập liệu thủ công từ tài liệu hình ảnh, hóa đơn hay, bảng biểu.
- **Hoạt động 24/7:** Bot túc trực liên tục trên Telegram, sẵn sàng hỗ trợ bất cứ lúc nào các sếp cần.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua [@BotFather](https://t.me/BotFather)).
- **Google Gemini API Key** (Lấy từ Google AI Studio để kết nối với Google Gemini Chat Model).
- **OCR API Key** (Tùy chọn, tùy thuộc vào dịch vụ OCR được cấu hình trong node `OCR`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow do tác giả Rudi Afandi chia sẻ (hoặc từ kho lưu trữ n8n với ID `5413`) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Telegram Trigger**: Kết nối với `telegramApi` credentials chứa Token của Bot Telegram mà các sếp đã tạo. Node này chịu trách nhiệm lắng nghe sự kiện khi có ảnh gửi vào bot.
- **get file**: Cấu hình lấy file từ Telegram dựa trên file_id nhận được từ trigger. Cần chọn đúng `telegramApi` credentials.
- **Convert to base64**: Sử dụng node `extractFromFile` với thao tác `binaryToPropery` để chuyển đổi định dạng tệp hình ảnh sang base64 phục vụ cho các bước xử lý tiếp theo.
- **OCR**: Node `httpRequest` thực hiện gọi API OCR để bóc tách văn bản thô từ hình ảnh. Các sếp nhớ kiểm tra lại endpoint URL và header xác thực (API Key) của dịch vụ OCR đang sử dụng.
- **Clean Input Data**: Node `set` dùng để làm sạch, định dạng lại dữ liệu văn bản sau khi OCR trước khi truyền vào AI.
- **Google Gemini Chat Model & AI Agent**: Cấu hình credentials `googlePalmApi` cho Google Gemini. Tại node `AI Agent`, các sếp có thể viết system prompt để hướng dẫn AI cách xử lý văn bản trích xuất (ví dụ: tóm tắt, dịch thuật, hay trả lời câu hỏi dựa trên nội dung ảnh).
- **Telegram**: Node cuối cùng dùng để gửi kết quả xử lý từ AI ngược trở lại đoạn chat Telegram cho người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tấm ảnh chứa chữ (hóa đơn, trang sách, tài liệu) vào Bot Telegram của các sếp để test thực tế.
- Kiểm tra kết quả trả về, nếu mọi thứ hoạt động trơn tru thì bật nút **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Kết hợp thêm node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử các nội dung đã trích xuất từ ảnh nhằm quản lý dễ dàng hơn.
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể tích hợp thêm **Slack** hoặc **Discord** để gửi kết quả trích xuất vào nhóm làm việc chung của công ty.
- **Phân loại tự động:** Tận dụng AI Agent để phân loại xem bức ảnh là hóa đơn, hợp đồng hay tài liệu cá nhân, từ đó điều hướng lưu trữ vào các thư mục Google Drive tương ứng.

### 📌 Kết luận
Workflow "Extract Text from Images with Telegram Bot & OCR" là một giải pháp cực kỳ thiết thực, giúp biến Telegram cá nhân thành một trợ lý AI thông minh chuyên xử lý hình ảnh và tài liệu. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp nhé!