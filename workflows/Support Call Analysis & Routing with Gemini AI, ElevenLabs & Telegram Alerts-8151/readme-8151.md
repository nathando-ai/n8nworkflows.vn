---
title: "🚀 Tự động phân tích cuộc gọi khách hàng với AI Gemini, thông báo Telegram và lưu log Google Sheets"
description: "Workflow n8n tự động phân tích cuộc gọi khách hàng từ Google Drive, sử dụng AI Gemini để đánh giá cảm xúc, thông báo Telegram và lưu log chi tiết vào Google Sheets. Giảm thiểu 80% thời gian xử lý thủ công."
slug: "tu-dong-phan-tich-cuoc-goi-khach-hang-voi-ai-gemini-telegram-google-sheets"
tags: [n8n, automation, no-code, ai, google-drive, telegram, google-sheets]
keywords: [n8n workflow, tự động hóa cuộc gọi, phân tích cảm xúc khách hàng, ai gemini, telegram alert, google sheets log]
---

# 🚀 Tự động phân tích cuộc gọi khách hàng với AI Gemini, thông báo Telegram và lưu log Google Sheets

[Các sếp đang gặp khó khăn khi phải nghe lại hàng trăm cuộc gọi khách hàng mỗi ngày để đánh giá chất lượng dịch vụ. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ ghi âm đến phân tích cảm xúc, thông báo và lưu log chỉ trong vài phút.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian**: Tự động xử lý hàng trăm cuộc gọi mỗi ngày mà không cần can thiệp thủ công.
- **Phân tích chính xác**: Sử dụng AI Gemini để đánh giá cảm xúc khách hàng với độ chính xác cao.
- **Thông báo tức thời**: Gửi cảnh báo ngay lập tức cho quản lý qua Telegram khi phát hiện cuộc gọi tiêu cực.
- **Lưu trữ dữ liệu**: Tự động lưu log chi tiết vào Google Sheets để theo dõi và báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive chứa các file ghi âm cuộc gọi.
- API Key của Google Gemini (Google PaLM API).
- Thông tin xác thực Telegram (Bot Token và Chat ID).
- Tài khoản Google Sheets để lưu log.
- API Key của dịch vụ chuyển đổi giọng nói thành văn bản (ví dụ: AssemblyAI, Deepgram).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8151](https://n8n.io/workflows/8151)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô URL và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Search For New Call Recordings"**:
  - Chọn credentials "googleDriveOAuth2Api"
  - Điền ID thư mục chứa các file ghi âm cuộc gọi vào trường "Folder ID"

- **Node "Google Gemini Chat Model"**:
  - Chọn credentials "googlePalmApi"
  - Đặt prompt phù hợp để phân tích cảm xúc khách hàng (ví dụ: "Analyze the sentiment of this customer call transcript. Return the result in JSON format with fields: sentiment (positive/negative/neutral), summary, and key_points")

- **Node "Send Alert To Managers"**:
  - Chọn credentials "telegramApi"
  - Điền Chat ID của nhóm quản lý vào trường "Chat ID"

- **Node "Send Kudos to Team"**:
  - Chọn credentials "telegramApi"
  - Điền Chat ID của kênh team vào trường "Chat ID"

- **Node "Log Recording Analysis"**:
  - Chọn credentials "googleSheetsOAuth2Api"
  - Điền ID Spreadsheet và tên Sheet vào các trường tương ứng
  - Đảm bảo các cột trong Google Sheets phù hợp với cấu trúc dữ liệu đầu ra của node "Structured Output Parser"

- **Node "Convert Speech To Text"**:
  - Chọn credentials "httpHeaderAuth" (nếu sử dụng dịch vụ có yêu cầu xác thực)
  - Điền URL API của dịch vụ chuyển đổi giọng nói thành văn bản
  - Cấu hình các header và body request phù hợp với API được sử dụng

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để kiểm tra với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn nút "Activate Workflow" để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thay thế node Telegram bằng node Slack để nhận thông báo trên Slack.
- **Lưu log chi tiết hơn**: Thêm các trường dữ liệu bổ sung vào Google Sheets như thời gian cuộc gọi, nhân viên hỗ trợ, v.v.
- **Phân tích sâu hơn**: Sử dụng các node AI khác để phân tích thêm các khía cạnh khác của cuộc gọi (ví dụ: độ chính xác thông tin, thời gian phản hồi).
- **Gửi báo cáo định kỳ**: Thêm node gửi email báo cáo tổng hợp hàng tuần/tháng về chất lượng dịch vụ.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình phân tích cuộc gọi khách hàng, từ ghi âm đến thông báo và lưu log. Với sự kết hợp của AI Gemini và các công cụ lưu trữ dữ liệu phổ biến, các sếp có thể nâng cao chất lượng dịch vụ khách hàng một cách hiệu quả và tiết kiệm thời gian đáng kể. Hãy áp dụng ngay để tối ưu hóa quy trình hỗ trợ khách hàng của bạn!