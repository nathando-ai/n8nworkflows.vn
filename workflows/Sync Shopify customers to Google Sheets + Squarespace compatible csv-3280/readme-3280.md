---
title: "🚀 Tự động đồng bộ khách hàng Shopify sang Google Sheets + CSV Squarespace"
description: "Hướng dẫn tự động hóa đồng bộ danh sách khách hàng từ Shopify sang Google Sheets và định dạng CSV tương thích với Squarespace, tiết kiệm thời gian và giảm thiểu lỗi thủ công."
slug: "tu-dong-dong-bo-khach-hang-shopify-sang-google-sheets-csv-squarespace"
tags: [n8n, automation, no-code, shopify, google-sheets, squarespace]
keywords: [n8n workflow, tự động hóa, shopify, google sheets, squarespace, csv, khách hàng]
---

# 🚀 Tự động đồng bộ khách hàng Shopify sang Google Sheets + CSV Squarespace

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động cập nhật danh sách khách hàng từ Shopify sang Google Sheets hàng ngày.
- Tạo file CSV tương thích với Squarespace để dễ dàng import danh sách khách hàng.
- Giảm thiểu thời gian và lỗi thủ công trong việc quản lý khách hàng.
- Hoạt động liên tục 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets.
- URL cửa hàng Shopify của bạn (ví dụ: `your-store.myshopify.com`).
- File Google Sheets mẫu đã được clone từ [đây](https://docs.google.com/spreadsheets/d/1E8i98hwiFW7XG9HuxIZrOWfuLxGFaDm3EOAGQBZjhfk/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản của bạn.
2. Nhấn vào nút **"Import from URL"** và dán link sau: `https://n8n.io/workflows/3280`.
3. Nhấn **"Import"** để tải workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Node "Get Customers"**:
  - Cập nhật URL của cửa hàng Shopify trong tham số `GET url`:
    ```
    https://{your-store}.myshopify.com/admin/api/2025-01/customers.json
    ```
  - Đảm bảo đã cấu hình `shopifyAccessTokenApi` credentials.

- **Node "Customers Spreadsheet"**:
  - Cập nhật `Google Sheets OAuth2 API` credentials.
  - Điền `Spreadsheet ID` từ file Google Sheets đã clone.
  - Đảm bảo file Google Sheets có cấu trúc đúng theo hướng dẫn:
    ```
    Email address
    First name (optional)
    Last name (optional)
    Shopify Customer ID (will be ignored)
    ```

- **Node "Convert to Squarespace contacts csv"**:
  - Kiểm tra định dạng file CSV đầu ra có tương thích với Squarespace không.

#### 3. Kích hoạt ⚡️
- Nhấn **"Test workflow"** để kiểm tra dữ liệu mẫu.
- Sau khi kiểm tra thành công, nhấn **"Activate"** để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập lịch chạy hàng ngày thông qua **Schedule Trigger**.
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log hoạt động vào Google Sheets để theo dõi lịch sử cập nhật.
- Gửi báo cáo định kỳ về số lượng khách hàng mới qua email.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý danh sách khách hàng. Bằng cách tự động đồng bộ dữ liệu từ Shopify sang Google Sheets và định dạng CSV tương thích với Squarespace, các sếp có thể tập trung vào các công việc quan trọng hơn. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc!