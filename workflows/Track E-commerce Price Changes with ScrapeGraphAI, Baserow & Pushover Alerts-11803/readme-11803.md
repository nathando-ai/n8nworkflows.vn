---
title: "🚀 Theo dõi giá sản phẩm E-commerce với ScrapeGraphAI, Baserow & Pushover Alerts"
description: "Hướng dẫn tự động hóa theo dõi giá sản phẩm E-commerce với n8n, ScrapeGraphAI, Baserow và Pushover Alerts. Tiết kiệm thời gian, nhận thông báo tức thì về giá giảm."
slug: "theo-doi-gia-san-pham-ecommerce-voi-scrapegraphai-baserow-pushover"
tags: [n8n, automation, no-code, ecommerce, market-research]
keywords: [n8n workflow, tự động hóa, theo dõi giá, ecommerce, scrapegraphai]
---

# 🚀 Theo dõi giá sản phẩm E-commerce với ScrapeGraphAI, Baserow & Pushover Alerts

[Các sếp đang làm việc với nhiều sản phẩm E-commerce khác nhau? Bạn mệt mỏi với việc phải kiểm tra giá thủ công mỗi ngày? Hãy để n8n và ScrapeGraphAI giúp bạn theo dõi giá sản phẩm một cách tự động và thông minh. Workflow này sẽ giúp bạn nhận thông báo tức thì về giá giảm, lưu lịch sử giá và quản lý dữ liệu một cách hiệu quả.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải kiểm tra giá thủ công mỗi ngày.
- **Nhận thông báo tức thì**: Nhận cảnh báo ngay khi giá sản phẩm giảm.
- **Lưu lịch sử giá**: Dữ liệu giá được lưu trữ và quản lý một cách hiệu quả.
- **Quản lý dữ liệu**: Dữ liệu được lưu trữ trong Baserow để dễ dàng truy cập và phân tích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScrapeGraphAI API (để lấy dữ liệu sản phẩm).
- Tài khoản Baserow API (để lưu trữ dữ liệu).
- Tài khoản Pushover (để nhận thông báo).
- Danh sách sản phẩm và ngưỡng giá giảm (để cấu hình trong node "Product Configuration").
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/11803](https://n8n.io/workflows/11803).
3. Hoặc tải file JSON từ trang n8n.io và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Price Monitor Webhook"**:
   - Đảm bảo cấu hình đúng path và httpMethod (POST).
   - Lưu ý URL webhook sau khi import để sử dụng cho các hệ thống khác.

2. **Node "Product Configuration"**:
   - Cập nhật danh sách sản phẩm và ngưỡng giá giảm trong node này.
   - Ví dụ cấu hình:
     ```javascript
     return [
       {
         url: "https://example.com/product1",
         threshold: 10 // Ngưỡng giá giảm 10%
       },
       {
         url: "https://example.com/product2",
         threshold: 5 // Ngưỡng giá giảm 5%
       }
     ];
     ```

3. **Node "Scrape Product Data"**:
   - Đảm bảo đã thêm ScrapeGraphAI API credentials.
   - Cấu hình prompt để trích xuất dữ liệu chính xác (title, price, currency, availability).

4. **Node "Fetch Historical Data"**:
   - Cập nhật URL của API lịch sử giá nếu cần thay đổi.

5. **Node "Insert rows in a table"**:
   - Đảm bảo đã thêm Baserow API credentials và cấu hình đúng table ID.

6. **Node "Send Pushover Alert" và "Send Error Alert"**:
   - Đảm bảo đã thêm Pushover credentials.
   - Cấu hình đúng user key và app token.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu theo dõi giá sản phẩm.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thay thế Pushover bằng Slack hoặc Telegram để nhận thông báo.
- **Lưu log**: Thêm node để lưu log hoạt động của workflow.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp về giá sản phẩm hàng tuần.
- **Kiểm tra giá nhiều trang web**: Mở rộng danh sách sản phẩm để theo dõi giá trên nhiều trang web khác nhau.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và nhận thông báo tức thì về giá sản phẩm giảm. Dữ liệu được lưu trữ và quản lý một cách hiệu quả trong Baserow, giúp dễ dàng truy cập và phân tích. Hãy áp dụng ngay để tối ưu hóa quá trình theo dõi giá sản phẩm E-commerce của bạn!