---
title: "🔄 Đồng bộ sự kiện & người tham dự giữa KlickTipp và Google Calendar"
description: "Tự động hóa hoàn toàn quá trình đồng bộ sự kiện và trạng thái tham dự giữa KlickTipp và Google Calendar, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "dong-bo-su-kien-nguoi-tham-du-klicktipp-google-calendar"
tags: [n8n, automation, no-code, email-marketing, event-management]
keywords: [n8n workflow, tự động hóa sự kiện, đồng bộ Google Calendar, KlickTipp, quản lý sự kiện]
---

# 🔄 Đồng bộ sự kiện & người tham dự giữa KlickTipp và Google Calendar

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý sự kiện thủ công. Giới thiệu workflow như giải pháp tự động hóa hoàn chỉnh.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Đồng bộ tự động toàn bộ chu kỳ sự kiện (tạo, cập nhật, hủy)
- Tự động cập nhật trạng thái tham dự (đồng ý, từ chối, xem xét)
- Tiết kiệm 80% thời gian quản lý thủ công
- Dữ liệu luôn đồng bộ giữa hai hệ thống
- Tự động lọc email nội bộ để bảo mật thông tin
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản KlickTipp với quyền truy cập API
- Tài khoản Google Calendar với quyền quản lý sự kiện
- Các thông tin sau:
  - Google Calendar API credentials (Client ID & Client Secret)
  - KlickTipp API credentials (Username & Password)
  - Danh sách email nội bộ cần lọc (nếu có)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10295](https://n8n.io/workflows/10295)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node quan trọng cần cấu hình:**
1. **Watch new Google Calendar events** (googleCalendarTrigger)
   - Chọn credentials: googleCalendarOAuth2Api
   - Đảm bảo tài khoản có quyền truy cập đầy đủ vào Google Calendar

2. **Watch updated Google Calendar events** (googleCalendarTrigger)
   - Chọn credentials: googleCalendarOAuth2Api
   - Cấu hình để theo dõi sự kiện được cập nhật

3. **Watch cancelled Google Calendar events** (googleCalendarTrigger)
   - Chọn credentials: googleCalendarOAuth2Api
   - Cấu hình để theo dõi sự kiện bị hủy

4. **Watch Tagging in KlickTipp** (n8n-nodes-klicktipp.klicktippTrigger)
   - Chọn credentials: klickTippApi
   - Cấu hình để theo dõi các thẻ "Send an event invitation via Google Calendar"

5. **Create a Google Calendar Event** (googleCalendar)
   - Chọn credentials: googleCalendarOAuth2Api
   - Cấu hình các trường dữ liệu cần đồng bộ (summary, description, location, start, end)

6. **Filter email domain** nodes (filter)
   - Cấu hình danh sách email nội bộ cần lọc (nếu có)
   - Ví dụ: @congty.com, @domain.com

7. **Create or update contact for attendee** nodes (n8n-nodes-klicktipp.klicktipp)
   - Chọn credentials: klickTippApi
   - Đảm bảo các trường custom fields đã được tạo trong KlickTipp

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn "Activate" trên mỗi node trigger
2. Thử chạy với dữ liệu mẫu để kiểm tra kết quả
3. Kiểm tra các sự kiện được tạo trong Google Calendar và trạng thái trong KlickTipp

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node gửi thông báo khi có sự kiện mới
2. **Báo cáo định kỳ**: Thêm node tạo báo cáo tổng hợp trạng thái sự kiện
3. **Xử lý lỗi tự động**: Cấu hình retry logic cho các node thất bại
4. **Lịch sử thay đổi**: Thêm node lưu log các thay đổi quan trọng

### 📌 Kết luận
Workflow này tạo ra một hệ thống đồng bộ hoàn chỉnh giữa KlickTipp và Google Calendar, giúp các sếp quản lý sự kiện một cách hiệu quả hơn. Với khả năng tự động hóa toàn bộ quá trình, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn thay vì phải theo dõi thủ công. Hãy thử ngay để trải nghiệm sự tiện lợi và hiệu quả mà nó mang lại!