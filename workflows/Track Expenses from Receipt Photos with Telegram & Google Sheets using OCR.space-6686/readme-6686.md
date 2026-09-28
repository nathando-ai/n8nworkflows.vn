---
title: "💰 Tự động theo dõi chi tiêu từ ảnh hóa đơn qua Telegram & Google Sheets với OCR.space"
description: "Hướng dẫn tự động hóa việc ghi chép chi tiêu từ ảnh hóa đơn qua Telegram và Google Sheets bằng công nghệ OCR, tiết kiệm thời gian và giảm lỗi thủ công."
slug: "tu-dong-theo-doi-chi-tieu-tu-anh-hoa-don-telegram-google-sheets"
tags: [n8n, automation, no-code, telegram, google-sheets]
keywords: [n8n workflow, tự động hóa chi tiêu, OCR, Telegram, Google Sheets]
---

# 💰 Tự động theo dõi chi tiêu từ ảnh hóa đơn qua Telegram & Google Sheets với OCR.space

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động ghi chép chi tiêu từ ảnh hóa đơn qua Telegram
- Tiết kiệm thời gian và giảm lỗi thủ công
- Dữ liệu được lưu trữ và quản lý trên Google Sheets
- Nhận thông báo xác nhận qua Telegram
- Hỗ trợ cả văn bản và ảnh hóa đơn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và Google Sheets
- API key của OCR.space (miễn phí cho mức sử dụng cơ bản)
- Tạo bot Telegram và lấy token
- Tạo Google Sheets và lấy ID
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/6686)
2. Copy nội dung JSON
3. Trong n8n Editor, chọn "Import from JSON" và dán nội dung đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Bot (Webhook) node**:
   - Chọn credentials của bot Telegram
   - Điền token bot vào trường "Bot Token"

2. **Google Sheets nodes**:
   - Chọn credentials của Google Sheets
   - Điền Spreadsheet ID của bảng Google Sheets
   - Điền tên sheet vào trường "Sheet Name"

3. **OCR.space Request node**:
   - Điền API key của OCR.space vào trường "API Key"

4. **Parse OCR Data node**:
   - Kiểm tra và điều chỉnh hàm xử lý dữ liệu OCR nếu cần

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi ảnh hóa đơn hoặc văn bản chi tiêu đến bot Telegram
   - Kiểm tra dữ liệu được ghi vào Google Sheets
2. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo
- Thêm chức năng phân loại chi tiêu tự động
- Tích hợp với các ứng dụng kế toán khác
- Thiết lập báo cáo định kỳ từ dữ liệu Google Sheets

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi chi tiêu từ ảnh hóa đơn, tiết kiệm thời gian và giảm lỗi thủ công. Với việc tích hợp Telegram và Google Sheets, dữ liệu được quản lý và truy cập dễ dàng. Hãy thử ngay để tối ưu hóa quá trình quản lý chi tiêu của bạn!