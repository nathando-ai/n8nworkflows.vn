---
title: "🚀 Tự động hóa tạo ảnh chụp màn hình Portfolio & nội dung Upwork với n8n, AI và Firecrawl"
description: "Hướng dẫn chi tiết workflow n8n giúp tự động cào dữ liệu website bằng Firecrawl, chụp ảnh đa góc độ, phân tích và viết nội dung portfolio Upwork bằng OpenAI, lưu trữ Google Drive/Sheets và thông báo qua Telegram."
slug: "tu-dong-hoa-tao-portfolio-screenshots-upwork-copy-n8n"
tags: [n8n, automation, ai, openai, firecrawl, google-workspace]
keywords: [n8n workflow, tạo portfolio tự động, upwork copy generator, firecrawl screenshot, openai n8n]
---

# 🚀 Tự động hóa tạo ảnh chụp màn hình Portfolio & nội dung Upwork với n8n, AI và Firecrawl

Chào các sếp! Việc xây dựng portfolio chuyên nghiệp hay chuẩn bị nội dung pitch dự án trên Upwork đôi khi chiếm rất nhiều thời gian thủ công: phải vào từng website, chụp ảnh màn hình từ desktop đến mobile, cào nội dung, rồi vắt óc viết mô tả sao cho thật cuốn hút khách hàng.

Nếu các sếp đang đau đầu vì quy trình thủ công này, workflow n8n này chính là "vũ khí bí mật" giải quyết trọn gói 100% tự động. Chỉ với một đường link website đầu vào qua Form, hệ thống sẽ tự động làm thay các sếp mọi công đoạn từ A-Z!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công chụp màn hình hay viết mô tả dự án từng cái một.
- **Chất lượng đỉnh cao:** Kết hợp Firecrawl render JavaScript mượt mà và ScreenshotOne chụp ảnh sắc nét (hero, fullpage, mobile).
- **Cá nhân hóa bằng AI:** OpenAI (GPT-4o-mini) tự động phân tích cấu trúc trang web và viết nội dung portfolio chuyên nghiệp dành riêng cho Upwork.
- **Đồng bộ toàn diện:** Tự động lưu ảnh lên Google Drive, gom kết quả vào Google Sheets và bắn thông báo báo cáo ngay lập tức về Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Firecrawl API Key** (Lấy tại [firecrawl.dev](https://firecrawl.dev)).
- **ScreenshotOne API Key** (Lấy tại [screenshotone.com](https://screenshotone.com)).
- **OpenAI API Key** (Lấy tại [platform.openai.com](https://platform.openai.com)).
- **Google Drive & Google Sheets** (Tài khoản Google để cấu hình OAuth2).
- **Telegram Bot Token & Chat ID** (Tạo bot qua `@BotFather`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào n8n Editor chọn **Add workflow** -> Dấu ba chấm góc trên bên phải -> **Import from Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các thành phần sau:

- **Node "Site Configuration" (Code):** 
  - Thêm `ScreenshotOne API Key` vào biến `API_KEY` trong đoạn code của node này.
  - Tùy chỉnh kích thước viewport (desktop `1920`, mobile `375`), độ trễ `delay: 3` giây để trang web kịp tải.
- **Node "Firecrawl Scrape" (HTTP Request):** 
  - Điền Firecrawl API Key vào phần Header `Authorization` (Bearer token).
- **Node "AI Site Analysis" & "AI Generate Upwork" (HTTP Request / OpenAI):** 
  - Thiết lập Credential loại **OpenAI API**.
  - Model mặc định sử dụng là `gpt-4o-mini` (có thể đổi sang `gpt-4o` ở node chuẩn bị request nếu muốn phân tích sâu hơn).
- **Node "Upload to Google Drive" (Google Drive):** 
  - Kết nối OAuth2 Google Drive.
  - **Bắt buộc:** Thay thế `Folder ID` bằng ID thư mục Google Drive của các sếp để lưu ảnh chụp màn hình. (Lấy ID từ URL thư mục: `drive.google.com/drive/folders/YOUR_ID`).
- **Node "Save to Google Sheets" (Google Sheets):** 
  - Kết nối OAuth2 Google Sheets.
  - **Bắt buộc:** Thay thế `Spreadsheet ID` bằng ID bảng tính Google Sheets của các sếp (Lấy từ URL: `docs.spreadsheets/d/YOUR_ID/edit`). Dòng đầu tiên của sheet sẽ tự động nhận tiêu đề khi chạy lần đầu.
- **Node "Telegram Notification" (Telegram):** 
  - Kết nối Credentials Telegram API (Bot Token).
  - Điền `Chat ID` cá nhân hoặc nhóm để nhận thông báo hoàn tất.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách mở link từ node **Portfolio Form** để submit một URL bất kỳ.
- Kiểm tra kết quả trên Google Drive, Google Sheets và Telegram. Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để chạy 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận thông báo:** Thay vì chỉ gửi Telegram, các sếp có thể nối thêm node Slack hoặc Discord để đội ngũ cùng nắm tiến độ portfolio.
- **Tự động hóa toàn diện:** Kết hợp Webhook từ Typeform hoặc Tally thay vì dùng Form tích hợp sẵn của n8n nếu muốn thu thập dữ liệu từ trang landing page riêng.
- **Quản lý Rate Limit:** Workflow đã tích hợp sẵn node **Wait 3s** và **Loop Over Items (Split in Batches)** để chụp nhiều ảnh tuần tự, tránh bị chặn do gửi request quá dồn dập.

### 📌 Kết luận
Một workflow hoàn hảo giúp tiết kiệm hàng tá giờ đồng hồ làm nội dung và thiết kế portfolio. Hãy triển khai ngay lên hệ thống n8n của các sếp để nâng tầm chuyên nghiệp cho hồ sơ năng lực trên Upwork nhé!