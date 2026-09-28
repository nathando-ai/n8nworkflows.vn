---
title: "🚀 Tự động hóa Thiết kế Nội thất với Telegram và AI Gemini - Workflow n8n"
description: "Hướng dẫn tự động hóa thiết kế nội thất qua Telegram với AI Gemini, quản lý danh mục đồ nội thất và tạo hình ảnh thiết kế bằng n8n"
slug: "tu-dong-hoa-thiet-ke-noi-that-voi-telegram-va-ai-gemini"
tags: [n8n, automation, no-code, telegram, ai, gemini, supabase]
keywords: [n8n workflow, tự động hóa nội thất, AI thiết kế, telegram bot, gemini ai]
---

# 🚀 Tự động hóa Thiết kế Nội thất với Telegram và AI Gemini - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp trong ngành thiết kế nội thất khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình thiết kế nội thất qua Telegram
- Quản lý danh mục đồ nội thất trong cơ sở dữ liệu Supabase
- Tạo hình ảnh thiết kế nội thất bằng AI Gemini
- Tiết kiệm thời gian và công sức cho các chuyên viên thiết kế
- Tăng hiệu quả làm việc với hệ thống tự động hóa hoàn chỉnh
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram
- API key từ OpenAI (để sử dụng AI Gemini)
- Cơ sở dữ liệu Supabase để lưu trữ thông tin
- Tài khoản Google Palm (cho các tính năng AI nâng cao)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/8772](https://n8n.io/workflows/8772)
2. Nhấn nút "Download" để tải file JSON của workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

**CATALOGUE ORGANISER TOOLS**
- **Telegram Trigger**: Cấu hình credentials cho tài khoản Telegram của bạn
- **Send a text message in Telegram**: Điền thông tin chat ID và nội dung tin nhắn
- **Send a photo message in Telegram**: Cấu hình để gửi hình ảnh qua Telegram
- **Create Catalogue Row**: Thiết lập kết nối với cơ sở dữ liệu Supabase
- **Get Many Catalogue Rows**: Cấu hình truy vấn để lấy danh mục đồ nội thất

**ROOM ORGANISER TOOLS**
- **AI Agent**: Cấu hình agent AI để xử lý yêu cầu thiết kế
- **OpenAI Chat Model**: Thiết lập kết nối với API OpenAI
- **Create Room Row**: Cấu hình để lưu thông tin phòng thiết kế vào Supabase
- **Get Many Room Rows**: Cấu hình truy vấn để lấy danh sách phòng thiết kế

**AI GEN IMAGE TOOL**
- **Nanobanana Caller**: Cấu hình kết nối với Google Palm API
- **Gen AI Image**: Thiết lập các tham số cho việc tạo hình ảnh AI
- **Gen Image Save**: Cấu hình để lưu hình ảnh tạo được vào Supabase
- **Get AI Generated Images**: Cấu hình truy vấn để lấy hình ảnh tạo bởi AI

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn nút "Activate" để kích hoạt workflow
2. Test workflow bằng cách gửi tin nhắn qua Telegram bot
3. Kiểm tra kết quả trong cơ sở dữ liệu Supabase

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo khi có yêu cầu thiết kế mới
- Thiết lập báo cáo hàng ngày về các yêu cầu thiết kế đã xử lý
- Tích hợp với các công cụ quản lý dự án để theo dõi tiến độ thiết kế
- Sử dụng các tính năng AI nâng cao để tạo ra nhiều phiên bản thiết kế khác nhau

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa thiết kế nội thất qua Telegram với AI Gemini. Với hệ thống quản lý danh mục đồ nội thất và tạo hình ảnh thiết kế bằng AI, các sếp có thể tối ưu hóa quy trình làm việc và nâng cao hiệu quả thiết kế nội thất.