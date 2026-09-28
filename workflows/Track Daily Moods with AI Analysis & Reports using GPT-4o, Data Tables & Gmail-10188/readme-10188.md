---
title: "🚀 Theo dõi tâm trạng hàng ngày với AI phân tích & báo cáo tự động bằng GPT-4o, Bảng dữ liệu & Gmail"
description: "Workflow n8n giúp bạn ghi lại tâm trạng hàng ngày, tự động phân tích tuần/tháng bằng AI và gửi báo cáo qua email - giải pháp hoàn hảo cho việc theo dõi sức khỏe tinh thần và cải thiện hiệu suất làm việc."
slug: "theo-doi-tam-trang-hang-ngay-voi-ai-phan-tich-bao-cao-tu-dong"
tags: [n8n, automation, no-code, ai, personal-productivity]
keywords: [n8n workflow, tự động hóa, theo dõi tâm trạng, AI phân tích, báo cáo tự động]
---

# 🚀 Theo dõi tâm trạng hàng ngày với AI phân tích & báo cáo tự động bằng GPT-4o, Bảng dữ liệu & Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian ghi chép và phân tích tâm trạng hàng ngày
- Nhận báo cáo tuần/tháng chi tiết về tâm trạng và xu hướng
- Cải thiện sức khỏe tinh thần và hiệu suất làm việc thông qua dữ liệu khách quan
- Tự động hóa hoàn toàn quá trình theo dõi và báo cáo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key để sử dụng GPT-4o
- Tài khoản Gmail với quyền truy cập OAuth2
- Bảng dữ liệu (Data Table) để lưu trữ thông tin tâm trạng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Webhook - Mood**: Cấu hình endpoint `/mood` với phương thức POST để nhận dữ liệu tâm trạng
- **Insert Mood Row**: Cấu hình ID của bảng dữ liệu (Data Table) để lưu trữ thông tin tâm trạng
- **ChatGPT Weekly Analysis & Monthly Analysis**: Cấu hình credentials OpenAI API và prompt cho phân tích
- **Gmail (Weekly) & Gmail (Monthly)**: Cấu hình credentials Gmail OAuth2 và địa chỉ email nhận báo cáo

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với ứng dụng theo dõi sức khỏe để tự động ghi nhận tâm trạng
- Thêm báo cáo định kỳ qua Slack hoặc Telegram
- Tích hợp với hệ thống quản lý công việc để liên kết tâm trạng với hiệu suất làm việc

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi tâm trạng hàng ngày, tự động phân tích và báo cáo - giúp các sếp có cái nhìn rõ ràng về sức khỏe tinh thần và cải thiện hiệu suất làm việc. Hãy thử ngay và trải nghiệm sự khác biệt của tự động hóa!