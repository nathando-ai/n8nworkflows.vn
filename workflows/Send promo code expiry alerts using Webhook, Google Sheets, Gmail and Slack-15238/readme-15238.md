---
title: "🚀 Tự động hóa cảnh báo mã khuyến mãi sắp hết hạn qua Webhook, Google Sheets, Gmail và Slack"
description: "Hướng dẫn tự động hóa cảnh báo mã khuyến mãi sắp hết hạn bằng n8n, tiết kiệm thời gian và tăng hiệu quả quản lý khuyến mãi cho doanh nghiệp"
slug: "tu-dong-hoa-canh-bao-ma-khuyen-mai-sap-het-han"
tags: [n8n, automation, no-code, google-sheets, slack]
keywords: [n8n workflow, tự động hóa, mã khuyến mãi, cảnh báo, google sheets]
---

# 🚀 Tự động hóa cảnh báo mã khuyến mãi sắp hết hạn bằng n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý mã khuyến mãi thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động cảnh báo mã khuyến mãi sắp hết hạn qua Slack và email
- Lưu trữ dữ liệu mã khuyến mãi trong Google Sheets để theo dõi và báo cáo
- Tiết kiệm thời gian quản lý mã khuyến mãi thủ công
- Nhận cảnh báo kịp thời khi mã khuyến mãi chỉ còn 1 ngày hoặc 2-3 ngày
- Tăng hiệu quả quản lý khuyến mãi và tăng doanh thu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail)
- Tài khoản Slack (để nhận cảnh báo)
- API key từ n8n (nếu sử dụng phiên bản cloud)
- Dữ liệu mẫu mã khuyến mãi để test workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/15238
3. Hoặc copy JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Receive Promo Request" (Webhook)**
   - Đảm bảo cấu hình đúng path: `27923033-a20e-4fc3-8bda-5308f6661a01`
   - Phương thức HTTP: POST

2. **Node "Send Promo Email" (Gmail)**
   - Cấu hình credentials "gmailOAuth2"
   - Điền địa chỉ email người nhận
   - Tùy chỉnh nội dung email cảnh báo

3. **Node "Save Promo to Sheet" (Google Sheets)**
   - Cấu hình credentials "googleSheetsOAuth2Api"
   - Chọn Spreadsheet ID và tên Sheet cần lưu dữ liệu
   - Đảm bảo các cột trong Sheet phù hợp với dữ liệu mã khuyến mãi

4. **Node "Slack Urgent Alert" và "Slack Warning Alert" (Slack)**
   - Cấu hình credentials "slackApi"
   - Chọn channel phù hợp để nhận cảnh báo
   - Tùy chỉnh nội dung cảnh báo

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu bằng cách gửi request POST đến webhook URL
- Kiểm tra email và Slack để xác nhận cảnh báo
- Bật Active workflow khi đã kiểm tra và cấu hình xong

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi SMS cảnh báo cho các quản lý quan trọng
- Kết hợp với hệ thống CRM để cập nhật trạng thái mã khuyến mãi
- Tạo báo cáo định kỳ về hiệu quả sử dụng mã khuyến mãi
- Thiết lập cảnh báo cho nhiều loại mã khuyến mãi khác nhau
- Kết nối với hệ thống thanh toán để tự động vô hiệu hóa mã hết hạn

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình quản lý mã khuyến mãi, từ nhận dữ liệu đến cảnh báo hết hạn. Với việc tích hợp Google Sheets, Gmail và Slack, các sếp có thể quản lý hiệu quả hơn và tăng doanh thu từ chương trình khuyến mãi. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả kinh doanh!