---
title: "🚀 Tự Động Tổng Hợp Xu Hướng TikTok Mỗi Ngày Lên Telegram Bằng AI và WayinVideo"
description: "Hướng dẫn xây dựng workflow n8n tự động cào link TikTok từ Google Sheets, tóm tắt video qua WayinVideo API, phân tích bằng GPT-4o-mini và gửi báo cáo tóm tắt xu hướng (Daily Digest) lên Telegram mỗi 8h sáng."
slug: "tu-dong-tong-hop-xu-huong-tiktok-telegram-wayinvideo-gpt4o"
tags: [n8n, automation, no-code, tiktok, ai-agent, telegram]
keywords: [n8n workflow, tiktok trend tracker, wayinvideo summarization, gpt-4o-mini, telegram bot automation, google sheets n8n]
---

# 🚀 Tự Động Tổng Hợp Xu Hướng TikTok Mỗi Ngày Lên Telegram Bằng AI

Các sếp làm trong lĩnh vực Social Media, content agencies hay brand management chắc chắn hiểu cảm giác mệt mỏi khi phải tốn hàng giờ mỗi ngày để xem video TikTok thủ công nhằm tìm kiếm xu hướng (trend). Việc này không chỉ tốn thời gian mà còn dễ bỏ lỡ các nội dung viral quan trọng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n hoàn toàn tự động giúp giải quyết triệt để bài toán trên. Workflow này sẽ tự động đọc danh sách video TikTok từ Google Sheets, gọi API tóm tắt, sử dụng sức mạnh của **GPT-4o-mini** để phân tích, và gửi một bản báo cáo xu hướng (Daily Digest) cực kỳ chuyên nghiệp thẳng vào nhóm Telegram của đội ngũ vào lúc 8 giờ sáng mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần phải ngồi xem hàng giờ liền các video TikTok thủ công mỗi sáng.
- **Báo cáo thông minh & sâu sắc:** GPT-4o-mini tự động phân tích và tổng hợp thành 5 phần rõ ràng: Tổng quan xu hướng, tóm tắt từng video, top 3 mẫu nội dung (content patterns), đề xuất hành động và các hashtag thịnh hành.
- **Tự động hóa toàn diện:** Chạy tự động vào 8h sáng hàng ngày, tự động đánh dấu đã xử lý và lưu log vào Google Sheets.
- **Thông báo tức thì:** Gửi trực tiếp bản tóm tắt định dạng Markdown gọn gàng qua Telegram Bot cho team.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** (Self-hosted hoặc n8n Cloud).
- **WayinVideo API Key:** Dùng để gửi yêu cầu tóm tắt video TikTok.
- **OpenAI Account:** Lấy API Key để sử dụng mô hình `gpt-4o-mini`.
- **Google Sheets Account:** Kết nối OAuth2 để đọc/ghi dữ liệu hàng chờ video và lưu log.
- **Telegram Bot:** Tạo bot thông qua `@BotFather` để lấy Bot Token và `Chat ID` của nhóm/kênh nhận tin.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này (hoặc tải file JSON từ n8n template), sau đó paste trực tiếp vào giao diện n8n Editor của mình thông qua tính năng Import từ Clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các thông số quan trọng sau:

- **Node `4. WayinVideo — Submit Summarization` & `6. WayinVideo — Get Summary Results`:** Thay thế đoạn `YOUR_WAYINVIDEO_API_KEY` bằng API Key thật của dịch vụ WayinVideo.
- **Node `12. OpenAI — GPT-4o-mini Model`:** Kết nối tài khoản OpenAI Credentials của các sếp và xác thực mô hình `gpt-4o-mini`.
- **Node `2. Google Sheets — Read Pending Videos`, `15. Google Sheets — Log Digest` & `16. Google Sheets — Mark Videos Processed`:** 
  - Kết nối tài khoản Google Sheets OAuth2.
  - Thay thế `YOUR_TREND_SHEET_ID` bằng ID của Google Sheet thực tế.
  - Chuẩn bị một Google Sheet có tên `TikTok Trend Tracker` gồm 2 tab:
    - **Tab 1 (`Video Queue`):** Các cột gồm `Video URL`, `Video Title`, `Niche / Category`, `Date Added`, `Status`, `Processed Date`.
    - **Tab 2 (`Digest Log`):** Các cột gồm `Digest Date`, `Niche`, `Videos Processed`, `Overview`, `Top Patterns`, `Action Recommendations`, `Top Tags`, `Telegram Sent`, `Sent On`.
- **Node `14. Telegram — Send Daily Digest`:** Kết nối Telegram Bot Credentials và điền `YOUR_TELEGRAM_CHAT_ID` chính xác để Bot biết gửi tin nhắn về đâu.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test run**) bằng cách bấm nút `Execute Workflow` để kiểm tra xem dòng dữ liệu từ Google Sheets qua AI và Telegram có mượt mà không.
- Nếu mọi thứ hoạt động hoàn hảo, bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy vào 8h sáng mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình làm việc hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng sau:
- **Đa kênh thông báo:** Kết hợp thêm node Slack hoặc Microsoft Teams để gửi bản tóm tắt song song với Telegram.
- **Cảnh báo lỗi:** Thêm một Error Trigger để nếu API WayinVideo hoặc OpenAI gặp lỗi, hệ thống sẽ tự động bắn tin nhắn báo động về kênh riêng cho IT/Dev xử lý.
- **Lọc theo Niche:** Thêm các điều kiện (IF) phân loại danh mục (Niche) để gửi báo cáo riêng biệt cho từng team chuyên trách (ví dụ: Team Beauty, Team Tech, Team F&B...).

### 📌 Kết luận
Với workflow n8n kết hợp WayinVideo và GPT-4o-mini này, việc nghiên cứu xu hướng TikTok mỗi sáng của đội ngũ marketing sẽ trở nên tự động và nhàn hạ hơn bao giờ hết. Chúc các sếp cài đặt thành công và xây dựng được những nội dung triệu view từ các xu hướng được tổng hợp!