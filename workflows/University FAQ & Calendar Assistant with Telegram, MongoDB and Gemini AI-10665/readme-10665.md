---
title: "🚀 Tự động hóa FAQ & Lịch học đại học với Telegram, MongoDB và Gemini AI"
description: "Giải pháp hoàn toàn tự động hóa giúp sinh viên và nhân viên đại học quản lý thông tin FAQ và lịch học thông qua Telegram, kết hợp trí tuệ nhân tạo Gemini AI và cơ sở dữ liệu MongoDB."
slug: "tu-dong-hoa-faq-lich-hoc-dai-hoc-voi-telegram-mongodb-gemini-ai"
tags: [n8n, automation, no-code, telegram, ai, mongodb, google-sheets]
keywords: [n8n workflow, tự động hóa, chatbot, telegram, ai, mongodb, google sheets]
---

# 🚀 Tự động hóa FAQ & Lịch học đại học với Telegram, MongoDB và Gemini AI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của sinh viên và nhân viên đại học khi phải trả lời hàng nghìn câu hỏi FAQ và quản lý lịch học thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động trả lời hàng nghìn câu hỏi FAQ hàng ngày
- Chính xác: Thông tin được cập nhật liên tục từ cơ sở dữ liệu chính xác
- Cá nhân hóa: Tạo ra các thông báo lịch học và thông tin cá nhân hóa cho từng sinh viên
- Hoạt động liên tục: Hệ thống hoạt động 24/7 mà không cần can thiệp thủ công
- Tích hợp đa nền tảng: Kết nối dễ dàng với Telegram, Google Sheets và MongoDB
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram API
- Tài khoản Google Sheets API
- Tài khoản MongoDB
- Tài khoản Google Gemini API
- Dữ liệu FAQ và lịch học đã được chuẩn bị trong Google Sheets
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang workflow gốc: [University FAQ & Calendar Assistant with Telegram, MongoDB and Gemini AI](https://n8n.io/workflows/10665)
2. Click vào nút "Download" để tải file JSON của workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về
4. Hoặc copy toàn bộ JSON từ trang web và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger - Inicio**:
   - Cấu hình credentials cho Telegram API
   - Đảm bảo bot Telegram đã được tạo và thêm vào nhóm/channel cần quản lý

2. **Google Sheets nodes**:
   - Cấu hình credentials cho Google Sheets API
   - Kiểm tra ID của Google Sheet chứa dữ liệu FAQ và lịch học
   - Đảm bảo các cột dữ liệu trong Google Sheet phù hợp với cấu trúc dữ liệu trong workflow

3. **MongoDB nodes**:
   - Cấu hình credentials cho MongoDB
   - Kiểm tra tên collection chứa dữ liệu FAQ
   - Đảm bảo cấu trúc dữ liệu trong MongoDB phù hợp với cấu trúc dữ liệu trong workflow

4. **Google Gemini nodes**:
   - Cấu hình credentials cho Google Gemini API
   - Kiểm tra các tham số như model, temperature, max tokens...

5. **Nodes xử lý dữ liệu**:
   - **Construir_Prompt_Gemini1**: Chỉnh sửa prompt template nếu cần
   - **Buscar_FAQs_Relevantes**: Cấu hình logic tìm kiếm FAQ phù hợp
   - **Detector_Calendario_Pre**: Cấu hình logic phát hiện yêu cầu lịch học
   - **Buscar_Eventos_Calendario1**: Cấu hình logic tìm kiếm sự kiện lịch học

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Thử gửi các câu hỏi mẫu qua Telegram bot
   - Kiểm tra kết quả trả về từ các node xử lý
2. Bật Active workflow:
   - Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, bật chế độ Active

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm các node để gửi thông báo lịch học và FAQ đến các nền tảng khác
2. **Lưu log hoạt động**: Thêm node để lưu log các tương tác giữa người dùng và bot
3. **Gửi báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo hàng tuần về số lượng câu hỏi được trả lời, số lượng người dùng mới...
4. **Tích hợp với hệ thống đăng ký học**: Kết nối với hệ thống quản lý sinh viên để cung cấp thông tin đăng ký học cá nhân hóa

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quản lý thông tin FAQ và lịch học đại học. Với sự kết hợp của trí tuệ nhân tạo Gemini AI và các công cụ lưu trữ dữ liệu như MongoDB và Google Sheets, hệ thống có thể cung cấp thông tin chính xác và cá nhân hóa cho từng sinh viên. Các sếp có thể tùy chỉnh và mở rộng workflow này để phù hợp với nhu cầu cụ thể của trường đại học, tạo ra trải nghiệm học tập tốt hơn cho sinh viên.