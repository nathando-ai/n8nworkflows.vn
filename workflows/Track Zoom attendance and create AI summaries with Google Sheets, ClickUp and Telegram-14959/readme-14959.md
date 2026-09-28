---
title: "🚀 Tự động hóa Zoom: Theo dõi điểm danh, tổng kết AI và thông báo Telegram"
description: "Workflow n8n tự động ghi nhận điểm danh Zoom, tổng kết nội dung bằng AI và thông báo qua Telegram. Tiết kiệm thời gian quản lý cuộc họp và theo dõi người tham gia."
slug: "tu-dong-hoa-zoom-diem-danh-tong-ket-ai-telegram"
tags: [n8n, automation, no-code, zoom, google-sheets, clickup, telegram, ai]
keywords: [n8n workflow, tự động hóa, quản lý cuộc họp, điểm danh, tổng kết AI, telegram]
---

# 🚀 Tự động hóa Zoom: Theo dõi điểm danh, tổng kết AI và thông báo Telegram

[Các sếp đang mệt mỏi với việc quản lý cuộc họp Zoom thủ công? Hãy để workflow n8n này tự động hóa toàn bộ quy trình từ ghi nhận điểm danh đến tổng kết nội dung và thông báo qua Telegram. Tiết kiệm thời gian quý giá và nâng cao hiệu quả quản lý cuộc họp.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động ghi nhận điểm danh và phân loại người tham gia (đúng giờ/đến muộn).
- **Tổng kết thông minh**: AI tự động viết báo cáo cuộc họp chi tiết và gửi qua Telegram.
- **Theo dõi hiệu quả**: Tạo task ClickUp tự động cho những người tham gia muộn.
- **Quản lý tập trung**: Tất cả dữ liệu được lưu trữ trong Google Sheets để theo dõi dài hạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zoom với quyền tạo Webhook Only App.
- Google Sheets với bảng tính dành riêng cho điểm danh.
- Tài khoản ClickUp để tạo task theo dõi.
- Bot Telegram và ID chat để nhận thông báo.
- API key OpenAI để sử dụng mô hình GPT-4o-mini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/14959)
2. Chọn "Copy JSON" và lưu file JSON vào máy
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON đã lưu

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node 2. Set — Config Values**: Cập nhật các giá trị cấu hình:
  - Telegram chat ID: ID của kênh/chat nhận thông báo
  - Google Sheet ID: ID của bảng tính điểm danh
  - Sheet tab name: Tên tab trong bảng tính
  - Host name: Tên người chủ trì cuộc họp
  - Late threshold minutes: Số phút tối đa cho phép đến muộn
  - ClickUp list ID: ID của danh sách task trong ClickUp

- **Node 1. Webhook — Zoom Meeting Ended**:
  - Copy webhook URL từ node này
  - Thêm webhook vào Zoom Marketplace với event "meeting.ended"

- **Node 4. Google Sheets — Log Participant Row**: Kết nối tài khoản Google Sheets OAuth2

- **Node 7. OpenAI — GPT-4o-mini Model**: Kết nối tài khoản OpenAI

- **Node 9. ClickUp — Create Late Participant Task**: Kết nối tài khoản ClickUp API

- **Node 12. Telegram — Send Meeting Summary**: Kết nối tài khoản Telegram Bot API

#### 3. Kích hoạt ⚡️
- Thực hiện test run với dữ liệu mẫu để kiểm tra toàn bộ chuỗi xử lý
- Bật Active workflow sau khi đã cấu hình đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo cùng với Telegram
- Cấu hình gửi báo cáo hàng tuần từ Google Sheets
- Tích hợp với Google Calendar để tự động tạo lịch nhắc nhở
- Sử dụng mô hình AI khác (như Claude) để so sánh kết quả tổng kết

### 📌 Kết luận
Workflow này giúp các sếp quản lý cuộc họp Zoom một cách hiệu quả hơn, từ ghi nhận điểm danh đến theo dõi người tham gia và tổng kết nội dung. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả quản lý!