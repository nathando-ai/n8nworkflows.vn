---
title: "🚀 Tự Động Tra Cứu Giá Đa Sàn Thương Mại Điện Tử Với Bright Data, Claude AI và Telegram"
description: "Workflow n8n giúp tự động cào dữ liệu giá sản phẩm từ nhiều sàn TMĐT (Amazon, eBay, Etsy, Target, BestBuy, Home Depot), phân tích bằng Claude AI và gửi thông báo deal tốt nhất qua Telegram."
slug: "tu-dong-tra-cuu-gia-da-san-thuong-mai-dien-tu"
tags: [n8n, automation, no-code, web-scraping, claude-ai, bright-data, telegram]
keywords: [n8n workflow, cào giá sản phẩm, bright data scraping, claude ai automation, telegram price alert, market research n8n]
---

# 🚀 Tự Động Tra Cứu Giá Đa Sàn Thương Mại Điện Tử Với Bright Data, Claude AI và Telegram

Việc theo dõi và so sánh giá sản phẩm thủ công trên hàng loạt các nền tảng thương mại điện tử lớn (như Amazon, eBay, Etsy, Target, BestBuy, Home Depot) là một "cực hình" mất rất nhiều thời gian đối với các nhà nghiên cứu thị trường, chủ cửa hàng dropshipping hay người mua sắm thông thái. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: Nhận yêu cầu từ form -> Cào dữ liệu giá đồng loạt từ nhiều sàn qua **Bright Data** -> Lưu trữ vào **Google Sheets** -> Sử dụng sức mạnh AI của **Claude (Anthropic)** để chọn ra sản phẩm giá hời nhất và viết nội dung quảng cáo -> Cuối cùng đẩy thông báo tức thì qua **Telegram**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [End-user / VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần phải mở hàng chục tab trình duyệt để tìm và so sánh giá thủ công nữa.
- **Dữ liệu đa sàn tập trung:** Toàn bộ thông tin tên sản phẩm, giá, đường dẫn từ Amazon, eBay, Etsy, Target, BestBuy, Home Depot được tự động đổ về Google Sheets gọn gàng.
- **AI thông minh chọn deal:** Tự động lọc ra sản phẩm có mức giá thấp nhất và dùng Claude AI tạo sẵn một thông điệp quảng cáo/deal hời cực kỳ thu hút.
- **Cảnh báo tức thì:** Nhận ngay kết quả sản phẩm rẻ nhất qua Telegram ngay sau khi quá trình quét hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Bright Data Account:** Tài khoản Bright Data API để thực hiện cào dữ liệu web (Web Scraping/Dataset APIs).
- **Anthropic API Key:** Để kết nối với mô hình Claude 4 Sonnet qua node AI Agent.
- **Telegram Bot Token:** Tạo một Telegram Bot qua BotFather để gửi tin nhắn thông báo.
- **Google Sheets Account:** Kết nối OAuth2 với n8n để ghi nhận dữ liệu vào bảng tính.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON từ n8n.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 79 nodes được thiết kế tỉ mỉ, các sếp cần cấu hình chính xác các thành phần sau để hệ thống chạy mượt mà:
- **On form submission (Form Trigger):** Node khởi chạy bằng giao diện form để người dùng nhập từ khóa sản phẩm cần tìm kiếm.
- **Các node HTTP Request (Triggers & Checks Bright Data):** Cần cấu hình Header chứa API Token/Key hợp lệ của Bright Data cho các sàn (Amazon, eBay, Etsy, Target, BestBuy, Home Depot) để kích hoạt quá trình lấy snapshot dữ liệu.
- **Google Sheets & Google Sheets1 đến Google Sheets7:** Chọn tài khoản Google Sheets OAuth2 và liên kết tới các bảng tính (Google Spreadsheet ID, Sheet Name) để lưu dữ liệu URL, tiêu đề và giá của từng nền tảng.
- **Anthropic Chat Model:** Điền thông tin `anthropicApi` credentials và đảm bảo model được chọn là `claude-sonnet-4-20250514` (Claude 4 Sonnet) để AI xử lý việc viết nội dung deal.
- **Telegram:** Cấu hình credentials `telegramApi` và chỉ định Chat ID của cá nhân hoặc kênh/group nhận thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền từ khóa vào Form Trigger để kiểm tra luồng chạy của dữ liệu qua từng node (Wait, If, Merge, Filter...).
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Telegram, các sếp có thể bổ sung node Slack, Microsoft Teams hoặc Email để gửi báo cáo giá cho đội ngũ kinh doanh.
- **Lưu log định kỳ:** Thiết lập thêm Google Sheets append định kỳ mỗi tuần để theo dõi biến động giá của một mặt hàng cụ thể theo thời gian (Price Tracking).
- **Tối ưu thời gian chờ (Wait Nodes):** Tùy chỉnh các node `Wait` sao cho phù hợp với tốc độ trả dữ liệu snapshot của Bright Data, tránh việc request quá nhanh khi dữ liệu chưa sẵn sàng (`status: ready`).

### 📌 Kết luận
Với sự kết hợp hoàn hảo giữa công nghệ cào dữ liệu mạnh mẽ của Bright Data, khả năng tư duy ngôn ngữ tuyệt vời của Claude AI và tốc độ thông báo của Telegram, workflow này là "vũ khí tối thượng" giúp các nhà kinh doanh và nghiên cứu thị trường nắm bắt giá cả thị trường trong chớp mắt. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!