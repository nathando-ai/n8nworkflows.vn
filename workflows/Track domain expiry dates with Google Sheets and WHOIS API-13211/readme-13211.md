---
title: "🚀 Theo dõi ngày hết hạn tên miền tự động với Google Sheets và WHOIS API"
description: "Hướng dẫn tự động hóa theo dõi ngày hết hạn tên miền từ Google Sheets thông qua WHOIS API, tiết kiệm thời gian và tránh bỏ lỡ hạn chót gia hạn"
slug: "theo-doi-ngay-het-han-ten-mien-tu-dong"
tags: [n8n, automation, no-code, google-sheets, whois-api]
keywords: [n8n workflow, tự động hóa tên miền, theo dõi tên miền, whois api, google sheets]
---

# 🚀 Theo dõi ngày hết hạn tên miền tự động với Google Sheets và WHOIS API

[Các sếp] có bao giờ phải tự tay kiểm tra hàng trăm tên miền để biết ngày hết hạn? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi ngày hết hạn tên miền từ Google Sheets thông qua WHOIS API, tiết kiệm thời gian và tránh bỏ lỡ hạn chót gia hạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình theo dõi tên miền
- Tiết kiệm thời gian đáng kể so với kiểm tra thủ công
- Nhận thông báo chính xác về ngày hết hạn
- Quản lý danh sách tên miền lớn một cách hiệu quả
- Tránh bỏ lỡ hạn chót gia hạn tên miền quan trọng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets
- API key từ RapidAPI WHOIS API
- Google Sheets OAuth credentials đã được thiết lập trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link sau: `https://n8n.io/workflows/13211`
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/13211) và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Set Sheet Configuration"**:
   - Thiết lập `Sheet ID` và `Sheet Name` trong tab "Parameters"
   - Sheet của bạn phải có cột "Websites" chứa danh sách tên miền

2. **Node "Read All Domains from Sheet"**:
   - Đảm bảo đã kết nối Google Sheets OAuth credentials
   - Thiết lập "Operation" thành "Read"

3. **Node "Fetch DNS Records via WHOIS API"**:
   - Thêm RapidAPI WHOIS API key vào "Authentication" tab
   - Đảm bảo URL API là `https://domain-checker7.p.rapidapi.com/whois`

4. **Node "Write Expiry Data to Sheet"**:
   - Đảm bảo đã kết nối Google Sheets OAuth credentials
   - Thiết lập "Operation" thành "Update"
   - Cấu hình "Columns" để ghi dữ liệu vào các cột phù hợp

#### 3. Kích hoạt ⚡️
1. Chạy test với một tên miền mẫu để kiểm tra workflow
2. Sau khi xác nhận hoạt động, kích hoạt workflow bằng cách nhấn "Active"

### ✍️ Mẹo & gợi ý nâng cao
1. Thiết lập thông báo qua email hoặc Slack khi tên miền sắp hết hạn
2. Kết hợp với workflow gia hạn tên miền tự động
3. Theo dõi nhiều loại thông tin khác từ WHOIS API (NS records, registrar info...)
4. Thiết lập lịch chạy định kỳ để cập nhật thông tin hàng tuần

### 📌 Kết luận
Workflow này giúp các sếp quản lý danh sách tên miền một cách hiệu quả, tiết kiệm thời gian và tránh bỏ lỡ hạn chót quan trọng. Hãy thử ngay và tự động hóa quá trình theo dõi tên miền của bạn!