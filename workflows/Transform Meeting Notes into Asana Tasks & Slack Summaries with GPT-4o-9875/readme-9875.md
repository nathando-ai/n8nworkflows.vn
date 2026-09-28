---
title: "🚀 Tự động hóa ghi chú cuộc họp thành công việc Asana và báo cáo Slack với GPT-4o"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi ghi chú cuộc họp thành công việc Asana và báo cáo Slack bằng n8n, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-ghi-chu-cuoc-hop-voi-gpt-4o"
tags: [n8n, automation, no-code, asana, slack]
keywords: [n8n workflow, tự động hóa, ghi chú cuộc họp, asana, slack]
---

# 🚀 Tự động hóa ghi chú cuộc họp thành công việc Asana và báo cáo Slack với GPT-4o

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình chuyển đổi ghi chú cuộc họp thành công việc Asana và báo cáo Slack.
- Nâng cao hiệu suất: Các công việc và quyết định từ cuộc họp được xử lý nhanh chóng và chính xác.
- Tăng cường sự liên kết: Tất cả thành viên trong nhóm đều được cập nhật về các quyết định quan trọng và công việc cần làm.
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công, giảm thiểu lỗi và tăng tính nhất quán.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Asana và API key để tạo công việc.
- Tài khoản Slack và thông tin kênh để gửi báo cáo.
- Tài khoản OpenAI và API key để sử dụng GPT-4o.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/9875).
2. Nhấn nút "Download" để tải file JSON.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Meeting Notes Form**: Cấu hình form để thu thập thông tin từ người dùng. Các trường cần điền bao gồm:
  - Company/Project name
  - Meeting notes
  - Asana project
  - Slack channel

- **AI Extract Data**: Cấu hình node OpenAI để sử dụng GPT-4o. Các tham số cần điền bao gồm:
  - API key của OpenAI
  - Prompt để trích xuất thông tin từ ghi chú cuộc họp

- **Structure Data**: Cấu hình node Code để định dạng dữ liệu trích xuất từ OpenAI. Các tham số cần điền bao gồm:
  - Mã JavaScript để định dạng dữ liệu

- **Create Asana Task**: Cấu hình node Asana để tạo công việc. Các tham số cần điền bao gồm:
  - API key của Asana
  - ID của dự án Asana
  - Thông tin công việc cần tạo

- **Combine Tasks**: Cấu hình node Aggregate để kết hợp các công việc đã tạo. Các tham số cần điền bao gồm:
  - Thông tin công việc cần kết hợp

- **Format Slack Message**: Cấu hình node Code để định dạng tin nhắn Slack. Các tham số cần điền bao gồm:
  - Mã JavaScript để định dạng tin nhắn

- **Send to Slack**: Cấu hình node Slack để gửi tin nhắn. Các tham số cần điền bao gồm:
  - API key của Slack
  - ID của kênh Slack

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Google Calendar để tự động hóa việc tạo lịch hẹn sau cuộc họp.
- Sử dụng node Email để gửi báo cáo qua email cho các thành viên không có quyền truy cập vào Slack.
- Tích hợp với các công cụ quản lý dự án khác như Trello hoặc Jira để tăng tính linh hoạt.

### 📌 Kết luận
Workflow này giúp tự động hóa quy trình chuyển đổi ghi chú cuộc họp thành công việc Asana và báo cáo Slack, tiết kiệm thời gian và nâng cao hiệu suất làm việc. Các sếp có thể áp dụng ngay để tối ưu hóa quy trình làm việc của mình.