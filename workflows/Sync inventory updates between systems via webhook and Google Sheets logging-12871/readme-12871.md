---
title: "🚀 Tự động đồng bộ tồn kho giữa các hệ thống qua webhook và Google Sheets"
description: "Hướng dẫn tự động đồng bộ tồn kho giữa các hệ thống như cửa hàng online, POS, ERP hoặc nền tảng kho hàng. Workflow này đảm bảo dữ liệu tồn kho luôn đồng bộ và được ghi lại trong Google Sheets."
slug: "tu-dong-dong-bo-ton-kho-giua-cac-he-thong"
tags: [n8n, automation, no-code, inventory, google-sheets]
keywords: [n8n workflow, tự động hóa tồn kho, đồng bộ dữ liệu, google sheets]
---

# 🚀 Tự động đồng bộ tồn kho giữa các hệ thống qua webhook và Google Sheets

[Các sếp đang gặp khó khăn khi phải thủ công đồng bộ tồn kho giữa nhiều hệ thống như cửa hàng online, POS, ERP hay kho hàng. Workflow này sẽ tự động hóa toàn bộ quy trình này, đảm bảo dữ liệu luôn đồng bộ và được ghi lại trong Google Sheets.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ tồn kho giữa các hệ thống mà không cần can thiệp thủ công.
- Chính xác: Dữ liệu tồn kho luôn đồng bộ và chính xác.
- Cá nhân hóa: Có thể tùy chỉnh dữ liệu được đồng bộ và cách ghi log.
- Hoạt động liên tục: Workflow chạy 24/7, không bị gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API key hoặc credentials để truy cập hệ thống kho hàng hoặc cửa hàng online.
- Địa chỉ endpoint của hệ thống thứ hai để nhận dữ liệu tồn kho.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/12871](https://n8n.io/workflows/12871).
3. Hoặc bạn có thể tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Inventory Webhook**:
   - Cấu hình webhook trong hệ thống nguồn để gửi dữ liệu tồn kho.
   - Đảm bảo payload chứa các trường thông tin cần thiết: SKU, số lượng tồn kho, hệ thống nguồn và thời gian sửa đổi.

2. **Log Inventory Sync To Google Sheet**:
   - Kết nối với Google Sheets của bạn.
   - Tạo một sheet mới và thêm các cột: SKU, số lượng tồn kho, hệ thống nguồn, trạng thái và thời gian.
   - Cập nhật thông tin credentials trong node Google Sheets.

3. **Send Inventory To Secondary API**:
   - Cập nhật địa chỉ endpoint của hệ thống thứ hai trong node HTTP Request.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu đồng bộ tồn kho tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack hoặc Telegram để nhận thông báo khi có sự cố đồng bộ.
- Tạo báo cáo định kỳ từ Google Sheets để theo dõi hiệu suất đồng bộ.
- Kết hợp với các hệ thống khác như CRM để cập nhật thông tin tồn kho cho khách hàng.

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ tồn kho giữa các hệ thống một cách dễ dàng và chính xác. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian và giảm thiểu lỗi do thủ công. Hãy thử ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!