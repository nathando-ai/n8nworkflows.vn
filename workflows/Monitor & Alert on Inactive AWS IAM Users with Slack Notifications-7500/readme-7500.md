---
title: "🚀 Tự động cảnh báo tài khoản AWS IAM không hoạt động qua Slack với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động quét và gửi cảnh báo qua Slack cho các tài khoản AWS IAM không hoạt động trên 90 ngày, giúp tối ưu bảo mật Cloud."
slug: "tu-dong-canh-bao-tai-khoan-aws-iam-khong-hoat-dong-qua-slack-n8n"
tags: [n8n, automation, aws, secops, slack, cloud-security]
keywords: [n8n workflow, aws iam security, tự động hóa secops, cảnh báo slack aws, quản lý iam inactive]
---

# 🚀 Tự động cảnh báo tài khoản AWS IAM không hoạt động qua Slack

Các sếp làm DevOps hoặc quản lý hạ tầng Cloud có bao giờ đau đầu vì các tài khoản IAM "bỏ hoang" (không sử dụng trong nhiều tháng) nhưng vẫn còn tồn tại quyền truy cập? Việc quên xóa các tài khoản này tạo ra lỗ hổng bảo mật cực kỳ nguy hiểm cho doanh nghiệp.

Thay vì phải thủ công kiểm tra AWS Console hàng tuần, workflow n8n này sẽ tự động hóa 100% quy trình: quét danh sách IAM users, lọc ra các tài khoản không hoạt động trên 90 ngày và gửi cảnh báo trực tiếp về kênh Slack của đội ngũ bảo mật.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng cường bảo mật Cloud:** Phát hiện và thu hồi kịp thời các tài khoản AWS IAM không còn sử dụng nhưng vẫn tiềm ẩn rủi ro lộ khóa.
- **Tiết kiệm thời gian:** Tự động hóa hoàn toàn tác vụ kiểm tra định kỳ hàng tuần mà không cần sự can thiệp thủ công.
- **Cảnh báo tức thì:** Thông báo chi tiết tên tài khoản, ARN và thời gian không hoạt động thẳng vào Slack để đội ngũ SRE xử lý ngay.
- **Dễ dàng mở rộng:** Có thể tùy biến mốc thời gian (60, 90, 180 ngày) hoặc tích hợp thêm các hành động tự động hóa khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt và đang hoạt động (phiên bản hiện tại).
- **AWS Credentials:** Tài khoản AWS với quyền đọc IAM (tối thiểu `iam:ListUsers`, `iam:GetUser`).
- **Slack Bot:** Đã tạo Slack App/Bot với quyền đăng bài vào kênh Slack mục tiêu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (ID: `7500`) và tiến hành Import trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng 8 nodes chính. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Weekly scheduler`**: Cấu hình lịch chạy tự động (mặc định vào thứ Hai hàng tuần lúc 09:00).
- **Node `Get many users` & `Get user` (awsIam)**: 
  - Chọn AWS Credentials đã chuẩn bị.
  - ⚠️ **Lưu ý quan trọng cực kỳ:** AWS SigV4 cho IAM **bắt buộc phải cấu hình Region là `us-east-1`** (ngay cả khi các dịch vụ AWS khác của sếp chạy ở region khác).
- **Node `Filter bad data` (filter)**: Lọc bỏ các tài khoản service-linked hoặc dữ liệu không hợp lệ để tránh nhiễu log.
- **Node `IAM user inactive for more than 90 days?` (if)**: Kiểm tra mốc thời gian `PasswordLastUsed` hoặc thời gian tạo so với hiện tại trừ đi 90 ngày. Sếp có thể tùy chỉnh lại số ngày trong biểu thức.
- **Node `Send a message` (slack)**: Chọn Slack OAuth2 Credentials và điền ID kênh Slack nhận thông báo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công để kiểm tra dữ liệu trả về từ AWS và định dạng tin nhắn trên Slack.
- Bật công tắc **Active workflow** để hệ thống tự động chạy ngầm theo lịch đã đặt.

---
![](https://wisestackai.s3.ap-southeast-1.amazonaws.com/Screenshot+2025-08-17+at+1.32.23%E2%80%AFPM.png)

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh khoảng thời gian:** Thay đổi mốc 90 ngày thành 60 hoặc 120 ngày tùy thuộc vào chính sách bảo mật nội bộ của công ty.
- **Lưu Audit Log:** Kết hợp thêm node Google Sheets hoặc Database để lưu trữ lịch sử kiểm tra định kỳ phục vụ việc báo cáo kiểm toán (Compliance).
- **Leo thang sự cố (Escalation):** Nếu tài khoản tiếp tục không hoạt động ở chu kỳ tiếp theo, cấu hình workflow tự động gắn thẻ `@security` trên Slack hoặc tạo ticket trên Jira.
- **Danh sách ngoại lệ (Exclude list):** Thêm bộ lọc tag hoặc danh sách tĩnh để bỏ qua các tài khoản dịch vụ (service accounts) đặc thù.

### 📌 Kết luận
Việc tự động hóa kiểm tra bảo mật AWS IAM không chỉ giúp doanh nghiệp tránh khỏi các rủi ro tấn công leo thang đặc quyền mà còn giải phóng rất nhiều thời gian cho đội ngũ kỹ thuật. Hãy áp dụng ngay workflow này vào hệ thống n8n của các sếp để nâng cấp lớp phòng thủ Cloud ngay hôm nay!