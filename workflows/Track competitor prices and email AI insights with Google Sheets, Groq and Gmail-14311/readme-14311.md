---
title: "💰 Theo dõi giá và khuyến mãi của đối thủ bằng Google Sheets, Groq và Gmail"
description: "Tự động hóa việc theo dõi giá và khuyến mãi của đối thủ, phân tích bằng AI và gửi báo cáo qua email - giải pháp hoàn hảo cho nghiên cứu thị trường và chiến lược giá"
slug: "theo-doi-gia-khuyen-mai-doi-thu-google-sheets-groq-gmail"
tags: [n8n, automation, no-code, market-research, ai-summarization]
keywords: [n8n workflow, tự động hóa, theo dõi giá, phân tích thị trường, AI, Google Sheets, Groq]
---

# 💰 Theo dõi giá và khuyến mãi của đối thủ bằng Google Sheets, Groq và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải theo dõi giá và khuyến mãi của đối thủ hàng ngày để bảo vệ lợi thế cạnh tranh của mình. Tuy nhiên, việc này thường tốn thời gian và dễ bị lỗi do phải làm thủ công. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến phân tích và báo cáo, giúp tiết kiệm thời gian và nâng cao hiệu quả nghiên cứu thị trường.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình theo dõi giá và khuyến mãi
- Chính xác cao: Sử dụng AI để trích xuất thông tin chính xác từ trang web
- Cá nhân hóa: Phân tích dữ liệu theo nhu cầu cụ thể của doanh nghiệp
- Hoạt động liên tục: Theo dõi 24/7 mà không cần can thiệp
- Báo cáo tự động: Nhận báo cáo thị trường hàng ngày qua email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets đã có dữ liệu sản phẩm và đối thủ cạnh tranh
- API Key của ScraperAPI (để trích xuất dữ liệu từ trang web)
- Tài khoản Groq (để sử dụng mô hình AI phân tích)
- Tài khoản Gmail (để gửi báo cáo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/14311)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Get row(s) in sheet" và "Get row(s) in sheet1"**:
   - Cấu hình Google Sheets credentials
   - Điền ID của Google Sheet chứa dữ liệu sản phẩm và đối thủ
   - Chỉ định tên sheet và phạm vi dữ liệu cần lấy

2. **Node "HTTP Request3"**:
   - Thêm API Key của ScraperAPI vào header Authorization
   - Cấu hình URL của trang web cần trích xuất dữ liệu

3. **Node "Groq Chat Model" và "Groq Chat Model1"**:
   - Cấu hình Groq credentials
   - Chọn mô hình "llama-3.3-70b-versatile"
   - Tùy chỉnh prompt để phù hợp với nhu cầu phân tích

4. **Node "Send a message"**:
   - Cấu hình Gmail credentials
   - Điền địa chỉ email nhận báo cáo
   - Tùy chỉnh nội dung email theo nhu cầu

5. **Node "Schedule Trigger"**:
   - Thiết lập thời gian chạy workflow hàng ngày
   - Có thể điều chỉnh để chạy nhiều lần trong ngày nếu cần

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, click vào nút "Activate" để kích hoạt workflow
2. Chạy thử với dữ liệu mẫu để kiểm tra hoạt động
3. Sau khi xác nhận hoạt động tốt, workflow sẽ tự động chạy theo lịch trình đã thiết lập

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo tức thời khi phát hiện thay đổi giá lớn
2. **Lưu log hoạt động**: Thêm node để lưu lại lịch sử thay đổi giá và khuyến mãi
3. **Báo cáo định kỳ**: Tùy chỉnh để gửi báo cáo tuần/tháng thay vì hàng ngày
4. **Phân tích sâu hơn**: Sử dụng các mô hình AI khác để phân tích xu hướng thị trường dài hạn

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi giá và khuyến mãi của đối thủ, giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả nghiên cứu thị trường. Với khả năng tự động hóa hoàn toàn và tích hợp AI, workflow này là công cụ không thể thiếu cho bất kỳ doanh nghiệp nào muốn duy trì lợi thế cạnh tranh trong thị trường cạnh tranh.