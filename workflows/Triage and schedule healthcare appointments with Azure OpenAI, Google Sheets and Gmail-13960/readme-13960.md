---
title: "🚀 Tự động hóa lịch hẹn khám bệnh với Azure OpenAI, Google Sheets và Gmail"
description: "Hướng dẫn tự động hóa toàn bộ quy trình đặt lịch khám bệnh từ tiếp nhận bệnh nhân đến gửi email nhắc nhở, giúp tiết kiệm thời gian và tối ưu hóa quy trình chăm sóc sức khỏe."
slug: "tu-dong-hoa-lich-hen-kham-benh-azure-openai-google-sheets-gmail"
tags: [n8n, automation, no-code, healthcare, ai-automation]
keywords: [n8n workflow, tự động hóa y tế, AI đặt lịch khám bệnh, Google Sheets automation, Gmail automation]
---

# 🚀 Tự động hóa lịch hẹn khám bệnh với Azure OpenAI, Google Sheets và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các cơ sở y tế khi xử lý thủ công các quy trình đặt lịch khám bệnh. Giới thiệu workflow như giải pháp tự động hóa toàn bộ quy trình từ tiếp nhận bệnh nhân đến gửi email nhắc nhở.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý thủ công lên tới 80% cho nhân viên y tế
- Tự động phân loại mức độ ưu tiên khám bệnh dựa trên triệu chứng
- Tối ưu hóa phân công bác sĩ dựa trên chuyên môn và lịch làm việc
- Tự động gửi email nhắc nhở cho bệnh nhân sau khi khám
- Giảm thiểu sai sót trong quá trình đặt lịch và quản lý bệnh nhân
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Azure OpenAI với API key và endpoint
- Tài khoản Google Workspace với quyền truy cập Google Sheets và Gmail
- Biểu mẫu tiếp nhận bệnh nhân có thể cấu hình để gửi dữ liệu đến webhook
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13960](https://n8n.io/workflows/13960)
2. Nhấn nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Node (🔔 Patient Lead Webhook)**:
   - Kích hoạt workflow bằng cách nhấn nút "Activate" trong node này
   - Lưu ý URL webhook được tạo ra (vd: `https://your-n8n-instance.com/webhook/patient-lead`)
   - Cấu hình biểu mẫu tiếp nhận bệnh nhân để gửi dữ liệu POST đến URL này

2. **Azure OpenAI Nodes (🧠 Azure OpenAI – Triage Model và 🧠 Azure OpenAI – Assignment Model)**:
   - Thêm credentials Azure OpenAI với các thông tin:
     - API Key
     - Endpoint URL
     - Deployment Name (sử dụng `gpt-4o-mini` cho cả hai node)
   - Đảm bảo tài khoản Azure OpenAI có đủ credit để xử lý các yêu cầu

3. **Google Sheets Nodes**:
   - Thêm credentials Google Sheets OAuth2 cho tất cả các node liên quan
   - Tạo một Google Sheet với ba tab:
     - `Patient forms` (dành cho dữ liệu triage)
     - `Doctor details` (danh sách bác sĩ và chuyên môn)
     - `Scheduled appointments` (lịch hẹn đã được phân công)
   - Đảm bảo các cột trong sheet khớp chính xác với dữ liệu được xử lý trong workflow

4. **Gmail Node (📧 Send Schedule Email to Doctor)**:
   - Thêm credentials Gmail OAuth2
   - Cập nhật địa chỉ email của bác sĩ trong node (hoặc sử dụng biến động từ dữ liệu sheet)

5. **Schedule Trigger Node (⏰ Hourly Feedback Schedule Trigger)**:
   - Điều chỉnh khoảng thời gian gửi email nhắc nhở theo nhu cầu của cơ sở y tế

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Kích hoạt workflow bằng cách nhấn nút "Activate" trong node Webhook
3. Kiểm tra email và Google Sheets để xác nhận dữ liệu được xử lý đúng

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để thông báo khi có lịch hẹn mới được tạo
- Tích hợp với hệ thống quản lý bệnh nhân (PMS) để cập nhật trạng thái khám
- Thêm bước xác nhận lịch hẹn qua SMS trước khi gửi email nhắc nhở
- Tạo báo cáo hàng ngày về số lượng bệnh nhân và lịch hẹn đã xử lý
- Thêm tính năng đánh giá sau khám để cải thiện chất lượng dịch vụ

### 📌 Kết luận
Workflow này tự động hóa hoàn toàn quy trình đặt lịch khám bệnh từ tiếp nhận bệnh nhân đến gửi email nhắc nhở, giúp các cơ sở y tế tiết kiệm thời gian và giảm thiểu sai sót. Bằng cách tích hợp Azure OpenAI, Google Sheets và Gmail, workflow này mang lại giải pháp toàn diện cho việc quản lý lịch hẹn và chăm sóc sức khỏe. Hãy áp dụng ngay để tối ưu hóa quy trình của bạn!