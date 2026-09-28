---
title: "💰 Tự động theo dõi chi tiêu & thu nhập từ Telegram với Google Sheets và Google Gemini"
description: "Hướng dẫn chi tiết cách tự động ghi chép chi tiêu và thu nhập qua Telegram, lưu vào Google Sheets và phân tích bằng AI Google Gemini - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-theo-doi-chi-tieu-thu-nhap-telegram-google-sheets-gemini"
tags: [n8n, automation, no-code, telegram, google-sheets, google-gemini, ai-chatbot]
keywords: [n8n workflow, tự động hóa chi tiêu, telegram bot, google sheets, google gemini, quản lý tài chính]
---

# 💰 Tự động theo dõi chi tiêu & thu nhập từ Telegram với Google Sheets và Google Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải ghi chép chi tiêu và thu nhập thủ công, dễ bị lỗi và mất thời gian. Workflow này giúp các sếp tự động hóa toàn bộ quy trình này chỉ với vài bước cấu hình đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian ghi chép thủ công
- Dữ liệu chi tiêu và thu nhập được lưu tự động vào Google Sheets
- Phân tích và tính toán tự động bằng AI Google Gemini
- Theo dõi chi tiêu hàng ngày, hàng tuần và hàng tháng
- Nhận báo cáo chi tiết qua Telegram
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets
- OAuth2 credentials từ Google Cloud Console
- Telegram Bot Token (tạo qua @BotFather)
- Google Gemini API Key (lấy từ Google AI Studio)
- Google Spreadsheet với cấu trúc như sau:
  - Các sheet chi tiêu theo tháng (định dạng: "Tháng 2 2026", "Tháng 3 2026",...)
  - Sheet thu nhập tĩnh (tên: "Income Log")
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/13557)
2. Click "Copy" để sao chép JSON workflow
3. Trong n8n Editor, click "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Tạo Credentials**:
   - Telegram API: Nhập Bot Token từ @BotFather
   - Google Sheets: Nhập OAuth2 credentials từ Google Cloud Console
   - Google Gemini: Nhập API Key từ Google AI Studio

2. **Cập nhật Google Sheets Document ID**:
   - Tìm Document ID trong URL của Google Sheets (phần `THIS_PART` trong `docs.google.com/spreadsheets/d/THIS_PART/edit`)
   - Cập nhật ID này vào tất cả 5 node Google Sheets:
     - add_expense
     - get_expense
     - delete_expense
     - add_income
     - get_income

3. **Gán Credentials cho các node**:
   - 4 node Telegram → Telegram API credential
   - 5 node Google Sheets → Google Sheets credential
   - 1 node Gemini Chat Model → Google Gemini credential

#### 3. Kích hoạt ⚡️
1. Click "Test Workflow" để kiểm tra
2. Gửi tin nhắn đến bot Telegram của các sếp
3. Kiểm tra phản hồi và dữ liệu trong Google Sheets
4. Khi đã hoạt động ổn định, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động tạo sheet mới**: Các sếp có thể thêm node để tự động tạo sheet mới cho mỗi tháng
2. **Báo cáo định kỳ**: Kết hợp với node gửi email để nhận báo cáo hàng tuần/tháng
3. **Kết nối với Slack**: Thêm node để gửi thông báo đến kênh Slack
4. **Phân tích nâng cao**: Sử dụng node để tạo biểu đồ và báo cáo chi tiết

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý tài chính cá nhân. Với sự kết hợp của Telegram, Google Sheets và AI Google Gemini, các sếp có thể theo dõi và phân tích chi tiêu một cách hiệu quả. Hãy áp dụng ngay để nâng cao hiệu suất quản lý tài chính của các sếp!