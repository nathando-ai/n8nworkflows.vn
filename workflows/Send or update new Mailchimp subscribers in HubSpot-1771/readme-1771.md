---
title: "🚀 Tự động đồng bộ danh sách Mailchimp với HubSpot mỗi ngày"
description: "Hướng dẫn tự động hóa đồng bộ danh sách thành viên Mailchimp sang HubSpot mỗi ngày để tối ưu hóa chiến dịch marketing và quản lý khách hàng"
slug: "tu-dong-dong-bo-mailchimp-voi-hubspot"
tags: [n8n, automation, no-code, marketing, sales]
keywords: [n8n workflow, tự động hóa marketing, đồng bộ danh sách, Mailchimp, HubSpot]
---

# 🚀 Tự động đồng bộ danh sách Mailchimp với HubSpot mỗi ngày

[Các sếp marketing đang gặp khó khăn khi phải thủ công đồng bộ danh sách thành viên giữa Mailchimp và HubSpot mỗi ngày. Việc này tốn thời gian, dễ gây lỗi và không hiệu quả. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này trong vòng 15 phút.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi ngày cho việc đồng bộ thủ công
- Đảm bảo dữ liệu luôn đồng bộ giữa hai hệ thống
- Giảm thiểu rủi ro lỗi do nhập liệu thủ công
- Tự động cập nhật thông tin khách hàng mới nhất
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mailchimp với quyền truy cập API
- Tài khoản HubSpot với quyền tạo/đọc thông tin liên hệ
- API Key của Mailchimp
- Access Token của HubSpot
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [n8n.io/workflows/1771](https://n8n.io/workflows/1771)
2. Click vào nút "Copy" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get changed members"**:
   - Chọn credentials là "mailchimpApi"
   - Điền "List ID" của danh sách Mailchimp bạn muốn đồng bộ
   - Thiết lập "Since" để chỉ lấy thành viên mới hoặc thay đổi trong ngày

2. **Node "Create/Update contact"**:
   - Chọn credentials là "hubspotAppToken"
   - Thiết lập các trường dữ liệu cần đồng bộ từ Mailchimp sang HubSpot
   - Đảm bảo các trường này đã được tạo trong HubSpot trước đó

3. **Node "Every day at 07:00"**:
   - Thiết lập thời gian chạy phù hợp với lịch làm việc của các sếp

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" để test với dữ liệu mẫu
2. Kiểm tra kết quả ở node cuối cùng để đảm bảo dữ liệu đã được đồng bộ đúng
3. Bật "Active" workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email báo cáo kết quả đồng bộ hàng ngày
- Kết hợp với Slack để nhận thông báo khi có lỗi xảy ra
- Thiết lập lưu log các thay đổi để theo dõi lịch sử
- Tự động gửi email chào mừng cho các thành viên mới được thêm vào danh sách

### 📌 Kết luận
Với workflow này, các sếp marketing có thể tự động hóa hoàn toàn quá trình đồng bộ danh sách giữa Mailchimp và HubSpot, tiết kiệm thời gian và giảm thiểu rủi ro lỗi. Hãy áp dụng ngay để tối ưu hóa chiến dịch marketing của các sếp!