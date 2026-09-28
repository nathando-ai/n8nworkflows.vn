---
title: "🚀 Tự động hóa Zoom: Tóm tắt cuộc họp, tạo nhiệm vụ với Claude, ClickUp, Calendar, Slack và Sheets"
description: "Giải pháp tự động hóa hoàn chỉnh giúp tóm tắt cuộc họp Zoom, tạo nhiệm vụ ClickUp, đặt lịch hẹn, thông báo Slack và lưu log Google Sheets - không cần can thiệp thủ công."
slug: "tu-dong-hoa-zoom-tom-tat-cuoc-hop-tao-nhiem-vu"
tags: [n8n, automation, no-code, zoom, ai, clickup, google, slack]
keywords: [n8n workflow, tự động hóa cuộc họp, tóm tắt AI, quản lý nhiệm vụ, lịch hẹn, thông báo nhóm]
---

# 🚀 Tự động hóa Zoom: Tóm tắt cuộc họp, tạo nhiệm vụ với Claude, ClickUp, Calendar, Slack và Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý toàn bộ quy trình sau mỗi cuộc họp (tóm tắt, tạo nhiệm vụ, đặt lịch...)
- **Chính xác cao**: Sử dụng AI Claude 3.7 Sonnet để phân tích và tóm tắt nội dung chính xác
- **Cá nhân hóa**: Gửi email tóm tắt riêng cho từng thành viên tham gia
- **Hệ thống hóa**: Lưu toàn bộ thông tin cuộc họp vào Google Sheets để theo dõi
- **Tích hợp hoàn chỉnh**: Kết nối liền mạch với các công cụ quản lý hiện có (ClickUp, Google Calendar, Slack)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zoom Pro (hoặc cao hơn) với Cloud Recording và Auto-Transcription đã bật
- API Key từ Anthropic (để sử dụng Claude 3.7 Sonnet)
- Tài khoản ClickUp với API Token
- Quyền truy cập Google Calendar và Google Sheets
- Kênh Slack để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15818)
2. Click nút "Copy" để sao chép JSON workflow
3. Trong n8n Editor, click "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node 1. Schedule — Every Day 9AM**:
   - Đặt thời gian chạy tự động hàng ngày (mặc định 9AM)

2. **Node 3. Zoom — Get All Meetings**:
   - Tạo ứng dụng OAuth2 trên [Zoom Marketplace](https://marketplace.zoom.us/)
   - Cần các quyền: `meeting:read`, `recording:read`
   - Kết nối credential trong n8n

3. **Node 10. Claude 3.7 — Generate Meeting Summary**:
   - Tạo API Key tại [Anthropic Console](https://console.anthropic.com/)
   - Kết nối credential trong node này
   - Chọn model: `claude-3-7-sonnet-20250219`

4. **Node 16. HTTP — Create ClickUp Task**:
   - Lấy API Token từ ClickUp Settings → Apps → API Token
   - Thay thế `YOUR_CLICKUP_API_TOKEN` và `YOUR_CLICKUP_LIST_ID`

5. **Node 19. Google Calendar — Create Follow-Up**:
   - Kết nối credential Google Calendar
   - Thay thế `YOUR_CALENDAR_ID` (thường là email của bạn)

6. **Node 20. Slack — Send Team Notification**:
   - Kết nối credential Slack
   - Thay thế `YOUR_SLACK_CHANNEL_ID`

7. **Node 21. Google Sheets — Log Meeting**:
   - Kết nối credential Google Sheets
   - Thay thế `YOUR_GOOGLE_SHEET_ID`
   - Tạo tab "Meeting Log" với các cột:
     - Date
     - Meeting Title
     - Meeting ID
     - Duration (min)
     - Participants
     - Summary Sent
     - Tasks Created
     - Follow-up Created
     - Processed At

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ luồng
2. Bật Active workflow
3. Kiểm tra email, ClickUp, Calendar và Slack để xác nhận các thông báo được gửi đúng

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh prompt AI**: Chỉnh sửa node 10 để điều chỉnh cách AI tóm tắt và định dạng đầu ra
- **Thêm bộ lọc**: Sử dụng node Filter để chỉ xử lý các cuộc họp quan trọng nhất
- **Báo cáo định kỳ**: Kết hợp với Google Data Studio để tạo báo cáo từ dữ liệu trong Sheets
- **Tích hợp với Notion**: Thay thế node 21 bằng Notion node để lưu log vào Notion

### 📌 Kết luận
Workflow này là giải pháp toàn diện giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý cuộc họp hàng ngày. Bằng cách tự động hóa toàn bộ quy trình từ tóm tắt đến tạo nhiệm vụ và đặt lịch, các sếp có thể tập trung vào công việc quan trọng hơn. Hãy thử ngay và trải nghiệm cách làm việc hiệu quả hơn với n8n!