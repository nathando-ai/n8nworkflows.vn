---
title: "🚀 Theo dõi Traffic & Backlinks tự động với Ahrefs API và Google Sheets"
description: "Tự động hóa việc theo dõi traffic và backlinks của website bằng Ahrefs API và lưu kết quả vào Google Sheets - giải pháp hoàn hảo cho SEO và digital marketing"
slug: "theo-doi-traffic-backlinks-tu-dong-voi-ahrefs-google-sheets"
tags: [n8n, automation, no-code, seo, digital-marketing]
keywords: [n8n workflow, tự động hóa, theo dõi traffic, backlinks, google sheets]
---

# 🚀 Theo dõi Traffic & Backlinks tự động với Ahrefs API và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp trong SEO và digital marketing khi phải theo dõi thủ công traffic và backlinks của nhiều website. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian theo dõi thủ công hàng ngày
- Dữ liệu chính xác và cập nhật tự động
- Theo dõi nhiều website cùng lúc
- Hoạt động liên tục 24/7
- Dữ liệu được lưu trữ và phân tích dễ dàng trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Ahrefs API (để lấy dữ liệu traffic và backlinks)
- Tài khoản Google Workspace (để sử dụng Google Sheets API)
- Cấu hình SMTP (để gửi email cảnh báo khi có lỗi)
- Tạo 2 Google Sheets: "Backlink Info" và "Traffic Data"
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8757](https://n8n.io/workflows/8757)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và paste vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Cấu hình form trigger để nhận input domain từ người dùng
   - Đảm bảo trường "Domain" được đặt là bắt buộc

2. **Node "Check Website Traffic API"**:
   - Thêm Ahrefs API credentials
   - Điền URL endpoint của Ahrefs API
   - Cấu hình headers bao gồm:
     ```
     Content-Type: multipart/form-data
     Authorization: Bearer YOUR_AHREFS_API_KEY
     ```

3. **Node "Send Failure Email Alert"**:
   - Thêm SMTP credentials
   - Cấu hình email nhận cảnh báo (ví dụ: seo@congty.com)
   - Tùy chỉnh nội dung email để bao gồm thông tin lỗi

4. **Node "Log Backlinks to Sheet" và "Log Traffic to Sheet"**:
   - Thêm Google API credentials
   - Chỉnh sửa Spreadsheet ID và Sheet Name tương ứng
   - Đảm bảo các cột trong Google Sheets đã được đặt tên đúng:
     - Backlink Info: ascore, referring_domains, total_backlinks
     - Traffic Data: organic_traffic, organic_keywords, organic_keywords_rank

#### 3. Kích hoạt ⚡️
1. Test run với một domain mẫu để kiểm tra kết quả
2. Kiểm tra dữ liệu trong Google Sheets
3. Bật Active workflow sau khi đã kiểm tra và xác nhận hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi có thay đổi đáng kể
- Tạo báo cáo tự động hàng tuần từ dữ liệu trong Google Sheets
- Kết hợp với các công cụ khác như Google Analytics để có cái nhìn toàn diện
- Thiết lập cảnh báo khi có thay đổi đột biến trong traffic hoặc backlinks

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc theo dõi traffic và backlinks của website. Dữ liệu được lưu trữ và phân tích dễ dàng trong Google Sheets, giúp các sếp đưa ra quyết định chiến lược hiệu quả hơn. Hãy thử ngay và nâng cao hiệu suất SEO của bạn!