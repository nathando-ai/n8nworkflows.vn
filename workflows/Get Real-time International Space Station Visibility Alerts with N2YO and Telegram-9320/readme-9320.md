---
title: "🚀 Nhận cảnh báo thời gian thực về Trạm Vũ trụ Quốc tế ISS qua Telegram với n8n"
description: "Hướng dẫn tự động hóa quy trình theo dõi Trạm Vũ trụ Quốc tế (ISS) bằng n8n, N2YO API và Telegram để nhận thông báo visibility trực tiếp ngay khi ISS bay qua."
slug: "nhận-cảnh-báo-iss-qua-telegram-n8n"
tags: [n8n, automation, telegram, api, space, iot]
keywords: [n8n workflow, tự động hóa telegram, theo dõi iss, n2yo api, n8n viet nam]
---

# 🚀 Tự động nhận cảnh báo Trạm Vũ trụ Quốc tế (ISS) qua Telegram

Các sếp có bao giờ tò mò muốn ngước lên bầu trời và vẫy tay chào các phi hành gia trên Trạm Vũ trụ Quốc tế (ISS) khi họ bay ngang qua đầu mình không? Việc tra cứu lịch thủ công trên các trang web thiên văn vừa mất thời gian lại dễ bỏ lỡ khoảnh khắc vàng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với một workflow n8n tự động hóa 100% không cần code. Workflow này sẽ tự động kết nối với API của N2YO để lấy dữ liệu thời gian thực và bắn tin nhắn cảnh báo ngay lập tức vào Telegram của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Hệ thống tự động kiểm tra lịch bay của ISS theo định kỳ mà không cần can thiệp thủ công.
- **Thông báo tức thì**: Nhận alert qua Telegram ngay khi ISS sắp xuất hiện trên bầu trời khu vực của các sếp.
- **Dữ liệu chính xác**: Sử dụng nguồn dữ liệu thiên văn chuẩn xác từ N2YO API kết hợp xử lý code linh hoạt.
- **Vận hành 24/7**: Chạy ổn định trên nền tảng n8n self-hosted hoặc cloud.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản và API Key miễn phí từ [N2YO API](https://www.n2yo.com/api/) (để lấy dữ liệu vệ tinh/ISS).
- Một Telegram Bot (tạo thông qua `@BotFather`) và Chat ID của các sếp để nhận tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ n8n.io (hoặc copy toàn bộ JSON), sau đó dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Schedule Trigger**: Thiết lập khoảng thời gian chạy (ví dụ: chạy mỗi vài giờ hoặc mỗi ngày một lần) để kiểm tra lịch bay của ISS.
- **HTTP Request**: 
  - Cấu hình gọi tới API của N2YO (lấy thông tin visual passes của ISS).
  - Điền các tham số tọa độ vĩ độ (Latitude), kinh độ (Longitude), độ cao (Altitude) của khu vực các sếp muốn theo dõi và **N2YO API Key** của các sếp vào header/query parameters.
- **Readable (Node Code)**: Xử lý và định dạng lại dữ liệu thô (JSON) trả về từ API thành các câu chữ tiếng Anh/Việt dễ đọc, lọc ra các thông tin quan trọng như thời điểm bắt đầu, thời gian thấy rõ (visible duration).
- **If**: Kiểm tra xem có lần bay qua nào thỏa mãn điều kiện (ví dụ: thời gian thấy được > 0 hoặc độ sáng đạt yêu cầu) hay không.
- **Send a text message (Telegram)**: 
  - Tạo và kết nối **Telegram Bot Credentials** của các sếp.
  - Điền **Chat ID** của cá nhân hoặc nhóm chat nhận thông báo.
  - Kéo dữ liệu từ node `Readable` vào phần nội dung tin nhắn.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu thực tế từ API.
- Kiểm tra xem Telegram đã nhận được tin nhắn cảnh báo chưa.
- Nếu mọi thứ xanh mượt, hãy bật **Active workflow** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Ngoài Telegram, các sếp có thể gắn thêm node **Slack**, **Discord** hoặc gửi email tự động qua **Gmail** để không bao giờ bỏ lỡ.
- **Lưu lịch sử**: Thêm node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử các lần ISS bay qua phục vụ việc quan sát hoặc nghiên cứu cá nhân.
- **Tích hợp AI**: Dùng thêm các node LLM (OpenAI/Anthropic) để biến nội dung thông báo trở nên hài hước, văn phong như một phi hành gia thực thụ gửi tin nhắn về Trái Đất.

### 📌 Kết luận
Chỉ với vài phút thiết lập cùng n8n, các sếp đã sở hữu ngay một hệ thống cảnh báo thiên văn công nghệ cao. Còn chần chờ gì nữa, hãy "lên đồ" và cài đặt ngay để chuẩn bị ngắm trạm vũ trụ vào tối nay thôi nào!