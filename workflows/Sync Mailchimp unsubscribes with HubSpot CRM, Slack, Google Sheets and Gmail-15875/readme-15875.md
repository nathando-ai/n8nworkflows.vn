---
title: "🚀 Tự động hóa Mailchimp: Đồng bộ hủy đăng ký với HubSpot, Slack, Google Sheets và Gmail"
description: "Tự động cập nhật thông tin khách hàng khi hủy đăng ký Mailchimp, gửi thông báo Slack, lưu dữ liệu vào Google Sheets và gửi email xác nhận - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-hoa-mailchimp-dong-bo-huy-dang-ky-voi-hubspot-slack-google-sheets-gmail"
tags: [n8n, automation, no-code, mailchimp, hubspot, google-sheets, slack, gmail]
keywords: [n8n workflow, tự động hóa mailchimp, quản lý hủy đăng ký, đồng bộ dữ liệu CRM, gửi email tự động]
---

# 🚀 Tự động hóa Mailchimp: Đồng bộ hủy đăng ký với HubSpot, Slack, Google Sheets và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi khách hàng hủy đăng ký nhận email từ Mailchimp, các sếp thường phải thực hiện nhiều bước thủ công: cập nhật trạng thái trong CRM, gửi thông báo cho đội ngũ, lưu dữ liệu vào bảng tính và gửi email xác nhận. Quá trình này tốn thời gian, dễ xảy ra lỗi và không đồng bộ giữa các hệ thống.

Workflow này giúp các sếp tự động hóa hoàn toàn quy trình này với chỉ 12 node đơn giản, tiết kiệm thời gian và giảm thiểu lỗi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động cập nhật trạng thái khách hàng trong HubSpot khi hủy đăng ký
- Gửi thông báo tức thời đến Slack để đội ngũ biết ngay
- Lưu trữ dữ liệu hủy đăng ký vào Google Sheets để theo dõi
- Gửi email xác nhận tự động đến khách hàng
- Tiết kiệm thời gian xử lý thủ công lên tới 90%
- Giảm thiểu lỗi do nhập liệu thủ công
- Đồng bộ dữ liệu giữa các hệ thống một cách chính xác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mailchimp với quyền truy cập API
- Tài khoản HubSpot với quyền truy cập API
- Tài khoản Slack với quyền gửi tin nhắn
- Tài khoản Google với quyền truy cập Google Sheets và Gmail
- API Key cho các dịch vụ tương ứng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15875)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Mailchimp - Unsubscribe Trigger** (Node đầu tiên):
   - Cấu hình credentials cho Mailchimp API
   - Đảm bảo tài khoản Mailchimp có quyền truy cập webhook

2. **Update HubSpot Contact** và **Create HubSpot Contact**:
   - Cấu hình credentials cho HubSpot API
   - Kiểm tra các tham số trong body của request (ID, email, status...)
   - Đảm bảo tài khoản HubSpot có quyền truy cập vào các trường dữ liệu cần cập nhật

3. **Slack - Alert** và **Slack - Log to**:
   - Cấu hình credentials cho Slack API
   - Chỉnh sửa nội dung thông báo theo nhu cầu của đội ngũ
   - Đảm bảo bot Slack có quyền gửi tin nhắn đến các kênh cần thiết

4. **Store Unsubscribe Details in Sheet**:
   - Cấu hình credentials cho Google Sheets OAuth2
   - Chỉnh sửa ID của Google Sheet và tên sheet cần ghi dữ liệu
   - Đảm bảo tài khoản Google có quyền truy cập vào sheet này

5. **Send a confirmation email**:
   - Cấu hình credentials cho Gmail OAuth2
   - Chỉnh sửa nội dung email xác nhận theo mẫu mong muốn
   - Đảm bảo tài khoản Gmail có quyền gửi email

6. **HubSpot - Search Contact by Email**:
   - Cấu hình credentials cho HubSpot API
   - Kiểm tra các tham số trong query của request (email, properties...)
   - Đảm bảo tài khoản HubSpot có quyền truy cập vào các trường dữ liệu cần tìm kiếm

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Tạo một hủy đăng ký mẫu trong Mailchimp
   - Kiểm tra xem workflow có bắt được sự kiện này không
   - Xác minh các hành động được thực hiện (cập nhật HubSpot, gửi Slack, lưu Google Sheets, gửi email...)

2. Bật Active workflow:
   - Sau khi test thành công, bật chế độ Active cho workflow
   - Đặt lịch chạy workflow theo nhu cầu (thường xuyên, định kỳ...)

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Telegram: Thay thế hoặc bổ sung Slack bằng bot Telegram để nhận thông báo
2. Lưu log chi tiết: Thêm node để lưu log chi tiết hơn vào Google Sheets hoặc cơ sở dữ liệu
3. Gửi báo cáo định kỳ: Tạo một workflow phụ để gửi báo cáo hàng tuần/tháng về các hủy đăng ký
4. Tích hợp với Zoho CRM: Thay thế HubSpot bằng Zoho CRM nếu sử dụng hệ thống này
5. Xử lý các trường hợp đặc biệt: Thêm logic để xử lý các trường hợp hủy đăng ký đặc biệt (ví dụ: hủy đăng ký từ nhiều danh sách)

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình xử lý hủy đăng ký từ Mailchimp, đồng bộ dữ liệu với HubSpot, thông báo qua Slack, lưu trữ vào Google Sheets và gửi email xác nhận. Với chỉ 12 node đơn giản, các sếp có thể tiết kiệm thời gian đáng kể và giảm thiểu lỗi do nhập liệu thủ công. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của đội ngũ!