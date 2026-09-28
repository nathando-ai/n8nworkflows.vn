---
title: "🚀 Tự động hóa kiểm tra email ZeroBounce và đồng bộ lead chất lượng sang Mautic từ Typeform"
description: "Workflow n8n tự động hóa việc kiểm tra email bằng ZeroBounce và đồng bộ lead chất lượng từ Typeform sang Mautic, giúp tiết kiệm thời gian và tăng hiệu quả chăm sóc khách hàng."
slug: "tu-dong-hoa-kiem-tra-email-zerobounce-dong-bo-lead-mautic"
tags: [n8n, automation, no-code, lead-generation, email-validation]
keywords: [n8n workflow, tự động hóa, kiểm tra email, ZeroBounce, Mautic, Typeform]
---

# 🚀 Tự động hóa kiểm tra email ZeroBounce và đồng bộ lead chất lượng sang Mautic từ Typeform

[Các sếp đang gặp khó khăn khi phải xử lý thủ công hàng nghìn lead từ Typeform mỗi ngày. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình kiểm tra email bằng ZeroBounce và đồng bộ lead chất lượng sang Mautic một cách nhanh chóng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình kiểm tra email và đồng bộ lead.
- **Chính xác cao**: Sử dụng ZeroBounce để kiểm tra email với độ chính xác 99.6%.
- **Tăng hiệu quả chăm sóc khách hàng**: Chỉ đồng bộ lead chất lượng cao sang Mautic.
- **Quản lý lead hiệu quả**: Lưu trữ lead bị từ chối vào Google Sheets để theo dõi và phân tích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Typeform với quyền truy cập API.
- Tài khoản ZeroBounce với API Key (tạo tại [đây](https://www.zerobounce.net/members/API)).
- Tài khoản Mautic với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow](https://n8n.io/workflows/13095).
2. Click vào nút "Download Workflow" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Typeform Trigger**:
   - Chọn credentials Typeform.
   - Cấu hình các trường dữ liệu cần lấy từ Typeform (ví dụ: Email, First Name, Last Name).

2. **ZeroBounce**:
   - Chọn credentials ZeroBounce.
   - Đảm bảo tài khoản ZeroBounce có đủ credits để thực hiện kiểm tra email.

3. **Mautic**:
   - Chọn credentials Mautic.
   - Cấu hình các trường dữ liệu cần đồng bộ sang Mautic (ví dụ: Email, First Name, Last Name).

4. **Google Sheets**:
   - Chọn credentials Google Sheets.
   - Cấu hình tên sheet và các trường dữ liệu cần lưu trữ (ví dụ: Accepted, Rejected).
   - Tạo các sheet với các cột sau:
     - **Accepted**:
       `Email,First Name,Last Name,Accepted At,Accepted Reason,ZB Status,ZB Sub Status,ZB Free Email,ZB Did You Mean,ZB Account,ZB Domain,ZB Domain Age Days,ZB SMTP Provider,ZB MX Found,ZB MX Record,ZB Score`
     - **Rejected**:
       `Email,First Name,Last Name,Rejected At,Rejected Reason,ZB Status,ZB Sub Status,ZB Free Email,ZB Did You Mean,ZB Account,ZB Domain,ZB Domain Age Days,ZB SMTP Provider,ZB MX Found,ZB MX Record,ZB Score`

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo khi có lead mới hoặc lead bị từ chối.
- **Lưu log hoạt động**: Thêm node để lưu log hoạt động của workflow để theo dõi và phân tích.
- **Gửi báo cáo định kỳ**: Tạo báo cáo định kỳ về số lượng lead được đồng bộ và lead bị từ chối.
- **Tích hợp với các dịch vụ khác**: Kết hợp với các dịch vụ khác như Sendinblue, HubSpot để tăng hiệu quả chăm sóc khách hàng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình kiểm tra email và đồng bộ lead chất lượng từ Typeform sang Mautic một cách nhanh chóng và chính xác. Với các lợi ích như tiết kiệm thời gian, chính xác cao và tăng hiệu quả chăm sóc khách hàng, workflow này là giải pháp hoàn hảo cho các doanh nghiệp muốn tối ưu hóa quy trình chăm sóc khách hàng. Hãy áp dụng ngay để trải nghiệm hiệu quả!