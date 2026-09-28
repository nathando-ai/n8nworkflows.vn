---
title: "🚀 Tự động lọc và phân tích video Bất động sản TikTok cho cặp đôi bằng AI, Apify và Google Sheets"
description: "Khám phá cách tự động hóa quy trình nghiên cứu thị trường bất động sản trên TikTok, dùng AI chọn lọc nhà cho cặp đôi trẻ, lưu vào Google Sheets và báo cáo qua Slack."
slug: "loc-video-bat-dong-san-tiktok-ai-apify-google-sheets"
tags: [n8n, automation, no-code, tiktok, real-estate, ai-agent, google-sheets]
keywords: [n8n workflow, tự động hóa tiktok, bất động sản tiktok, apify scraper, ai agent n8n, google sheets automation]
---

# 🚀 Tự động lọc và phân tích video Bất động sản TikTok bằng AI và Apify

Các môi giới bất động sản hay các bạn trẻ đang tìm nhà có đang tốn hàng giờ đồng hồ lướt TikTok để tìm kiếm những căn phòng trọ, căn hộ chung cư ưng ý? Việc cào dữ liệu thủ công, sàng lọc video phù hợp với tiêu chí cụ thể (ví dụ: dành riêng cho các cặp đôi 20-30 tuổi) cực kỳ mất thời gian và dễ bỏ sót.

Đừng lo, workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Cào video TikTok qua Apify 👉 Dùng AI Agent (OpenRouter) phân tích, chấm điểm và viết lý do giới thiệu 👉 Lưu kết quả vào Google Sheets 👉 Bắn thông báo trực quan qua Slack. Không cần viết code, chỉ cần "lên đồ" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần lướt TikTok thủ công, hệ thống tự động cào và lọc hàng loạt video theo hashtag.
- **AI thông minh chọn lọc:** AI Agent phân tích nội dung video, xác định xem căn hộ đó có thực sự phù hợp với "cặp đôi 20s" hay không và tự động viết lý do đề xuất.
- **Quản lý tập trung:** Toàn bộ thông tin video, link và đánh giá của AI được lưu gọn gàng vào Google Sheets.
- **Cảnh báo thời gian thực:** Nhận ngay thông báo qua Slack mỗi khi có bất động sản "hot" được tìm thấy.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn:
- Một instance n8n (Phiên bản v1.0 trở lên).
- Tài khoản **Apify** (để cào dữ liệu TikTok).
- Tài khoản **OpenRouter** (cung cấp LLM cho AI Agent).
- Tài khoản Google (Google Sheets để lưu dữ liệu).
- Workspace **Slack** (để nhận thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, paste trực tiếp vào n8n Editor của mình hoặc import file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

- **Run an Actor and get dataset (Apify Node):** 
  - Chọn Credentials của Apify.
  - Cấu hình Actor để cào TikTok theo các hashtag mục tiêu (ví dụ: `#rental`, `#apartment`, `#phongtro`).
- **OpenRouter Chat Model & OpenRouter Chat Model1 (AI Model Nodes):**
  - Nhập API Key của OpenRouter.
  - Lựa chọn mô hình AI phù hợp (ví dụ: `anthropic/claude-3.5-sonnet` hoặc `openai/gpt-4o-mini`).
- **AI Agent & AI Agent1 (LangChain Nodes):**
  - Tùy chỉnh System Prompt để hướng dẫn AI cách nhận diện nhà cho "cặp đôi trong độ tuổi 20" và yêu cầu tạo lý do đề xuất (Recommendation reasons).
- **Append or update row in sheet (Google Sheets Node):**
  - Kết nối tài khoản Google OAuth2.
  - Chọn đúng file Google Spreadsheet và Sheet Name để lưu thông tin video, link và đánh giá từ AI.
- **Send a message (Slack Node):**
  - Kết nối Slack OAuth2.
  - Chọn Channel đích (ví dụ: `#real-estate-leads` hoặc `#tiktok-radar`) để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Bấm nút **When clicking ‘Execute workflow’** (Manual Trigger) để test chạy thử với dữ liệu mẫu xem hệ thống hoạt động ổn định chưa.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chạy theo lịch trình (hoặc trigger tùy ý).

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nguồn dữ liệu:** Có thể mở rộng kết hợp thêm các Actor cào Reels từ Instagram hoặc Shorts từ YouTube vào chung một luồng xử lý.
- **Lưu trữ nâng cao:** Thay vì chỉ dùng Google Sheets, các sếp có thể đẩy dữ liệu vào Airtable hoặc Notion để quản lý trực quan hơn.
- **Tích hợp kênh thông báo khác:** Bên cạnh Slack, có thể bổ sung node Telegram để bắn tin trực tiếp vào nhóm chat cá nhân hoặc nhóm Telegram của team kinh doanh.

### 📌 Kết luận
Workflow "Filter TikTok Real Estate Videos for Couples" là giải pháp tuyệt vời tận dụng sức mạnh của AI và No-code để khai thác nguồn dữ liệu khổng lồ từ mạng xã hội. Hãy cài đặt ngay hôm nay để tối ưu hóa công việc nghiên cứu thị trường bất động sản của các sếp!