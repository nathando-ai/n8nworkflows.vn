---
title: "🚀 Tự động Giám sát Giá E-commerce với Firecrawl, Claude-Sonnet & Telegram"
description: "Hướng dẫn xây dựng hệ thống theo dõi giá đối thủ tự động 24/7 bằng n8n, Firecrawl, Claude AI và Google Sheets, gửi cảnh báo tức thì qua Telegram."
slug: "tu-dong-giam-sat-gia-e-commerce-voi-firecrawl-claude-ai-telegram"
tags: [n8n, automation, no-code, e-commerce, ai-summarization, market-research]
keywords: [n8n workflow, giám sát giá, tự động hóa e-commerce, firecrawl, claude sonnet, telegram alert]
keywords: [n8n workflow, tự động hóa, giám sát giá, e-commerce, firecrawl, claude ai, telegram]
---

# 🚀 Tự động Giám sát Giá E-commerce với Firecrawl, Claude-Sonnet & Telegram

Các sếp làm trong ngành thương mại điện tử hoặc nghiên cứu thị trường chắc chắn hiểu rõ cảm giác "mệt mỏi" cỡ nào khi phải thủ công kiểm tra giá và tình trạng tồn kho của đối thủ mỗi ngày. Việc làm thủ công này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ lỡ các biến động giá chớp nhoáng, khiến chiến lược Dynamic Pricing (Định giá linh hoạt) bị chậm chân.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% do chuyên gia Cheng Siong Chin thiết kế sẽ thay các sếp làm toàn bộ việc cào dữ liệu, phân tích bằng AI, so sánh lịch sử và bắn thông báo thẳng vào Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo sập nguồn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2+ giờ mỗi ngày:** Không cần mở hàng loạt tab trình duyệt để check giá thủ công.
- **Cảnh báo thời gian thực:** Nhận ngay tin nhắn Telegram khi đối thủ thay đổi giá hoặc hết hàng.
- **Dữ liệu lịch sử chuẩn xác:** Tự động lưu vết biến động giá vào Google Sheets để phân tích xu hướng.
- **AI thông minh:** Trích xuất chính xác thông tin sản phẩm từ các trang web phức tạp nhờ Claude-Sonnet 4.5.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n instance** (Self-hosted hoặc Cloud).
- **Firecrawl API Key** (Dùng để cào dữ liệu web).
- **Apify API Key & Actor** (Hỗ trợ cào dữ liệu nâng cao).
- **Anthropic API Key** (Dùng Claude-Sonnet AI để xử lý dữ liệu).
- **Perplexity API Key** (Dùng cho node truy vấn phụ trợ).
- **Google Sheets account** (Lưu trữ lịch sử giá).
- **Telegram Bot Token & Chat ID** (Gửi thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào n8n editor, chọn **Import from JSON** hoặc dán trực tiếp vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 17 nodes phối hợp nhịp nhàng, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **⏰ Monitor Every 6 Hours (`scheduleTrigger`) hoặc 🖱️ When clicking ‘Execute workflow’ (`manualTrigger`):** Chọn tần suất quét mong muốn (ví dụ: mỗi 6 tiếng một lần hoặc chạy thủ công để test).
- **Scrape a url and get its content (`@mendable/n8n-nodes-firecrawl.firecrawl`):** Thêm Firecrawl API Credentials và cấu hình URL sản phẩm cần theo dõi.
- **🤖 AI Extract Product Data using Claude-Sonnet 4.5 (`anthropic`):** Thêm Anthropic API Credentials, chọn model Claude-Sonnet để trích xuất tên, giá, trạng thái tồn kho từ dữ liệu thô.
- **📊 Read Historical Data & 💾 Update Historical Data1 & 📝 Log Alert Details (`googleSheets`):** 
  - Kết nối Google Sheets OAuth2.
  - Chuẩn bị Google Sheet với các cột bắt buộc: 
    - `Product Name` (Cột A)
    - `Current Price` (Cột B)
    - `Previous Price` (Cột C)
    - `Stock Status` (Cột D)
    - `Last Updated` (Cột E)
    - `URL` (Cột F)
    - `Change Detected` (Cột G)
- **Send a text message (`telegram`):** Điền Telegram API Credentials, Bot Token và Chat ID để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm với 1 URL mẫu, kiểm tra xem dữ liệu có đẩy về Google Sheets và Telegram hay không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Email để gửi báo cáo tổng hợp cho đội ngũ Sales/Marketing vào cuối ngày.
- **Tùy chỉnh ngưỡng cảnh báo:** Chỉnh sửa code trong node `🔍 Detect Price & Stock Changes1` để chỉ cảnh báo khi giá giảm hoặc tăng trên một % nhất định (tránh bị spam tin nhắn khi giá biến động nhỏ).
- **Lưu trữ Big Data:** Thay vì dùng Google Sheets, có thể kết nối PostgreSQL hoặc Airtable nếu danh mục sản phẩm của các sếp lên tới hàng chục ngàn mặt hàng.

### 📌 Kết luận
Hệ thống giám sát giá tự động này là thứ vũ khí tối tân giúp doanh nghiệp e-commerce nắm thế chủ động trong cuộc đua giá cả. Thiết lập ngay hôm nay để tối ưu hóa chiến lược kinh doanh của các sếp!