---
title: "🚀 Theo dõi giá Amazon & Giám sát đối thủ cạnh tranh với Apify và Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi giá sản phẩm Amazon và giám sát đối thủ cạnh tranh thông qua Apify và Google Sheets với n8n. Tiết kiệm thời gian và nhận thông tin cập nhật liên tục."
slug: "theo-doi-gia-amazon-voi-apify-google-sheets"
tags: [n8n, automation, no-code, amazon, market-research]
keywords: [n8n workflow, tự động hóa, theo dõi giá, giám sát đối thủ, google sheets]
---

# 🚀 Theo dõi giá Amazon & Giám sát đối thủ cạnh tranh với Apify và Google Sheets

[Các sếp] có bao giờ phải tự tay vào trang Amazon để kiểm tra giá sản phẩm của mình và đối thủ không? Việc này không chỉ tốn thời gian mà còn dễ bỏ sót. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi giá hàng ngày chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải vào trang Amazon hàng ngày để kiểm tra giá.
- **Chính xác**: Dữ liệu được cập nhật tự động từ Apify, đảm bảo độ chính xác cao.
- **Cá nhân hóa**: Theo dõi nhiều sản phẩm và đối thủ cạnh tranh chỉ với một workflow duy nhất.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được chia sẻ cho n8n.
- Tài khoản Apify với API key (cần gói $40/month với 14 ngày dùng thử).
- Danh sách sản phẩm và URL đối thủ cạnh tranh đã được nhập vào Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/11062).
2. Click vào nút "Import" và chọn "Import from URL".
3. Dán link workflow vào ô nhập liệu và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình thời gian chạy hàng ngày (ví dụ: 8:00 AM mỗi ngày).

2. **Get row(s) in sheet**:
   - Chọn credentials Google Sheets đã được thiết lập.
   - Nhập **Sheet ID** và **Range** chứa danh sách sản phẩm và URL đối thủ cạnh tranh.

3. **Run an Actor**:
   - Chọn credentials Apify đã được thiết lập.
   - Chọn **Actor ID** của Amazon Product Scraper (hoặc sử dụng actor khác phù hợp).
   - Cấu hình tham số đầu vào cho actor (ví dụ: `startUrls`, `maxItems`).

4. **HTTP Request1**:
   - Đảm bảo URL của Apify actor được cấu hình đúng.
   - Thêm header `Authorization` với API key của Apify.

5. **Append or update row in sheet**:
   - Chọn credentials Google Sheets đã được thiết lập.
   - Cấu hình **Sheet ID** và **Range** để lưu kết quả.
   - Đảm bảo các cột trong Google Sheets đã được đặt tên đúng (ví dụ: `Product URL`, `Competitor URL`, `Price`).

6. **Code in JavaScript**:
   - Kiểm tra và chỉnh sửa mã JavaScript để trích xuất và định dạng dữ liệu giá từ kết quả của Apify actor.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Chạy workflow một lần với dữ liệu mẫu để kiểm tra kết quả.
2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, bật workflow để chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm cảnh báo giá giảm**: Sử dụng node **Email** hoặc **Slack** để gửi thông báo khi giá sản phẩm giảm.
- **Phát hiện chủ sở hữu Buy Box**: Kết hợp với actor Apify khác để phát hiện chủ sở hữu Buy Box.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để tổng hợp và gửi báo cáo hàng tuần.
- **Mở rộng đối thủ cạnh tranh**: Thêm các cột mới trong Google Sheets và sao chép cấu trúc node để theo dõi thêm đối thủ.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình theo dõi giá Amazon và giám sát đối thủ cạnh tranh. Với việc cấu hình đúng các thông số và kích hoạt workflow, các sếp sẽ nhận được dữ liệu cập nhật liên tục mà không cần phải can thiệp thủ công. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả kinh doanh!