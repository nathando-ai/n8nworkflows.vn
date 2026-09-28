---
title: "🚀 Tự động hóa Web Scraping & Screenshot với GPT 4.1 mini và Firecrawl"
description: "Hướng dẫn tự động hóa thu thập thông tin từ website, tổng hợp nội dung bằng AI và chụp ảnh trang web một cách nhanh chóng và hiệu quả."
slug: "tu-dong-hoa-web-scraping-screenshot-voi-gpt-4-1-mini-va-firecrawl"
tags: [n8n, automation, no-code, web-scraping, ai]
keywords: [n8n workflow, tự động hóa, web scraping, AI summarization, Firecrawl]
---

# 🚀 Tự động hóa Web Scraping & Screenshot với GPT 4.1 mini và Firecrawl

[Các sếp đang gặp khó khăn khi phải thu thập thông tin từ nhiều trang web khác nhau, tổng hợp nội dung và chụp ảnh trang web một cách thủ công. Workflow này sẽ giúp các sếp tự động hóa quy trình này một cách nhanh chóng và hiệu quả.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian thu thập thông tin từ nhiều trang web khác nhau.
- Tổng hợp nội dung một cách nhanh chóng và hiệu quả.
- Chụp ảnh trang web một cách tự động và chính xác.
- Tăng hiệu suất làm việc và giảm thiểu lỗi thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenRouter để sử dụng GPT 4.1 mini.
- Tài khoản Firecrawl để thực hiện tìm kiếm và chụp ảnh trang web.
- URL của trang web cần thu thập thông tin.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Site**: Node này được sử dụng để nhập URL của trang web cần thu thập thông tin.
- **In URL**: Node này được sử dụng để nhập từ khóa cần xuất hiện trong URL của trang web.
- **Exclusion**: Node này được sử dụng để nhập từ khóa cần loại trừ khỏi kết quả tìm kiếm.
- **Pro**: Node này được sử dụng để nhập từ khóa cần xuất hiện trong nội dung của trang web.
- **When chat message received**: Node này được sử dụng để kích hoạt workflow khi nhận được tin nhắn chat.
- **GPT 4.1 mini**: Node này được sử dụng để tổng hợp nội dung từ trang web.
- **Firecrawl Search**: Node này được sử dụng để tìm kiếm thông tin trên trang web.
- **Search Agent**: Node này được sử dụng để thực hiện tìm kiếm và chụp ảnh trang web.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log các kết quả tìm kiếm để theo dõi và phân tích.
- Gửi báo cáo định kỳ về kết quả tìm kiếm và tổng hợp nội dung.

### 📌 Kết luận
Workflow này sẽ giúp các sếp tự động hóa quy trình thu thập thông tin từ trang web, tổng hợp nội dung và chụp ảnh trang web một cách nhanh chóng và hiệu quả. Hãy áp dụng ngay để tăng hiệu suất làm việc và giảm thiểu lỗi thủ công.