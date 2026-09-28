---
title: "🚀 Tự động phân loại sự cố Microsoft 365 vào Jira với GPT-4o-mini, PagerDuty và Teams"
description: "Hướng dẫn tự động hóa phân loại sự cố Microsoft 365 vào Jira với AI, PagerDuty và Teams - Tiết kiệm thời gian xử lý sự cố, tăng tính chính xác và tự động hóa toàn bộ quy trình."
slug: "tu-dong-phan-loai-su-co-microsoft-365-vao-jira-voi-gpt-4o-mini-pagerduty-teams"
tags: [n8n, automation, no-code, Microsoft 365, Jira, PagerDuty, Teams]
keywords: [n8n workflow, tự động hóa, Microsoft 365, Jira, PagerDuty, Teams, AI, GPT-4o-mini]
---

# 🚀 Tự động phân loại sự cố Microsoft 365 vào Jira với GPT-4o-mini, PagerDuty và Teams

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi xử lý thủ công các sự cố Microsoft 365. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý sự cố Microsoft 365 lên đến 80%
- Tăng tính chính xác trong phân loại và xử lý sự cố
- Tự động hóa toàn bộ quy trình từ nhận thông báo đến tạo ticket và thông báo
- Tăng tính minh bạch với các thành viên trong nhóm thông qua Teams
- Giảm thời gian phản hồi cho các sự cố quan trọng (P1/P2)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft 365 với quyền truy cập webhook
- Tài khoản Jira với quyền tạo issue
- Tài khoản PagerDuty với quyền tạo incident
- Tài khoản Microsoft Teams với quyền tạo webhook
- API key cho OpenAI (GPT-4o-mini)
- Biến môi trường WEBHOOK_SECRET
- Biến môi trường JIRA_PROJECT_KEY và JIRA_DOMAIN
- Biến môi trường PagerDuty SERVICE_ID và EMAIL
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15674)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Microsoft 365 Trigger** node:
   - Đảm bảo webhook được cấu hình đúng với endpoint của bạn
   - Kiểm tra lại biến môi trường WEBHOOK_SECRET

2. **AI Brain (GPT-4o-mini)** node:
   - Xác nhận sử dụng model GPT-4o-mini
   - Kiểm tra API key và cấu hình credentials

3. **Create Jira Incident** node:
   - Cấu hình đúng JIRA_PROJECT_KEY và JIRA_DOMAIN
   - Đảm bảo tài khoản có quyền tạo issue

4. **Trigger PagerDuty** node:
   - Cấu hình đúng PagerDuty SERVICE_ID và EMAIL
   - Đảm bảo tài khoản có quyền tạo incident

5. **Post to Teams** node:
   - Cấu hình webhook Teams đúng với endpoint của bạn
   - Kiểm tra định dạng Adaptive Card

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Kiểm tra lại tất cả các node và cấu hình
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo khi có sự cố mới
- Cấu hình gửi báo cáo hàng ngày về các sự cố đã xử lý
- Tích hợp với các công cụ giám sát khác để tăng tính toàn vẹn dữ liệu
- Thêm node để lưu log chi tiết các sự cố vào Google Sheets

### 📌 Kết luận
Workflow này giúp tự động hóa toàn bộ quy trình phân loại và xử lý sự cố Microsoft 365, từ nhận thông báo đến tạo ticket và thông báo. Với sự hỗ trợ của AI (GPT-4o-mini), workflow này đảm bảo tính chính xác cao trong phân loại và xử lý sự cố. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu suất xử lý sự cố trong tổ chức của bạn!