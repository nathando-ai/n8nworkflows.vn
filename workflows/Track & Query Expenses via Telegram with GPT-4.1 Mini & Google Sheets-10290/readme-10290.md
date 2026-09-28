---
title: "💰 Tự động theo dõi & truy vấn chi tiêu qua Telegram với GPT-4.1 Mini & Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi chi tiêu và truy vấn thông minh qua Telegram với AI GPT-4.1 Mini và Google Sheets - Giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-theo-doi-chi-tieu-qua-telegram-voi-gpt-4-1-mini-va-google-sheets"
tags: [n8n, automation, no-code, telegram, google-sheets, ai, gpt-4-1-mini]
keywords: [n8n workflow, tự động hóa chi tiêu, telegram automation, google sheets automation, gpt-4-1-mini, quản lý tài chính cá nhân]
---

# 💰 Tự động theo dõi & truy vấn chi tiêu qua Telegram với GPT-4.1 Mini & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết rằng theo dõi chi tiêu thủ công là một công việc tốn thời gian và dễ gây lỗi? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi chi tiêu và truy vấn thông minh thông qua Telegram, kết hợp với sức mạnh của AI GPT-4.1 Mini và Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quá trình theo dõi chi tiêu qua Telegram
- Truy vấn thông minh với AI GPT-4.1 Mini
- Lưu trữ và quản lý dữ liệu chi tiêu trên Google Sheets
- Nhận cảnh báo khi số dư tài khoản thấp
- Tiết kiệm thời gian đáng kể trong việc quản lý tài chính cá nhân
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram
- Tài khoản Google và Google Sheets
- API key của AssemblyAI (để chuyển đổi giọng nói thành văn bản)
- API key của OpenAI (để sử dụng GPT-4.1 Mini)
- Tài khoản Gmail (để gửi cảnh báo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/10290)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Input** (telegramTrigger):
   - Tạo bot Telegram mới và lấy token
   - Thêm bot vào nhóm Telegram của bạn
   - Cấu hình credentials trong n8n với token vừa lấy

2. **GPT-4.1 Mini Model** (lmChatOpenAi):
   - Tạo tài khoản OpenAI và lấy API key
   - Cấu hình credentials với API key
   - Chọn model là "gpt-4.1-mini"

3. **Read Transaction History** và **Append Transaction to Sheet** (googleSheets):
   - Tạo Google Sheet mới với các cột: Date, Description, Amount, Balance
   - Chia sẻ Google Sheet với tài khoản dịch vụ của n8n
   - Cấu hình credentials với thông tin Google Sheet

4. **Upload to AssemblyAI** và các node liên quan (httpRequest):
   - Tạo tài khoản AssemblyAI và lấy API key
   - Cấu hình credentials với API key

5. **Send Low Balance Alert** (gmailTool):
   - Cấu hình credentials với tài khoản Gmail của bạn

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi một tin nhắn mẫu qua Telegram
   - Kiểm tra kết quả trên Google Sheets
2. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo khi có giao dịch mới
- Lưu log các giao dịch vào Google Sheets để phân tích sau này
- Gửi báo cáo định kỳ về tình hình tài chính qua email
- Kết hợp với các dịch vụ ngân hàng để tự động cập nhật giao dịch
- Tích hợp với các công cụ phân tích tài chính khác như QuickBooks

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình theo dõi và quản lý chi tiêu thông qua Telegram, kết hợp với sức mạnh của AI GPT-4.1 Mini và Google Sheets. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian đáng kể trong việc quản lý tài chính cá nhân và nhận được cảnh báo kịp thời khi số dư tài khoản thấp. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!