---
title: "💰 Tự động hóa theo dõi chi tiêu qua Telegram với GPT-4 và Google Sheets (học tự động phân loại)"
description: "Hướng dẫn chi tiết cách tự động hóa việc ghi chép chi tiêu từ Telegram sang Google Sheets bằng AI, tiết kiệm thời gian và tránh sai sót thủ công"
slug: "tu-dong-hoa-theo-doi-chi-tieu-telegram-google-sheets"
tags: [n8n, automation, no-code, telegram, google-sheets, ai, expense-tracking]
keywords: [n8n workflow, tự động hóa chi tiêu, telegram expense tracker, google sheets automation, ai expense categorization]
---

# 💰 Tự động hóa theo dõi chi tiêu qua Telegram với GPT-4 và Google Sheets (học tự động phân loại)

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 30-50% thời gian ghi chép chi tiêu thủ công
- Tự động phân loại chi tiêu chính xác với hệ thống học tự động
- Dữ liệu được lưu trữ cấu trúc trong Google Sheets
- Hỗ trợ nhiều người dùng với phân quyền chi tiêu cá nhân/chung
- Hệ thống xác nhận 2 bước trước khi lưu dữ liệu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
1. Tài khoản Telegram và Chat ID của người dùng
2. Tài khoản Google với Google Sheets API đã kích hoạt
3. API Key từ OpenAI (GPT-4)
4. Tạo 2 bảng Google Sheets với cấu trúc:
   - **EXPENSES**: date, amount, category, description, common_expense, Person
   - **EXPENSE_CATEGORIES**: category, description, examples
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/13667)
2. Chọn "Download" để tải file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**1. Cấu hình Telegram**
- Node **"Telegram - Receive Message"**: Thêm Telegram Credentials
- Node **"Security — Allow Approved Chat IDs"**: Thay thế Chat ID bằng ID của người dùng

**2. Cấu hình Google Sheets**
- Các node liên quan đến Google Sheets:
  - **"Sheets — Load Existing Categories"**
  - **"Sheets — Add Suggested Category"**
  - **"Sheets — Add Edited Category"**
  - **"Sheets — Save Expense"**
- Kết nối với bảng Google Sheets đã tạo trước đó

**3. Cấu hình OpenAI**
- Các node liên quan đến OpenAI:
  - **"AI — Detect Expense Message"**
  - **"AI — Classify Expense Category"**
  - **"AI — Extract Structured Expense Data"**
- Thêm OpenAI Credentials

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để kiểm tra toàn bộ chuỗi xử lý
2. Bật Active workflow sau khi đã cấu hình đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node gửi thông báo qua Slack khi có chi tiêu mới
2. **Báo cáo định kỳ**: Kết hợp với node gửi email báo cáo chi tiêu hàng tháng
3. **Phân tích dữ liệu**: Kết nối với Power BI/Tableau để tạo dashboard chi tiêu
4. **Hỗ trợ nhiều ngôn ngữ**: Thêm node xử lý ngôn ngữ tự nhiên cho các ngôn ngữ khác

### 📌 Kết luận
Workflow này chuyển đổi tin nhắn Telegram thành dữ liệu chi tiêu có cấu trúc, tiết kiệm thời gian và giảm sai sót thủ công. Hệ thống học tự động phân loại giúp cải thiện chính xác độ theo thời gian. Các sếp có thể áp dụng ngay để tối ưu hóa việc quản lý chi tiêu cá nhân hoặc doanh nghiệp.