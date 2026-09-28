---
title: "📊 Tự động hóa theo dõi thị trường bất động sản Idealista hàng tuần và gửi báo cáo Google Sheets"
description: "Workflow n8n tự động thu thập dữ liệu thị trường bất động sản từ Idealista, phân tích và gửi báo cáo Google Sheets hàng tuần - giải pháp chuyên nghiệp cho nhà đầu tư bất động sản"
slug: "tu-dong-hoa-theo-doi-thi-truong-idealista"
tags: [n8n, automation, no-code, real-estate, market-research]
keywords: [n8n workflow, tự động hóa bất động sản, phân tích thị trường, Idealista, Google Sheets]
---

# 📊 Tự động hóa theo dõi thị trường bất động sản Idealista hàng tuần và gửi báo cáo Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của nhà đầu tư bất động sản khi phải theo dõi thị trường thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho việc thu thập và phân tích dữ liệu thị trường
- Nhận báo cáo định kỳ với các chỉ số thống kê chuyên nghiệp (giá trung bình, giá/m², diện tích trung bình...)
- Theo dõi xu hướng thị trường qua dữ liệu lịch sử trong Google Sheets
- Tự động hóa hoàn toàn quy trình phân tích thị trường bất động sản
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apify API ([lấy token tại đây](https://console.apify.com/account/integrations))
- Tài khoản Gmail (đã cấu hình OAuth2)
- Google Sheet với tab tên "MarketHistory"
- Tài khoản n8n đã cài đặt node cộng đồng `n8n-nodes-idealista-scraper`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15008)
2. Click "Copy JSON" và lưu file JSON vào máy
3. Trong n8n Editor, click "Import from File" và chọn file JSON đã lưu

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Every Monday 8am"**:
   - Đảm bảo múi giờ của n8n đã được cấu hình đúng (UTC+1 cho Tây Ban Nha)
   - Kiểm tra lịch trình thực thi hàng tuần

2. **Nodes "Scrape Madrid" và "Scrape Barcelona"**:
   - Đảm bảo đã thêm credential Apify API
   - Có thể thay đổi tham số `operation` từ "sale" sang "rent" để theo dõi thị trường cho thuê
   - Có thể điều chỉnh số lượng trang thu thập (mặc định là 3 trang)

3. **Nodes "Analyze Madrid" và "Analyze Barcelona"**:
   - Kiểm tra logic tính toán trong code node (giá trung bình, giá/m², diện tích trung bình...)
   - Có thể thêm các chỉ số phân tích mới nếu cần

4. **Node "Email Report"**:
   - Thêm credential Gmail
   - Cập nhật địa chỉ email nhận báo cáo
   - Có thể tùy chỉnh nội dung email trong code node "Build HTML Report"

5. **Node "Log to Market History"**:
   - Thêm credential Google Sheets
   - Đảm bảo Google Sheet có tab "MarketHistory" với cấu trúc phù hợp
   - Kiểm tra định dạng dữ liệu khi ghi vào Google Sheets

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra email nhận báo cáo và Google Sheets cập nhật dữ liệu
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm thành phố mới**: Sao chép cặp node "Scrape" + "Analyze" và cấu hình cho thành phố mới (Valencia, Rome, Lisbon, Milan...)
2. **Phân tích thị trường chi tiết hơn**: Thêm bộ lọc giá để tập trung vào các phân khúc cụ thể (nhà cao cấp >1 triệu EUR, nhà giá rẻ <200.000 EUR)
3. **Tính toán tỷ suất sinh lời**: Thu thập dữ liệu cả bán và cho thuê cho cùng một khu vực
4. **Tích hợp Slack/Telegram**: Thêm node gửi thông báo qua Slack hoặc Telegram khi giá bất động sản thay đổi đáng kể

### 📌 Kết luận
Workflow này giúp các nhà đầu tư bất động sản tiết kiệm thời gian quý giá và nhận được báo cáo thị trường chuyên nghiệp hàng tuần. Bằng cách tự động hóa quy trình phân tích thị trường, các sếp có thể đưa ra quyết định đầu tư thông minh hơn và theo dõi xu hướng thị trường một cách liên tục. Hãy thử ngay và nâng cấp chiến lược đầu tư bất động sản của bạn!