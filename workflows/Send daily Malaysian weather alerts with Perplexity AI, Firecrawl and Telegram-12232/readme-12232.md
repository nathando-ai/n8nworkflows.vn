---
title: "🚀 Tự động gửi cảnh báo thời tiết Malaysia hàng ngày với Perplexity AI, Firecrawl và Telegram"
description: "Xây dựng hệ thống tự động hóa n8n lấy dữ liệu thời tiết chính thống, kết hợp AI tìm kiếm tin tức, cào dữ liệu và gửi cảnh báo trực quan qua Telegram."
slug: "tu-dong-gui-canh-bao-thoi-tiet-malaysia-voi-n8n"
tags: [n8n, automation, no-code, ai-agent, telegram, firecrawl]
keywords: [n8n workflow, tự động hóa thời tiết, perplexity ai, firecrawl, telegram bot, openrouter]
---

# 🚀 Tự động gửi cảnh báo thời tiết Malaysia hàng ngày với Perplexity AI, Firecrawl và Telegram

Các sếp có đang mất thời gian mỗi ngày để tổng hợp thông tin thời tiết, tìm kiếm tin tức cảnh báo từ các mặt báo và gửi thủ công cho đội ngũ hoặc cộng đồng? Việc cập nhật chậm trễ các bản tin thời tiết cực đoan có thể gây ảnh hưởng lớn đến công việc và sinh hoạt.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% bằng n8n, kết hợp sức mạnh của AI (Perplexity & OpenAI), công cụ cào web (Firecrawl) và kênh thông báo nhanh (Telegram) để làm thay toàn bộ công việc đó cho các sếp! Workflow này được thiết kế bởi chuyên gia Wan Dinie, tối ưu hóa chi phí và sẵn sàng vận hành thực tế (production-ready).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Lịch trình chạy định kỳ mỗi 9 giờ sáng mà không cần con người can thiệp.
- **Thông tin đa chiều, chính xác**: Lấy dữ liệu từ API chính phủ Malaysia, kết hợp AI tìm kiếm các bài báo mới nhất trong vòng 3 ngày từ các hãng thông tấn lớn (Utusan, Harian Metro, Berita Harian, Kosmo).
- **Tóm tắt chuyên nghiệp**: Sử dụng OpenAI để tổng hợp, tinh chỉnh báo cáo thời tiết rõ ràng, kèm nguồn trích dẫn chi tiết.
- **Phân phối tức thì**: Gửi thẳng bản tin trực quan đến nhóm hoặc kênh Telegram cá nhân bằng tiếng Anh (hoặc ngôn ngữ tùy chỉnh).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **OpenAI API Key**: Dùng cho node tổng hợp báo cáo (`Make a summary`).
- **OpenRouter API Key**: Dùng cho mô hình Perplexity Sonar Pro (`Perplexity Sonar Pro Model`).
- **Firecrawl API Key**: Dùng để cào nội dung các bài báo (`Scrape Website with Firecrawl`). Tài khoản miễn phí (Free tier) có giới hạn số lượng request mỗi giờ.
- **Telegram Bot Token & Chat ID**: Tạo bot thông qua `@BotFather` trên Telegram để gửi tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ nguồn gốc.
- Mở giao diện n8n Editor của các sếp, chọn **Add workflow** -> Dán (Paste) hoặc Import vào hệ thống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số sau trong các node tương ứng:
- **Node `Make a summary`**: Chọn/Thêm Credentials của OpenAI API Key.
- **Node `Perplexity Sonar Pro Model`**: Chọn/Thêm Credentials của OpenRouter API Key (đảm bảo model được chọn là `perplexity/sonar-pro-search`).
- **Node `Scrape Website with Firecrawl`**: Điền Authorization header theo định dạng `Bearer fc-YOUR-KEY` với API key lấy từ Firecrawl.
- **Node `Send to Telegram`**: Kết nối Telegram API credentials và cập nhật chính xác Chat ID của kênh hoặc nhóm Telegram muốn nhận tin.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm với dữ liệu giả lập hoặc chạy thử lần đầu.
- Kiểm tra kết quả hiển thị trên Telegram.
- Nếu mọi thứ hoạt động trơn tru, hãy chuyển trạng thái workflow sang **Active** để hệ thống tự chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này theo nhu cầu riêng, các sếp có thể thử:
- **Đổi khung giờ chạy**: Điều chỉnh node `Schedule Trigger` sang mốc thời gian phù hợp hơn với múi giờ hoặc chiến dịch của doanh nghiệp.
- **Tùy chỉnh ngôn ngữ**: Thay đổi system prompt trong node `Make a summary` nếu muốn xuất bản báo cáo bằng tiếng Mã Lai (Bahasa Malaysia) hoặc tiếng Việt.
- **Mở rộng nguồn lưu trữ**: Gắn thêm node Google Sheets hoặc Supabase phía sau để lưu lại lịch sử cảnh báo thời tiết phục vụ việc phân tích dữ liệu (Business Intelligence).
- **Đa kênh thông báo**: Kết hợp thêm node gửi email, WhatsApp hoặc Slack cùng lúc với Telegram để mở rộng phạm vi tiếp cận cảnh báo.

### 📌 Kết luận
Workflow tự động hóa cảnh báo thời tiết Malaysia kết hợp AI, Firecrawl và Telegram này là một minh chứng tuyệt vời cho việc ứng dụng công nghệ no-code vào đời sống và kinh doanh thực tế. Hãy cài đặt ngay trên hệ thống n8n của các sếp để tối ưu hóa thời gian và nâng cao độ chuyên nghiệp trong việc cập nhật thông tin quan trọng!