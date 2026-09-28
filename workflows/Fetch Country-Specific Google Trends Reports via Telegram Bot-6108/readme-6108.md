---
title: "🚀 Tự động lấy báo cáo Google Trends theo quốc gia qua Telegram Bot bằng n8n"
description: "Hướng dẫn cài đặt và sử dụng workflow n8n để tự động tra cứu, phân tích xu hướng tìm kiếm Google Trends theo mã quốc gia và gửi kết quả tức thì qua Telegram Bot."
slug: "fetch-google-trends-telegram-bot-n8n"
tags: [n8n, automation, no-code, telegram, google-trends, market-research]
keywords: [n8n workflow, google trends telegram, tự động hóa nghiên cứu thị trường, telegram bot n8n, fetch trends]
---

# 🚀 Tự động lấy báo cáo Google Trends theo quốc gia qua Telegram Bot

Các sếp có đang tốn hàng giờ mỗi ngày để truy cập Google Trends, tìm kiếm từ khóa theo từng quốc gia để làm báo cáo nghiên cứu thị trường hay sáng tạo nội dung không? Việc này vừa thủ công, nhàm chán lại cực kỳ mất thời gian khi phải lặp đi lặp lại.

Giải pháp ở đây là gì? Tự động hóa 100% quy trình này với workflow n8n! Chỉ cần gửi một mã quốc gia (ví dụ: `US`, `VN`, `EG`, `SA`) tới Telegram Bot của các sếp, hệ thống sẽ tự động fetch dữ liệu Google Trends mới nhất, xử lý và gửi lại báo cáo gọn gàng ngay trong khung chat Telegram. Không cần viết code phức tạp, không mất phí duy trì đắt đỏ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ chớp nhoáng:** Nhận báo cáo Google Trends của bất kỳ quốc gia nào chỉ trong vài giây ngay trên Telegram.
- **Tiết kiệm nhân lực:** Không cần nhân sự ngồi canh Google Trends thủ công mỗi ngày.
- **Linh hoạt theo nhu cầu:** Tra cứu mọi lúc mọi nơi, chỉ bằng cách gửi mã quốc gia (ví dụ: `US`, `VN`).
- **Hoạt động 24/7:** Bot tự động túc trực và phản hồi yêu cầu bất kể ngày đêm trên nền tảng n8n tự động hóa.
:::

### 📦 Các loại nodes sử dụng trong Workflow
Workflow này được xây dựng từ 5 nodes tối ưu:
1. **Telegram Trigger:** Lắng nghe tin nhắn mã quốc gia từ người dùng gửi tới Bot.
2. **HTTP Request:** Gọi API ngầm để lấy nguồn dữ liệu RSS/XML Google Trends theo mã quốc gia.
3. **XML Node:** Chuyển đổi dữ liệu XML thô từ Google thành định dạng có cấu trúc.
4. **Code Node:** Xử lý, lọc và chuẩn hóa dữ liệu thành báo cáo hoàn chỉnh.
5. **Send a text message (Telegram):** Gửi kết quả báo cáo xu hướng trực tiếp về Telegram cho người dùng.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted trên VPS).
- Một **Telegram Bot Token** (tạo nhanh thông qua [@BotFather](https://t.me/BotFather)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó vào n8n Editor, chọn **New** -> **Import from Clipboard** và dán vào là xong!

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần cấu hình chính xác các điểm sau:
- **Telegram Trigger & Send a text message:** Tạo mới hoặc chọn sẵn **Telegram API Credentials**. Các sếp cần nhập **Access Token** lấy từ `@BotFather` vào đây để n8n có quyền đọc tin nhắn và gửi phản hồi.
- **HTTP Request:** Node này sẽ gọi đường dẫn RSS Trends của Google (thường có dạng `https://trends.google.com/trends/trendingsearches/daily/rss?geo=QUỐC_GIA`). Hãy đảm bảo tham số mã quốc gia được truyền động từ tin nhắn của **Telegram Trigger** (ví dụ: `{{ $json.message.text }}`).
- **Code Node:** Kiểm tra lại đoạn script JavaScript bên trong node này để đảm bảo nó bóc tách đúng tiêu đề (titles) và mô tả (descriptions) từ XML trả về của Google Trends.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và thử gửi một tin nhắn chứa mã quốc gia (ví dụ: `US` hoặc `VN`) tới Telegram Bot của các sếp để test.
- Nếu nhận được tin nhắn phản hồi chứa danh sách xu hướng, hãy gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Kết nối thêm node **Google Sheets** hoặc **Notion** sau bước Code để lưu lại lịch sử các xu hướng tìm kiếm phục vụ phân tích dài hạn.
- **Đa kênh thông báo:** Ngoài Telegram, các sếp có thể clone nhánh để đẩy báo cáo này về **Slack**, **Discord** hoặc email cá nhân.
- **Lọc từ khóa thông minh:** Tích hợp thêm một AI node (như OpenAI) vào Code Node để tự động tóm tắt hoặc dịch xu hướng sang tiếng Việt trước khi gửi về Telegram.

### 📌 Kết luận
Việc nghiên cứu thị trường và bắt trend chưa bao giờ dễ dàng đến thế khi đã có trợ lý ảo n8n và Telegram Bot. Hãy cài đặt ngay workflow này để tối ưu hóa công việc marketing và sáng tạo nội dung của các sếp ngay hôm nay!