---
title: "🚀 Theo dõi chi tiêu hóa đơn từ Google Drive với GPT-4o và cảnh báo Telegram"
description: "Tự động hóa quy trình xử lý hóa đơn, theo dõi ngân sách và nhận cảnh báo thông minh qua Telegram với công nghệ AI tiên tiến"
slug: "theo-doi-chi-tieu-hoa-don-voi-gpt-4o-va-telegram"
tags: [n8n, automation, no-code, google-drive, telegram, ai, ocr, budget-tracking]
keywords: [n8n workflow, tự động hóa hóa đơn, theo dõi ngân sách, AI xử lý hóa đơn, Telegram cảnh báo, OCR hóa đơn]
---

# 🚀 Theo dõi chi tiêu hóa đơn với GPT-4o và cảnh báo Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quy trình xử lý hóa đơn
- Theo dõi chi tiêu theo danh mục ngân sách
- Nhận cảnh báo thông minh khi chi tiêu vượt ngân sách
- Tiết kiệm thời gian xử lý thủ công lên đến 90%
- Nhận báo cáo tuần/tháng tự động qua Telegram
- Dữ liệu hóa đơn được tổ chức theo tháng trong Google Drive
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập đầy đủ
- Tài khoản Telegram và bot Telegram đã tạo
- API Key từ OpenRouter cho GPT-4o
- Tài khoản Ainoflow và API Key
- Thư mục "Invoices" trong Google Drive để lưu trữ hóa đơn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/13115)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**1. Cấu hình Google Drive:**
- Tạo credentials OAuth2 cho Google Drive theo hướng dẫn [tại đây](https://docs.n8n.io/integrations/builtin/credentials/google/)
- Cấu hình các node Google Drive:
  - DownloadInvoice
  - GetFiles
  - RenameFile
  - SearchMonthFolder
  - CreateMonthFolder
  - MoveToMonth
  - RenameToReview
  - RenameAsDuplicate

**2. Cấu hình Telegram:**
- Tạo bot Telegram theo hướng dẫn [tại đây](https://blog.n8n.io/create-telegram-bot/)
- Cấu hình các node Telegram:
  - BudgetTrigger
  - AlertMessage
  - ErrorAlert
  - SuccessLog
  - DuplicateLog
  - BudgetReply
  - WelcomeMessage
  - NotAuthorizedMessage
  - WeeklySummaryMessage
  - MonthlySummaryMessage

**3. Cấu hình OpenRouter:**
- Tạo API Key từ OpenRouter theo hướng dẫn [tại đây](https://docs.n8n.io/integrations/builtin/credentials/openrouter/)
- Cấu hình các node GPT-4o:
  - Gpt4oCategorizer
  - Gpt4oBudgetAgent

**4. Cấu hình Ainoflow:**
- Tạo tài khoản và API Key từ Ainoflow [tại đây](https://www.ainoflow.io/signup)
- Cấu hình các node HTTP Bearer Auth:
  - OcrExtract
  - CheckInvoiceExists
  - SaveInvoice
  - GetBudgets
  - GetSummary
  - SaveSummary
  - GetWeeklySummary
  - GetMonthlySummary
  - GetAppSettings (3 nodes)
  - GetAppConfig2
  - SaveAppSettings
  - ForEachCategory
  - ForEachCategoryItem
  - DeleteItem
- Cấu hình node MCP Bearer Auth:
  - JsonStorageMcp

**5. Cấu hình các node khác:**
- Trong node **SetDefaults**, chỉnh sửa `allowed_categories` để phù hợp với nhu cầu của bạn
- Trong node **WorkflowConfig**, chỉnh sửa các tham số:
  - `alert_threshold` - ngưỡng cảnh báo ngân sách (mặc định: 80)
  - `review_prefix` - tiền tố cho file cần xem lại
  - `duplicate_prefix` - tiền tố cho file trùng lặp

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Test Workflow" để kiểm tra
2. Gửi lệnh `/start` đến bot Telegram của bạn để đăng ký chat_id
3. Bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm các danh mục ngân sách mới bằng cách chỉnh sửa node **SetDefaults** và gửi lại lệnh `/start`
- Tùy chỉnh các thông báo Telegram bằng cách chỉnh sửa nội dung trong các node Telegram
- Kết hợp với các dịch vụ khác như Slack để nhận cảnh báo
- Thiết lập báo cáo định kỳ theo nhu cầu của bạn
- Sử dụng tính năng "Data Reset" cẩn thận khi cần xóa toàn bộ dữ liệu

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa xử lý hóa đơn, theo dõi ngân sách và nhận cảnh báo thông minh. Với sự kết hợp của công nghệ AI và Telegram, các sếp có thể quản lý chi tiêu một cách hiệu quả và nhanh chóng. Hãy thử ngay và tiết kiệm thời gian quý giá của bạn!