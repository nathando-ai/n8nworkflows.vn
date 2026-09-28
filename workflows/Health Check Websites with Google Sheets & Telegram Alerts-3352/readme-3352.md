---
title: "🚀 Tự động giám sát website và cảnh báo lỗi qua Telegram với n8n và Google Sheets"
description: "Xây dựng hệ thống Health Check website tự động 100%, quét danh sách URL từ Google Sheets và gửi cảnh báo ngay lập tức qua Telegram khi có sự cố."
slug: "tu-dong-giam-sat-website-telegram-google-sheets"
tags: [n8n, automation, devops, telegram, google-sheets, monitoring]
keywords: [n8n workflow, giám sát website, health check website, telegram alert, tự động hóa n8n]
keywords: [n8n workflow, giám sát website, health check website, telegram alert, tự động hóa n8n]
---

# 🚀 Tự động giám sát website và cảnh báo lỗi qua Telegram với n8n và Google Sheets

Các sếp có đang gặp tình trạng website của công ty, hệ thống bán hàng hoặc blog cá nhân bị "sập" mà không hề hay biết, dẫn đến mất khách hàng và doanh thu? Việc kiểm tra thủ công từng link một mỗi ngày vừa tốn thời gian, vừa kém hiệu quả.

Giải pháp ở đây là để n8n lo! Workflow **Health Check Websites with Google Sheets & Telegram Alerts** sẽ giúp các sếp tự động hóa toàn bộ quy trình kiểm tra sức khỏe website 24/7. Hệ thống sẽ tự động đọc danh sách URL từ Google Sheets, tiến hành kiểm tra trạng thái phản hồi và bắn tin nhắn cảnh báo ngay lập tức qua Telegram nếu có bất kỳ website nào gặp sự cố. Không cần code phức tạp, setup một lần chạy mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sự cố tức thì:** Nhận cảnh báo ngay lập tức qua Telegram khi website phản hồi lỗi (HTTP status code bất thường).
- **Quản lý danh sách linh hoạt:** Dễ dàng thêm, bớt hoặc chỉnh sửa danh sách website cần giám sát trực tiếp trên Google Sheets mà không cần chạm vào n8n.
- **Hoạt động 24/7 không mệt mỏi:** Lên lịch chạy tự động định kỳ (ví dụ: mỗi 30 phút hoặc 1 tiếng quét một lần).
- **Tiết kiệm nguồn lực:** Thay vì nhân sự túc trực kiểm tra thủ công, thời gian đó có thể dành cho các công việc tối ưu doanh số khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
- **Google Sheets:** Một tài khoản Google và file Google Sheets chứa danh sách URL cần kiểm tra.
- **Telegram Bot:** Một Telegram Bot Token và Chat ID để nhận tin nhắn cảnh báo (có thể tạo nhanh qua BotFather).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow hoặc tải file JSON từ nguồn gốc, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Schedule Trigger:** Thiết lập chu kỳ thời gian muốn workflow quét lại toàn bộ danh sách website (ví dụ: chạy mỗi 15 phút, 1 tiếng...).
- **Fetch Urls (Google Sheets node):** 
  - Kết nối tài khoản Google thông qua `Google Sheets OAuth2 API`.
  - Chọn đúng File Google Sheet và Sheet Name nơi các sếp lưu danh sách URL. 
  - *Lưu ý cấu trúc:* Theo hướng dẫn gốc, ô `A1` là tiêu đề, từ hàng `A2` trở xuống là danh sách các đường link website cần kiểm tra (ví dụ: `https://example.com`).
- **Check URL (HTTP Request node):** Node này sẽ thực hiện request đến từng URL lấy từ Google Sheets để kiểm tra mã trạng thái (status code).
- **Telegram node:** 
  - Kết nối tài khoản thông qua `Telegram API` (Nhập Bot Token).
  - Điền chính xác `Chat ID` của cá nhân hoặc nhóm Telegram muốn nhận thông báo cảnh báo lỗi.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm xem luồng chạy có mượt mà và lấy được dữ liệu từ Google Sheets hay không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để hệ thống chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh nhận tin:** Ngoài Telegram, các sếp có thể thay thế hoặc bổ sung bằng node **Slack**, **Discord**, hoặc gửi email qua **Gmail** / **SendGrid**.
- **Lưu log lỗi:** Kết hợp thêm một bước ghi log ngược lại vào Google Sheets (cột trạng thái OK/Error và thời gian kiểm tra) để tiện theo dõi lịch sử uptime của hệ thống.
- **Tùy chỉnh điều kiện cảnh báo:** Thêm node **If** sau bước *Check URL* để chỉ gửi cảnh báo khi status code khác `200` (tránh việc báo động giả khi trang web bảo trì hoặc lỗi mạng tạm thời).

### 📌 Kết luận
Việc giám sát hệ thống website chưa bao giờ dễ dàng đến thế với sự kết hợp của n8n, Google Sheets và Telegram. Hãy tranh thủ "lên đồ" ngay một con bot cảnh báo cho riêng mình để giấc ngủ của các sếp trở nên trọn vẹn hơn, không còn lo website sập giữa đêm!