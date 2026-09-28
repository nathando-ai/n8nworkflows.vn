---
title: "🚀 Tự động giám sát và phản hồi đánh giá Google Maps bằng AI, Apify và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động cào đánh giá Google Maps, phân tích bằng AI qua OpenRouter, lưu Google Sheets và cảnh báo qua Slack."
slug: "tu-dong-giam-sat-danh-gia-google-maps-ai-apify-slack"
tags: [n8n, automation, ai-agent, google-maps, slack, apify]
keywords: [n8n workflow, apify google maps, ai agent review, tu dong hoa google sheets, slack alert]
---

# 🚀 Tự động giám sát và phản hồi đánh giá Google Maps bằng AI, Apify và Slack

Việc theo dõi thủ công các đánh giá trên Google Maps cho cửa hàng hoặc chuỗi doanh nghiệp tốn rất nhiều thời gian và nếu bỏ lỡ đánh giá 1-2 sao, bạn có thể đánh mất khách hàng vĩnh viễn. 

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Quét đánh giá mới mỗi ngày qua Apify, lọc bỏ trùng lặp với Google Sheets, sử dụng AI (OpenRouter) để phân tích cảm xúc và viết sẵn câu trả lời lịch sự, sau đó bắn thông báo phân loại qua Slack (kênh cảnh báo sao thấp, kênh ăn mừng sao cao).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần vào từng địa điểm Google Maps kiểm tra thủ công mỗi ngày.
- **Phản ứng tức thì với khủng hoảng:** Đánh giá dưới 4 sao được đẩy ngay lập tức lên kênh Slack hỗ trợ khách hàng để xử lý khẩn cấp.
- **Cá nhân hóa phản hồi bằng AI:** AI tự động tóm tắt và soạn thảo sẵn câu trả lời chuyên nghiệp (xin lỗi nếu đánh giá thấp, cảm ơn nếu đánh giá cao).
- **Lưu trữ dữ liệu tập trung:** Toàn bộ lịch sử đánh giá được đồng bộ sạch sẽ vào Google Sheets để làm báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Cloud hoặc Self-hosted (phiên bản v1.0 trở lên).
- **Apify Account:** Tài khoản Apify để chạy actor *Google Maps Reviews Scraper*.
- **Google Sheets API:** Tài khoản Google Cloud Platform để cấp quyền đọc/ghi Google Sheets.
- **Slack Workspace:** Đã kết nối Webhook hoặc OAuth để gửi tin nhắn thông báo.
- **OpenRouter (hoặc OpenAI) API Key:** Để AI Agent xử lý và sinh nội dung phản hồi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này từ n8n template (ID: 11053) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `CONFIG (Edit Here)`:** Điền các thông số quan trọng:
  - `MAPS_URL`: Link Google Maps đầy đủ của cửa hàng/doanh nghiệp.
  - `SHEET_ID`: ID của Google Sheet lấy từ đường dẫn URL của file.
  - `SHOP_NAME`: Tên thương hiệu hoặc cửa hàng của các sếp.
- **Node `Save to Google Sheets` & `Get Existing IDs`:** Chọn tài khoản Google Sheets Credentials và trỏ tới file Google Sheet đã chuẩn bị sẵn với các cột: `reviewId`, `publishedAt`, `reviewerName`, `stars`, `text`, `ai_summary`, `ai_reply`, `reviewUrl`, `output`, `publishedAt date`.
- **Node `Run an Actor and get dataset`:** Cấu hình Apify API Key để node gọi được Scraper Google Maps.
- **Node `OpenRouter Chat Model` & `AI Agent`:** Nhập OpenRouter API Key và kiểm tra System Message của AI Agent để đảm bảo văn phong phản hồi phù hợp với thương hiệu.
- **Node `Slack (Alert)` & `Slack (Alert)1`:** Chọn kết nối Slack và chỉ định đúng kênh nhận tin (ví dụ: kênh `#customer-support` cho đánh giá thấp và `#wins` cho đánh giá cao).

#### 3. Kích hoạt ⚡️
- Chạy thử thủ công (Test run) một lần để kiểm tra dòng dữ liệu từ Apify qua AI và ghi vào Google Sheets.
- Bật công tắc **Active** để workflow tự động chạy ngầm theo lịch hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng kênh thông báo:** Có thể tích hợp thêm Telegram Bot thay vì chỉ dùng Slack nếu đội ngũ của các sếp quen dùng Telegram.
- **Mở rộng nhiều cơ sở:** Chạy vòng lặp qua một danh sách chứa nhiều URL Google Maps nếu doanh nghiệp của các sếp có chuỗi nhiều cửa hàng.
- **Tạo báo cáo tuần:** Kết hợp thêm node Schedule Trigger hàng tuần để tổng hợp số lượng đánh giá tốt/xấu từ Google Sheets và gửi báo cáo tóm tắt cho sếp lớn.

### 📌 Kết luận
Workflow này là một "trợ lý ảo" hoàn hảo giúp doanh nghiệp kiểm soát chặt chẽ uy tín trực tuyến trên Google Maps mà không tốn một chút sức lực thủ công nào. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và xử lý khủng hoảng truyền thông kịp thời nhé các sếp!