---
title: "🚀 Theo dõi thay đổi công nghệ với BuiltWith và lưu vào Google Sheets"
description: "Hướng dẫn tự động hóa quy trình theo dõi các trang web sử dụng công nghệ cụ thể thông qua BuiltWith API và lưu kết quả vào Google Sheets"
slug: "theo-doi-thay-doi-cong-nghe-builtwith-google-sheets"
tags: [n8n, automation, no-code, BuiltWith, Google Sheets]
keywords: [n8n workflow, tự động hóa, BuiltWith, Google Sheets, công nghệ web]
---

# 🚀 Theo dõi thay đổi công nghệ với BuiltWith và lưu vào Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình theo dõi thay đổi công nghệ
- Chính xác: Lấy dữ liệu trực tiếp từ BuiltWith API
- Cá nhân hóa: Theo dõi các công nghệ cụ thể mà doanh nghiệp quan tâm
- Hoạt động liên tục: Theo dõi 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản BuiltWith với API Key
- Tài khoản Google với quyền truy cập Google Sheets
- Google Sheets đã tạo sẵn để lưu kết quả
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/4787](https://n8n.io/workflows/4787)
2. Click vào nút "Import" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node Manual Trigger**:
   - Không cần cấu hình gì đặc biệt, chỉ cần click "Execute Workflow" khi muốn chạy thủ công

2. **Node Set Technology**:
   - Cần cấu hình trường "technologies" với tên công nghệ muốn theo dõi (ví dụ: "Shopify")

3. **Node Fetch BuiltWith Data**:
   - Cần cấu hình credentials với API Key của BuiltWith
   - Đảm bảo URL API chứa tham số `TECH` với giá trị tương ứng với công nghệ đã đặt trong node Set Technology

4. **Node Extract Site Info**:
   - Không cần cấu hình gì đặc biệt, node này tự động xử lý dữ liệu từ BuiltWith API

5. **Node Log to Google Sheet**:
   - Cần cấu hình credentials với tài khoản Google OAuth2
   - Cần chỉ định Spreadsheet ID và tên Sheet cần ghi dữ liệu
   - Đảm bảo Google Sheet đã có các cột: Domain, Technology, First Indexed, Vertical

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong các node, click vào nút "Activate" để kích hoạt workflow
2. Để kiểm tra hoạt động, click "Execute Workflow" và theo dõi kết quả trong Google Sheet

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo khi có thay đổi mới
- Kết hợp với Slack để nhận thông báo tức thời
- Thiết lập lịch chạy định kỳ để theo dõi hàng ngày
- Lưu log các lần chạy để theo dõi lịch sử thay đổi

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình theo dõi thay đổi công nghệ trên web một cách hiệu quả và chính xác. Bằng cách tích hợp BuiltWith API và Google Sheets, workflow cung cấp giải pháp toàn diện cho việc giám sát thị trường công nghệ. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả kinh doanh!