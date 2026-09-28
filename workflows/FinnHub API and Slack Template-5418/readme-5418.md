---
title: "🚀 Tự động hóa bản tin chứng khoán hàng ngày từ FinnHub API lên Slack với n8n"
description: "Hướng dẫn cài đặt và sử dụng workflow n8n để tự động lấy tin tức công ty theo danh sách mã cổ phiếu từ FinnHub API và gửi báo cáo trực tiếp vào kênh Slack."
slug: "tu-dong-hoa-tin-tuc-chung-khoan-finnhub-slack-n8n"
tags: [n8n, automation, finnhub, slack, crypto-trading, stock-market]
keywords: [n8n workflow, finnhub api, slack automation, tin tức chứng khoán, bot tự động n8n]
---

# 🚀 Xây dựng Bot Cập Nhật Tin Tức Chứng Khoán Hàng Ngày Lên Slack tự động với n8n

Các nhà đầu tư và trader thường xuyên phải đối mặt với áp lực thời gian: Làm sao để cập nhật nhanh nhất tin tức mới nhất của các mã cổ phiếu (stock tickers) mình đang quan tâm mà không phải tốn hàng giờ lướt web thủ công mỗi sáng? 

Việc theo dõi thủ công không chỉ tẻ nhạt mà còn dễ bỏ lỡ các tin tức quan trọng ảnh hưởng đến thị trường. Giải pháp là gì? Hãy để hệ thống tự động hóa lo thay các sếp! Workflow n8n **FinnHub API and Slack Template** (do chuyên gia Fan Luo xây dựng) sẽ tự động lấy tin tức từ FinnHub API và bắn thông báo gọn gàng, đẹp mắt thẳng vào kênh Slack của team mỗi ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Tự động hóa 100% quy trình thu thập và tổng hợp tin tức tài chính mỗi sáng.
- **Cập nhật có chiến lược:** Chỉ theo dõi đúng những mã cổ phiếu (tickers) các sếp quan tâm.
- **Bảo vệ API Rate Limit:** Tích hợp bộ đếm thời gian thông minh (Wait node) giúp tránh việc gửi quá nhiều request cùng lúc lên FinnHub bản miễn phí.
- **Teamwork hiệu quả:** Tin tức được định dạng Markdown gọn gàng và đẩy thẳng vào kênh Slack chung của nhóm đầu tư.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **FinnHub API Key:** Đăng ký tài khoản miễn phí tại [FinnHub API](https://finnhub.io/) để lấy API Key.
- **Slack App / Webhook:** Tạo một Slack App và kích hoạt Incoming Webhooks để bot có quyền gửi tin nhắn vào kênh Slack mong muốn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trên n8n của các sếp, sau đó copy toàn bộ mã JSON của template này và paste trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình các điểm sau:

- **Daily Market News Trigger (`scheduleTrigger`):** Mặc định lịch chạy được đặt vào mỗi sáng các ngày trong tuần lúc 9:15 AM. Các sếp có thể đổi lại múi giờ hoặc thời gian tuỳ ý trong node này.
- **Prep Tickers (`code`):** Đây là nơi định nghĩa danh sách các mã cổ phiếu (ví dụ: AAPL, TSLA, GOOGL...). Hãy sửa lại danh sách này thành các mã cổ phiếu mà các sếp đang quan tâm.
- **HTTP Request (`httpRequest`):** 
  - Gọi tới endpoint tin tức công ty của FinnHub.
  - Cần tạo một credential loại **Header Auth** trong n8n, điền API Key lấy từ trang FinnHub vào để xác thực.
- **Wait (`wait`):** Thiết lập thời gian chờ 5 giây giữa các lần gọi API. Việc này cực kỳ quan trọng để không bị vượt quá giới hạn (rate limit) của gói FinnHub Free.
- **Format (`code`):** Node code xử lý dữ liệu thô từ API thành định dạng Markdown đẹp mắt trước khi đẩy lên Slack.
- **Slack (`slack`):** Kết nối với Slack Webhook hoặc sử dụng Slack API Credential để chọn đúng kênh (Channel) nhận tin nhắn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công xem tin nhắn có bắn về Slack thành công không.
- Nếu mọi thứ hiển thị đẹp đẽ, hãy bật **Active** để bot tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo:** Ngoài Slack, các sếp có thể nhân bản nhánh gửi tin để đẩy đồng thời sang Telegram Bot hoặc Discord Webhook.
- **Lưu trữ lịch sử:** Thêm một node Google Sheets hoặc Airtable vào sau bước format để lưu lại lịch sử tin tức phục vụ việc backtest hoặc phân tích về sau.
- **Bộ lọc thông minh:** Chỉnh sửa code trong node `Format` để chỉ lấy các tin tức có từ khóa quan trọng (như "earnings", "acquisition", "lawsuit"...).

### 📌 Kết luận
Với workflow **FinnHub API and Slack Template**, việc cập nhật tin tức thị trường mỗi ngày nay đã hoàn toàn tự động hóa, giúp các sếp ra quyết định đầu tư nhanh chóng và chính xác hơn. Hãy cài đặt ngay hôm nay và tối ưu hóa quy trình giao dịch của mình!