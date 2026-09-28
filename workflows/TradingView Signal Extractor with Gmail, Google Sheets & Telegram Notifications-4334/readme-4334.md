---
title: "🚀 Tự động hóa giao dịch: Trích xuất tín hiệu TradingView từ Gmail, Google Sheets & Telegram"
description: "Hướng dẫn tự động hóa quy trình trích xuất tín hiệu giao dịch từ email TradingView, lưu vào Google Sheets và thông báo qua Telegram - giải pháp tiết kiệm thời gian 100% không cần code."
slug: "tu-dong-hoa-giao-dich-tradingview-gmail-google-sheets-telegram"
tags: [n8n, automation, no-code, trading, finance, google-sheets]
keywords: [n8n workflow, tự động hóa giao dịch, tradingview, google sheets, telegram]
---

# 🚀 Tự động hóa giao dịch: Trích xuất tín hiệu TradingView từ Gmail, Google Sheets & Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các nhà giao dịch khi phải theo dõi email thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động trích xuất tín hiệu mua/bán từ email TradingView
- Lưu dữ liệu giao dịch vào Google Sheets với thời gian thực
- Nhận thông báo tức thì qua Telegram
- Tiết kiệm 30-50% thời gian theo dõi thủ công
- Dữ liệu được lưu trữ an toàn và có thể truy xuất bất kỳ lúc nào
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail (đã bật IMAP)
- Tài khoản Google Sheets
- Tài khoản Telegram
- API keys cho các dịch vụ trên (sẽ hướng dẫn chi tiết trong phần cấu hình)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4334](https://n8n.io/workflows/4334)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Email Received" (gmailTrigger)**:
   - Cấu hình credentials: Chọn tài khoản Gmail của bạn
   - Tham số quan trọng: Điền địa chỉ email nhận tín hiệu TradingView

2. **Node "Get Email" (gmail)**:
   - Cấu hình credentials: Chọn tài khoản Gmail của bạn
   - Tham số quan trọng: Để mặc định "get" operation

3. **Node "Verify Mail" (if)**:
   - Cấu hình điều kiện: Chỉ xử lý email có tiêu đề chứa "TradingView Alert"
   - Sử dụng biểu thức: `{{ $node["Email Received"].json["subject"] }}.includes("TradingView Alert")`

4. **Node "Clean Email" (code)**:
   - Không cần cấu hình, node này sẽ tự động xử lý nội dung email

5. **Node "Extract Company Name" (code)**:
   - Không cần cấu hình, node này sẽ tự động trích xuất tên công ty từ email

6. **Node "Google Sheets" (googleSheets)**:
   - Cấu hình credentials: Chọn tài khoản Google Sheets của bạn
   - Tham số quan trọng:
     - Spreadsheet ID: ID của Google Sheet bạn muốn lưu dữ liệu
     - Sheet Name: Tên sheet trong Google Sheet
     - Data to append: `{{ $node["Extract Company Name"].json }}`

7. **Node "Send Message" (telegram)**:
   - Cấu hình credentials: Chọn tài khoản Telegram của bạn
   - Tham số quan trọng:
     - Chat ID: ID của chat Telegram bạn muốn nhận thông báo
     - Message: `{{ $node["Extract Company Name"].json["message"] }}`

8. **Node "Current Date & Time" (dateTime)**:
   - Không cần cấu hình, node này sẽ tự động lấy thời gian hiện tại

9. **Node "Formatted Date & Time" (dateTime)**:
   - Tham số quan trọng: Format: "YYYY-MM-DD HH:mm:ss"

10. **Node "Gmail" (gmail)**:
    - Cấu hình credentials: Chọn tài khoản Gmail của bạn
    - Tham số quan trọng: Operation: "markAsRead"

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với email mẫu
2. Sau khi test thành công, click vào nút "Activate" để bật workflow
3. Workflow sẽ tự động chạy mỗi khi nhận được email tín hiệu từ TradingView

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập thông báo chỉ cho tín hiệu mua/bán mạnh (ví dụ: chỉ thông báo khi tín hiệu có xác suất > 80%)
- Kết hợp với workflow khác để tự động thực hiện giao dịch khi nhận tín hiệu
- Thêm node để lưu log các giao dịch vào Google Sheets
- Thiết lập báo cáo định kỳ về hiệu suất giao dịch
- Kết nối với các sàn giao dịch khác để tự động thực hiện lệnh mua/bán

### 📌 Kết luận
Workflow này giúp các nhà giao dịch tiết kiệm thời gian đáng kể trong việc theo dõi và xử lý tín hiệu giao dịch. Bằng cách tự động hóa quy trình này, bạn có thể tập trung vào phân tích và quyết định giao dịch thay vì phải theo dõi email thủ công. Hãy thử ngay và nâng cao hiệu suất giao dịch của bạn!