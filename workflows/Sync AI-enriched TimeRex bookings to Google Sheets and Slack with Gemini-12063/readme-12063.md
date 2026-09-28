---
title: "🚀 Tự động hóa đặt lịch TimeRex với AI và Slack - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu đặt lịch TimeRex sang Google Sheets và Slack với AI phân tích thông minh bằng Gemini"
slug: "tu-dong-hoa-dat-lich-timerex-voi-ai-va-slack"
tags: [n8n, automation, no-code, timerex, google-sheets, slack, ai, gemini]
keywords: [n8n workflow, tự động hóa đặt lịch, timerex, google sheets, slack, ai, gemini]
---

# 🚀 Tự động hóa đặt lịch TimeRex với AI và Slack - Workflow n8n hoàn chỉnh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi phải xử lý thủ công hàng trăm cuộc hẹn hàng ngày từ TimeRex, dẫn đến:
- Thông tin đặt lịch bị phân mảnh giữa nhiều công cụ
- Không có cách nào tự động phân loại và tóm tắt nội dung cuộc hẹn
- Thông báo đến Slack thủ công tốn thời gian và dễ bỏ sót

Với workflow này, các sếp sẽ có được giải pháp toàn diện để:
- Tự động đồng bộ dữ liệu đặt lịch từ TimeRex sang Google Sheets
- Phân tích thông minh nội dung cuộc hẹn bằng AI Gemini
- Nhận thông báo tự động trên Slack với thông tin bổ sung từ AI

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi ngày cho việc quản lý đặt lịch
- Dữ liệu đặt lịch được lưu trữ tập trung trên Google Sheets
- Thông tin cuộc hẹn được tự động phân loại và tóm tắt
- Thông báo Slack được cá nhân hóa với thông tin từ AI
- Hệ thống hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản TimeRex với quyền quản trị
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Slack với quyền gửi tin nhắn
- API Key của Google Gemini
- Google Sheets đã được tạo với cấu trúc cột như yêu cầu
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12063](https://n8n.io/workflows/12063)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

Hoặc có thể copy/paste JSON trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **TimeRex Webhook** (Node đầu tiên):
   - Cần cấu hình URL webhook trong TimeRex Settings
   - Đặt path là `/timerex-booking` và method là POST

2. **Google Sheets Credentials**:
   - Tất cả các node Google Sheets cần được cấu hình với cùng một tài khoản Google
   - Đảm bảo tài khoản có quyền truy cập vào Google Sheets được chỉ định

3. **Verify Security Token** (Node quan trọng):
   - Cần đặt giá trị `x-timerex-authorization` trong header của request từ TimeRex
   - Nếu không có token, các sếp có thể tạm thời bỏ qua node này (nhưng không khuyến khích)

4. **Google Gemini Nodes**:
   - Cần cấu hình API Key của Google Gemini
   - Đảm bảo tài khoản có đủ credit để sử dụng dịch vụ

5. **Slack Nodes**:
   - Cần chọn channel phù hợp để nhận thông báo
   - Đảm bảo bot Slack có quyền gửi tin nhắn đến channel đã chọn

6. **Google Sheets Configuration**:
   - Cần cập nhật ID của Google Sheet trong tất cả các node Google Sheets
   - Đảm bảo cấu trúc cột phù hợp với yêu cầu:
     ```
     event_id | booking_date | guest_name | guest_email | calendar_name | meeting_url | host_name | media_source | company_name | booking_category | ai_meeting_brief | created_at
     ```

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu xử lý dữ liệu thực tế

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Telegram**: Thay thế node Slack bằng node Telegram để nhận thông báo trên ứng dụng ưa thích hơn
2. **Lưu log hoạt động**: Thêm node để lưu log các hoạt động quan trọng vào Google Sheets hoặc cơ sở dữ liệu
3. **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo tổng hợp hàng ngày/ hàng tuần về các cuộc hẹn
4. **Xử lý lỗi nâng cao**: Thêm node để xử lý các trường hợp lỗi và gửi thông báo cảnh báo

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quản lý đặt lịch TimeRex với các tính năng thông minh từ AI. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian đáng kể, đảm bảo dữ liệu được quản lý tập trung và nhận được thông báo kịp thời với thông tin bổ sung từ AI.

Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n!