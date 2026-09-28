---
title: "🚀 Theo dõi giá Amazon giảm giá với Scavio và Google Sheets - Tự động hóa hoàn toàn"
description: "Hướng dẫn chi tiết cách tự động theo dõi giá sản phẩm Amazon giảm giá và nhận thông báo qua email, sử dụng công nghệ Scavio và Google Sheets. Tiết kiệm thời gian và không cần lập trình."
slug: "theo-doi-gia-amazon-giam-gia-voi-scavio-va-google-sheets"
tags: [n8n, automation, no-code, amazon, google-sheets]
keywords: [n8n workflow, tự động hóa, theo dõi giá, amazon, scavio, google sheets]
---

# 🚀 Theo dõi giá Amazon giảm giá với Scavio và Google Sheets - Tự động hóa hoàn toàn

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ phải theo dõi giá hàng ngày trên Amazon để tìm cơ hội mua sắm tốt? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi giá sản phẩm Amazon và nhận thông báo ngay khi giá giảm xuống mức mong muốn. Không cần phải mở trang web hàng ngày hay mất thời gian so sánh giá thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần theo dõi giá hàng ngày, nhận thông báo tự động.
- Chính xác: Theo dõi giá thời gian thực từ Scavio API.
- Cá nhân hóa: Thiết lập ngưỡng giá riêng cho từng sản phẩm.
- Hoạt động liên tục: Theo dõi 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã kích hoạt.
- Tài khoản Gmail để nhận thông báo.
- API key từ Scavio (miễn phí 500 credits/tháng).
- Danh sách sản phẩm Amazon cần theo dõi cùng với giá mong muốn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15380](https://n8n.io/workflows/15380)
2. Nhấn nút "Import" trên trang workflow.
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow.
4. Hoàn tất import và mở workflow trong Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Read watchlist" và "Save state"**:
   - Cấu hình credentials Google Sheets OAuth2.
   - Chọn spreadsheet và tab chứa danh sách sản phẩm.
   - Đảm bảo có 3 cột: `product_url`, `price_threshold`, `last_alerted_price`.

2. **Node "Live price"**:
   - Cấu hình credentials Scavio API.
   - Đảm bảo có API key từ Scavio (đăng ký tại [scavio.dev](https://scavio.dev)).

3. **Node "Email"**:
   - Cấu hình credentials Gmail OAuth2.
   - Điền địa chỉ email nhận thông báo vào trường `sendTo`.

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Test Workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập ngưỡng giá khác nhau cho từng sản phẩm trong Google Sheets.
- Kết hợp với Slack hoặc Telegram để nhận thông báo trên các nền tảng khác.
- Lưu log các thông báo đã gửi để theo dõi lịch sử giá.
- Gửi báo cáo định kỳ về các sản phẩm đang theo dõi.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tiền bạc khi mua sắm trên Amazon. Bằng cách tự động hóa quá trình theo dõi giá, các sếp có thể nhận thông báo ngay khi giá sản phẩm giảm xuống mức mong muốn. Hãy áp dụng ngay để bắt đầu tiết kiệm!