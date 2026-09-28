---
title: "🚀 Tự động hóa GitHub Digest: Nhận báo cáo hàng tuần về releases, commits và trending repos qua Gmail"
description: "Workflow n8n tự động gửi báo cáo hàng tuần về các releases mới, commits gần đây và trending repos từ GitHub qua email Gmail. Tiết kiệm thời gian theo dõi thủ công và nhận thông tin quan trọng một cách nhanh chóng."
slug: "tu-dong-hoa-github-digest-voi-n8n"
tags: [n8n, automation, no-code, github, gmail]
keywords: [n8n workflow, tự động hóa, github digest, báo cáo hàng tuần, trending repos]
---

# 🚀 Tự động hóa GitHub Digest: Nhận báo cáo hàng tuần về releases, commits và trending repos qua Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thủ công các releases mới, commits gần đây và trending repos từ GitHub hàng tuần. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công các releases mới, commits gần đây và trending repos từ GitHub hàng tuần.
- **Nhận thông tin quan trọng một cách nhanh chóng**: Nhận báo cáo hàng tuần về các releases mới, commits gần đây và trending repos từ GitHub qua email Gmail.
- **Tăng hiệu suất làm việc**: Tự động hóa quy trình theo dõi giúp các sếp tập trung vào công việc quan trọng hơn.
- **Hoạt động liên tục**: Workflow chạy tự động vào mỗi thứ Hai lúc 9 giờ sáng, đảm bảo các sếp không bỏ lỡ bất kỳ thông tin quan trọng nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để nhận báo cáo hàng tuần.
- Danh sách các repositories và người dùng GitHub mà các sếp muốn theo dõi.
- Credentials Gmail OAuth2 để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Set Variables**: Cấu hình các biến cần thiết như `recipient_email`, `days_back`, `release_repos`, và `tracked_entities`.
- **Send Weekly Digest**: Cấu hình credentials Gmail OAuth2 để gửi email.
- **Fetch Latest Release**: Cấu hình URL để lấy thông tin về các releases mới từ các repositories đã theo dõi.
- **Fetch Entity Data**: Cấu hình URL để lấy thông tin về các commits gần đây từ các người dùng và repositories đã theo dõi.
- **Fetch GitHub Trending Page**: Cấu hình URL để lấy thông tin về các trending repos từ GitHub.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm GitHub Token**: Để tăng giới hạn yêu cầu API, các sếp có thể thêm GitHub Token vào header của các node HTTP Request.
- **Tùy chỉnh email template**: Các sếp có thể tùy chỉnh template email để phù hợp với nhu cầu của mình.
- **Kết hợp với Slack/Telegram**: Các sếp có thể kết hợp workflow với các kênh thông báo khác như Slack hoặc Telegram để nhận báo cáo hàng tuần.
- **Lưu log**: Các sếp có thể lưu log các báo cáo hàng tuần để theo dõi lịch sử và phân tích dữ liệu.

### 📌 Kết luận
Workflow n8n tự động gửi báo cáo hàng tuần về các releases mới, commits gần đây và trending repos từ GitHub qua email Gmail giúp các sếp tiết kiệm thời gian và nhận thông tin quan trọng một cách nhanh chóng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!