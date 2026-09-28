---
title: "🚀 Tự Động Theo Dõi Giá Đối Thủ Với Google Shopping & Cảnh Báo Qua Slack, Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động giám sát giá sản phẩm đối thủ từ Google Shopping, lưu trữ vào Google Sheets và gửi cảnh báo thông minh qua Slack, Gmail."
slug: "tu-dong-theo-doi-gia-doi-thu-google-shopping-n8n"
tags: [n8n, automation, no-code, market-research, google-sheets, slack, gmail]
keywords: [n8n workflow, theo dõi giá đối thủ, google shopping automation, tự động hóa n8n, cảnh báo giá slack gmail]
---

# 🚀 Tự Động Theo Dõi Giá Đối Thủ Với Google Shopping & Cảnh Báo Qua Slack, Gmail

Trong thị trường cạnh tranh khốc liệt hiện nay, việc nắm bắt nhanh chóng biến động giá cả của đối thủ cạnh tranh là chìa khóa sống còn để điều chỉnh chiến lược kinh doanh. Tuy nhiên, việc thủ công tra cứu từng sản phẩm mỗi ngày trên Google Shopping tốn rất nhiều thời gian và dễ bỏ sót. 

Giải pháp tuyệt vời cho các sếp đây: Workflow n8n tự động hóa 100% giúp quét giá đối thủ định kỳ, lưu dữ liệu hệ thống Google Sheets và lập tức bắn tin nhắn cảnh báo qua Slack hoặc Gmail khi có biến động, giúp đội ngũ Sales/Marketing luôn đi trước một bước!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Chạy theo lịch trình định sẵn (Schedule Trigger) mà không cần can thiệp thủ công.
- **Cập nhật dữ liệu liền mạch:** Tự động đồng bộ và cập nhật giá mới nhất vào Google Sheets để tiện theo dõi, phân tích.
- **Cảnh báo tức thì:** Nhận thông báo trực tiếp qua kênh Slack của team hoặc email qua Gmail ngay khi phát hiện thay đổi về giá.
- **Tối ưu chiến lược giá:** Giúp doanh nghiệp phản ứng nhanh chóng với các chương trình khuyến mãi hay điều chỉnh giá của đối thủ.
:::

### 🏆 Tác giả
Workflow này được xây dựng bởi **Veena Pandian** - một chuyên gia GTM Engineer với 6 năm kinh nghiệm trong lĩnh vực Revenue Operations, chuyên thiết kế các hệ thống tự động hóa thông minh giúp tối ưu hóa quy trình kinh doanh.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** File Google Sheets chứa danh sách sản phẩm và từ khóa cần theo dõi.
- **Tài khoản Google/Gmail:** Để gửi email cảnh báo tự động.
- **Tài khoản Slack:** Tạo Webhook hoặc tích hợp Bot để nhận tin nhắn thông báo.
- **API/HTTP Request:** Dịch vụ hoặc API dùng để lấy dữ liệu từ Google Shopping.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc hoặc copy trực tiếp mã nguồn JSON và paste vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:
- **Schedule Trigger:** Thiết lập chu kỳ chạy mong muốn (ví dụ: chạy 1 lần/ngày vào lúc 8h sáng).
- **Google Sheets Node:** Kết nối tài khoản Google, trỏ tới đúng File ID và Sheet Name chứa danh sách sản phẩm cần theo dõi giá.
- **HTTP Request / Code Node:** Cấu hình nguồn dữ liệu để cào hoặc gọi API lấy thông tin giá sản phẩm từ Google Shopping dựa trên danh sách từ Google Sheets.
- **Split In Batches & Filter Node:** Xử lý dữ liệu theo từng lô (batch) để tránh quá tải API và lọc ra các sản phẩm có sự thay đổi giá đáng chú ý.
- **Slack & Gmail Nodes:** Kết nối credentials tương ứng, thiết lập nội dung tin nhắn và email cảnh báo (gắn kèm tên sản phẩm, giá cũ, giá mới, link Google Shopping).

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để chạy thử nghiệm với dữ liệu mẫu, đảm bảo không có lỗi ở các node.
- Kiểm tra kết quả trên Google Sheets và kênh Slack/Gmail xem thông báo đã chuẩn xác chưa.
- Gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Microsoft Teams để gửi thông báo đa kênh cho ban quản lý.
- **Lưu lịch sử giá:** Thiết lập thêm một bảng phụ trong Google Sheets để lưu trữ lịch sử biến động giá theo thời gian (Time-series), phục vụ cho việc vẽ biểu đồ xu hướng.
- **Tích hợp AI Summarization:** Sử dụng thêm các node AI để phân tích xu hướng giá của đối thủ trong tuần/tháng và gửi báo cáo tóm tắt tự động vào sáng thứ Hai hàng tuần.

### 📌 Kết luận
Việc theo dõi giá đối thủ chưa bao giờ dễ dàng đến thế với sức mạnh của tự động hóa n8n. Hãy áp dụng ngay workflow này để tiết kiệm hàng giờ làm việc thủ công và giúp doanh nghiệp luôn làm chủ cuộc đua về giá trên thị trường!