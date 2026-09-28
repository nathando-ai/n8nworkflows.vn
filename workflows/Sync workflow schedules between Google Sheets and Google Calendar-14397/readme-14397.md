---
title: "🚀 Tự động đồng bộ lịch trình workflow n8n với Google Calendar & Sheets"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp các sếp theo dõi lịch trình workflow n8n trên Google Calendar và Google Sheets một cách dễ dàng và chính xác."
slug: "tu-dong-dong-bo-lich-trinh-workflow-n8n-google-calendar-sheets"
tags: [n8n, automation, no-code, google-calendar, google-sheets]
keywords: [n8n workflow, tự động hóa, google calendar, google sheets, quản lý workflow]
---

# 🚀 Tự động đồng bộ lịch trình workflow n8n với Google Calendar & Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý nhiều workflow n8n với lịch trình khác nhau. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động đồng bộ lịch trình workflow mỗi 30 phút mà không cần can thiệp thủ công.
- **Chính xác**: So sánh và cập nhật lịch trình workflow một cách tự động, tránh sai sót.
- **Cá nhân hóa**: Theo dõi lịch trình workflow trên Google Calendar và Google Sheets theo cách dễ hiểu.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7 mà không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n với API key đã kích hoạt.
- Tài khoản Google với quyền truy cập Google Calendar và Google Sheets.
- Google Service Account (không hết hạn) và Google Calendar OAuth2 (có thể hết hạn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/14397](https://n8n.io/workflows/14397).
3. Hoặc tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Đảm bảo lịch trình chạy mỗi 30 phút (`*/30 * * * *`).

2. **Get many workflows**:
   - Cấu hình credentials cho `n8n account` (API key của n8n).

3. **Sheets: Lookup ExistOnCalendar**:
   - Cấu hình credentials cho `GCP_SA` (Google Service Account).
   - Điền `YOUR_SPREADSHEET_ID` và tên tab `n8n Scheduling`.

4. **Sheets: OnCalendar=YES**:
   - Cấu hình credentials cho `GCP_SA` (Google Service Account).
   - Điền `YOUR_SPREADSHEET_ID` và tên tab `n8n Scheduling`.

5. **Create an event**:
   - Cấu hình credentials cho `Oauth GCalendar` (Google Calendar OAuth2).
   - Đảm bảo tài khoản Google Calendar được chia sẻ với Service Account.

6. **Delete an event**:
   - Cấu hình credentials cho `Oauth GCalendar` (Google Calendar OAuth2).

7. **Webhook**:
   - Cấu hình đường dẫn `delete-calendar` cho webhook.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi có sự thay đổi trong lịch trình workflow.
- **Lưu log**: Thêm node lưu log các thay đổi vào Google Sheets hoặc cơ sở dữ liệu.
- **Gửi báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo tổng hợp lịch trình workflow hàng tuần.

### 📌 Kết luận
Workflow "Sync workflow schedules between Google Sheets and Google Calendar" giúp các sếp quản lý lịch trình workflow n8n một cách dễ dàng và chính xác. Với việc tự động đồng bộ lịch trình mỗi 30 phút, các sếp có thể tập trung vào công việc quan trọng hơn. Hãy áp dụng ngay để tối ưu hóa quá trình quản lý workflow của bạn!