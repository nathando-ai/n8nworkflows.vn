---
title: "📧 [Tự động hóa] Gửi email theo dõi khách hàng tiềm năng từ Google Sheets với ZeptoMail"
description: "Hướng dẫn tự động gửi email theo dõi khách hàng tiềm năng theo lịch trình hàng ngày từ Google Sheets đến ZeptoMail - tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng"
slug: "tu-dong-hoa-gui-email-theo-doi-khach-hang-tiem-nang-tu-google-sheets-voi-zeptomail"
tags: [n8n, automation, no-code, email-marketing, lead-nurturing]
keywords: [n8n workflow, tự động hóa email, lead nurturing, ZeptoMail, Google Sheets]
---

# 📧 [Tự động hóa] Gửi email theo dõi khách hàng tiềm năng từ Google Sheets với ZeptoMail

[Các sếp đang gặp khó khăn khi phải theo dõi và gửi email theo dõi khách hàng tiềm năng theo lịch trình hàng ngày một cách thủ công. Việc này tốn thời gian, dễ bỏ sót và không thể cá nhân hóa. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động gửi email theo dõi hàng ngày mà không cần can thiệp thủ công.
- Cá nhân hóa cao: Email được tùy chỉnh theo từng giai đoạn của khách hàng tiềm năng.
- Chính xác: Đảm bảo không bỏ sót bất kỳ khách hàng nào cần theo dõi.
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần giám sát.
- Theo dõi hiệu quả: Cập nhật trạng thái khách hàng trong Google Sheets ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được chia sẻ cho n8n.
- Tài khoản ZeptoMail với API key.
- Google Sheet có cấu trúc dữ liệu khách hàng tiềm năng với các cột: email, tên, trạng thái, ngày theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14813](https://n8n.io/workflows/14813)
2. Chọn "Import into n8n" và đăng nhập vào tài khoản n8n của bạn.
3. Hoặc copy toàn bộ JSON workflow và dán vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Read Tracking Sheet"**:
   - Chọn credentials Google Sheets đã kết nối.
   - Điền Sheet ID và Range chứa dữ liệu khách hàng tiềm năng.

2. **Nodes "Build Follow-up 1 Email", "Build Follow-up 2 Email", "Build Follow-up 3 Email"**:
   - Chỉnh sửa nội dung email theo nhu cầu của doanh nghiệp.
   - Thay đổi các biến động như tên khách hàng, liên kết theo dõi, v.v.

3. **Nodes "Send Follow-up 1", "Send Follow-up 2", "Send Follow-up 3"**:
   - Chọn credentials ZeptoMail đã kết nối.
   - Điền thông tin người gửi (From Email, From Name).
   - Đảm bảo các trường dữ liệu từ Google Sheets được ánh xạ đúng với các trường trong node gửi email.

4. **Nodes "Update Status → followup_1", "Update Status → followup_2", "Update Status → completed"**:
   - Đảm bảo các tham số cập nhật trạng thái khách hàng trong Google Sheets được cấu hình chính xác.

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật chế độ Active cho workflow.
3. Kiểm tra email được gửi và cập nhật trạng thái trong Google Sheets.

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành hoặc gặp lỗi.
2. **Lưu log hoạt động**: Thêm node ghi log hoạt động vào Google Sheets hoặc cơ sở dữ liệu.
3. **Gửi báo cáo định kỳ**: Tạo workflow phụ để tổng hợp và gửi báo cáo hiệu quả chăm sóc khách hàng hàng tuần.
4. **Tích hợp với CRM**: Kết nối với các hệ thống CRM như HubSpot, Salesforce để cập nhật trạng thái khách hàng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình gửi email theo dõi khách hàng tiềm năng một cách hiệu quả và chuyên nghiệp. Với việc chạy tự động 24/7, các sếp có thể tập trung vào các nhiệm vụ quan trọng khác trong doanh nghiệp. Hãy áp dụng ngay để nâng cao hiệu quả chăm sóc khách hàng và tăng doanh thu!