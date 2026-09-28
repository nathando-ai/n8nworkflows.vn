---
title: "🚀 [Tự động hóa DevOps] Gửi thông báo Slack khi có phiên bản mới trên Github"
description: "Hướng dẫn tự động hóa gửi thông báo Slack khi có phiên bản mới của các kho lưu trữ công khai trên Github. Tiết kiệm thời gian theo dõi thủ công và nhận thông báo tức thì."
slug: "tu-dong-hoa-thong-bao-slack-github-release"
tags: [n8n, automation, no-code, devops, github]
keywords: [n8n workflow, tự động hóa, github release, slack notification, devops]
---

# 🚀 [Tự động hóa DevOps] Gửi thông báo Slack khi có phiên bản mới trên Github

[Các sếp làm DevOps thường phải theo dõi thủ công các phiên bản mới của các kho lưu trữ Github công khai. Việc này tốn thời gian và dễ bỏ sót. Workflow này sẽ tự động hóa quy trình này bằng cách kiểm tra hàng ngày và gửi thông báo Slack tức thì khi có phiên bản mới.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian theo dõi thủ công.
- Nhận thông báo tức thì khi có phiên bản mới.
- Hoạt động liên tục 24/7 mà không cần can thiệp.
- Tự động hóa quy trình DevOps.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack và quyền gửi tin nhắn.
- API key của Slack.
- Danh sách các kho lưu trữ Github cần theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **RepoConfig**: Cấu hình danh sách các kho lưu trữ Github cần theo dõi. Thêm các đối tượng JSON vào mảng với các thuộc tính `org` và `repo`.
- **Send Message**: Cập nhật node này để tùy chỉnh thông báo Slack. Cấu hình các tham số như `channel`, `text`, `blocks` để định dạng thông báo theo ý muốn.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Telegram để nhận thông báo.
- Lưu log các phiên bản đã kiểm tra để theo dõi lịch sử.
- Gửi báo cáo định kỳ về các phiên bản mới.

### 📌 Kết luận
Workflow này giúp các sếp DevOps tiết kiệm thời gian và nhận thông báo tức thì khi có phiên bản mới trên Github. Hãy áp dụng ngay để tự động hóa quy trình DevOps của bạn!