---
title: "🚀 Tự động hóa thông tin trước cuộc họp với OpenAI, Google Calendar và Slack"
description: "Hướng dẫn tự động hóa gửi thông tin ngữ cảnh cho người tham gia trước cuộc họp bằng n8n, tiết kiệm thời gian chuẩn bị và nâng cao hiệu quả cuộc họp"
slug: "tu-dong-hoa-thong-tin-truoc-cuoc-hop-openai-google-calendar-slack"
tags: [n8n, automation, no-code, AI, Google Calendar, Slack]
keywords: [n8n workflow, tự động hóa, AI chatbot, Google Calendar, Slack]
---

# 🚀 Tự động hóa thông tin trước cuộc họp với OpenAI, Google Calendar và Slack

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải chuẩn bị thông tin trước mỗi cuộc họp không? Với workflow này, các sếp có thể tự động hóa việc thu thập và tổng hợp thông tin ngữ cảnh cho người tham gia cuộc họp, giúp tiết kiệm thời gian quý giá và nâng cao hiệu quả cuộc họp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian chuẩn bị trước cuộc họp lên tới 70%
- Tự động tổng hợp thông tin từ email và lịch Google Calendar
- Cung cấp ngữ cảnh chi tiết cho mỗi người tham gia
- Tăng cường hiệu quả cuộc họp với thông tin chính xác và đầy đủ
- Hoạt động liên tục 24/7 với lịch trình tự động
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Gmail và Google Calendar
- Tài khoản Slack để nhận thông báo
- API Key từ OpenAI để sử dụng các tính năng AI
- Thiết lập các credentials cho các dịch vụ trên n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/11148)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Schedule Trigger** (Node 6):
   - Thiết lập tần suất kiểm tra lịch (mặc định 1 giờ)
   - Điều chỉnh theo nhu cầu của các sếp (ví dụ: 30 phút cho các cuộc họp thường xuyên)

2. **Google Calendar** (Node 3):
   - Thiết lập credentials cho Google Calendar
   - Đảm bảo tài khoản có quyền truy cập đầy đủ vào lịch của các sếp

3. **Gmail** (Nodes 1 và 5):
   - Thiết lập credentials cho Gmail
   - Cấu hình bộ lọc email để chỉ lấy các email liên quan đến cuộc họp

4. **OpenAI Models** (Nodes 13, 15, 16):
   - Thiết lập credentials cho OpenAI
   - Chọn model phù hợp (gợi ý: gpt-3.5-turbo hoặc gpt-4)
   - Điều chỉnh prompt trong các node chainLlm (Nodes 11 và 12) nếu cần

5. **Slack** (Node 14):
   - Thiết lập credentials cho Slack
   - Chọn channel hoặc người nhận thông báo

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Thêm một cuộc họp vào Google Calendar
   - Kiểm tra email của người tham gia
   - Chạy workflow trong chế độ test

2. Bật Active workflow:
   - Sau khi test thành công, bật workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với các nền tảng khác**:
   - Thay thế node Slack bằng Telegram, Microsoft Teams hoặc Email để nhận thông báo

2. **Tùy chỉnh thông báo**:
   - Điều chỉnh prompt trong các node chainLlm để thay đổi nội dung thông báo
   - Thêm thông tin từ các nguồn khác như Notion, Trello...

3. **Lưu log hoạt động**:
   - Thêm node Google Sheets để lưu trữ lịch sử thông báo
   - Tạo báo cáo định kỳ về hiệu suất workflow

4. **Xử lý lỗi nâng cao**:
   - Thiết lập email thông báo khi workflow gặp lỗi
   - Tạo backup dữ liệu quan trọng

### 📌 Kết luận
Workflow này là công cụ mạnh mẽ để tự động hóa việc chuẩn bị thông tin trước cuộc họp, giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả công việc. Với sự kết hợp của Google Calendar, Gmail và OpenAI, workflow cung cấp thông tin ngữ cảnh đầy đủ và chính xác cho mỗi người tham gia, giúp họ chuẩn bị tốt hơn cho cuộc họp sắp tới.

Hãy thử áp dụng ngay workflow này vào quy trình làm việc hàng ngày của các sếp để trải nghiệm sự khác biệt!