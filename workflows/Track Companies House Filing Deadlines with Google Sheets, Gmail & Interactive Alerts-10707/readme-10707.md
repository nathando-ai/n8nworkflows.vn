---
title: "🚀 Tự động hóa theo dõi hạn nộp công ty tại UK với Google Sheets, Gmail và cảnh báo tương tác"
description: "Hướng dẫn chi tiết cách tự động theo dõi hạn nộp công ty tại UK, nhận cảnh báo qua email với mức độ ưu tiên và cập nhật trạng thái hoàn thành thông qua nút nhấn tương tác."
slug: "tu-dong-hoa-theo-doi-han-nop-cong-ty-tai-uk"
tags: [n8n, automation, no-code, google-sheets, gmail, companies-house]
keywords: [n8n workflow, tự động hóa, theo dõi hạn nộp, công ty UK, cảnh báo email, google sheets]
---

# 🚀 Tự động hóa theo dõi hạn nộp công ty tại UK với Google Sheets, Gmail và cảnh báo tương tác

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các công ty kế toán khi phải theo dõi thủ công các hạn nộp công ty tại UK. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho việc theo dõi thủ công.
- Giảm thiểu lỗi do quên hạn nộp, tránh phạt tiền từ £150 đến £1,500.
- Cảnh báo ưu tiên với màu sắc (đỏ, cam, vàng, xanh) giúp tập trung vào các hạn nộp quan trọng nhất.
- Tạo ra một hệ thống theo dõi hoàn chỉnh trong Google Sheets với lịch sử cập nhật đầy đủ.
- Tăng tính minh bạch và trách nhiệm trong đội ngũ với tính năng xác nhận tương tác qua email.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets với bảng dữ liệu có cấu trúc như sau:
  - company_number (nhập thủ công)
  - company_name (nhập thủ công)
  - accounts_due (cập nhật tự động)
  - confirmation_due (cập nhật tự động)
  - confirmation_submitted (cập nhật qua email)
  - last_updated (timestamp tự động)
- API Key từ Companies House (miễn phí từ [api.company-information.service.gov.uk](https://api.company-information.service.gov.uk/)).
- Tài khoản Gmail để gửi cảnh báo.
- Cập nhật URL webhook trong node "Build Interactive Email" để khớp với instance n8n của bạn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/10707).
2. Nhấn nút "Copy to clipboard" để sao chép JSON workflow.
3. Trong n8n Editor, nhấn vào "Import from Clipboard" và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Webhook - Receive Confirmation Update**:
  - Đảm bảo đường dẫn "confirmation-updates" là duy nhất và khớp với URL webhook của bạn.
  - Cập nhật URL này trong node "Build Interactive Email" để tạo liên kết xác nhận chính xác.

- **Read Company Database**:
  - Chọn credentials Google Sheets OAuth2 đã được thiết lập.
  - Điền ID của Google Sheet chứa dữ liệu công ty.
  - Đảm bảo tên bảng và phạm vi dữ liệu khớp với cấu trúc đã định nghĩa.

- **Get Company Data**:
  - Thêm API Key từ Companies House vào credentials HTTP Basic Auth.
  - Đảm bảo endpoint API là chính xác và có quyền truy cập.

- **Send via Gmail**:
  - Thiết lập credentials Gmail OAuth2.
  - Cấu hình địa chỉ email người nhận và chủ đề email.

- **Update Due Dates in Sheet**:
  - Sử dụng cùng credentials Google Sheets OAuth2 với node "Read Company Database".
  - Đảm bảo tên bảng và phạm vi dữ liệu khớp với cấu trúc đã định nghĩa.

#### 3. Kích hoạt ⚡️
- Chạy thử với dữ liệu mẫu để kiểm tra toàn bộ chuỗi hoạt động.
- Bật Active workflow để hệ thống tự động chạy hàng ngày lúc 17:00 (GMT).

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận cảnh báo cùng lúc với email.
- Tạo bản sao lưu tự động của Google Sheet hàng tuần.
- Thêm tính năng nhắc nhở nhẹ nhàng cho các hạn nộp sắp tới (ví dụ: 3 ngày trước hạn).
- Kết hợp với hệ thống báo cáo định kỳ để theo dõi hiệu suất của đội ngũ theo dõi hạn nộp.

### 📌 Kết luận
Workflow này không chỉ giúp các công ty kế toán tiết kiệm thời gian mà còn nâng cao tính chính xác và minh bạch trong quá trình theo dõi hạn nộp công ty tại UK. Với hệ thống cảnh báo ưu tiên và tính năng xác nhận tương tác, các sếp có thể yên tâm rằng không có hạn nộp nào bị bỏ sót. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!