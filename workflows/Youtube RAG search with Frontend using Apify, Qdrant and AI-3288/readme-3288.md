---
title: "🎥 Tự động hóa tìm kiếm video YouTube với AI - Giải pháp RAG hoàn chỉnh"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tìm kiếm video YouTube thông minh sử dụng n8n, Apify, Qdrant và AI. Tiết kiệm thời gian và nâng cao trải nghiệm tìm kiếm video."
slug: "tu-dong-hoa-tim-kiem-video-youtube-voi-ai"
tags: [n8n, automation, no-code, AI, RAG, Qdrant, Apify]
keywords: [n8n workflow, tự động hóa, tìm kiếm video, AI, RAG, Qdrant, Apify]
---

# 🎥 Tự động hóa tìm kiếm video YouTube với AI - Giải pháp RAG hoàn chỉnh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải tìm kiếm thông tin trong hàng nghìn video YouTube. Quá trình này tốn thời gian và không hiệu quả. Workflow này sẽ giúp các sếp xây dựng hệ thống tìm kiếm video YouTube thông minh sử dụng công nghệ RAG (Retrieval-Augmented Generation) với n8n, Apify, Qdrant và AI.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tìm kiếm thông tin trong video YouTube
- Nâng cao trải nghiệm tìm kiếm video với kết quả chính xác và liên quan
- Tự động hóa quá trình xử lý transcript video
- Xây dựng hệ thống tìm kiếm video thông minh với AI
- Tích hợp dễ dàng với các công cụ khác như Slack, Telegram,...
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apify để scrape video YouTube
- Tài khoản Qdrant để lưu trữ vector embeddings
- Tài khoản OpenAI để sử dụng mô hình AI
- Tài khoản Redis để quản lý rate limiting (tùy chọn)
- Kiến thức cơ bản về n8n và các công cụ liên quan
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Node "Get Video Subtitles"**: Cấu hình credentials cho Apify để scrape video YouTube.
- **Node "Qdrant Vector Store"**: Cấu hình credentials cho Qdrant và tạo collection "n8n_videos" với vector size 1536.
- **Node "Embeddings"**: Cấu hình credentials cho OpenAI và chọn mô hình phù hợp (gpt-4o-mini).
- **Node "SEARCH API"**: Cấu hình path cho webhook (n8n_videos/api/search).
- **Node "Incr Rate Limit"**: Cấu hình credentials cho Redis để quản lý rate limiting (tùy chọn).
- **Node "WEB UI"**: Cấu hình path cho webhook (n8n_videos/).
- **Node "Qdrant Groups Search"**: Cấu hình credentials cho Qdrant và cấu hình search parameters.
- **Node "Get Embeddings"**: Cấu hình credentials cho OpenAI.
- **Node "Schedule Trigger"**: Cấu hình thời gian chạy định kỳ để cập nhật video mới.
- **Node "Get Latest Youtube Videos"**: Cấu hình credentials cho Apify để scrape video mới nhất.
- **Node "OpenAI Chat Model"**: Cấu hình credentials cho OpenAI và chọn mô hình phù hợp (gpt-4o-mini).

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có video mới.
- Lưu log tìm kiếm để phân tích hành vi người dùng.
- Gửi báo cáo định kỳ về các video được tìm kiếm nhiều nhất.
- Tích hợp với các công cụ khác như Google Analytics để theo dõi hiệu suất.

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn chỉnh để xây dựng hệ thống tìm kiếm video YouTube thông minh với AI. Các sếp có thể tùy chỉnh và mở rộng theo nhu cầu của mình. Hãy áp dụng ngay để nâng cao trải nghiệm tìm kiếm video và tiết kiệm thời gian cho doanh nghiệp!