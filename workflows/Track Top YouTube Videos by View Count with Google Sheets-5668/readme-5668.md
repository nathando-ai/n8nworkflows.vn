---
title: "📊 Tự động theo dõi video YouTube hàng đầu theo lượt xem và lưu vào Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa việc theo dõi video YouTube hàng đầu theo lượt xem và lưu kết quả vào Google Sheets với n8n"
slug: "tu-dong-theo-doi-video-youtube-hang-dau-theo-luot-xem"
tags: [n8n, automation, no-code, youtube, google-sheets]
keywords: [n8n workflow, tự động hóa, youtube api, google sheets, phân tích thị trường]
---

# 📊 Tự động theo dõi video YouTube hàng đầu theo lượt xem và lưu vào Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc theo dõi nội dung YouTube hàng đầu
- Dữ liệu được cập nhật tự động vào Google Sheets hàng ngày
- Có thể phân tích xu hướng thị trường dễ dàng hơn
- Tự động hóa hoàn toàn quá trình theo dõi nội dung
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- API Key của YouTube Data API v3
- Google Sheet đã được thiết lập theo mẫu
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấp vào biểu tượng "+" ở góc trái màn hình
3. Chọn "Import from URL"
4. Dán link sau vào ô nhập liệu: https://n8n.io/workflows/5668
5. Nhấp vào "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When clicking ‘Execute workflow’" (manualTrigger)**
   - Node này sẽ kích hoạt workflow khi bạn nhấp vào nút "Execute workflow"

2. **Node "Fetch Most-Viewed Videos via YouTube API" (httpRequest)**
   - Thay thế `YOUR_YOUTUBE_API_KEY` bằng API Key của bạn
   - Đảm bảo bạn đã kích hoạt YouTube Data API v3 trong Google Cloud Console

3. **Node "Read Channel Info from Sheet" (googleSheets)**
   - Chọn credential Google Sheets của bạn
   - Nhập Spreadsheet ID của Google Sheet của bạn
   - Nhập tên của Input Sheet (thường là "Input")

4. **Node "Append Video Details to Sheet" (googleSheets)**
   - Chọn credential Google Sheets của bạn
   - Nhập Spreadsheet ID của Google Sheet của bạn
   - Nhập tên của Output Sheet (thường là "Output")

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Execute workflow" để kiểm tra workflow
2. Kiểm tra kết quả trong Google Sheet của bạn
3. Nếu mọi thứ hoạt động tốt, bạn có thể kích hoạt workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập lịch chạy tự động hàng ngày để cập nhật dữ liệu mới nhất
- Kết hợp với các công cụ phân tích dữ liệu khác để có cái nhìn sâu hơn về xu hướng thị trường
- Thêm thông báo qua email hoặc Slack khi có video mới nổi bật
- Tạo báo cáo định kỳ dựa trên dữ liệu được thu thập

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi nội dung YouTube hàng đầu. Bằng cách tự động hóa quá trình này, bạn có thể tập trung vào việc phân tích dữ liệu và đưa ra quyết định kinh doanh tốt hơn. Hãy thử ngay và trải nghiệm lợi ích của tự động hóa!