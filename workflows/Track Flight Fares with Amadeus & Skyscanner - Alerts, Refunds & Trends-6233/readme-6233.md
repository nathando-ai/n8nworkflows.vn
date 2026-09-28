---
title: "🚀 Theo dõi giá vé máy bay với Amadeus & Skyscanner - Cảnh báo, hoàn tiền & xu hướng"
description: "Tự động theo dõi giá vé máy bay, cảnh báo khi giá giảm, kiểm tra hoàn tiền và phân tích xu hướng giá với workflow n8n hoàn toàn không cần code"
slug: "theo-doi-gia-ve-may-bay-voi-amadeus-skyscanner"
tags: [n8n, automation, no-code, travel, market-research]
keywords: [n8n workflow, tự động hóa giá vé, cảnh báo giá vé, hoàn tiền vé máy bay, phân tích xu hướng giá vé]
---

# 🚀 Theo dõi giá vé máy bay với Amadeus & Skyscanner - Cảnh báo, hoàn tiền & xu hướng

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải theo dõi giá vé máy bay hàng ngày? Khi giá vé giảm đột ngột, các sếp phải nhanh chóng hành động để không bỏ lỡ cơ hội tốt. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi giá vé, cảnh báo khi giá giảm, kiểm tra hoàn tiền và phân tích xu hướng giá - tất cả đều không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động theo dõi giá vé hàng ngày mà không cần can thiệp thủ công.
- **Cảnh báo tức thì**: Nhận thông báo ngay khi giá vé giảm đáng kể.
- **Kiểm tra hoàn tiền**: Tự động kiểm tra và xử lý hoàn tiền khi có cơ hội.
- **Phân tích xu hướng**: Dữ liệu lịch sử giá vé để đưa ra quyết định thông minh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản PostgreSQL để lưu trữ dữ liệu vé.
- API keys từ Amadeus và Skyscanner.
- Tài khoản email/SMS (Twilio, SMTP) để gửi cảnh báo.
- Webhook URL từ Slack để thông báo nhóm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6233](https://n8n.io/workflows/6233)
2. Click vào nút "Import" để tải file JSON về máy.
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Fare Check Trigger**: Cấu hình lịch chạy (ví dụ: hàng ngày lúc 8h sáng).
- **Get Tracked Bookings**: Cấu hình kết nối PostgreSQL và truy vấn dữ liệu vé đã theo dõi.
- **Prepare Fare Search**: Chỉnh sửa mã JavaScript để chuẩn bị tham số tìm kiếm giá vé.
- **Search Current Fares**: Cấu hình API credentials từ Skyscanner.
- **Analyze Fare Drops**: Chỉnh sửa mã JavaScript để xác định mức giảm giá đáng kể.
- **Update Fare Tracking**: Cập nhật kết nối PostgreSQL để lưu trữ dữ liệu giá vé mới.
- **Send Fare Drop Email**: Cấu hình API email (SMTP) và template email cảnh báo.
- **Send SMS Alert**: Cấu hình API SMS (Twilio) và nội dung tin nhắn cảnh báo.
- **Notify Slack Team**: Cấu hình webhook URL từ Slack để gửi thông báo nhóm.
- **Initiate Refund Process**: Cấu hình API hoàn tiền từ nhà cung cấp dịch vụ.

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu.
2. Kiểm tra các cảnh báo được gửi đến email, SMS và Slack.
3. Bật Active workflow để chạy tự động theo lịch đã cấu hình.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log hoạt động của workflow.
- Kết hợp với Google Sheets để lưu trữ và phân tích dữ liệu lịch sử giá vé.
- Tạo báo cáo định kỳ về xu hướng giá vé và gửi đến email của các sếp.
- Kết nối với các nền tảng đặt vé khác để mở rộng phạm vi tìm kiếm giá vé.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian, tối ưu hóa chi phí du lịch và luôn nắm bắt cơ hội tốt nhất. Hãy áp dụng ngay để tự động hóa toàn bộ quá trình theo dõi giá vé và không bỏ lỡ bất kỳ cơ hội nào!