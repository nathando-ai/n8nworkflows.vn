---
title: "🏨 Tự động hóa thông điệp chào khách sạn cá nhân hóa bằng OpenAI, Google Sheets & Slack"
description: "Hướng dẫn tự động hóa thông điệp chào khách sạn cá nhân hóa 2 ngày trước khi khách đến, sử dụng công nghệ AI và Google Sheets để quản lý dữ liệu khách hàng."
slug: "tu-dong-hoa-thong-diep-chao-khach-san-ca-nhan-hoa"
tags: [n8n, automation, no-code, ai, google-sheets, slack]
keywords: [n8n workflow, tự động hóa khách sạn, thông điệp cá nhân hóa, AI khách sạn, quản lý khách hàng]
---

# 🏨 Tự động hóa thông điệp chào khách sạn cá nhân hóa bằng OpenAI, Google Sheets & Slack

[Các sếp khách sạn] đang gặp khó khăn khi phải gửi thông điệp chào khách hàng thủ công, đặc biệt là khi phải đối mặt với lượng lớn khách hàng và các yêu cầu cá nhân hóa khác nhau. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code, giúp tiết kiệm thời gian và tạo trải nghiệm khách hàng tuyệt vời hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc gửi thông điệp chào khách hàng thủ công.
- Tạo thông điệp cá nhân hóa dựa trên sở thích và lịch sử khách hàng.
- Tự động hóa toàn bộ quy trình quản lý khách hàng, từ lưu trữ dữ liệu đến gửi thông báo.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets với 3 sheet: profiles, updates, và message log.
- API key của OpenAI để tạo thông điệp cá nhân hóa.
- Tài khoản Slack để gửi thông báo.
- Thông tin SMTP để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12948](https://n8n.io/workflows/12948) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc copy toàn bộ nội dung JSON từ trang web và dán vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Fetch Guest Profiles**: Cấu hình Google Sheets OAuth2 để đọc dữ liệu từ sheet "profiles".
- **Generate Personalized Welcome Message**: Cập nhật OpenAI API key và prompt để tạo thông điệp cá nhân hóa.
- **Send Welcome Email**: Cấu hình SMTP để gửi email thông điệp chào.
- **Send Slack Notification**: Cập nhật Slack API key để gửi thông báo.
- **Daily Check Schedule**: Thiết lập lịch chạy workflow hàng ngày (khuyến nghị: 9 AM).

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo khi có khách hàng mới.
- Lưu log các thông điệp đã gửi vào Google Sheets để theo dõi.
- Gửi báo cáo hàng tuần về số lượng thông điệp đã gửi và tỷ lệ mở.

### 📌 Kết luận
Workflow này giúp các sếp khách sạn tự động hóa toàn bộ quy trình gửi thông điệp chào khách hàng cá nhân hóa, tiết kiệm thời gian và tạo trải nghiệm khách hàng tuyệt vời. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh!