---
title: "🚀 Tự động hóa chuyển đổi khách hàng thành công HubSpot thành khách hàng tiềm năng tương tự với CompanyEnrich"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tìm kiếm và thêm khách hàng tiềm năng tương tự từ các công ty đã thành công trong HubSpot vào Google Sheets bằng n8n và CompanyEnrich API"
slug: "tu-dong-hoa-khach-hang-tiem-nang-tuong-tu-hubspot-companyenrich"
tags: [n8n, automation, no-code, lead generation, sales automation]
keywords: [n8n workflow, tự động hóa khách hàng tiềm năng, CompanyEnrich, HubSpot, Google Sheets]
---

# 🚀 Tự động hóa chuyển đổi khách hàng thành công HubSpot thành khách hàng tiềm năng tương tự với CompanyEnrich

[Các sếp đang gặp khó khăn khi phải thủ công tìm kiếm và thêm khách hàng tiềm năng tương tự từ các công ty đã thành công trong HubSpot vào Google Sheets. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc tìm kiếm và thêm khách hàng tiềm năng
- Tự động hóa toàn bộ quá trình từ HubSpot đến Google Sheets
- Lấy dữ liệu khách hàng tiềm năng tương tự từ các công ty đã thành công
- Hoạt động liên tục theo lịch trình đã đặt
- Tăng khả năng phát hiện khách hàng tiềm năng chất lượng cao
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập vào API và các scope cần thiết
- API Key từ CompanyEnrich
- Tài khoản Google với Google Sheets đã tạo sẵn và có cột 'domain'
- Tài khoản n8n đã cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này bằng cách:
1. Truy cập vào n8n Editor
2. Chọn "Import from URL" và nhập link: https://n8n.io/workflows/12227
3. Hoặc copy/paste nội dung JSON từ link trên vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình lại các node quan trọng sau:

1. **HubSpot Get Companies**:
   - Chọn credentials là "hubspotAppToken"
   - Đảm bảo tài khoản HubSpot có các scope cần thiết (company read và write)

2. **HTTP Request** (CompanyEnrich API):
   - Thêm API Key của CompanyEnrich vào header với key là "Authorization" và value là "Bearer YOUR_API_KEY"
   - Thay thế "YOUR_API_KEY" bằng API Key thực tế của các sếp

3. **Append or update row in sheet**:
   - Chọn credentials là "googleSheetsOAuth2Api"
   - Chọn resource là "sheet"
   - Điền tên tài liệu và tên sheet đã tạo sẵn
   - Đảm bảo sheet có cột 'domain' để tránh trùng lặp

4. **Schedule Trigger**:
   - Thiết lập lịch chạy workflow (mặc định là mỗi tuần)

5. **Filter Best**:
   - Điều chỉnh giá trị Top_Percent trong code của node này
   - Sử dụng giá trị cao hơn (10–20%) nếu có ít công ty
   - Sử dụng giá trị thấp hơn (khoảng 1%) nếu có nhiều công ty

#### 3. Kích hoạt ⚡️
- Các sếp nên test run workflow với dữ liệu mẫu trước khi kích hoạt hoàn toàn
- Sau khi cấu hình xong, bật Active workflow để chạy theo lịch trình đã đặt

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack/Telegram để nhận thông báo khi có khách hàng tiềm năng mới
- Thêm node lưu log hoạt động để theo dõi hiệu suất workflow
- Tạo báo cáo định kỳ từ Google Sheets để theo dõi tiến độ tìm kiếm khách hàng tiềm năng
- Kết hợp với các công cụ phân tích dữ liệu để đánh giá chất lượng khách hàng tiềm năng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình tìm kiếm và thêm khách hàng tiềm năng tương tự từ các công ty đã thành công trong HubSpot vào Google Sheets. Với việc tự động hóa này, các sếp có thể tiết kiệm thời gian đáng kể và tập trung vào các hoạt động quan trọng khác trong quá trình bán hàng. Hãy áp dụng ngay workflow này để nâng cao hiệu quả tìm kiếm khách hàng tiềm năng!