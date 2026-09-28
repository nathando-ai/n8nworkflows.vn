---
title: "🚀 Tự Động Theo Dõi Xu Hướng Hashtag TikTok Bằng Apify và Gmail với n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động cào dữ liệu hashtag TikTok qua Apify, chấm điểm xếp hạng thông minh và gửi báo cáo chi tiết qua Gmail."
slug: "tu-dong-theo-doi-xu-huong-hashtag-tiktok-apify-gmail"
tags: [n8n, automation, tiktok, apify, gmail, market-research]
keywords: [n8n workflow, tự động hóa tiktok, apify tiktok scraper, theo dõi xu hướng hashtag, gửi báo cáo gmail]
---

# 🚀 Tự Động Theo Dõi Xu Hướng Hashtag TikTok Bằng Apify và Gmail

Các sếp có đang tốn hàng giờ mỗi tuần để thủ công tìm kiếm, lọc và phân tích các video xu hướng trên TikTok theo từng hashtag ngành hàng không? Việc này vừa mất thời gian, dễ bỏ sót thông tin quan trọng lại vừa khó tổng hợp số liệu để làm báo cáo cho team.

Giải pháp hoàn hảo là đây! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, tự động hóa toàn bộ quy trình: lấy danh sách từ khóa/hashtag từ Data Table, gọi API Apify để cào bài viết mới nhất trên TikTok, sử dụng thuật toán chấm điểm thông minh để xếp hạng, lưu trữ dữ liệu và tự động gửi báo cáo trực tiếp qua Gmail 100% không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần thủ công tìm kiếm hay cào dữ liệu TikTok nữa.
- **Báo cáo định động qua Email:** Nhận ngay bảng xếp hạng các video hot nhất theo hashtag trực tiếp qua Gmail theo lịch trình (hàng ngày/hàng tuần).
- **Chấm điểm thông minh (Scoring Algorithm):** Tự động phân loại, tính điểm tương tác (lượt xem, tim, bình luận) để chọn ra các nội dung chất lượng nhất.
- **Lưu trữ dữ liệu lịch sử:** Tự động lưu toàn bộ kết quả vào n8n Data Table để dễ dàng tra cứu, phân tích xu hướng dài hạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động.
- Tài khoản **Apify** kèm API Token để gọi TikTok Scraper API.
- Tài khoản **Google Gmail** (cấu hình OAuth2 để n8n có thể gửi email tự động).
- **n8n Data Table** để lưu trữ danh sách từ khóa tìm kiếm và bảng xếp hạng kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 15074) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:
- **When Schedule Triggers:** Cấu hình tần suất chạy mong muốn (ví dụ: chạy mỗi ngày 1 lần vào 8 giờ sáng).
- **Get Queries from Table1 (dataTable):** Chọn đúng bảng dữ liệu chứa danh sách các hashtag hoặc từ khóa cần theo dõi.
- **Scrape TikTok via Apify (httpRequest):** Điền Apify API Key của các sếp vào phần credentials và kiểm tra endpoint POST tới Apify TikTok Scraper API (`https://api.apify.com/v2/acts/...`).
- **Score and Sort TikTok Posts & Rank TikTok Posts1 (code):** Xem xét lại logic tính điểm (tùy chỉnh trọng số cho lượt views, likes, comments) nếu muốn phù hợp hơn với tiêu chí đánh giá của doanh nghiệp.
- **Save Rankings to Table1 (dataTable):** Trỏ đến bảng lưu trữ kết quả xếp hạng.
- **Send TikTok Report by Email (gmail):** Kết nối tài khoản Gmail qua OAuth2, thiết lập người nhận, tiêu đề và định dạng nội dung email báo cáo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test Run) với một vài từ khóa mẫu và kiểm tra kết quả trả về ở các node.
- Nếu mọi thứ hoạt động trơn tru, hãy chuyển trạng thái sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc nội bộ:** Thay vì chỉ gửi qua Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack để bắn thông báo ngay khi có báo cáo mới cho team Marketing.
- **Kết hợp AI tóm tắt nội dung:** Sử dụng thêm các node AI (OpenAI/Anthropic) để phân tích xu hướng và viết sẵn bản tóm tắt insights insights trong email.
- **Mở rộng nguồn dữ liệu:** Tương tự với TikTok, các sếp có thể nhân bản cấu trúc này để cào thêm Instagram Reels hoặc YouTube Shorts.

### 📌 Kết luận
Workflow tự động hóa theo dõi xu hướng TikTok bằng Apify và Gmail này là "vũ khí" đắc lực giúp các team Digital Marketing, Content Creator tiết kiệm hàng đống thời gian nghiên cứu thị trường. Hãy triển khai ngay hôm nay để nắm bắt nhanh chóng mọi trào lưu hot nhất trên mạng xã hội!