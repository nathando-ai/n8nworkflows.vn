---
title: "🚀 Tự động hóa tuân thủ IAM AWS: Ép buộc MFA và vô hiệu hóa Access Key kém bảo mật"
description: "Hướng dẫn cài đặt workflow n8n tự động quét tài khoản AWS IAM hàng ngày, phát hiện người dùng chưa bật MFA, gửi cảnh báo qua Slack và tự động vô hiệu hóa Access Key."
slug: "tu-dong-hoa-tuan-thu-iam-aws-mfa"
tags: [n8n, automation, no-code, aws, secops, slack]
keywords: [n8n workflow, tự động hóa aws iam, ép buộc mfa aws, bảo mật cloud secops, n8n aws iam compliance]
---

# 🚀 Tự động hóa tuân thủ IAM AWS: Ép buộc MFA và vô hiệu hóa Access Key kém bảo mật

Các kỹ sư DevOps và SecOps chắc chắn hiểu rõ nỗi đau khi quản lý bảo mật trên AWS. Việc người dùng quên bật MFA (Xác thực đa yếu tố) hoặc để lộ các Access Key không an toàn là "cửa ngõ" chính cho các cuộc tấn công chiếm đoạt tài khoản cloud. Làm thủ công việc kiểm tra này mỗi ngày là bất khả thi và tốn kém thời gian.

Workflow n8n này sinh ra để giải quyết triệt để bài toán đó: tự động quét toàn bộ tài khoản AWS IAM, phát hiện các tài khoản "vô kỷ luật" chưa bật MFA, gửi cảnh báo qua Slack và tự động vô hiệu hóa các Access Key nguy hiểm một cách hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối an toàn với AWS, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật 24/7:** Chủ động rà soát tài khoản AWS hàng ngày mà không cần thao tác thủ công.
- **Cảnh báo tức thì:** Gửi thông báo trực tiếp qua Slack để đội ngũ nắm bắt tình hình ngay lập tức.
- **Ngăn chặn rủi ro kịp thời:** Tự động khóa các Access Key của tài khoản không tuân thủ quy định MFA.
- **Tiết kiệm thời gian:** Thay vì tốn hàng giờ kiểm tra Console, hệ thống tự động hóa 100%.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt sẵn n8n (Self-hosted hoặc Cloud).
- **AWS Credentials:** Tài khoản IAM User hoặc IAM Role có các quyền tối thiểu:
  - `iam:ListUsers`
  - `iam:ListMFADevices`
  - `iam:ListAccessKeys`
  - `iam:UpdateAccessKey`
- **Slack Workspace:** Đã tạo Bot Token với quyền `chat:write` để gửi tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn mã JSON của workflow từ n8n hoặc import file trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình các node quan trọng sau:

- **Daily scheduler**: Cấu hình lịch chạy định kỳ (ví dụ: Chạy lúc 9:00 sáng mỗi ngày).
- **Get many users** & **Get IAM User MFA Devices** & **Get User Access Key(s)** & **Deactivate Access Key(s)**: Chọn đúng **AWS Credentials** đã chuẩn bị ở phần yêu cầu. Đảm bảo các quyền IAM đáp ứng đủ để gọi các API tương ứng (`ListUsers`, `ListMFADevices`, `ListAccessKeys`, `UpdateAccessKey`).
- **Send warning message(s)** & **Send message and wait for response**: Kết nối với tài khoản Slack thông qua `slackOAuth2Api`, sau đó chọn kênh (Channel) nhận thông báo cảnh báo bảo mật.
- **Parse the list of user access key(s)** (Code node): Node này xử lý logic bóc tách dữ liệu JSON trả về từ AWS để lấy thông tin `AccessKeyId`, `Status`, và `UserName`. Kiểm tra kỹ đoạn code JS bên trong nếu muốn tùy biến cấu trúc dữ liệu.
- **Filter out IAM user with MFA device** & **Filter out inactive keys**: Kiểm tra điều kiện lọc dữ liệu đảm bảo hệ thống chỉ chọn các user chưa bật MFA và các Access Key đang ở trạng thái `Active`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test Run) với dữ liệu thực tế và kiểm tra kết quả trên Slack cũng như AWS.
- Nếu mọi thứ hoạt động mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thời gian ân hạn (Delay):** Thay vì khóa ngay lập tức, hãy thêm node Wait để cảnh báo user trong 24h, nếu họ không bật MFA thì mới tiến hành khóa Access Key.
- **Loại trừ ngoại lệ (Whitelist):** Thêm một node IF để bỏ qua các tài khoản Service Accounts hoặc tài khoản quản trị đặc biệt không áp dụng chính sách MFA này.
- **Lưu nhật ký kiểm toán (Audit Log):** Kết nối thêm node Google Sheets hoặc Airtable để lưu lịch sử các user vi phạm và thời gian Access Key bị khóa phục vụ việc báo cáo kiểm toán bảo mật.
- **Đa kênh thông báo:** Ngoài Slack, có thể tích hợp thêm Telegram Bot hoặc gửi Email cảnh báo cho đội ngũ quản trị.

### 📌 Kết luận
Bảo mật đám mây luôn là ưu tiên hàng đầu của mọi doanh nghiệp. Với workflow n8n tự động hóa tuân thủ AWS IAM này, các sếp có thể yên tâm rằng hệ thống luôn được giám sát chặt chẽ, loại bỏ hoàn toàn các lỗ hổng do con người gây ra. Áp dụng ngay hôm nay để tối ưu hóa vận hành SecOps cho tổ chức của mình!