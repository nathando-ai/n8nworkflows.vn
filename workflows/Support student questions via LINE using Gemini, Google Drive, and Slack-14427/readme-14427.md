---
title: "🤖 Tự động trả lời câu hỏi học sinh qua LINE bằng Gemini và Google Drive"
description: "Hướng dẫn tự động hóa quy trình hỗ trợ học sinh bằng n8n, kết hợp LINE, Google Sheets, Google Drive và Slack để tạo chatbot AI thông minh"
slug: "tu-dong-ho-tro-hoc-sinh-qua-line-bang-gemini-google-drive"
tags: [n8n, automation, no-code, chatbot, ai]
keywords: [n8n workflow, tự động hóa, chatbot học sinh, ai giáo dục, google sheets]
---

# 🤖 Tự động trả lời câu hỏi học sinh qua LINE bằng Gemini và Google Drive

[Các sếp giáo viên] có bao giờ cảm thấy mệt mỏi khi phải trả lời hàng trăm câu hỏi học sinh mỗi ngày? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình hỗ trợ học sinh thông qua LINE, không cần phải can thiệp trực tiếp mỗi lần.

Workflow này sẽ tự động:
- Nhận câu hỏi từ học sinh qua LINE
- Tìm kiếm tài liệu giảng dạy trên Google Drive
- Trả lời bằng AI thông minh (Gemini)
- Ghi lại lịch sử trò chuyện trên Google Sheets
- Thông báo cho giáo viên qua Slack nếu không tìm thấy câu trả lời

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian trả lời hàng trăm câu hỏi mỗi ngày
- Tạo ra hệ thống hỗ trợ học sinh 24/7
- Lịch sử trò chuyện được lưu trữ tự động
- Tự động cảnh báo khi không tìm thấy câu trả lời
- Học sinh có thể học tập bất cứ lúc nào
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản LINE Messaging API
- Google Sheets để lưu lịch sử trò chuyện
- Google Drive chứa tài liệu giảng dạy
- Tài khoản Slack để nhận thông báo
- API Key của Google Gemini
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14427](https://n8n.io/workflows/14427)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên
4. Hoàn tất import và mở workflow trong Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node LINE Receiver:**
- Đảm bảo đã cấu hình LINE Messaging API credentials
- Path nên để mặc định là "line-study-bot"
- HTTP Method nên để POST

**Node Set Config:**
- Cập nhật Google Sheets ID (ID của file lưu lịch sử trò chuyện)
- Cập nhật Google Drive folder ID (ID của thư mục chứa tài liệu giảng dạy)
- Cập nhật Slack webhook URL (để nhận thông báo)
- Cập nhật LINE token (từ LINE Messaging API)

**Node Load Chat History:**
- Đảm bảo Google Sheets đã được chia sẻ với tài khoản n8n
- Kiểm tra lại tên sheet và phạm vi dữ liệu cần đọc

**Node Gemini Model:**
- Đảm bảo đã cấu hình Google Palm API credentials
- Kiểm tra lại model parameters nếu cần tùy chỉnh

#### 3. Kích hoạt ⚡️
1. Kiểm tra lại tất cả các node quan trọng đã được cấu hình đúng
2. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo khi có câu hỏi mới
- Thêm chức năng đánh giá câu trả lời từ học sinh
- Tích hợp với Google Calendar để đặt lịch học
- Tạo báo cáo hàng tuần về các câu hỏi thường gặp
- Kết hợp với Telegram để hỗ trợ đa nền tảng

### 📌 Kết luận
Workflow này giúp các sếp giáo viên tiết kiệm thời gian đáng kể trong việc hỗ trợ học sinh. Hệ thống tự động hóa này không chỉ giúp trả lời câu hỏi nhanh chóng mà còn cung cấp dữ liệu quan trọng để cải thiện chất lượng giảng dạy. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn!