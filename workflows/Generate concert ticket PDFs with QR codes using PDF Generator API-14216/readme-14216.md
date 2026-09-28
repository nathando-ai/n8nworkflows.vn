---
title: "🚀 Tự động tạo vé hòa nhạc kèm mã QR độc đáo với n8n và PDF Generator API"
description: "Hướng dẫn xây dựng workflow n8n tự động tiếp nhận đăng ký vé, tạo file PDF cá nhân hóa chứa mã QR, gửi email cho khách hàng, lưu vào Google Sheets và thông báo qua Slack."
slug: "tu-dong-tao-ve-hoa-nhac-kem-qr-code-n8n"
tags: [n8n, automation, pdf-generator-api, google-sheets, gmail, slack]
keywords: [n8n workflow, tạo vé tự động, pdf generator api, google sheets automation, tự động hóa bán vé]
keywords: [n8n workflow, tự động hóa, tạo vé pdf tự động, pdf generator api, google sheets, slack notification]
---

# 🚀 Tự động tạo vé hòa nhạc kèm mã QR độc đáo với n8n và PDF Generator API

Đã bao giờ các sếp cảm thấy đau đầu khi phải xử lý thủ công từng đơn đăng ký vé sự kiện: từ việc nhập liệu thông tin, thiết kế file vé, tạo mã QR, gửi email xác nhận cho khách cho đến việc cập nhật danh sách vào Google Sheets? Quy trình thủ công này không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-Code), giúp các sếp tối ưu toàn bộ quy trình bán và cấp phát vé sự kiện một cách mượt mà, chuyên nghiệp nhất!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Khách hàng điền form là nhận ngay vé PDF đẹp mắt kèm mã QR trong vài giây.
- **Cá nhân hóa cao:** Tùy biến linh hoạt tên khách hàng, số ghế, hạng vé (VIP, General, Backstage).
- **Đồng bộ dữ liệu thông minh:** Tự động lưu trữ và cập nhật trạng thái vé vào Google Sheets để quản lý check-in.
- **Thông báo thời gian thực:** Gửi alert tức thì qua Slack cho ban tổ chức mỗi khi có vé mới được phát hành.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance:** Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **PDF Generator API Account:** Đăng ký tài khoản tại [pdfgeneratorapi.com](https://pdfgeneratorapi.com) để tạo template vé.
- **Google Account:** Để sử dụng Gmail gửi vé và Google Sheets lưu trữ dữ liệu.
- **Slack Workspace:** (Tùy chọn) Để nhận thông báo vé mới.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải về từ kho lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình kỹ các node trọng điểm sau:

- **Node `Concert Ticket Form` (Form Trigger):** Node này tạo sẵn một trang web form để người dùng điền thông tin đặt vé. Các sếp có thể mở đường dẫn form do n8n cung cấp để test trực tiếp.
- **Node `Generate Concert Ticket PDF` (PDF Generator API):** 
  - Kết nối Credentials với tài khoản PDF Generator API của sếp.
  - Thay thế Template ID mặc định (`123456`) bằng **Template ID** thực tế từ trang quản trị của PDF Generator API.
  - *Mẹo về QR Code:* Mã QR được thiết kế trực tiếp trên template của PDF Generator API bằng cách trỏ data field đến biến `{{ ticket_id }}`. Workflow sẽ tự động truyền ID độc nhất vào đây mà không cần tool tạo QR riêng.
- **Node `Send Ticket to Attendee` (Gmail):** Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp để gửi email kèm link PDF vé (hoặc file đính kèm nếu đổi định dạng sang File).
- **Node `Log Ticket Sale` (Google Sheets):** 
  - Tạo sẵn một Google Sheet với tab tên là **Tickets** và các cột tiêu đề: `Ticket ID`, `Attendee`, `Email`, `Event`, `Venue`, `Date`, `Seat`, `Tier`, `PDF URL`, `Issued At`.
  - Kết nối tài khoản Google và trỏ Spreadsheet ID vào node này (chọn operation `appendOrUpdate`).
- **Node `Notify Event Organizer` (Slack):** Kết nối workspace Slack và chọn kênh nhận thông báo (ví dụ: `#tickets` hoặc `#events`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một bản đăng ký qua form để test luồng dữ liệu.
- Kiểm tra email nhận vé, dữ liệu trên Google Sheets và thông báo trên Slack.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Zalo/Telegram:** Thay thế hoặc bổ sung node Slack bằng Telegram Bot để gửi thông báo vé mới thẳng vào điện thoại của ban tổ chức.
- **Quản lý Check-in tại cửa:** Sử dụng file Google Sheets được log tự động kết hợp với các app quét mã QR để soát vé nhanh chóng trong ngày diễn ra sự kiện.
- **Gửi email nhắc nhở:** Thêm một nhánh trì hoãn (Wait node) để gửi email nhắc nhở khách hàng 24h trước khi sự kiện diễn ra.

### 📌 Kết luận
Với workflow n8n tích hợp PDF Generator API này, các sếp hoàn toàn có thể tự xây dựng một hệ thống phát hành vé tự động chuyên nghiệp chỉ trong tích tắc. Hãy áp dụng ngay vào sự kiện tiếp theo của doanh nghiệp để tiết kiệm hàng chục giờ làm việc thủ công!