```yaml
---
title: "🚀 Tự động đồng bộ dữ liệu Lead từ Facebook Ads sang Google Sheets & Salesforce CRM"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình đồng bộ dữ liệu lead từ Facebook Ads sang Google Sheets và Salesforce CRM bằng n8n, tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng."
slug: "tu-dong-dong-bo-lead-facebook-ads-google-sheets-salesforce"
tags: [n8n, automation, no-code, facebook-ads, salesforce, google-sheets]
keywords: [n8n workflow, tự động hóa lead, facebook ads, salesforce, google sheets]
---
```

# 🚀 Tự động đồng bộ dữ liệu Lead từ Facebook Ads sang Google Sheets & Salesforce CRM

[Các sếp đang làm thủ công việc đồng bộ dữ liệu lead từ Facebook Ads sang Google Sheets và Salesforce CRM? Bạn đã thử tự động hóa quy trình này chưa? Với workflow này, các sếp có thể tiết kiệm hàng giờ mỗi ngày chỉ bằng cách nhấn một nút!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động đồng bộ dữ liệu lead từ Facebook Ads sang Google Sheets và Salesforce CRM mà không cần can thiệp thủ công.
- **Chính xác**: Dữ liệu được đồng bộ chính xác và kịp thời, giảm thiểu lỗi do nhập liệu thủ công.
- **Tích hợp liền mạch**: Kết nối các công cụ quan trọng trong quy trình marketing và bán hàng.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào thời gian làm việc của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Facebook Ads với quyền truy cập vào dữ liệu lead.
- Tài khoản Google với quyền truy cập vào Google Sheets.
- Tài khoản Salesforce với quyền tạo lead.
- API keys cho Facebook Ads, Google Sheets và Salesforce.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập link: [https://n8n.io/workflows/6687](https://n8n.io/workflows/6687).
3. Hoặc tải file JSON về và nhấn "Import from File".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Facebook Lead Ad**:
   - Chọn credentials là `facebookLeadAdsTriggerApi`.
   - Đảm bảo tài khoản Facebook Ads có quyền truy cập vào dữ liệu lead.

2. **Node Log Lead to Google Sheets**:
   - Chọn credentials là `googleSheetsApi`.
   - Chỉnh sửa tên sheet và cấu trúc dữ liệu phù hợp với yêu cầu của các sếp.

3. **Node Create Lead in Salesforce**:
   - Chọn credentials là `salesforceApi`.
   - Đảm bảo tài khoản Salesforce có quyền tạo lead.

4. **Node Prepare CRM Data**:
   - Chỉnh sửa các trường dữ liệu cần đồng bộ từ Facebook Ads sang Salesforce.

5. **Node Update Status in Sheet**:
   - Chọn credentials là `googleSheetsApi`.
   - Chỉnh sửa tên sheet và cấu trúc dữ liệu phù hợp với yêu cầu của các sếp.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Nhấn vào nút "Execute Workflow" để kiểm tra workflow hoạt động đúng với dữ liệu mẫu.
2. **Bật Active workflow**:
   - Nhấn vào nút "Activate Workflow" để workflow chạy tự động khi có dữ liệu lead mới từ Facebook Ads.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi có lead mới được đồng bộ thành công.
- **Lưu log**: Thêm node lưu log hoạt động của workflow để theo dõi và giải quyết vấn đề nếu có.
- **Gửi báo cáo định kỳ**: Thêm node gửi báo cáo tổng hợp dữ liệu lead hàng ngày hoặc hàng tuần.
- **Xử lý lỗi tự động**: Thêm node xử lý lỗi và gửi thông báo khi workflow gặp sự cố.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động đồng bộ dữ liệu lead từ Facebook Ads sang Google Sheets và Salesforce CRM một cách liền mạch và hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng!