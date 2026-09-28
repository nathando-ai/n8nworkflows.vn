---
title: "🚀 Tự động hóa tìm kiếm xu hướng YouTube với n8n - Giải pháp nghiên cứu thị trường không cần code"
description: "Hướng dẫn chi tiết cách tự động hóa tìm kiếm xu hướng YouTube bằng n8n, tiết kiệm thời gian và phát hiện nội dung hot nhanh chóng"
slug: "tu-dong-hoa-tim-kiem-xu-huong-youtube-voi-n8n"
tags: [n8n, automation, no-code, youtube, google-sheets]
keywords: [n8n workflow, tự động hóa, youtube trends, nghiên cứu thị trường, no-code]
---

# 🚀 Tự động hóa tìm kiếm xu hướng YouTube với n8n - Giải pháp nghiên cứu thị trường không cần code

[Bài viết này sẽ giúp các sếp tiết kiệm hàng giờ mỗi ngày khi tìm kiếm xu hướng YouTube thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ tìm kiếm đến phân tích và báo cáo, chỉ với vài bước cấu hình đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **hàng giờ mỗi ngày** khi không cần tìm kiếm xu hướng thủ công
- Phát hiện **nội dung hot** nhanh chóng với bộ lọc thông minh
- Tự động hóa **báo cáo xu hướng** vào Google Sheets
- Lấy dữ liệu **chính xác và cập nhật liên tục**
- Tiết kiệm **chi phí quảng cáo** bằng cách tập trung vào nội dung có tiềm năng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập YouTube Data API
- Tài khoản Google với quyền truy cập Google Sheets API
- API Key từ Google Cloud Console (YouTube Data API v3)
- OAuth2 Credentials cho cả YouTube và Google Sheets
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7888](https://n8n.io/workflows/7888)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission" (Form Trigger)**:
   - Chỉnh sửa các trường nhập liệu (Topic Name, Last How Many Days) theo nhu cầu của các sếp
   - Thêm các trường tùy chỉnh nếu cần thiết

2. **Node "Get many videos" (YouTube)**:
   - Thêm YouTube OAuth2 credentials
   - Cập nhật `regionCode` nếu muốn tìm kiếm theo khu vực khác (mặc định là "US")

3. **Node "Get Data" (HTTP Request)**:
   - Thay thế `Your Project API Key` bằng API Key thực tế từ Google Cloud Console

4. **Node "Create spreadsheet" và "Append row in sheet" (Google Sheets)**:
   - Thêm Google Sheets OAuth2 credentials
   - Cập nhật tên sheet và cấu trúc dữ liệu theo nhu cầu

5. **Node "Engagement Rate Check" (If)**:
   - Điều chỉnh ngưỡng engagement rate (mặc định 2%) theo tiêu chuẩn chất lượng của các sếp

6. **Node "If"**:
   - Cập nhật các điều kiện lọc video (views tối thiểu, thời gian, loại bỏ tiêu đề chứa hashtag...)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn nút "Execute Node" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Google Sheets
3. Bật chế độ "Active" để workflow chạy tự động khi có dữ liệu mới

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node gửi thông báo khi phát hiện xu hướng mới
2. **Lịch sử tìm kiếm**: Lưu trữ các tìm kiếm trước đó để so sánh xu hướng
3. **Báo cáo định kỳ**: Tự động gửi báo cáo hàng tuần/tháng qua email
4. **Phân tích sâu hơn**: Kết hợp với các công cụ phân tích dữ liệu khác như Google Analytics

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày khi tìm kiếm xu hướng YouTube thủ công. Với khả năng tự động hóa toàn bộ quy trình từ tìm kiếm đến phân tích và báo cáo, các sếp có thể tập trung vào những việc quan trọng hơn. Hãy thử ngay và bắt đầu phát hiện nội dung hot một cách nhanh chóng và hiệu quả!