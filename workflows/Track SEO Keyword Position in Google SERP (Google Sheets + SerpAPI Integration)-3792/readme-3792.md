---
title: "🔍 Theo dõi vị trí từ khóa SEO trên Google với n8n + Google Sheets"
description: "Tự động hóa việc theo dõi vị trí từ khóa SEO trên Google và lưu kết quả vào Google Sheets với workflow n8n này. Nhận thông báo ngay khi từ khóa của bạn bị rớt vị trí."
slug: "theo-doi-vi-tri-tu-khoa-seo-google-sheets"
tags: [n8n, automation, no-code, seo, google-sheets]
keywords: [n8n workflow, tự động hóa seo, theo dõi từ khóa, google sheets, serp]
---

# 🔍 Theo dõi vị trí từ khóa SEO trên Google với n8n + Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình theo dõi vị trí từ khóa SEO
- Lưu kết quả vào Google Sheets để theo dõi lịch sử
- Nhận thông báo ngay khi từ khóa của bạn bị rớt vị trí
- Tiết kiệm thời gian và công sức cho việc theo dõi thủ công
- Dễ dàng tích hợp với các công cụ SEO khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt
- API key từ SerpAPI (để truy vấn kết quả tìm kiếm Google)
- Tài khoản WhatsApp Business API (tùy chọn, để nhận thông báo qua WhatsApp)
- Tài khoản Gmail (tùy chọn, để nhận thông báo qua email)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/3792)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Schedule Trigger**: Cấu hình lịch chạy workflow (ví dụ: hàng ngày lúc 8h sáng)
- **Set Keyword (s)**: Chỉnh sửa node này để nhập danh sách từ khóa bạn muốn theo dõi
- **Google Serp Request**: Cấu hình credentials cho SerpAPI
- **Google Sheets**: Cấu hình credentials cho Google Sheets và chỉ định sheet ID và tên sheet
- **Notifications Switch**: Chọn phương thức nhận thông báo (email hoặc WhatsApp)
- **GMAIL Start Checks Notification**: Cấu hình credentials cho Gmail và địa chỉ email nhận thông báo
- **WA Start Checks Notification**: Cấu hình credentials cho WhatsApp Business API

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách click vào nút "Test workflow"
2. Sau khi test thành công, bật Active workflow bằng cách click vào nút "Activate"

### ✍️ Mẹo & gợi ý nâng cao
- Thêm nhiều từ khóa hơn để theo dõi toàn diện hơn
- Kết hợp với các công cụ SEO khác như Ahrefs hoặc SEMrush để phân tích sâu hơn
- Thiết lập báo cáo định kỳ để theo dõi xu hướng SEO
- Tích hợp với các công cụ quản lý dự án như Trello hoặc Asana để theo dõi tiến độ SEO

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức cho việc theo dõi vị trí từ khóa SEO. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong công việc. Hãy thử ngay và nâng cao hiệu quả SEO của bạn!