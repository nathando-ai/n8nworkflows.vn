---
title: "🚀 Tự động hóa kiểm tra tuân thủ tài sản và điều phối hành động với OpenAI, Google Calendar, Gmail, Slack và Google Sheets"
description: "Hướng dẫn tự động hóa kiểm tra tuân thủ tài sản và điều phối hành động với OpenAI, Google Calendar, Gmail, Slack và Google Sheets. Tiết kiệm thời gian và đảm bảo tuân thủ quy định."
slug: "tu-dong-hoa-kiem-tra-tuan-thu-tai-san-va-dieu-phoi-hanh-dong"
tags: [n8n, automation, no-code, openai, google-calendar, gmail, slack, google-sheets]
keywords: [n8n workflow, tự động hóa, openai, google calendar, gmail, slack, google sheets]
---

# 🚀 Tự động hóa kiểm tra tuân thủ tài sản và điều phối hành động với OpenAI, Google Calendar, Gmail, Slack và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức cho các chuyên viên kiểm tra tài sản
- Đảm bảo tuân thủ quy định và quy trình kiểm tra
- Tự động hóa các hành động điều phối và thông báo
- Giảm thiểu lỗi và tăng độ chính xác trong quá trình kiểm tra
- Tích hợp các công cụ quản lý và thông báo hiện đại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API
- Tài khoản Google Calendar API
- Tài khoản Gmail API
- Tài khoản Slack API
- Tài khoản Google Sheets API
- Dữ liệu tài sản và cơ sở dữ liệu tuân thủ
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Schedule Property Monitoring**: Cấu hình lịch trình kiểm tra tài sản.
- **Workflow Configuration**: Cấu hình các tham số cơ bản cho workflow.
- **Fetch Property Sensor Data**: Cấu hình API để lấy dữ liệu từ cảm biến tài sản.
- **Fetch Compliance Database**: Cấu hình API để lấy dữ liệu từ cơ sở dữ liệu tuân thủ.
- **Combine Property Data**: Kết hợp dữ liệu từ các nguồn khác nhau.
- **Property Validation Agent**: Cấu hình mô hình OpenAI để kiểm tra tài sản.
- **OpenAI Model - Validation Agent**: Chọn mô hình OpenAI và cấu hình các tham số.
- **Validation Output Parser**: Cấu hình để phân tích đầu ra từ mô hình OpenAI.
- **Route by Validation Status**: Cấu hình để điều hướng dựa trên trạng thái kiểm tra.
- **Governance Orchestration Agent**: Cấu hình mô hình OpenAI để điều phối hành động.
- **OpenAI Model - Orchestration Agent**: Chọn mô hình OpenAI và cấu hình các tham số.
- **Orchestration Output Parser**: Cấu hình để phân tích đầu ra từ mô hình OpenAI.
- **Google Calendar Tool - Schedule Repairs**: Cấu hình để lên lịch sửa chữa.
- **Gmail Tool - Send Notifications**: Cấu hình để gửi thông báo qua email.
- **Slack Tool - Alert Teams**: Cấu hình để gửi thông báo qua Slack.
- **Google Sheets Tool - Log Actions**: Cấu hình để ghi log các hành động vào Google Sheets.
- **Repair Scheduling Agent Tool**: Cấu hình để lên lịch sửa chữa.
- **OpenAI Model - Repair Agent**: Chọn mô hình OpenAI và cấu hình các tham số.
- **Repair Agent Output Parser**: Cấu hình để phân tích đầu ra từ mô hình OpenAI.
- **Compliance Inspection Agent Tool**: Cấu hình để kiểm tra tuân thủ.
- **OpenAI Model - Compliance Agent**: Chọn mô hình OpenAI và cấu hình các tham số.
- **Compliance Agent Output Parser**: Cấu hình để phân tích đầu ra từ mô hình OpenAI.
- **Lease Management Agent Tool**: Cấu hình để quản lý hợp đồng thuê.
- **OpenAI Model - Lease Agent**: Chọn mô hình OpenAI và cấu hình các tham số.
- **Lease Agent Output Parser**: Cấu hình để phân tích đầu ra từ mô hình OpenAI.
- **Store Validation Results**: Lưu kết quả kiểm tra.
- **Store Orchestration Decisions**: Lưu quyết định điều phối.
- **Calculate Risk Scores**: Tính toán điểm số rủi ro.
- **Check Critical Threshold**: Kiểm tra ngưỡng rủi ro.
- **Consolidate All Actions**: Kết hợp tất cả các hành động.
- **Format Audit Report**: Định dạng báo cáo kiểm tra.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo thời gian thực.
- Lưu log các hành động vào Google Sheets để theo dõi.
- Gửi báo cáo định kỳ qua email.
- Tích hợp với các hệ thống quản lý tài sản khác.

### 📌 Kết luận
Workflow này giúp tự động hóa kiểm tra tuân thủ tài sản và điều phối hành động một cách hiệu quả. Các sếp có thể tiết kiệm thời gian và đảm bảo tuân thủ quy định một cách dễ dàng.