---
title: "🚀 Tự động đồng bộ Workflow GitHub sang n8n sau khi Pull Request được merge"
description: "Hướng dẫn tự động hóa đồng bộ các workflow từ GitHub sang n8n sau khi pull request được merge, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-workflow-github-sang-n8n"
tags: [n8n, automation, no-code, devops, github]
keywords: [n8n workflow, tự động hóa, devops, github, pull request]
---

# 🚀 Tự động đồng bộ Workflow GitHub sang n8n sau khi Pull Request được merge

[Các sếp đang gặp khó khăn khi phải thủ công đồng bộ các workflow từ GitHub sang n8n sau khi pull request được merge. Việc này tốn thời gian, dễ xảy ra lỗi và không hiệu quả. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này, đảm bảo đồng bộ liên tục và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ các workflow từ GitHub sang n8n sau khi pull request được merge
- Giảm thiểu thời gian và công sức cho việc thủ công đồng bộ
- Đảm bảo tính chính xác và liên tục trong quá trình đồng bộ
- Tiết kiệm thời gian cho các công việc khác quan trọng hơn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với quyền truy cập vào repository chứa các workflow
- Tài khoản n8n với quyền truy cập API
- GitHub Personal Access Token (PAT) với các quyền `repo` và `admin:repo_hook`
- Thông tin về repository GitHub (owner và tên repository)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn file JSON của workflow hoặc copy/paste JSON vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Define Local Variables"**:
   - Cập nhật các biến `github_owner` và `repo_name` với thông tin của repository GitHub của các sếp

2. **Node "Github Trigger - When there is new pull request"**:
   - Cấu hình credentials cho GitHub API
   - Đảm bảo đã tạo webhook cho repository GitHub với sự kiện `pull_request`

3. **Node "Fetch merged commit details via GitHub API"**:
   - Cấu hình credentials cho GitHub API

4. **Node "Fetch workflow content from Git" và "Fetch workflow content from Git1"**:
   - Cấu hình credentials cho GitHub API

5. **Node "Update workflow in n8n" và "Create new workflow in n8n"**:
   - Cấu hình credentials cho n8n API

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu tự động đồng bộ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có sự kiện pull request được merge
- Lưu log các hoạt động đồng bộ để theo dõi và kiểm tra
- Tự động gửi báo cáo định kỳ về các workflow đã được đồng bộ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình đồng bộ workflow từ GitHub sang n8n sau khi pull request được merge, tiết kiệm thời gian và giảm thiểu lỗi thủ công. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!