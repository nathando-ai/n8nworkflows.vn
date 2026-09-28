---
title: "🌙 Tự động hóa chu kỳ kinh nguyệt với Gmail và GPT-4o - Workflow n8n hoàn hảo"
description: "Hướng dẫn chi tiết cách tự động theo dõi chu kỳ kinh nguyệt, gửi email nhắc nhở thông minh và tạo nội dung sức khỏe cá nhân hóa với GPT-4o và Google Sheets"
slug: "tu-dong-hoa-chu-ky-kinh-nguyet-voi-gmail-gpt4o"
tags: [n8n, automation, no-code, google-sheets, openai, personal-productivity]
keywords: [n8n workflow, tự động hóa chu kỳ kinh nguyệt, gmail automation, gpt-4o sức khỏe, workflow cá nhân hóa]
---

# 🌙 Tự động hóa chu kỳ kinh nguyệt với Gmail và GPT-4o - Workflow n8n hoàn hảo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần với tự động hóa hoàn toàn
- Nhận nhắc nhở chu kỳ kinh nguyệt chính xác đến từng ngày
- Nội dung sức khỏe cá nhân hóa với GPT-4o
- Theo dõi dữ liệu chu kỳ kinh nguyệt trên Google Sheets
- Hệ thống hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail)
- Tài khoản OpenAI (cho GPT-4o)
- Google Sheets với 2 bảng: "Subscribers" và "Send Log"
- Tài khoản n8n đã cài đặt các credentials: gmailOAuth2, googleSheetsOAuth2Api, openAiApi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [Workflow gốc trên n8n.io](https://n8n.io/workflows/14019)
2. Click "Download" để tải file JSON
3. Trong n8n Editor, chọn "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Cycle Wellness Form"**:
   - Cấu hình form với các trường: Name, Email, Last Period Date, Cycle Length
   - Thiết lập URL endpoint cho form (ví dụ: /cycle-form)

2. **Node "Save to Subscribers"**:
   - Chỉnh sheet ID và tên bảng "Subscribers"
   - Đảm bảo các cột: Name, Email, Last Period Date, Cycle Length, Next Period, Ovulation Day, Fertile Window, PMS Start

3. **Node "Log to Send Log" và "Log to Send Log1"**:
   - Cập nhật sheet ID và tên bảng "Send Log"
   - Thiết lập các cột: Email, Phase, Date Sent

4. **Node "Send Welcome Email", "Send Reminder Email" và "Send Wellness Digest"**:
   - Cấu hình credentials Gmail OAuth2
   - Thiết lập email người gửi và chủ đề email

5. **Node "Wellness Coach"**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo model được chọn là GPT-4o
   - Thiết lập prompt template phù hợp

6. **Node "Calculate Cycle Dates", "Build Welcome Email", "Build Reminder Email", "Calculate Today's Phase" và "Parse & Build Wellness Email"**:
   - Kiểm tra logic JavaScript trong các node code
   - Điều chỉnh các ngày nhắc nhở nếu cần

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Submit form với email của bạn
   - Kiểm tra email chào mừng và nhắc nhở
   - Xác nhận dữ liệu được lưu trong Google Sheets

2. Bật Active workflow:
   - Kích hoạt các schedule triggers: "Daily 8AM Trigger" và "Weekly Sunday 9AM Trigger"

### ✍️ Mẹo & gợi ý nâng cao
1. Kết nối với Slack/Telegram để nhận thông báo chu kỳ kinh nguyệt
2. Thêm node lưu log chi tiết vào Google Sheets cho từng email gửi đi
3. Tạo báo cáo tuần hàng tuần về tiến trình chu kỳ kinh nguyệt
4. Thêm tính năng gửi email nhắc nhở cho các ngày quan trọng khác (như ngày sinh sản)

### 📌 Kết luận
Workflow này biến việc theo dõi chu kỳ kinh nguyệt từ công việc thủ công thành tự động hoàn toàn, mang lại hiệu quả cao với chi phí thấp. Bằng cách tích hợp GPT-4o, bạn có thể cung cấp nội dung sức khỏe cá nhân hóa chất lượng cao mà không cần can thiệp thủ công. Hãy áp dụng ngay để tối ưu hóa sức khỏe và năng suất cá nhân!