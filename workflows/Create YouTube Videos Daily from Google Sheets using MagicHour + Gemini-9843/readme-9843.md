---
title: "🚀 Tự động hóa sản xuất và đăng tải Video YouTube mỗi ngày từ Google Sheets với MagicHour & Gemini AI"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động hóa tạo video, tối ưu tiêu đề/thẻ tag bằng Gemini AI, render qua MagicHour và tự động upload lên YouTube Shorts hoặc video dài từ Google Sheets."
slug: "tu-dong-hoa-tao-video-youtube-tu-google-sheets-magichour-gemini"
tags: [n8n, automation, youtube, gemini-ai, magichour, google-sheets, ai-video]
keywords: [n8n workflow, tạo video tự động, magic hour ai, google gemini n8n, youtube automation, auto youtube shorts]
---

# 🚀 Tự động hóa sản xuất và đăng tải Video YouTube mỗi ngày từ Google Sheets với MagicHour & Gemini AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải lên ý tưởng, viết kịch bản, tạo video, tối ưu SEO tiêu đề, mô tả rồi thủ công upload lên YouTube mỗi ngày? Công việc lặp đi lặp lại này ngốn rất nhiều thời gian mà hiệu quả đôi khi không cao.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ, giúp tự động hóa 100% quy trình từ việc nhận diện dòng mới trong **Google Sheets**, sử dụng sức mạnh AI của **Google Gemini** để lập thông số video, gọi API **MagicHour** để tạo video (hỗ trợ cả YouTube Shorts), xử lý âm thanh, cho đến bước cuối cùng là **tự động upload lên kênh YouTube** và cập nhật ngược lại kết quả vào Google Sheets. Tất cả diễn ra hoàn toàn tự động mà không cần sự can thiệp thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Chỉ cần điền ý tưởng/prompt vào Google Sheet, hệ thống sẽ tự sinh video, gắn thẻ, tiêu đề chuẩn SEO và đăng lên YouTube.
- **Xử lý linh hoạt YouTube Shorts**: AI tự động nhận diện nếu prompt yêu cầu tạo Shorts (ví dụ: *"make a shorts of..."*) để cấu hình đúng tỷ lệ khung hình và thời lượng.
- **Tích hợp AI thông minh**: Sử dụng Google Gemini (LangChain Agent) để phân tích kịch bản và tạo metadata chuẩn xác.
- **Quản lý vòng đời video mượt mà**: Kiểm tra trạng thái render video qua API, tự động chờ (Wait & Retry), tải xuống và update kết quả trực tiếp vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Phiên bản n8n (Khuyên dùng Self-hosted hoặc n8n Cloud bản Pro để hỗ trợ một số node đặc thù như MediaFX).
- **Google Account & Google Cloud Console**: Để cấu hình Google Sheets API và YouTube Data API v3.
- **Google AI Studio / Gemini API Key**: Dành cho các node AI Agent.
- **MagicHour API Key**: Nền tảng tạo video AI.
- **Google Sheets**: File Google Sheets chuẩn bị sẵn chứa các cột: Prompt, Youtube URL, Youtube Title, Youtube Tags, Youtube Description, Download URL.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình các Credentials quan trọng sau:

- **Google Sheets & Drive Credentials**:
  - Vào Google Cloud Console → Tạo/chọn project.
  - Bật **Google Sheets API** và **Google Drive API**.
  - Tạo OAuth client credentials (Web application), thêm Authorized redirect URI: `https://<your-n8n-domain>/rest/oauth2-credential/callback`.
  - Kết nối trong n8n cho node `Sheet Row Added` (Trigger) và `Update Results` (Google Sheets).
  - *Lưu ý cấu trúc Google Sheet cần có các cột:* `Prompt`, `Youtube URL`, `Youtube Title`, `Youtube Tags`, `Youtube Description`, `Download URL`.

- **Google Gemini API Credentials**:
  - Tạo API Key tại Google AI Studio.
  - Thêm credential dạng Google PaLM/Gemini API trong n8n và gán vào các node `Gemini AI Model` / `Google Gemini Chat Model` dùng cho LangChain agents (`Generate Video Parameters` và `Generate YouTube Data`).

- **MagicHour API Credentials**:
  - Đăng ký tài khoản MagicHour, vào mục Developer/API dashboard để tạo API Key.
  - Trong n8n, tạo credential mới dạng **HTTP Bearer Auth**, dán token vào.
  - Gắn credential này vào 2 node HTTP Request: `Create Video` và `Check Video Status`.

- **YouTube Data API v3 Credentials**:
  - Trong cùng Google Cloud Project ở trên, bật **YouTube Data API v3**.
  - Tạo OAuth client credentials (có thể dùng chung hoặc tạo mới OAuth client với cùng redirect URI).
  - Cấp quyền cho node `Upload a video` (YouTube node) để tự động publish video lên kênh của các sếp với các thiết lập `regionCode`, `categoryId`, `privacyStatus`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một dòng dữ liệu mẫu trong Google Sheet để kiểm tra vòng lặp render video của MagicHour.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động hoạt động 24/7.

### ✍️ Gợi ý nâng cao & Mở rộng
- **Tích hợp thông báo Telegram/Slack**: Thêm node Telegram ngay sau bước `Upload a video` để nhận thông báo tức thì kèm link video khi hoàn tất xuất bản.
- **Lưu trữ Log lỗi**: Thêm nhánh Error Trigger để ghi nhận lại nếu MagicHour render thất bại do lỗi kịch bản hoặc hết quota API.
- **Hẹn giờ định kỳ**: Thay vì dùng Google Sheets Trigger (thời gian thực), có thể kết hợp thêm node Schedule Trigger để tự động cào ý tưởng và tạo video hàng ngày theo lịch cố định.

### 📌 Kết luận
Với workflow n8n kết hợp giữa Google Sheets, Gemini AI và MagicHour này, các sếp đã sở hữu một "phòng dựng phim tự động" thu nhỏ. Tiết kiệm hàng giờ đồng hồ mỗi ngày để tập trung vào chiến lược phát triển kênh thay vì làm thủ công. Chúc các sếp cấu hình thành công!