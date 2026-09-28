---
title: "🔍 Tự động hóa Skip Trace với ScraperCity và lưu kết quả vào Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tìm kiếm thông tin người dùng bằng ScraperCity và lưu kết quả vào Google Sheets bằng n8n"
slug: "tu-dong-hoa-skip-trace-voi-scrapercity-va-google-sheets"
tags: [n8n, automation, no-code, lead generation, web scraping]
keywords: [n8n workflow, tự động hóa, skip trace, lead generation, web scraping]
---

# 🔍 Tự động hóa Skip Trace với ScraperCity và lưu kết quả vào Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quá trình tìm kiếm thông tin người dùng
- Chính xác: Lấy dữ liệu từ nguồn đáng tin cậy như ScraperCity
- Cá nhân hóa: Xử lý dữ liệu theo nhu cầu cụ thể của từng doanh nghiệp
- Hoạt động liên tục: Chạy 24/7 mà không cần can thiệp thủ công
- Tích hợp dễ dàng: Kết nối liền mạch với Google Sheets cho báo cáo và phân tích
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScraperCity với API Key
- Tài khoản Google với quyền truy cập Google Sheets
- Dữ liệu đầu vào (tên, số điện thoại hoặc email cần tìm kiếm)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/13883](https://n8n.io/workflows/13883)
3. Hoặc tải file JSON từ link trên và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Configure Search Inputs"**:
   - Chỉnh sửa dữ liệu đầu vào trong node này với danh sách tên, số điện thoại hoặc email cần tìm kiếm, cách nhau bởi dấu phẩy

2. **Node "Submit Skip Trace Job"**:
   - Tạo một credential mới loại "HTTP Header Auth" với tên "ScraperCity API Key"
   - Đặt header là "Authorization" và value là "Bearer YOUR_KEY" (thay YOUR_KEY bằng API Key của bạn)

3. **Node "Write Results to Google Sheets"**:
   - Tạo một credential Google Sheets OAuth2
   - Chỉnh sửa ID của Google Sheet trong node này
   - Đảm bảo rằng tài khoản Google có quyền truy cập vào sheet này

#### 3. Kích hoạt ⚡️
1. Nhấn "Execute workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheets của bạn
3. Sau khi xác nhận hoạt động đúng, bạn có thể kích hoạt workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log các lần chạy để theo dõi hiệu suất
- Tạo báo cáo định kỳ từ dữ liệu thu thập được
- Kết nối với các công cụ CRM khác để tự động cập nhật thông tin liên hệ

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong quá trình tìm kiếm thông tin người dùng. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong kinh doanh. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!