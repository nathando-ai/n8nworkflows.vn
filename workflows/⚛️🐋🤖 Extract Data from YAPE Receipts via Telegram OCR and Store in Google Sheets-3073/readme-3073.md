---
title: "⚛️🐋🤖 Tự động hóa hóa đơn YAPE qua Telegram OCR và lưu vào Google Sheets"
description: "Hướng dẫn tự động hóa trích xuất dữ liệu từ hóa đơn YAPE qua Telegram OCR và lưu vào Google Sheets bằng n8n - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-hoa-hoa-don-yape-qua-telegram-ocr-va-luu-vao-google-sheets"
tags: [n8n, automation, no-code, finance, ai]
keywords: [n8n workflow, tự động hóa, trích xuất hóa đơn, OCR, Google Sheets, Telegram]
---

# ⚛️🐋🤖 Tự động hóa hóa đơn YAPE qua Telegram OCR và lưu vào Google Sheets

[Các sếp đang mệt mỏi với việc phải nhập tay dữ liệu từ hóa đơn YAPE? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ nhận ảnh hóa đơn đến lưu dữ liệu vào Google Sheets chỉ trong vài giây!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** nhập liệu thủ công
- Dữ liệu được trích xuất **chính xác 100%** nhờ công nghệ OCR tiên tiến
- Tự động lưu trữ dữ liệu vào Google Sheets **liên tục 24/7**
- Nhận kết quả phân tích **tự động qua Telegram** ngay sau khi xử lý
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **Telegram Bot** (cần lấy API Token)
- Tài khoản **Google Cloud** với quyền truy cập Google Drive và Google Sheets
- **OpenAI API Key** (hoặc DeepSeek API Key nếu sử dụng model này)
- **Google Sheets** đã tạo sẵn để lưu dữ liệu (cần ID của sheet)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/3073)
2. Click vào nút **"Download"** để tải file JSON
3. Trong n8n Editor, click vào **"Import from File"** và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **🛎️Telegram Listener**:
   - Cấu hình credentials cho Telegram Bot
   - Điền **Telegram Bot Token** đã lấy từ BotFather

2. **📄 Extract Text with OCR**:
   - Chọn credentials cho OpenAI (hoặc DeepSeek nếu sử dụng model này)
   - Điền **OpenAI API Key** vào trường tương ứng
   - Tùy chỉnh prompt nếu cần (mặc định đã được tối ưu cho trích xuất hóa đơn)

3. **🔍 Find Google Sheet in Drive**:
   - Cấu hình credentials cho Google Drive
   - Điền **Google Sheet ID** của sheet cần lưu dữ liệu

4. **📑 Insert Data into Google Sheets**:
   - Đảm bảo sheet đã có các cột phù hợp với dữ liệu trích xuất
   - Kiểm tra lại tên sheet trong trường "Sheet Name"

#### 3. Kích hoạt ⚡️
1. Click vào nút **"Execute Workflow"** để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Google Sheets và Telegram
3. Sau khi test thành công, click vào **"Activate"** để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack**: Thêm node Slack để nhận thông báo khi có hóa đơn mới
2. **Lưu log xử lý**: Thêm node lưu log vào Google Sheets để theo dõi lịch sử xử lý
3. **Xử lý nhiều loại hóa đơn**: Mở rộng workflow để xử lý nhiều định dạng hóa đơn khác nhau
4. **Gửi báo cáo định kỳ**: Thêm node gửi báo cáo tổng hợp dữ liệu hàng tuần qua email

### 📌 Kết luận
Workflow này đã giúp các sếp tự động hóa hoàn toàn quy trình xử lý hóa đơn YAPE, tiết kiệm thời gian đáng kể và giảm thiểu lỗi nhập liệu. Hãy thử ngay và trải nghiệm sức mạnh của tự động hóa với n8n!