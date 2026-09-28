---
title: "🚀 Tự động gửi email tuyển dụng kỹ sư dữ liệu cá nhân hóa với PredictLeads, OpenAI và Gmail"
description: "Hướng dẫn tự động hóa quy trình tìm kiếm và gửi email tuyển dụng cá nhân hóa cho các công ty đang tuyển dụng kỹ sư dữ liệu bằng n8n, PredictLeads và OpenAI"
slug: "tu-dong-gui-email-tuyen-dung-ky-su-du-lieu-ca-nhan-hoa"
tags: [n8n, automation, no-code, lead-generation, ai]
keywords: [n8n workflow, tự động hóa, lead generation, email cá nhân hóa, tuyển dụng kỹ sư dữ liệu]
---

# 🚀 Tự động gửi email tuyển dụng kỹ sư dữ liệu cá nhân hóa với PredictLeads, OpenAI và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các công ty tuyển dụng khi phải gửi hàng trăm email tuyển dụng thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình tìm kiếm và gửi email tuyển dụng
- Tăng độ chính xác: Cá nhân hóa nội dung email dựa trên công nghệ đang sử dụng của công ty
- Tăng tỷ lệ phản hồi: Email được cá nhân hóa sẽ có độ tin cậy cao hơn
- Hoạt động liên tục: Gửi email hàng ngày mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản PredictLeads API
- Tài khoản OpenAI API
- Tài khoản Gmail với OAuth2 đã được cấu hình
- Domain của công ty để tìm kiếm công việc tuyển dụng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **⏰ Daily Schedule**: Cấu hình thời gian chạy workflow hàng ngày
- **🔍 Fetch Data Engineer Job Openings**: Cấu hình PredictLeads API và domain của công ty
- **🔀 Split by Company**: Cấu hình số lượng công ty xử lý trong mỗi batch
- **🏢 Get Company Info**: Cấu hình PredictLeads API để lấy thông tin công ty
- **💻 Get Technology Stack**: Cấu hình PredictLeads API để lấy thông tin công nghệ đang sử dụng
- **⚙️ Build Personalized Prompt**: Cấu hình prompt cho OpenAI để tạo nội dung email cá nhân hóa
- **🤖 Generate Personalized Email**: Cấu hình OpenAI API để tạo email cá nhân hóa
- **📧 Send Personalized Email**: Cấu hình Gmail OAuth2 để gửi email

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy thành công
- Lưu log các email đã gửi để theo dõi hiệu quả
- Gửi báo cáo định kỳ về hiệu quả của chiến dịch tuyển dụng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình tìm kiếm và gửi email tuyển dụng cá nhân hóa cho các công ty đang tuyển dụng kỹ sư dữ liệu. Với việc kết hợp PredictLeads, OpenAI và Gmail, workflow này mang lại hiệu quả cao trong việc tăng tỷ lệ phản hồi và tiết kiệm thời gian cho các sếp.