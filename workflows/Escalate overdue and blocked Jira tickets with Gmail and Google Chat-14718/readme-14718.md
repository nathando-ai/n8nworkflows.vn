---
title: "🚀 Tự động hóa cảnh báo & leo thang sự cố Jira quá hạn, bị tắc nghẽn với Gmail & Google Chat"
description: "Xây dựng hệ thống tự động giám sát ticket Jira, phân cấp cảnh báo thông minh qua Gmail và Google Chat dựa trên số ngày quá hạn hoặc bị tắc nghẽn."
slug: "tu-dong-hoa-canh-bao-jira-qua-han-blocked"
tags: [n8n, automation, jira, gmail, google-chat, project-management]
keywords: [n8n workflow, jira automation, tự động hóa jira, cảnh báo quá hạn jira, google chat webhook, gmail oauth2]
---

# 🚀 Tự động hóa cảnh báo & leo thang sự cố Jira quá hạn, bị tắc nghẽn

Trong quản lý dự án, việc các ticket Jira bị quá hạn (Overdue) hoặc bị tắc nghẽn (Blocked) mà không được xử lý kịp thời thường làm chậm tiến độ toàn dự án. Việc theo dõi thủ công mỗi ngày là một cực hình và rất dễ bỏ sót.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: quét các ticket mở hàng ngày, tính toán thời gian quá hạn/bị chặn, sau đó phân cấp thông báo từ nhắc nhở nhẹ nhàng cho nhân sự, cảnh báo nhóm qua Google Chat, cho đến leo thang lên cấp quản lý qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ mỗi ngày nhờ `Schedule Trigger`, không cần can thiệp thủ công.
- **Phân cấp thông minh (Progressive Escalation):** 
  - 🧠 *Nhắc nhở (0-2 ngày tới hạn):* Gửi email trực tiếp cho người được giao (Assignee).
  - ⚠️ *Cảnh báo (1-4 ngày quá hạn / 1-2 ngày bị chặn):* Gửi email hoặc thông báo vào kênh Google Chat của team.
  - 🚨 *Leo thang (Quá hạn >4 ngày / Bị chặn 3 ngày):* Gửi email trực tiếp cho Manager.
- **Kiểm soát rate limit:** Tích hợp các node `Wait` và `Split In Batches` để tránh bị Google API block do gửi quá nhiều request cùng lúc.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Jira Software Cloud** (Tài khoản và quyền truy cập API).
- **Gmail (OAuth2)** để gửi email tự động.
- **Google Chat Webhook URL** để gửi thông báo vào không gian làm việc (Space/Channel).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc hoặc copy trực tiếp mã nguồn JSON dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này được thiết kế cực kỳ thông minh: **Các sếp chỉ cần chỉnh sửa đúng một node duy nhất là `⚙️ CONFIG`**.

- **`⚙️ CONFIG` (Set Node):** Điền chính xác 4 tham số quan trọng sau:
  - `JIRA_DOMAIN`: Ví dụ `my-company.atlassian.net`
  - `JIRA_PROJECT_KEY`: Mã dự án của sếp, ví dụ `PROJ`
  - `MANAGER_EMAILS`: Email của quản lý nhận báo cáo leo thang.
  - `GOOGLE_CHAT_WEBHOOK_URL`: Webhook URL của Google Chat Space.
- **Kết nối Credentials:**
  - `GET_JIRA_ISSUES`: Chọn Jira Software Cloud API credentials.
  - Các node gửi email (`MANAGER_ESCALATION`, `SEND_DUEDATE_REMINDER`, `SEND_BLOCKED_WARNING`, v.v.): Chọn Gmail OAuth2 credentials.

#### 3. Kích hoạt ⚡️
- Nhấn `Execute Workflow` bằng nút `When clicking ‘Execute workflow’` để chạy thử nghiệm dữ liệu mẫu.
- Sau khi kiểm tra mọi thứ trơn tru, bật trạng thái **Active** cho `Schedule Trigger` để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Google Chat và Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack ở các nhánh cảnh báo `NOTIFY_TEAM`.
- **Tối ưu Quota:** Lưu ý giới hạn của Gmail (2,000 người nhận/ngày với Workspace) và Google Chat (60 tin nhắn/phút/space). Workflow đã tích hợp sẵn cơ chế chờ (`Wait - Rate Limit`), các sếp giữ nguyên để hệ thống chạy mượt mà.
- **Lưu lịch sử:** Có thể bổ sung thêm một node Google Sheets để ghi log mỗi khi có ticket bị leo thang lên Manager nhằm phục vụ việc đánh giá hiệu suất đội ngũ.

### 📌 Kết luận
Với workflow này, việc theo dõi tiến độ Jira không còn là nỗi ám ảnh mỗi sáng thứ Hai. Thiết lập ngay một lần và để hệ thống tự động hóa toàn bộ quy trình nhắc nhở, cảnh báo cho doanh nghiệp của các sếp!