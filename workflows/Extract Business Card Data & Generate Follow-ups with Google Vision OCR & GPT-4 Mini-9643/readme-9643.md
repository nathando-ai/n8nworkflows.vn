---
title: "🚀 Tự động hóa danh thiếp thông minh: Đọc OCR, phân tích bằng GPT-4 Mini và lưu Google Sheets"
description: "Hướng dẫn chi tiết workflow n8n giúp chụp ảnh danh thiếp gửi Telegram, AI bóc tách thông tin, soạn email chăm sóc tự động và lưu trữ chuyên nghiệp."
slug: "tu-dong-hoa-danh-thiep-google-vision-gpt4-telegram"
tags: [n8n, automation, ai-agent, openai, google-sheets, telegram]
keywords: [n8n workflow, scan danh thiếp tự động, gpt-4 mini, google vision ocr, telegram bot n8n]
---

# 🚀 Tự động hóa danh thiếp thông minh với Google Vision OCR & GPT-4 Mini

Các sếp đi sự kiện (networking), hội thảo về cầm hàng đống danh thiếp (name card) rồi tối về còng lưng gõ lại từng cái vào Excel, soạn email chào hỏi từng người thủ công? Quá mất thời gian và dễ bỏ lỡ cơ hội vàng chốt đơn!

Với workflow n8n cực đỉnh được chia sẻ bởi **Aditya Malur**, các sếp chỉ cần **chụp ảnh danh thiếp gửi qua Telegram**, phần việc còn lại để hệ thống lo từ A-Z: từ đọc chữ, bóc tách thông tin, viết email chăm sóc cá nhân hóa cho đến lưu thẳng vào Google Sheets. Tất cả tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải gõ tay thông tin từ danh thiếp vào danh sách khách hàng.
- **Phản ứng siêu tốc:** Gặp đối tác xong, vừa bước ra khỏi cửa là đã có sẵn email follow-up chuyên nghiệp được AI soạn sẵn để gửi đi.
- **Lưu trữ gọn gàng:** Mọi dữ liệu (Tên, Công ty, Email, SĐT, Ý tưởng hợp tác) được đồng bộ hóa hoàn hảo vào Google Sheets.
- **Hoạt động 24/7:** Bot Telegram sẵn sàng nhận ảnh bất cứ lúc nào, ngay cả trên điện thoại khi đang di chuyển.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **Google Vision API Key** (để quét chữ trên ảnh danh thiếp).
- **OpenAI API Key** (cho AI Agent sử dụng mô hình GPT-4 Mini).
- **Google Sheets** (tạo sẵn một trang tính để lưu dữ liệu).
- **Tài khoản Gmail** (để gửi bản nháp email follow-up về cho các sếp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow và paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây để workflow hoạt động mượt mà:

- **Telegram Trigger:** 
  - Kết nối tài khoản Telegram Bot thông qua Token của BotFather.
  - Cài đặt `Update Type`: `message` và bật `Download` thành `✅` để hệ thống tải được tệp hình ảnh.
  - Gắn Webhook URL mà n8n cung cấp vào Telegram bot.
- **Convert Image to Base64 & Extract Raw Text (Code Nodes):** 
  - Không cần cấu hình gì thêm, các đoạn code đã được viết sẵn để chuyển đổi ảnh sang định dạng Base64 và trích xuất chữ thô.
- **HTTP Request (Google Vision OCR):** 
  - Điền URL kèm API Key của Google Vision: `https://vision.googleapis.com/v1/images:annotate?key=YOUR_API_KEY`.
  - Phương thức: `POST`.
- **AI Agent & OpenAI Chat Model:** 
  - Kết nối OpenAI API Credentials.
  - Chọn model: `gpt-4.1-mini`.
  - Sử dụng prompt đã được chuẩn hóa sẵn trong workflow để AI tự động trích xuất cấu trúc (Tên, Công ty, Email, SĐT...) và soạn thảo nội dung email chăm sóc.
- **Clean AI Output (Code Node):** 
  - Node này tự động làm sạch định dạng JSON trả về từ AI, đảm bảo dữ liệu chuẩn xác trước khi lưu trữ.
- **Check for Email Found (If Node):** 
  - Kiểm tra xem AI có tìm thấy ít nhất một địa chỉ email hợp lệ hay không (`{{$json.emails[0]}}` là `not empty`).
- **Append Row in Sheet (Google Sheets):** 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Điền `Sheet ID` và chọn tên trang tính (`Sheet Name`), sau đó map các cột tương ứng với dữ liệu từ AI.
- **Send a Message (Gmail):** 
  - Kết nối tài khoản Gmail cá nhân/doanh nghiệp để hệ thống gửi bản tóm tắt nội dung email chào hỏi do AI soạn thảo về hộp thư của chính các sếp.

#### 3. Kích hoạt ⚡️
- Gửi thử một tấm ảnh danh thiếp vào bot Telegram của các sếp để Test Run.
- Kiểm tra xem dữ liệu đã đổ về Google Sheets và Gmail chưa.
- Nếu mọi thứ chạy mượt, hãy bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Zalo/Slack:** Thay vì chỉ gửi email về Gmail cá nhân, các sếp có thể cấu hình thêm node gửi thông báo qua Slack hoặc nhóm Telegram nội bộ khi có một khách hàng tiềm năng mới quét từ danh thiếp.
- **Tự động gửi Email trực tiếp:** Nếu tin tưởng AI, các sếp có thể cấu hình node Gmail gửi thẳng email chăm sóc đến khách hàng thay vì chỉ gửi bản nháp về cho mình.
- **Lưu trữ hình ảnh:** Kết hợp lưu ảnh danh thiếp gốc lên Google Drive để dễ dàng tra cứu lại khi cần thiết.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" cực kỳ hữu ích cho đội ngũ sales, founders và những ai thường xuyên tham gia các sự kiện networking. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình chăm sóc khách hàng và không bỏ lỡ bất kỳ mối quan hệ kinh doanh giá trị nào!