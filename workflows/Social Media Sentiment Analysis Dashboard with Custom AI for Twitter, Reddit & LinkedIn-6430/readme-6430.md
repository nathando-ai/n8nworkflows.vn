---
title: "🚀 Tự động hóa Phân tích Cảm xúc Mạng xã hội với AI Tùy chỉnh cho Twitter, Reddit & LinkedIn"
description: "Hướng dẫn chi tiết cách tự động thu thập, phân tích cảm xúc và cảnh báo từ các nền tảng mạng xã hội chính với n8n và ScrapeGraphAI"
slug: "tu-dong-hoa-phan-tich-cam-xuc-mang-xa-hoi-voi-ai-tu-chinh"
tags: [n8n, automation, no-code, social media, sentiment analysis]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, mạng xã hội, ScrapeGraphAI]
---

# 🚀 Tự động hóa Phân tích Cảm xúc Mạng xã hội với AI Tùy chỉnh cho Twitter, Reddit & LinkedIn

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Theo dõi liên tục**: Nhận thông tin thời gian thực từ Twitter, Reddit và LinkedIn
- **Phân tích cảm xúc tiên tiến**: AI phân loại từ rất tích cực đến rất tiêu cực
- **Cảnh báo sớm**: Nhận thông báo ngay khi phát hiện vấn đề nghiêm trọng
- **Báo cáo trực quan**: Dashboard Google Sheets với dữ liệu lịch sử và báo cáo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScrapeGraphAI (để thu thập dữ liệu từ mạng xã hội)
- Tài khoản Google (để tạo và cập nhật Google Sheets)
- Tài khoản Slack (để nhận cảnh báo)
- Thương hiệu/brand cần theo dõi (tên thương hiệu, hashtag, từ khóa)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6430](https://n8n.io/workflows/6430)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node "Social Media Monitor Trigger" (scheduleTrigger)**
- Thiết lập tần suất theo dõi (mặc định là mỗi 4 giờ)
- Có thể thay đổi theo nhu cầu của bạn

**Node "Manual Sentiment Check Webhook" (webhook)**
- Đảm bảo endpoint `/sentiment-webhook` không bị trùng với các endpoint khác
- Có thể thay đổi path nếu cần

**Nodes Scraper (Twitter, Reddit, LinkedIn)**
- Tất cả 3 nodes này đều sử dụng cùng một credential "scrapegraphAIApi"
- Cần cấu hình các tham số:
  - `query`: Thay thế bằng thương hiệu/brand của bạn
  - `max_results`: Số lượng kết quả tối đa muốn lấy (mặc định 10)
  - `language`: Ngôn ngữ của nội dung (mặc định 'en')

**Node "Advanced Sentiment Analysis & Brand Intelligence" (code)**
- Node này chứa logic phân tích cảm xúc và nhận dạng thương hiệu
- Có thể tùy chỉnh các ngưỡng cảm xúc trong code nếu cần

**Node "Google Sheets Sentiment Dashboard" (googleSheets)**
- Cần cấu hình credential "googleSheetsOAuth2Api"
- Thiết lập các tham số:
  - `spreadsheetId`: ID của Google Sheet bạn muốn cập nhật
  - `range`: Phạm vi dữ liệu trong sheet (ví dụ: "Sheet1!A1")
  - `data`: Dữ liệu sẽ được tự động truyền từ các node trước

**Nodes "Crisis & Priority Alert Filter" và "Positive Sentiment Filter" (if)**
- Có thể điều chỉnh các điều kiện lọc trong các node này
- Ví dụ: Thay đổi ngưỡng cảnh báo từ "negative" thành "very negative"

**Nodes Slack Alert (slack)**
- Cả hai nodes này đều sử dụng credential "slackOAuth2Api"
- Cần cấu hình:
  - `channel`: Kênh Slack để nhận thông báo
  - `message`: Nội dung thông báo (có thể tùy chỉnh)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn nút "Activate Workflow"
2. Thử chạy workflow với dữ liệu mẫu bằng cách nhấn nút "Execute Workflow"
3. Kiểm tra kết quả trên Google Sheets và Slack

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Telegram**: Thêm node Telegram để nhận cảnh báo ngoài Slack
- **Lưu log**: Thêm node để lưu log các hoạt động quan trọng
- **Báo cáo định kỳ**: Thiết lập workflow con để gửi báo cáo hàng tuần
- **Theo dõi thêm nền tảng**: Thêm nodes để theo dõi Instagram, Facebook, TikTok

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi và phân tích cảm xúc thương hiệu trên mạng xã hội. Với khả năng tự động hóa hoàn toàn, các sếp có thể tiết kiệm thời gian quý giá và nhận được thông tin quan trọng một cách nhanh chóng. Hãy thử ngay và nâng cao khả năng quản lý thương hiệu của bạn!