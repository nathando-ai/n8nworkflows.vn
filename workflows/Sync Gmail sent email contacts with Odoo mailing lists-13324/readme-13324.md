---
title: "🚀 Tự động đồng bộ danh sách liên hệ email từ Gmail sang Odoo - Giảm thiểu 80% công việc thủ công"
description: "Workflow n8n tự động trích xuất email nhận từ thư gửi, kiểm tra tính hợp lệ và đồng bộ danh sách liên hệ vào Odoo Mailing List. Giúp giảm thiểu 80% công việc thủ công và tăng hiệu quả chiến dịch email."
slug: "tu-dong-dong-bo-danh-sach-lien-he-email-gmail-sang-odoo"
tags: [n8n, automation, no-code, crm, odoo, gmail, email-marketing]
keywords: [n8n workflow, tự động hóa email, đồng bộ liên hệ, odoo mailing list, gmail api]
---

# 🚀 Tự động đồng bộ danh sách liên hệ email từ Gmail sang Odoo - Giảm thiểu 80% công việc thủ công

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý danh sách liên hệ email]

Các sếp thường gặp phải những vấn đề sau khi quản lý danh sách liên hệ email:
- Email khách hàng bị phân tán trong lịch sử gửi thư thay vì tập trung trong một danh sách trung tâm
- Sao chép thủ công các địa chỉ nhận vào Odoo tốn thời gian và dễ xảy ra lỗi
- Thư gửi có thể chứa các địa chỉ không hợp lệ hoặc bị trả lại
- Xuất hiện nhiều liên hệ trùng lặp
- Khó theo dõi những người nhận đã trả lời hay chưa để theo dõi tiếp

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động xây dựng danh sách liên hệ từ thực tế gửi email
- Không cần nhập liệu thủ công
- Chỉ lưu trữ các email hợp lệ trong Odoo
- Giảm tỷ lệ email bị trả lại
- Không còn liên hệ trùng lặp
- Theo dõi dễ dàng cho việc theo dõi tiếp
- Hệ thống CRM sạch sẽ và hiệu quả chiến dịch tốt hơn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Phiên bản n8n 2.4.6 trở lên
- Tài khoản Gmail với quyền truy cập API
- Odoo API Key
- Google Sheets (tùy chọn, để lưu log các sự kiện)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Step 1: Schedule Trigger every day at 7 AM"**
   - Cấu hình lịch chạy hàng ngày lúc 7 giờ sáng

2. **Node "Step 2: Set Variables"**
   - Thiết lập biến `days_ago` để điều chỉnh số ngày lấy lịch sử email (mặc định 10 ngày)

3. **Node "Step 4:Get the list of emails sent 10 days ago."**
   - Cấu hình credentials Gmail OAuth2
   - Đảm bảo quyền truy cập đầy đủ vào hộp thư gửi

4. **Node "Step 14: Search email in Mailing List Contacts"**
   - Cấu hình Odoo API credentials
   - Đảm bảo endpoint API chính xác cho danh sách liên hệ

5. **Node "Step 22: Search email in Blacklisted Email Addresses"**
   - Cấu hình Odoo API credentials
   - Đảm bảo endpoint API chính xác cho danh sách email bị chặn

6. **Node "Step 24.2: Add new email in Blacklisted Email Addresses"**
   - Cấu hình Odoo API credentials
   - Đảm bảo endpoint API chính xác cho thêm email bị chặn

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động theo dõi tiếp nếu không có phản hồi sau X ngày**
   - Kết hợp với node gửi email để tự động nhắc nhở

2. **Tự động loại bỏ các email bị trả lại vĩnh viễn**
   - Thêm logic kiểm tra trạng thái email bị trả lại

3. **Điểm đánh giá tương tác**
   - Thêm điểm đánh giá cho các liên hệ dựa trên hành vi tương tác

4. **Bảng điều khiển phân tích phản hồi**
   - Tạo báo cáo tổng hợp về tỷ lệ phản hồi và hiệu suất chiến dịch

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình quản lý danh sách liên hệ email, giảm thiểu công việc thủ công lên đến 80% và nâng cao hiệu quả chiến dịch email. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ marketing và bán hàng!