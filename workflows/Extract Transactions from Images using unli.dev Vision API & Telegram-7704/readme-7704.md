---
title: "🚀 Trích xuất thông tin giao dịch từ ảnh chụp hóa đơn qua Telegram và unli.dev Vision API tự động"
description: "Hướng dẫn tự động hóa quy trình đọc hóa đơn, biên lai chuyển khoản từ ảnh gửi qua Telegram bằng unli.dev Vision API kết hợp n8n."
slug: "trich-xuat-giao-dich-tu-anh-telegram-vision-api-n8n"
tags: [n8n, automation, no-code, telegram, invoice-processing, multimodal-ai]
keywords: [n8n workflow, trích xuất hóa đơn, unli.dev vision api, telegram bot tự động, xử lý ảnh n8n]
---

# 🚀 Tự động hóa trích xuất hóa đơn và giao dịch từ Telegram bằng Vision API

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công nhập liệu từng con số, tên cửa hàng, mã giao dịch từ hàng chục tấm ảnh chụp biên lai, hóa đơn gửi tới từ nhân viên hoặc khách hàng? Việc này không chỉ tốn thời gian mà còn cực kỳ dễ xảy ra sai sót. 

Giải pháp cho các sếp đây: một workflow n8n hoàn toàn tự động, tích hợp **Telegram Bot** và **unli.dev Vision API**. Chỉ cần gửi một tấm ảnh chụp hóa đơn vào chat bot, hệ thống sẽ tự động "đọc hiểu" bức ảnh, trích xuất toàn bộ thông tin giao dịch chính xác và gửi kết quả về ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nhập liệu:** Không còn cảnh căng mắt đọc từng con số trên ảnh chuyển khoản hay hóa đơn giấy.
- **Xử lý đa phương thức (Multimodal AI):** Nhận diện cực tốt các dạng ảnh chụp hóa đơn mờ, góc nghiêng hoặc biên lai chuyển khoản ngân hàng khác nhau.
- **Phản hồi tức thì:** Gửi ảnh lên Telegram là có kết quả trả về ngay trong vòng vài giây.
- **Hoạt động 24/7:** Bot tự động túc trực nhận ảnh và xử lý mọi lúc mọi nơi mà không cần nhân sự can thiệp.
:::

### 🔑 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram để làm cổng nhận/gửi ảnh.
- **unli.dev Vision API Key:** Tài khoản và khóa API để gọi dịch vụ AI đọc ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON thông qua menu tuỳ chọn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Telegram Trigger:** 
  - Chọn hoặc tạo mới `telegramApi` credentials bằng Bot Token của các sếp.
  - Node này sẽ lắng nghe sự kiện khi có tin nhắn dạng hình ảnh gửi tới Bot.
- **📥 Download Image:**
  - Sử dụng chung `telegramApi` credentials.
  - Cấu hình lấy file ID từ sự kiện kích hoạt của Telegram Trigger để tải tệp hình ảnh về n8n.
- **Convert to Base:**
  - Node `code` (JavaScript/Python) dùng để chuyển đổi định dạng nhị phân của ảnh sang chuỗi Base64 chuẩn bị gửi cho AI.
- **Set Request:**
  - Node `set` dùng để định hình cấu trúc payload gửi đi, bao gồm prompt hướng dẫn AI trích xuất dữ liệu gì (ví dụ: Số tiền, Ngày giao dịch, Tên đơn vị, Nội dung...).
- **Call Vision API:**
  - Cấu hình node `httpRequest` kết nối tới unli.dev Vision API.
  - Thêm `httpHeaderAuth` credentials để xác thực API Key.
  - Trỏ endpoint đến API Vision và truyền payload Base64 hình ảnh vừa xử lý.
- **📤 Send Response:**
  - Sử dụng `telegramApi` credentials để gửi kết quả trích xuất dạng văn bản sạch sẽ, dễ đọc ngược lại cho người dùng Telegram.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tấm ảnh hóa đơn thử nghiệm vào Bot Telegram của các sếp để kiểm tra kết quả.
- Nếu mọi thứ trả về chính xác, hãy gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu vào Google Sheets / Airtable:** Thay vì chỉ gửi tin nhắn trả về Telegram, các sếp có thể nối thêm node Google Sheets để tự động lưu toàn bộ dữ liệu giao dịch thành một cuốn sổ thu chi chuyên nghiệp.
- **Bắn thông báo quản lý:** Thêm nhánh gửi tin nhắn cảnh báo hoặc tổng kết chi phí vào một kênh Telegram riêng của phòng kế toán.
- **Xử lý ngoại lệ:** Thêm điều kiện (If node) để kiểm tra nếu ảnh gửi lên không phải hóa đơn, bot sẽ phản hồi nhắc nhở người dùng gửi lại ảnh khác.

### 📌 Kết luận
Một workflow gọn gàng nhưng mang lại sức mạnh tự động hóa cực lớn cho các công việc liên quan đến tài chính, kế toán và xử lý chứng từ. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ của các sếp nhé!