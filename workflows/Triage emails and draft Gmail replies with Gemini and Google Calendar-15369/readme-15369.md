---
title: "🚀 Tự động phân loại email và soạn nháp trả lời bằng Gemini và Google Calendar"
description: "Giải pháp tự động hóa 100% không cần code giúp các sếp tiết kiệm thời gian xử lý email hàng ngày bằng cách phân loại tự động và soạn nháp trả lời thông minh bằng AI Gemini."
slug: "tu-dong-phan-loai-email-soan-nhap-gmail-gemini-google-calendar"
tags: [n8n, automation, no-code, email, ai, gmail, google-calendar, gemini]
keywords: [n8n workflow, tự động hóa email, phân loại email, soạn nháp email, ai email, gemini email]
---

# 🚀 Tự động phân loại email và soạn nháp trả lời bằng Gemini và Google Calendar

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải xử lý hàng trăm email hàng ngày không? Với workflow này, các sếp có thể tự động phân loại email đến và soạn nháp trả lời thông minh bằng AI Gemini, đồng thời kiểm tra lịch Google Calendar để đưa ra phản hồi phù hợp nhất.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý email hàng ngày lên tới 80%
- Phản hồi email nhanh chóng và chuyên nghiệp với nội dung được soạn sẵn bởi AI
- Tự động phân loại email theo nhãn phù hợp
- Kết hợp thông tin từ Google Calendar để đưa ra phản hồi chính xác hơn
- Tăng năng suất làm việc với hệ thống tự động hóa hoàn toàn không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ
- API Key cho Google Gemini (PaLM)
- Quyền truy cập Google Calendar
- Các nhãn email đã được thiết lập trong Gmail
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/15369](https://n8n.io/workflows/15369)
2. Nhấn nút "Import" để tải xuống file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Gmail OAuth2 Credential**: Cần thiết lập credential cho tất cả các node Gmail (Gmail - Nouveaux emails, Get a message, Remove label from thread, Draft into label, Get label for response, Labelliser, Mark a message as unread)
- **Google Gemini (PaLM) API Credential**: Cần thiết lập credential cho node GEMINI bên trong AI Agent
- **Google Calendar OAuth2 Credential**: Cần thiết lập credential cho node AGENDA bên trong AI Agent
- **Cấu hình Gmail Trigger**: Cần cấu hình node Gmail Trigger với nhãn/filter phù hợp để theo dõi email mới cần xử lý
- **Nhãn email**: Cần kiểm tra và cập nhật tên nhãn trong các node 'Remove label from thread', 'Get label for response', và 'Labelliser' để phù hợp với thiết lập nhãn email của các sếp
- **Chữ ký email**: Cần tùy chỉnh HTML signature trong node 'Code in JavaScript' để phù hợp với chữ ký email cá nhân hoặc công ty
- **Điều kiện routing**: Cần xem lại các điều kiện trong node Switch1 để đảm bảo phù hợp với cấu trúc đầu ra từ AI Agent

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, các sếp nên test workflow với một email mẫu để đảm bảo hoạt động đúng như mong đợi
2. Khi đã kiểm tra và xác nhận hoạt động ổn định, các sếp có thể kích hoạt workflow bằng cách nhấn nút "Active" trên giao diện n8n Editor

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể tùy chỉnh prompt của AI Agent để thay đổi phong cách hoặc cấu trúc của các email trả lời
- Có thể thêm các nhánh routing mới trong node Switch1 để xử lý các trường hợp đặc biệt (ví dụ: chuyển tiếp, lưu trữ, chuyển tiếp lên cấp trên)
- Có thể kết hợp với các dịch vụ khác như Slack để thông báo khi có email mới cần xử lý
- Các sếp có thể thiết lập lịch gửi email tự động cho các nháp đã được soạn sẵn
- Có thể thêm chức năng lưu log các email đã xử lý để theo dõi và phân tích sau này

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa xử lý email hàng ngày, giúp các sếp tiết kiệm thời gian và tăng năng suất làm việc. Với sự kết hợp của AI Gemini và Google Calendar, các sếp có thể đưa ra phản hồi nhanh chóng và chính xác hơn. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình làm việc của các sếp!