---
title: "🚀 Tự động hóa ghi âm cuộc họp thành công việc Jira/ClickUp/Linear với Whisper và Claude"
description: "Hướng dẫn tự động hóa chuyển đổi ghi âm cuộc họp thành công việc trong Jira, ClickUp và Linear bằng công nghệ AI Whisper và Claude. Tiết kiệm thời gian và nâng cao năng suất làm việc."
slug: "tu-dong-hoa-ghi-am-cuoc-hop-thanh-cong-viec-jira-clickup-linear"
tags: [n8n, automation, no-code, jira, clickup, linear, ai, whisper, claude]
keywords: [n8n workflow, tự động hóa, ghi âm cuộc họp, jira, clickup, linear, whisper, claude]
---

# 🚀 Tự động hóa ghi âm cuộc họp thành công việc Jira/ClickUp/Linear với Whisper và Claude

[Các sếp đang gặp khó khăn khi phải chuyển đổi ghi âm cuộc họp thành công việc trong các công cụ quản lý dự án như Jira, ClickUp hay Linear. Việc này tốn thời gian và dễ gây lỗi. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này bằng công nghệ AI tiên tiến.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động chuyển đổi ghi âm thành công việc trong 5-10 phút.
- Tăng độ chính xác: AI Whisper và Claude đảm bảo chất lượng chuyển đổi cao.
- Cá nhân hóa: Tự động gán công việc cho thành viên phù hợp.
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần can thiệp.
- Tích hợp đa nền tảng: Hỗ trợ Zoom, Google Meet và các công cụ quản lý dự án phổ biến.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zoom/Google Meet để tải ghi âm cuộc họp.
- Tài khoản Jira/ClickUp/Linear để tạo công việc.
- API keys cho các dịch vụ: OpenAI (Whisper), Anthropic (Claude), Slack (tùy chọn).
- Tài khoản Google Drive để lưu trữ bản tóm tắt (tùy chọn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/15114](https://n8n.io/workflows/15114).
2. Click vào nút "Download" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive Meeting Recording Webhook"**:
   - Đảm bảo cấu hình đúng path và HTTP method (POST).
   - Ví dụ: `http://your-n8n-instance.com/webhook/meeting-automator`.

2. **Node "Validate Config & Build Params"**:
   - Cập nhật danh sách thành viên trong công ty và ánh xạ tên thành viên với ID người dùng trong các công cụ quản lý dự án.

3. **Node "Download Zoom Recording"**:
   - Cấu hình credentials cho Zoom OAuth2 API.
   - Đảm bảo tài khoản Zoom có quyền truy cập vào ghi âm cuộc họp.

4. **Node "Download Google Meet Recording"**:
   - Cấu hình credentials cho Google OAuth2 API.
   - Đảm bảo tài khoản Google có quyền truy cập vào ghi âm cuộc họp.

5. **Node "Transcribe Audio with Whisper"**:
   - Cấu hình credentials cho OpenAI API.
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng dịch vụ Whisper.

6. **Node "Analyze Transcript with Claude AI"**:
   - Cấu hình credentials cho Anthropic API.
   - Đảm bảo tài khoản Anthropic có đủ credit để sử dụng mô hình Claude.

7. **Node "Create Jira Task"**:
   - Cấu hình credentials cho Jira Software Cloud API.
   - Đảm bảo tài khoản Jira có quyền tạo công việc mới.

8. **Node "Create ClickUp Task"**:
   - Cấu hình credentials cho ClickUp API.
   - Đảm bảo tài khoản ClickUp có quyền tạo công việc mới.

9. **Node "Send Slack Notification"**:
   - Cấu hình credentials cho Slack API (tùy chọn).
   - Đảm bảo tài khoản Slack có quyền gửi thông báo.

10. **Node "Save Summary to Google Drive"**:
    - Cấu hình credentials cho Google Drive OAuth2 API (tùy chọn).
    - Đảm bảo tài khoản Google có quyền lưu trữ file.

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu.
2. Kiểm tra các node quan trọng để đảm bảo dữ liệu được xử lý đúng.
3. Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo khi có công việc mới được tạo.
- Lưu log hoạt động của workflow để theo dõi và kiểm tra.
- Tự động gửi báo cáo hàng tuần về các công việc đã được tạo từ ghi âm cuộc họp.
- Kết hợp với công cụ quản lý dự án khác như Notion hoặc Trello để lưu trữ bản tóm tắt cuộc họp.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình chuyển đổi ghi âm cuộc họp thành công việc trong các công cụ quản lý dự án. Với công nghệ AI tiên tiến và tích hợp đa nền tảng, workflow này sẽ giúp các sếp tiết kiệm thời gian, tăng độ chính xác và nâng cao năng suất làm việc. Hãy áp dụng ngay để trải nghiệm sự khác biệt!