---
title: "🚀 Tự động hóa tìm kiếm chuyến đi thông minh: Kết hợp vé máy bay và khách sạn từ Skyscanner & Booking.com"
description: "Workflow n8n này tự động tìm kiếm vé máy bay và khách sạn, tạo lịch trình du lịch cá nhân hóa và gửi qua email. Tiết kiệm thời gian lên tới 2-3 giờ mỗi chuyến đi."
slug: "tu-dong-hoa-tim-kiem-chuyen-di-thong-minh"
tags: [n8n, automation, no-code, du lịch, tự động hóa]
keywords: [n8n workflow, tự động hóa du lịch, tìm kiếm vé máy bay, tìm kiếm khách sạn, Skyscanner, Booking.com]
---

# 🚀 Tự động hóa tìm kiếm chuyến đi thông minh: Kết hợp vé máy bay và khách sạn từ Skyscanner & Booking.com

[Các sếp] có bao giờ phải mất 2-3 giờ chỉ để tìm kiếm vé máy bay và khách sạn cho chuyến đi của mình không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài phút, nhận được lịch trình du lịch cá nhân hóa qua email.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình tìm kiếm và so sánh giá vé máy bay và khách sạn.
- **Lịch trình cá nhân hóa**: Nhận được lịch trình du lịch được tối ưu hóa theo ngân sách và sở thích của bạn.
- **Thông tin chính xác**: Dữ liệu được lấy trực tiếp từ các nền tảng hàng đầu như Skyscanner và Booking.com.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi thiết lập.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Skyscanner với API key
- Tài khoản Booking.com với API credentials
- Tài khoản Gmail đã cấu hình OAuth2
- Instance n8n đã cài đặt
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/10354](https://n8n.io/workflows/10354)
3. Hoặc tải file JSON về và import từ local.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **📥 Travel Request Webhook**:
   - Đảm bảo cấu hình đúng path và HTTP method trong node này.
   - Ví dụ: `path: travel-search`, `httpMethod: POST`.

2. **✈️ Search Flights (Skyscanner)**:
   - Thêm Skyscanner API credentials trong n8n.
   - Cấu hình các tham số như `origin`, `destination`, `departureDate`, `returnDate`.

3. **🏨 Search Hotels (Booking.com)**:
   - Thêm Booking.com API credentials trong n8n.
   - Cấu hình các tham số như `destination`, `checkInDate`, `checkOutDate`, `adults`.

4. **✉️ Send via Gmail**:
   - Cấu hình OAuth2 cho tài khoản Gmail.
   - Điền thông tin người nhận email trong node này.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm các API khác như Kiwi, Expedia để mở rộng phạm vi tìm kiếm.
- Tùy chỉnh ngân sách và bộ lọc theo sở thích cá nhân.
- Thêm node để lưu log các yêu cầu tìm kiếm.
- Tích hợp với Slack hoặc Telegram để nhận thông báo khi có kết quả mới.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc tìm kiếm và so sánh giá vé máy bay và khách sạn. Với sự tự động hóa hoàn toàn, các sếp có thể tập trung vào việc chuẩn bị cho chuyến đi của mình thay vì phải mất hàng giờ để tìm kiếm thông tin. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!