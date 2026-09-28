---
title: "🚀 Trích xuất văn bản từ hình ảnh tự động qua Telegram Bot với Gemini 2.0 Flash OCR"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Telegram Bot và Gemini 2.0 Flash để trích xuất văn bản (OCR) từ hình ảnh cực kỳ nhanh chóng và chính xác."
slug: "trich-xuat-van-ban-tu-hinh-anh-telegram-gemini-ocr"
tags: [n8n, automation, no-code, telegram, ai, ocr, gemini]
keywords: [n8n workflow, telegram bot ocr, gemini 2.0 flash, trích xuất văn bản từ ảnh, tự động hóa n8n]
---

# 🚀 Trích xuất văn bản từ hình ảnh tự động qua Telegram Bot với Gemini 2.0 Flash OCR

Các sếp có bao giờ cảm thấy mệt mỏi khi phải gõ lại văn bản từ các bức ảnh chụp tài liệu, hóa đơn hay màn hình máy tính? Việc chuyển đổi thủ công này không chỉ tốn thời gian mà còn dễ xảy ra sai sót. 

Giải pháp là đây! Với workflow n8n kết hợp giữa **Telegram Bot** và **Gemini 2.0 Flash AI**, các sếp chỉ cần gửi một bức ảnh vào chat Telegram, hệ thống sẽ tự động đọc, xử lý và trả về toàn bộ văn bản có trong ảnh ngay lập tức. Hoàn toàn tự động, nhanh chóng và chính xác 100% mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Gửi ảnh qua Telegram, nhận lại text ngay lập tức mà không cần thao tác phức tạp.
- **Sức mạnh AI đỉnh cao**: Sử dụng mô hình đa phương thức Gemini 2.0 Flash giúp nhận diện văn bản cực kỳ chính xác, kể cả chữ viết tay hoặc ảnh chụp mờ.
- **Tiết kiệm thời gian**: Giải phóng hàng giờ gõ văn bản thủ công mỗi tuần cho nhân sự.
- **Hoạt động 24/7**: Bot luôn sẵn sàng phục vụ các sếp bất cứ lúc nào, trên mọi thiết bị có Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua [@BotFather](https://t.me/BotFather)).
- **Google AI Studio API Key** (Lấy miễn phí tại [Google AI Studio](https://aistudio.google.com/)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng 6 nodes chính, các sếp cần cấu hình kỹ các điểm sau để bot chạy mượt mà:

- **Telegram Trigger** và **get file / Telegram**: 
  - Cần tạo và chọn credentials loại **Telegram API** bằng cách nhập Bot Token lấy từ `@BotFather`.
  - Node `Telegram Trigger` sẽ lắng nghe sự kiện khi các sếp gửi ảnh vào chat với bot.
  - Node `get file` thực hiện nhiệm vụ tải file hình ảnh mà các sếp vừa gửi lên hệ thống n8n.

- **Clean Input Data (Set)** & **Extract from File**:
  - Xử lý và chuẩn hóa định dạng dữ liệu nhị phân (binary data) của hình ảnh trước khi chuyển sang bước gọi AI.

- **Gemini OCR (HTTP Request)**:
  - **URL cấu hình**: Sử dụng endpoint của Gemini API với cấu trúc:
    `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent`
  - **Authentication**: Chọn kiểu *Generic Credential Type* -> *Query Auth*. Nhập API Key lấy từ Google AI Studio vào phần thông tin xác thực.
  - **Body Content Type**: Chọn `JSON` và cấu trúc body để truyền dữ liệu hình ảnh dưới dạng `inlineData` kèm theo câu lệnh (prompt) yêu cầu trích xuất văn bản (`Extract text`).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** và gửi thử một bức ảnh chứa chữ vào Telegram Bot của các sếp để kiểm tra kết quả trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ kết quả**: Kết hợp thêm node **Google Sheets** hoặc **Notion** để tự động lưu lại các đoạn văn bản được trích xuất thành một cơ sở dữ liệu gọn gàng.
- **Thông báo đa kênh**: Tích hợp thêm Slack hoặc gửi email tự động chứa nội dung văn bản vừa OCR nếu cần chia sẻ cho đồng nghiệp.
- **Tùy chỉnh Prompt**: Thay đổi câu lệnh "Extract text" trong node Gemini OCR thành các yêu cầu cụ thể hơn như *"Tóm tắt nội dung ảnh này"* hoặc *"Trích xuất hóa đơn thành bảng JSON"*.

### 📌 Kết luận
Workflow trích xuất văn bản từ hình ảnh qua Telegram Bot và Gemini 2.0 Flash là một công cụ cực kỳ mạnh mẽ, biến chiếc điện thoại của các sếp thành một máy scan thông minh thu nhỏ. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình làm việc của mình nhé!