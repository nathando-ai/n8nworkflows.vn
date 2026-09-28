---
title: "🚀 Tự động trích xuất và lưu trữ n8n Community Workflows mới nhất với ScrapeGraphAI & Gemini"
description: "Hướng dẫn xây dựng pipeline tự động thông minh kết hợp ScrapeGraphAI, Gemini và Google Sheets để cào, phân tích và lưu trữ các workflow mới nhất từ cộng đồng n8n."
slug: "tu-dong-trich-xuat-n8n-community-workflows-voi-scrapegraphai-va-gemini"
tags: [n8n, automation, no-code, ai-scraping, scrapegraphai, google-gemini, google-sheets]
keywords: [n8n workflow, scrapegraphai, google gemini, tự động hóa web scraping, AI extraction, google sheets automation]
---

# 🚀 Tự động trích xuất và lưu trữ n8n Community Workflows mới nhất với ScrapeGraphAI & Gemini

Chào các sếp! Việc theo dõi các workflow mới được chia sẻ trên cộng đồng n8n để cập nhật xu hướng và ý tưởng tự động hóa là vô cùng quan trọng đối với một "tín đồ" No-Code. Tuy nhiên, nếu làm thủ công hàng ngày sẽ cực kỳ tốn thời gian. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh (do tác giả Davide xây dựng), tự động sử dụng **ScrapeGraphAI**, **Google Gemini**, và **OpenAI** để cào dữ liệu web, trích xuất thông tin chi tiết, tóm tắt nội dung và lưu thẳng vào **Google Sheets** một cách hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn 100%**: Thay vì lướt web thủ công, lịch trình (`Schedule Trigger`) sẽ tự động kích hoạt workflow định kỳ.
- **Sức mạnh AI thông minh**: Kết hợp ScrapeGraphAI để cào dữ liệu dạng Markdown cùng các mô hình AI lớn như Gemini và OpenAI để trích xuất cấu trúc dữ liệu và tóm tắt nội dung cực kỳ chính xác.
- **Lưu trữ trực quan**: Toàn bộ thông tin workflow mới (tiêu đề, mô tả, link, tác giả...) được đẩy thẳng vào Google Sheets để dễ dàng quản lý và tra cứu.
- **Không cần code phức tạp**: Sử dụng các node LangChain và AI tiên tiến ngay trong giao diện trực quan của n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lắp ráp", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
1. **Tài khoản n8n** (bản Cloud hoặc Self-hosted đã cài đặt community node `ScrapeGraphAI`).
2. **ScrapeGraphAI API Key**: Đăng ký miễn phí tại [ScrapeGraphAI Dashboard](https://dashboard.scrapegraphai.com/?via=n3witalia).
3. **Google Gemini API Key / Google Palm API Credentials**.
4. **OpenAI API Key** (dành cho node OpenAI Chat Model).
5. **Google Sheets OAuth2 API** và bản sao (clone) của [Google Sheet mẫu tại đây](https://docs.google.com/spreadsheets/d/1CnTq5kkHkdv8GPfGrjRkeK66R0XHOys25BF_Me2OX6I/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ nguồn cung cấp.
- Trong giao diện n8n, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp vào màn hình canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:
- **Cài đặt ScrapeGraphAI Community Node**: Đảm bảo instance n8n của các sếp đã cài đặt gói node `n8n-nodes-scrapegraphai`.
- **Node `Scrape main page` & `Scrape single Workflow`**: 
  - Chọn credential loại `scrapegraphAIApi` và điền API Key đã lấy từ ScrapeGraphAI.
  - Resource được thiết lập sẵn là `markdownify` để chuyển đổi trang web thành văn bản Markdown sạch cho AI xử lý.
- **Các node AI (Google Gemini Chat Model, OpenAI Chat Model1, Information Extractor)**:
  - Kiểm tra và liên kết các Credentials tương ứng (`googlePalmApi` cho Gemini, `openAiApi` cho OpenAI).
  - Đảm bảo model được chọn (ví dụ: `gpt-5-mini` hoặc các model Gemini mới nhất) hoạt động bình thường trong tài khoản của các sếp.
- **Node `Add row` (Google Sheets)**:
  - Kết nối tài khoản Google thông qua `googleSheetsOAuth2Api`.
  - Chọn đúng file Google Sheet đã clone từ [đường dẫn mẫu](https://docs.google.com/spreadsheets/d/1CnTq5kkHkdv8GPfGrjRkeK66R0XHOys25BF_Me2OX6I/edit?usp=sharing) và chọn đúng Sheet Name để dữ liệu đổ về đúng cột.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** (hoặc dùng node `When clicking ‘Execute workflow’`) để chạy thử nghiệm với dữ liệu mẫu xem các bước cào và tóm tắt AI hoạt động đúng chưa.
- Kiểm tra lại Google Sheets xem dữ liệu đã được thêm mới thành công hay chưa.
- Nếu mọi thứ ổn định, bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động theo lịch của node `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ở cuối luồng để nhận tin nhắn ngay lập tức mỗi khi có workflow mới xuất hiện trên cộng đồng n8n.
- **Lọc thông minh**: Thêm node `If` sau bước trích xuất để chỉ lưu lại những workflow có chứa từ khóa liên quan đến lĩnh vực các sếp quan tâm (ví dụ: `AI`, `Marketing`, `Notion`).
- **Báo cáo định kỳ**: Tạo một workflow phụ để tổng hợp các workflow mới trong tuần từ Google Sheets và gửi email tóm tắt vào mỗi thứ Hai hàng tuần.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho thấy sức mạnh kết hợp giữa n8n, Web Scraping thế hệ mới (ScrapeGraphAI) và Trí tuệ nhân tạo (Gemini/OpenAI). Chúc các sếp ứng dụng thành công và xây dựng được kho tài nguyên tự động hóa của riêng mình! Nếu gặp khó khăn gì trong quá trình cài đặt, cứ để lại bình luận trao đổi nhé!