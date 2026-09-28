---
title: "🚀 Tự động hóa WhatsApp với Gemini AI và Google Calendar qua Evolution API"
description: "Hướng dẫn tự động hóa quản lý lịch Google Calendar thông qua WhatsApp với công nghệ AI Gemini và Evolution API - giải pháp hoàn toàn không cần code cho doanh nghiệp"
slug: "tu-dong-hoa-whatsapp-gemini-google-calendar"
tags: [n8n, automation, no-code, whatsapp, google-calendar, ai]
keywords: [n8n workflow, tự động hóa, whatsapp, google calendar, ai]
---

# 🚀 Tự động hóa WhatsApp với Gemini AI và Google Calendar qua Evolution API

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý lịch Google Calendar thủ công qua WhatsApp. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quản lý lịch Google Calendar qua WhatsApp
- Tiết kiệm thời gian xử lý yêu cầu lịch hẹn
- Hỗ trợ nhiều định dạng tin nhắn (text, hình ảnh, âm thanh, tài liệu)
- Tích hợp AI Gemini để hiểu và xử lý yêu cầu phức tạp
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Evolution API đã cấu hình sẵn instance
- API key của Google Gemini
- Quyền truy cập Google Calendar API
- MCP Server (nội bộ hoặc bên ngoài) đã cấu hình với URL kết nối
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/10944)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, chọn "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Webhook Node**:
   - Đảm bảo đường dẫn là "/Calendar" và phương thức là POST
   - Sau khi import, copy URL webhook được tạo ra

2. **Evolution API Nodes**:
   - Trong tất cả các node Evolution API, điền tên instance của bạn vào trường "instance"

3. **Google Calendar Credentials**:
   - Tạo mới credential Google Calendar OAuth2 trong n8n
   - Áp dụng credential này cho tất cả các node Google Calendar (Get, Create, Update, Delete)

4. **MCP Server Configuration**:
   - Copy URL của MCP Server và dán vào trường "Endpoint" của MCP Tool
   - Đảm bảo MCP Server đã được cấu hình với các công cụ cần thiết (Google Calendar)

5. **Evolution API Webhook Configuration**:
   - Trong panel Evolution API, truy cập vào instance > webhook
   - Dán URL webhook đã copy vào trường tương ứng

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để kiểm tra toàn bộ chuỗi xử lý
2. Kích hoạt workflow bằng cách bật nút Active
3. Kiểm tra lại các thông báo từ Evolution API để đảm bảo webhook đã được kích hoạt

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh MCP Tools**:
   - Thêm các công cụ MCP mới như Google Sheets, Notion, ClickUp
   - Chỉ cần cập nhật prompt của agent mà không cần thay đổi cấu trúc workflow

2. **Cải thiện bộ nhớ**:
   - Thay đổi loại bộ nhớ từ Simple Memory sang loại nhớ khác nếu muốn agent ghi nhớ toàn bộ cuộc trò chuyện

3. **Kết nối với các nền tảng khác**:
   - Nếu sử dụng Chatwoot hoặc TypeBot, chỉ cần thay đổi URL webhook và điều chỉnh các đối tượng mà node switch sử dụng

4. **Tích hợp Slack/Telegram**:
   - Thêm các node tương ứng để nhận tin nhắn từ các nền tảng này
   - Điều chỉnh node switch để xử lý các loại tin nhắn từ các nền tảng mới

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quản lý lịch Google Calendar thông qua WhatsApp với công nghệ AI Gemini. Với cấu hình đơn giản và khả năng mở rộng cao, các sếp có thể triển khai ngay để tiết kiệm thời gian và nâng cao hiệu quả quản lý lịch hẹn.