```yaml
---
title: "🚀 Tự động hóa đồng bộ và phân tích kết nối LinkedIn hàng tuần với Apify và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ và phân tích kết nối LinkedIn hàng tuần, tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-hoa-dong-bo-phan-tich-ket-noi-linkedin-hang-tuan"
tags: [n8n, automation, no-code, LinkedIn, Google Sheets]
keywords: [n8n workflow, tự động hóa, LinkedIn, Google Sheets, Apify]
---
```

# 🚀 Tự động hóa đồng bộ và phân tích kết nối LinkedIn hàng tuần với Apify và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải theo dõi thủ công kết nối LinkedIn hàng tuần. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ và phân tích kết nối LinkedIn hàng tuần mà không cần can thiệp thủ công.
- Chính xác: Dữ liệu được cập nhật và xử lý tự động, giảm thiểu lỗi con người.
- Cá nhân hóa: Phân tích dữ liệu kết nối theo nhu cầu cụ thể của doanh nghiệp.
- Hoạt động liên tục: Workflow chạy tự động vào mỗi Chủ Nhật lúc 2 giờ sáng, đảm bảo dữ liệu luôn mới nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apify với API key để scrape dữ liệu từ LinkedIn.
- Tài khoản Google với quyền truy cập vào Google Sheets để lưu trữ dữ liệu.
- Credentials cho các node Google Sheets và HTTP Request trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/8041](https://n8n.io/workflows/8041).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Weekly Sync (Sunday 2AM)"**: Đảm bảo cron schedule được đặt chính xác để chạy vào Chủ Nhật lúc 2 giờ sáng.
- **Node "Start LinkedIn Scrape"**: Cấu hình HTTP Request với URL và API key của Apify để bắt đầu quá trình scrape.
- **Node "Extract Run ID"**: Kiểm tra và chỉnh sửa code để trích xuất Run ID từ phản hồi của Apify.
- **Node "Check Scrape Status"**: Cập nhật URL và API key để kiểm tra trạng thái của quá trình scrape.
- **Node "Get Scraped Data"**: Đảm bảo URL và API key được cấu hình chính xác để lấy dữ liệu đã scrape.
- **Node "Process Connections Data"**: Chỉnh sửa code để xử lý dữ liệu kết nối theo nhu cầu cụ thể của bạn.
- **Node "Clear Existing Data"**: Cấu hình Google Sheets với Spreadsheet ID và tên Sheet để xóa dữ liệu cũ.
- **Node "Save Connections to Sheets"**: Cập nhật Spreadsheet ID và tên Sheet để lưu trữ dữ liệu mới.
- **Node "Generate Sync Summary"**: Chỉnh sửa code để tạo báo cáo tổng kết đồng bộ.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để chạy tự động hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi đồng bộ hoàn thành.
- Lưu log hoạt động của workflow để theo dõi hiệu suất.
- Gửi báo cáo định kỳ qua email để theo dõi tiến độ kết nối hàng tuần.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả làm việc bằng cách tự động hóa việc đồng bộ và phân tích kết nối LinkedIn hàng tuần. Hãy áp dụng ngay để tối ưu hóa quá trình quản lý mạng lưới kết nối của bạn!