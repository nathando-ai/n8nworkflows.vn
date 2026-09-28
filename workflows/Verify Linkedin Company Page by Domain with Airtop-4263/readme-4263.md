---
title: "🔍 Xác minh trang công ty LinkedIn bằng tên miền với Airtop - Tự động hóa 100% không cần code"
description: "Hướng dẫn tự động hóa xác minh trang công ty LinkedIn bằng tên miền sử dụng Airtop API trong n8n. Giải pháp chính xác hóa dữ liệu liên quan đến LinkedIn cho các sếp Sales."
slug: "xac-minh-trang-cong-ty-linkedin-bang-ten-mien-voi-airtop"
tags: [n8n, automation, no-code, sales, linkedin]
keywords: [n8n workflow, tự động hóa, linkedin, sales, airtop]
---

# 🔍 Xác minh trang công ty LinkedIn bằng tên miền với Airtop - Tự động hóa 100% không cần code

[Các sếp Sales thường gặp khó khăn khi phải xác minh thủ công các trang công ty LinkedIn để đảm bảo tính chính xác của dữ liệu. Với workflow này, các sếp có thể tự động hóa quy trình này một cách hoàn toàn không cần code, giúp tiết kiệm thời gian và giảm thiểu lỗi.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xác minh trang LinkedIn thủ công
- Đảm bảo tính chính xác của dữ liệu liên quan đến LinkedIn
- Tự động hóa quy trình xác minh một cách liên tục
- Giảm thiểu lỗi do nhập liệu thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtop với API Key
- Profile Airtop đã được xác thực với LinkedIn
- Dữ liệu đầu vào bao gồm:
  - URL trang LinkedIn của công ty
  - Tên miền công ty mong muốn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/4263](https://n8n.io/workflows/4263)
3. Hoặc copy nội dung JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Cấu hình form input với các trường:
     - `companyLinkedIn`: URL trang LinkedIn của công ty
     - `companyDomain`: Tên miền công ty mong muốn

2. **Node "Get company website from LinkedIn profile"**:
   - Chọn credentials "airtopApi" đã được cấu hình
   - Đảm bảo profile Airtop đã được xác thực với LinkedIn
   - Giữ nguyên prompt: "This is a Company's LinkedIn profile page, extract the URL for the website."

3. **Node "Filter"**:
   - Cấu hình điều kiện lọc để so sánh tên miền trích xuất được với tên miền mong muốn

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các workflow khác để tự động cập nhật thông tin công ty vào CRM
- Thêm bước gửi thông báo qua Slack/Email khi xác minh thành công
- Lưu log các lần xác minh để theo dõi lịch sử hoạt động
- Tích hợp với các công cụ khác như HubSpot để tự động cập nhật thông tin công ty

### 📌 Kết luận
Workflow này giúp các sếp Sales tự động hóa quy trình xác minh trang công ty LinkedIn một cách chính xác và hiệu quả. Bằng cách tích hợp với Airtop API, các sếp có thể đảm bảo tính chính xác của dữ liệu liên quan đến LinkedIn mà không cần phải can thiệp thủ công. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ Sales!