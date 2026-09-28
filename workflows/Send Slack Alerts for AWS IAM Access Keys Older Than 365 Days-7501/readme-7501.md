---
title: "🚨 [Tự động cảnh báo Slack khi AWS IAM Access Keys quá 365 ngày]"
description: "Hướng dẫn tự động hóa kiểm tra và cảnh báo các access keys AWS quá 365 ngày qua Slack, đảm bảo an toàn tài khoản AWS của bạn."
slug: "tu-dong-kiem-tra-aws-iam-access-keys-qua-365-ngay"
tags: [n8n, automation, no-code, AWS, security, DevOps]
keywords: [n8n workflow, tự động hóa, AWS IAM, security, DevOps]
---

# 🚨 [Tự động cảnh báo Slack khi AWS IAM Access Keys quá 365 ngày]

[Các sếp đang gặp khó khăn khi phải kiểm tra thủ công các access keys AWS để đảm bảo an ninh tài khoản. Với workflow này, các sếp có thể tự động hóa quy trình này và nhận cảnh báo ngay khi có access keys quá 365 ngày.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động kiểm tra hàng tuần mà không cần can thiệp thủ công.
- Đảm bảo an ninh: Nhận cảnh báo ngay khi có access keys quá 365 ngày.
- Tăng tính minh bạch: Ghi lại và theo dõi các access keys trong tài khoản AWS.
- Hoạt động liên tục: Workflow chạy tự động mà không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản AWS với quyền truy cập IAM.
- Credentials AWS trong n8n với các quyền: `iam:ListUsers`, `iam:ListAccessKeys`.
- Credentials Slack trong n8n với quyền gửi tin nhắn vào kênh mong muốn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Click vào "Import from URL" và nhập link: [https://n8n.io/workflows/7501](https://n8n.io/workflows/7501).
3. Hoặc copy/paste JSON từ file workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Weekly scheduler**: Cấu hình lịch chạy hàng tuần (ví dụ: mỗi thứ Hai).
- **Get many users**: Đảm bảo credentials AWS được chọn đúng và có quyền truy cập vào tài khoản IAM.
- **Get User Access Key(s)**: Đảm bảo credentials AWS được chọn đúng và có quyền truy cập vào tài khoản IAM.
- **Send a message**: Cấu hình credentials Slack và kênh nhận thông báo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để chạy tự động hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi ngưỡng**: Điều chỉnh điều kiện `365 days` thành 90, 180 ngày hoặc bất kỳ chính sách nào khác.
- **Tăng cường cảnh báo**: Đề cập đến `@security` hoặc tạo ticket Jira khi phát hiện access keys cũ.
- **Lưu log**: Đẩy kết quả vào Google Sheet, cơ sở dữ liệu hoặc hệ thống quản lý log để kiểm toán.
- **Tự động hóa thêm**: Thay vì chỉ cảnh báo, thêm bước tự động vô hiệu hóa access keys cũ sau khi được phê duyệt.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc kiểm tra và cảnh báo các access keys AWS quá 365 ngày, đảm bảo an ninh tài khoản AWS của mình. Hãy áp dụng ngay để tiết kiệm thời gian và tăng tính minh bạch trong quản lý tài khoản AWS.