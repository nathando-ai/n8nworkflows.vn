---
title: "🚀 Tự động phân loại ticket hỗ trợ bằng AI Gemini và kiểm tra schema"
description: "Hướng dẫn tự động hóa phân loại ticket hỗ trợ bằng AI Gemini của Google và kiểm tra tính hợp lệ của dữ liệu đầu ra trong n8n"
slug: "tu-dong-phan-loai-ticket-ho-tro-bang-ai-gemini-va-kiem-tra-schema"
tags: [n8n, automation, no-code, ticket-management, ai]
keywords: [n8n workflow, tự động hóa, phân loại ticket, AI Gemini, kiểm tra schema]
---

# 🚀 Tự động phân loại ticket hỗ trợ bằng AI Gemini và kiểm tra schema

[Các sếp đang gặp khó khăn khi phải phân loại hàng nghìn ticket hỗ trợ hàng ngày một cách thủ công. Workflow này giúp tự động hóa quy trình này bằng cách sử dụng AI Gemini của Google để phân loại ticket và kiểm tra tính hợp lệ của dữ liệu đầu ra.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý ticket: Tự động phân loại ticket theo danh mục, mức độ ưu tiên và độ tin cậy.
- Tăng độ chính xác: Kiểm tra tính hợp lệ của dữ liệu đầu ra từ AI để đảm bảo chất lượng.
- Tự động hóa quy trình: Giảm thiểu lỗi con người và tăng hiệu suất xử lý ticket.
- Tích hợp dễ dàng: Kết nối với các hệ thống khác như Jira, Slack để thực hiện các hành động tiếp theo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenRouter để sử dụng AI Gemini của Google.
- Dữ liệu ticket hỗ trợ cần phân loại (chủ đề, nội dung, email khách hàng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link workflow: [https://n8n.io/workflows/13851](https://n8n.io/workflows/13851).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Webhook - Receive Support Ticket**: Cấu hình đường dẫn và phương thức HTTP (POST) để nhận ticket.
- **Clean Ticket Data**: Chỉnh sửa mã JavaScript để xử lý dữ liệu ticket trước khi phân loại.
- **AI - Classify Ticket**: Cấu hình node Agent và node OpenRouter Chat Model để sử dụng AI Gemini của Google.
- **Validate AI Output**: Chỉnh sửa mã JavaScript để kiểm tra tính hợp lệ của dữ liệu đầu ra từ AI.
- **Is Output Valid?**: Cấu hình điều kiện để kiểm tra dữ liệu đầu ra từ AI.
- **Respond - Classification Result**: Cấu hình phản hồi khi dữ liệu đầu ra hợp lệ.
- **Respond - Needs Review**: Cấu hình phản hồi khi dữ liệu đầu ra không hợp lệ.

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với OpenRouter và cấu hình API key.
2. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
3. Bật Active workflow để bắt đầu tự động phân loại ticket.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm logic retry để gửi lại ticket không hợp lệ cho AI với thông báo lỗi.
- Thay đổi node Respond để thực hiện các hành động tiếp theo như tạo ticket trong Jira hoặc gửi thông báo trên Slack.
- Tích hợp với các hệ thống khác như Google Sheets để lưu trữ dữ liệu phân loại.

### 📌 Kết luận
Workflow này giúp các sếp tự động phân loại ticket hỗ trợ bằng AI Gemini của Google và kiểm tra tính hợp lệ của dữ liệu đầu ra. Với việc tự động hóa quy trình này, các sếp có thể tiết kiệm thời gian và tăng độ chính xác trong việc xử lý ticket. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ hỗ trợ!