---
title: "🚀 Tự động hóa: Đồng bộ danh sách người tham gia webinar Zoom vào Mailchimp với xác thực email kép và lọc email"
description: "Hướng dẫn tự động hóa quy trình đồng bộ danh sách người tham gia webinar Zoom vào Mailchimp với xác thực email kép và lọc email nội bộ. Tiết kiệm thời gian và nâng cao hiệu quả quản lý khách hàng tiềm năng."
slug: "tu-dong-hoa-dong-bo-danh-sach-nguoi-tham-gia-webinar-zoom-vao-mailchimp"
tags: [n8n, automation, no-code, marketing, email-marketing]
keywords: [n8n workflow, tự động hóa, đồng bộ dữ liệu, webinar, Mailchimp, xác thực email kép]
---

# 🚀 Tự động hóa: Đồng bộ danh sách người tham gia webinar Zoom vào Mailchimp với xác thực email kép và lọc email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý danh sách người tham gia webinar thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý danh sách thủ công
- Đảm bảo chỉ đồng bộ những email hợp lệ
- Tự động gắn thẻ "Leads" cho khách hàng tiềm năng
- Tăng cường xác thực email kép để tránh spam
- Quản lý danh sách khách hàng tiềm năng một cách chuyên nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mailchimp với API key
- Tài khoản Zoom với quyền truy cập API
- Danh sách email nội bộ cần lọc (nếu có)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11593](https://n8n.io/workflows/11593)
2. Nhấn nút "Import" để tải file JSON workflow
3. Hoặc copy toàn bộ JSON và dán vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Type in IDs"**:
   - Cấu hình `webinar_id` và `occurrence_id` từ Zoom
   - Lấy thông tin này từ URL webinar Zoom hoặc API Zoom

2. **Node "Get Webinar Attendees from Zoom"**:
   - Đảm bảo đã tạo credentials cho Zoom API
   - Kiểm tra quyền truy cập API của tài khoản Zoom

3. **Node "Filter Out Internal Emails"**:
   - Cập nhật danh sách email nội bộ cần lọc trong node này
   - Sử dụng biểu thức điều kiện: `{{ $node["Get Webinar Attendees from Zoom"].json["registrants"].map(r => r.email).filter(email => !email.includes("@congtycuaban.com")) }}`

4. **Node "Update a member"**:
   - Đảm bảo đã tạo credentials cho Mailchimp API
   - Cấu hình đúng List ID trong Mailchimp

5. **Node "Mailchimp - Send Double Opt in Email"**:
   - Cấu hình đúng API endpoint của Mailchimp
   - Kiểm tra template email xác thực

6. **Node "Mailchimp - Add Leads Tag"**:
   - Đảm bảo tag "Leads" đã tồn tại trong Mailchimp
   - Cấu hình đúng API endpoint cho thao tác thêm tag

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra workflow
2. Sau khi kiểm tra thành công, nhấn "Active" để kích hoạt workflow
3. Cấu hình lịch chạy phù hợp với tần suất webinar của bạn

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy
2. Thêm node lưu log hoạt động để theo dõi hiệu suất
3. Tạo báo cáo định kỳ về số lượng người tham gia và tỷ lệ chuyển đổi
4. Kết nối với Google Sheets để lưu trữ dữ liệu bổ sung

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình đồng bộ danh sách người tham gia webinar từ Zoom vào Mailchimp một cách hiệu quả. Với xác thực email kép và lọc email nội bộ, các sếp có thể quản lý danh sách khách hàng tiềm năng một cách chuyên nghiệp và chuyên nghiệp. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả marketing!