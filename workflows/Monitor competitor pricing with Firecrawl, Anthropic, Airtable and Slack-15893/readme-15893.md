---
title: "🚀 Tự động Giám sát Giá Đối thủ Cạnh tranh với Firecrawl, Anthropic, Airtable và Slack"
description: "Xây dựng hệ thống theo dõi giá và tồn kho đối thủ 24/7 tự động hoàn toàn, phân tích chênh lệch giá bằng AI và gửi cảnh báo thông minh qua Slack."
slug: "giam-sat-gia-doi-thu-voi-firecrawl-anthropic-slack"
tags: [n8n, automation, no-code, firecrawl, anthropic, slack]
keywords: [n8n workflow, giám sát giá đối thủ, competitor pricing automation, firecrawl n8n, ai price tracking]
keywords: [n8n workflow, giám sát giá đối thủ, competitor pricing automation, firecrawl n8n, ai price tracking]
---

# 🚀 Tự động Giám sát Giá Đối thủ Cạnh tranh với Firecrawl, Anthropic, Airtable và Slack

Các sếp có đang tốn hàng giờ mỗi tuần để thủ công truy cập website đối thủ, check giá sản phẩm, cập nhật file Excel rồi tính toán xem họ tăng hay giảm bao nhiêu không? Việc này vừa mất thời gian, dễ bỏ lỡ các biến động giá chớp nhoáng, lại chẳng thể đưa ra chiến lược ứng phó kịp thời.

Workflow n8n chuyên nghiệp này sẽ giải quyết triệt để vấn đề đó! Hệ thống sẽ tự động cào dữ liệu trang sản phẩm của đối thủ, trích xuất giá và tình trạng kho bằng AI, tính toán biên độ chênh lệch, phân loại mức độ ưu tiên và bắn thông báo chiến lược thẳng vào Slack, đồng thời lưu lịch sử vào Airtable và Google Sheets hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% lịch trình 6 tiếng/lần**: Không cần con người can thiệp, hệ thống tự động quét sạch danh sách đối thủ.
- **Trích xuất thông minh bằng AI**: Sử dụng Firecrawl kết hợp Anthropic API để lấy chính xác giá và trạng thái kho dưới dạng cấu trúc chuẩn.
- **Cảnh báo thông minh theo cấp độ**: Phân loại mức độ thay đổi (Critical, High, Medium, Info) để bắn tin nhắn Slack kèm gợi ý chiến lược đối phó ngay lập tức.
- **Lưu trữ dữ liệu toàn diện**: Tự động cập nhật trạng thái mới nhất vào Airtable và ghi log lịch sử chi tiết vào Google Sheets để phân tích xu hướng dài hạn.
:::

### yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Firecrawl API**: Dùng để scrape nội dung trang sản phẩm của đối thủ.
- **Anthropic API (Claude)**: Dùng để trích xuất dữ liệu giá và sinh chiến lược đối phó.
- **Airtable**: Cơ sở dữ liệu lưu danh sách đối thủ (Competitor Name, Product Name, Product URL, Last Price, In Stock).
- **Slack**: Kênh nhận thông báo cảnh báo biến động giá.
- **Google Sheets**: Bảng tính lưu log lịch sử giá theo thời gian.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn mã JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp nhớ cấu hình kỹ các điểm sau:
- **Node `Get Competitor List` (Airtable) và `Synchronize Active State` (Airtable)**: Thay thế `appYYYYYY` bằng Base ID thực tế của các sếp và `tblCompetitors` bằng Table ID chứa danh sách đối thủ.
- **Node `Immediate Slack Notification` và `Standard Slack Log` (Slack)**: Thay thế mã kênh Slack mẫu (`C08AAAAAA`) bằng Channel ID thực tế của nhóm làm việc.
- **Node `Append Historical Sheet Log` (Google Sheets)**: Thay `REPLACE_WITH_YOUR_GOOGLE_SHEET_ID` bằng Google Sheet ID và điền đúng tên Tab chứa dữ liệu log lịch sử.
- **Credentials**: Kết nối đầy đủ tài khoản API cho Firecrawl, Anthropic, Airtable, Slack và Google Sheets vào các node tương ứng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm (Test Run) với danh sách mẫu xem các node có xử lý mượt mà không.
- Nếu mọi thứ xanh mướt, hãy bật nút **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm mỗi 6 tiếng!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Ngoài Slack, các sếp có thể gắn thêm node Telegram hoặc Email để nhận cảnh báo ngay trên điện thoại khi có đối thủ hạ giá sốc.
- **Tích hợp Webhook**: Thêm một Webhook Trigger để chủ động kích hoạt quét giá thủ công ngay khi có tin đồn đối thủ chuẩn bị tung sản phẩm mới.
- **Dashboard báo cáo**: Kết nối Google Sheets với Looker Studio để vẽ biểu đồ theo dõi xu hướng giá thị trường theo thời gian thực.

### 📌 Kết luận
Việc theo dõi giá đối thủ thủ công đã là chuyện của thế kỷ trước. Với workflow n8n kết hợp AI mạnh mẽ này, các sếp sẽ luôn chiếm thế chủ động trong mọi cuộc đua về giá trên thị trường. Lên đồ ngay thôi các sếp ơi!