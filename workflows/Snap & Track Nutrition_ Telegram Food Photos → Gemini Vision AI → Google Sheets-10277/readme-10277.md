---
title: "🍽️ Tự động hóa theo dõi dinh dưỡng từ ảnh thức ăn qua Telegram và AI Gemini"
description: "Hướng dẫn chi tiết cách tự động hóa việc ghi nhận thông tin dinh dưỡng từ ảnh thức ăn qua Telegram, xử lý bằng AI Gemini và lưu vào Google Sheets - tiết kiệm thời gian và nâng cao sức khỏe"
slug: "tu-dong-hoa-theo-doi-dinh-duong-tu-anh-thuc-an"
tags: [n8n, automation, no-code, telegram, google-sheets, ai, gemini]
keywords: [n8n workflow, tự động hóa, theo dõi dinh dưỡng, google sheets, gemini ai, telegram bot]
---

# 🍽️ Tự động hóa theo dõi dinh dưỡng từ ảnh thức ăn qua Telegram và AI Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết không? Theo dõi dinh dưỡng hàng ngày thông qua ảnh thức ăn là một trong những thói quen quan trọng nhất để duy trì sức khỏe. Tuy nhiên, việc chụp ảnh, phân tích và ghi nhận thông tin thủ công lại tốn rất nhiều thời gian và công sức. Đó chính là lúc mà workflow này ra đời để giải quyết triệt để vấn đề này!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ chụp ảnh đến ghi nhận dữ liệu
- **Chính xác cao**: Sử dụng AI Gemini để phân tích hình ảnh và tính toán dinh dưỡng
- **Dễ theo dõi**: Tất cả dữ liệu được lưu trữ và cập nhật tự động trong Google Sheets
- **Tích hợp hoàn hảo**: Kết nối liền mạch giữa Telegram, AI và Google Workspace
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và một bot được tạo qua @BotFather
- API key của Google Gemini với tính năng Vision được kích hoạt
- Tài khoản Google để truy cập Google Sheets và Google Drive
- Một Google Sheet để lưu trữ dữ liệu dinh dưỡng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể:
1. Truy cập [link workflow gốc](https://n8n.io/workflows/10277)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

Hoặc các sếp cũng có thể copy/paste JSON từ trang workflow gốc vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Trigger** (Node đầu tiên):
   - Cần cấu hình credentials cho Telegram API
   - Đảm bảo bot token được nhập chính xác
   - Kích hoạt workflow sau khi cấu hình xong

2. **Google Gemini Chat Model** và **Analyze an image**:
   - Cần cấu hình credentials cho Google Palm API
   - Đảm bảo API key có quyền truy cập vào Google Gemini Vision
   - Có thể điều chỉnh prompt trong node này để phù hợp với nhu cầu cụ thể

3. **Append row in sheet**:
   - Cần cấu hình credentials cho Google Sheets OAuth2 API
   - Chọn Google Sheet đã tạo trước đó
   - Đảm bảo tên cột trong sheet khớp với dữ liệu đầu ra của workflow

4. **Upload file**:
   - Cần cấu hình credentials cho Google Drive OAuth2 API
   - Chọn thư mục trong Google Drive để lưu ảnh thức ăn
   - Đảm bảo tài khoản Google có quyền truy cập vào thư mục này

#### 3. Kích hoạt ⚡️
- Sau khi cấu hình xong tất cả các node quan trọng, các sếp nên:
1. Test run với dữ liệu mẫu để kiểm tra toàn bộ quy trình
2. Kiểm tra:
   - Ảnh được lưu vào Google Drive
   - Dữ liệu được ghi vào Google Sheets
   - Bot Telegram trả lời đúng với thông tin dinh dưỡng
3. Bật Active workflow sau khi đã kiểm tra và xác nhận mọi thứ hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Teams**: Thêm node để gửi thông báo dinh dưỡng hàng ngày đến kênh Slack/Teams
- **Báo cáo định kỳ**: Tạo một node mới để tổng hợp dữ liệu dinh dưỡng hàng tuần và gửi email báo cáo
- **Nhắc nhở uống nước**: Kết hợp với một bot nhắc nhở uống nước để tạo thói quen tốt hơn
- **Phân tích dữ liệu**: Sử dụng Google Data Studio để tạo báo cáo trực quan từ dữ liệu dinh dưỡng

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn nâng cao đáng kể chất lượng theo dõi dinh dưỡng hàng ngày. Với sự kết hợp hoàn hảo giữa Telegram, AI Gemini và Google Workspace, các sếp có thể dễ dàng theo dõi và phân tích thông tin dinh dưỡng một cách khoa học và hiệu quả. Hãy áp dụng ngay để cải thiện sức khỏe và hiệu suất làm việc của mình!