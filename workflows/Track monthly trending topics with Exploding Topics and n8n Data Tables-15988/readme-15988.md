---
title: "🚀 Theo dõi xu hướng hàng tháng với Exploding Topics và n8n Data Tables"
description: "Tự động hóa việc theo dõi xu hướng thị trường hàng tháng với Exploding Topics API và n8n Data Tables - tiết kiệm thời gian và tối ưu hóa quy trình nghiên cứu thị trường"
slug: "theo-doi-xu-huong-hang-thang-voi-exploding-topics-va-n8n-data-tables"
tags: [n8n, automation, no-code, market-research, trend-analysis]
keywords: [n8n workflow, tự động hóa thị trường, phân tích xu hướng, Exploding Topics API, n8n Data Tables]
---

# 🚀 Theo dõi xu hướng hàng tháng với Exploding Topics và n8n Data Tables

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi xu hướng thị trường thủ công hàng tháng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động cập nhật xu hướng hàng tháng mà không cần can thiệp thủ công
- Dữ liệu chính xác: Lấy thông tin từ API uy tín của Exploding Topics
- Dễ quản lý: Lưu trữ và cập nhật dữ liệu trong bảng dữ liệu n8n
- Tránh trùng lặp: Hệ thống tự động nhận biết và cập nhật xu hướng đã có
- Tích hợp linh hoạt: Có thể kết nối với các công cụ khác trong hệ sinh thái n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Exploding Topics Pro (để lấy API key)
- Quyền truy cập vào n8n Editor
- (Tùy chọn) Tài khoản email để nhận báo cáo (nếu mở rộng workflow)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15988)
2. Chọn "Import" và sao chép JSON vào n8n Editor
3. Hoặc tải file JSON về máy và import trực tiếp trong n8n

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Configure API Parameters** node:
   - Thay thế `YOUR_EXPLODING_TOPICS_API_KEY` bằng API key thực của bạn
   - Cập nhật các tham số khác theo nhu cầu:
     - `type`: Chọn loại xu hướng (`exploding`, `all`, v.v.)
     - `categories`: Chọn lĩnh vực quan tâm (`technology`, `health`, v.v.)
     - `sort`: Cài đặt thứ tự sắp xếp (`growth`, `popularity`, v.v.)
     - `timeframe`: Thời gian theo dõi (ví dụ: `12` tháng)
     - `limit`: Số lượng xu hướng trả về (ví dụ: `50`)

2. **Monthly Schedule Trigger** node:
   - Cấu hình lịch chạy hàng tháng (nếu cần thay đổi tần suất)

3. **Save or Update Trends in Data Table** node:
   - Đảm bảo tên bảng dữ liệu là `Monthly Trending Topics` hoặc thay đổi theo ý muốn

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết nối API
2. Kích hoạt workflow bằng cách bật nút Active
3. Đợi đến ngày đầu tiên của tháng tiếp theo để xem kết quả đầu tiên

### ✍️ Mẹo & gợi ý nâng cao
1. Kết nối với Slack/Teams để nhận thông báo khi có xu hướng mới
2. Thêm node gửi email báo cáo hàng tháng
3. Tích hợp với Google Sheets để chia sẻ dữ liệu với nhóm
4. Thiết lập cảnh báo khi phát hiện xu hướng đột biến

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi xu hướng thị trường hàng tháng. Với cấu hình đơn giản và kết quả tự động cập nhật, đây là công cụ lý tưởng cho các chuyên gia nghiên cứu thị trường. Hãy thử ngay và tối ưu hóa quy trình phân tích của bạn!