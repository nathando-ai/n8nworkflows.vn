---
title: "📞 Tự động trích xuất số điện thoại & email từ TruePeopleSearch với Zyte API"
description: "Hướng dẫn chi tiết workflow n8n tự động hóa việc trích xuất thông tin liên lạc từ TruePeopleSearch, bao gồm cả trường hợp fallback khi không tìm thấy số điện thoại chính"
slug: "tu-dong-trich-xuat-so-dien-thoai-email-tu-truepeoplesearch"
tags: [n8n, automation, no-code, scraping, lead-generation]
keywords: [n8n workflow, tự động hóa, trích xuất dữ liệu, lead generation, scraping]
---

# 📞 Tự động trích xuất số điện thoại & email từ TruePeopleSearch với Zyte API

[Các sếp] có bao giờ phải tra cứu thông tin liên lạc của khách hàng một cách thủ công trên TruePeopleSearch? Quá trình này tốn thời gian, dễ bị lỗi và không thể thực hiện hàng loạt. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này với n8n, bao gồm cả trường hợp fallback khi không tìm thấy số điện thoại chính.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động trích xuất thông tin liên lạc từ TruePeopleSearch với độ chính xác cao
- Xử lý hàng loạt dữ liệu từ Google Sheets mà không cần can thiệp thủ công
- Trường hợp fallback khi không tìm thấy số điện thoại chính
- Tiết kiệm thời gian và giảm thiểu lỗi con người
- Hoạt động liên tục 24/7 mà không cần giám sát
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản Zyte API (để bypass captcha và bot protection)
- Dữ liệu đầu vào trong Google Sheets với các cột: Name, Age, Address (để tìm kiếm trên TruePeopleSearch)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6886](https://n8n.io/workflows/6886)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node Webhook:**
- Đảm bảo đường dẫn webhook là duy nhất và bảo mật
- Có thể thay đổi path trong phần "Path" của node Webhook nếu cần

**Node Get row(s) in sheet:**
- Cấu hình credentials Google Sheets OAuth2
- Chỉ định chính xác Sheet ID và tên Sheet trong phần "Resource"

**Node Make HTTP Request for SearchURL:**
- Cấu hình credentials HTTP Basic Auth với Zyte API
- Thay thế user ID trong phần "Authentication" bằng ID của tài khoản Zyte của bạn
- Để trống phần "Password"

**Node Make HTTP Request for PersonURL:**
- Cấu hình tương tự như node Make HTTP Request for SearchURL
- Sử dụng cùng credentials HTTP Basic Auth với Zyte API

**Node Make HTTP Request for RelativeURL:**
- Cấu hình tương tự như node Make HTTP Request for SearchURL
- Sử dụng cùng credentials HTTP Basic Auth với Zyte API

**Các node Update Sheet:**
- Đảm bảo cấu hình credentials Google Sheets OAuth2
- Chỉ định chính xác Sheet ID và tên Sheet trong phần "Resource"
- Kiểm tra các cột trong Google Sheets để đảm bảo chúng khớp với dữ liệu được trích xuất

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Test workflow bằng cách gửi một yêu cầu đến webhook hoặc kích hoạt thủ công từ n8n Editor
3. Kiểm tra kết quả trong Google Sheets để đảm bảo dữ liệu được cập nhật đúng cách

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi workflow hoàn thành hoặc gặp lỗi
- Thiết lập lịch chạy định kỳ để xử lý dữ liệu mới hàng ngày
- Kết hợp với các workflow khác để tự động hóa toàn bộ chuỗi lead generation
- Thêm node để lưu log hoạt động của workflow để theo dõi hiệu suất

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình trích xuất thông tin liên lạc từ TruePeopleSearch, bao gồm cả trường hợp fallback khi không tìm thấy số điện thoại chính. Với việc tích hợp Zyte API, workflow này có thể vượt qua các cơ chế bảo vệ của TruePeopleSearch và hoạt động ổn định 24/7. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả lead generation!