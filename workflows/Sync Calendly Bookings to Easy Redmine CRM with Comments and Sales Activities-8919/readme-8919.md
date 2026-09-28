---
title: "🚀 Tự động đồng bộ lịch hẹn Calendly với Easy Redmine CRM cùng bình luận và hoạt động bán hàng"
description: "Hướng dẫn tự động hóa quy trình đồng bộ lịch hẹn Calendly với Easy Redmine CRM, tạo bình luận và hoạt động bán hàng, gửi thông báo Outlook - tiết kiệm thời gian và nâng cao hiệu quả quản lý khách hàng."
slug: "tu-dong-dong-bo-calendly-voi-easy-redmine-crm"
tags: [n8n, automation, no-code, crm, calendly, outlook, easy-redmine]
keywords: [n8n workflow, tự động hóa, crm, calendly, easy redmine, outlook]
---

# 🚀 Tự động đồng bộ lịch hẹn Calendly với Easy Redmine CRM cùng bình luận và hoạt động bán hàng

[Các sếp đang gặp khó khăn khi phải thủ công cập nhật thông tin lịch hẹn từ Calendly vào Easy Redmine CRM và Outlook. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, tiết kiệm thời gian quý giá và giảm thiểu lỗi nhập liệu.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động cập nhật thông tin lịch hẹn từ Calendly vào CRM và Outlook mà không cần can thiệp thủ công.
- **Chính xác cao**: Giảm thiểu lỗi nhập liệu nhờ tự động hóa toàn bộ quy trình.
- **Tăng cường quản lý**: Ghi lại tất cả các cuộc họp và tương tác với khách hàng trong một nơi duy nhất.
- **Hiệu quả cao hơn**: Các sếp có thể tập trung vào công việc quan trọng hơn thay vì quản lý dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Calendly với quyền truy cập API
- Easy Redmine CRM với API được kích hoạt
- Tài khoản Outlook với quyền truy cập API
- Các thông tin xác thực (credentials) cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/8919](https://n8n.io/workflows/8919)
2. Click vào nút "Import" để tải xuống file JSON của workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải xuống

Hoặc bạn có thể copy/paste JSON từ trang web vào n8n Editor bằng cách:
1. Click vào nút "Import from Clipboard"
2. Dán nội dung JSON từ trang web vào hộp thoại

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Calendly Trigger**:
   - Đảm bảo đã thiết lập credentials cho Calendly trong n8n
   - Kiểm tra event type là "invitee.created"

2. **Get ID of Account from email**:
   - Cập nhật URL endpoint của Easy Redmine CRM để tìm kiếm lead theo email
   - Đảm bảo đã thiết lập credentials cho HTTP Header Auth

3. **Add Comment**:
   - Cập nhật thông tin credentials cho Easy Redmine
   - Kiểm tra các tham số operation và resource đã được thiết lập đúng
   - Tùy chỉnh nội dung bình luận theo nhu cầu của các sếp

4. **Sales Activity POST**:
   - Cập nhật URL endpoint của Easy Redmine CRM cho hoạt động bán hàng
   - Đảm bảo đã thiết lập credentials cho HTTP Header Auth
   - Kiểm tra các trường dữ liệu cần thiết cho hoạt động bán hàng

5. **Send a message**:
   - Đảm bảo đã thiết lập credentials cho Microsoft Outlook
   - Tùy chỉnh nội dung email theo nhu cầu của các sếp

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Thực hiện một cuộc hẹn thử nghiệm trên Calendly để kiểm tra workflow hoạt động như mong đợi
3. Kiểm tra Easy Redmine CRM, Outlook và các hệ thống khác để đảm bảo thông tin đã được cập nhật đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung bình luận**: Các sếp có thể thêm các thẻ hoặc định dạng đặc biệt vào bình luận để dễ dàng phân loại các cuộc hẹn.
2. **Thêm logic điều kiện**: Ví dụ chỉ xử lý các cuộc hẹn có liên quan đến khách hàng tiềm năng hoặc các cuộc hẹn quan trọng.
3. **Tạo lead mới nếu không tìm thấy**: Mở rộng workflow để tự động tạo lead mới trong Easy Redmine CRM nếu không tìm thấy lead nào khớp với email của người tham gia.
4. **Gửi thông báo đến nhiều người**: Các sếp có thể cấu hình để gửi thông báo đến nhiều người quản lý hoặc bộ phận liên quan.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình đồng bộ lịch hẹn từ Calendly với Easy Redmine CRM và Outlook, tiết kiệm thời gian và nâng cao hiệu quả quản lý khách hàng. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!