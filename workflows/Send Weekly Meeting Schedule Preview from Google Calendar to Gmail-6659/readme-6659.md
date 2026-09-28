```yaml
---
title: "📅 [Tự động hóa] Gửi Tóm tắt Lịch Họp Hàng Tuần từ Google Calendar sang Gmail"
description: "Workflow n8n tự động gửi tóm tắt lịch họp hàng tuần từ Google Calendar sang email Gmail mỗi Chủ Nhật tối. Tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-hoa-gui-tom-tat-lich-hop-hang-tuan-tu-google-calendar-sang-gmail"
tags: [n8n, automation, no-code, google-calendar, gmail]
keywords: [n8n workflow, tự động hóa lịch họp, google calendar, gmail, workflow n8n]
---
```

# 📅 [Tự động hóa] Gửi Tóm tắt Lịch Họp Hàng Tuần từ Google Calendar sang Gmail

[Các sếp thường phải tốn thời gian hàng tuần để kiểm tra và tổng hợp lịch họp từ Google Calendar để gửi email thông báo. Với workflow này, các sếp sẽ tự động nhận được tóm tắt lịch họp hàng tuần vào Chủ Nhật tối, giúp tiết kiệm thời gian và nâng cao hiệu quả làm việc.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **30 phút** mỗi tuần cho việc tổng hợp lịch họp
- Nhận được email tóm tắt lịch họp hàng tuần một cách tự động
- Giảm thiểu sai sót trong việc kiểm tra và gửi thông báo
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Calendar đã được chia sẻ với các sếp
- Tài khoản Gmail để gửi email thông báo
- Quyền truy cập API cho cả Google Calendar và Gmail
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này bằng cách:
1. Truy cập [link gốc workflow](https://n8n.io/workflows/6659)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow vào
4. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình lại các node quan trọng sau:

1. **Node "Sunday Evening Trigger" (cron)**
   - Đảm bảo thời gian trigger phù hợp với múi giờ của các sếp
   - Ví dụ: `0 18 * * 0` (8:00 PM mỗi Chủ Nhật)

2. **Node "Get Calendar Events" (googleCalendar)**
   - Chọn credentials là `googleCalendarOAuth2Api`
   - Điền Calendar ID của các sếp
   - Thiết lập thời gian bắt đầu và kết thúc cho tuần (ví dụ: từ Chủ Nhật đến Thứ Bảy)

3. **Node "Send Summary Email" (gmail)**
   - Chọn credentials là `gmailApi`
   - Điền địa chỉ email nhận thông báo
   - Tùy chỉnh tiêu đề và nội dung email theo nhu cầu

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong:
1. Click vào nút "Execute Node" để test với dữ liệu mẫu
2. Kiểm tra email nhận được để đảm bảo nội dung đúng
3. Bật Active workflow để chạy tự động hàng tuần

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể thêm node Slack để nhận thông báo trên kênh Slack
- Có thể lưu log các email đã gửi để theo dõi lịch sử
- Có thể thiết lập gửi báo cáo định kỳ theo tháng hoặc quý
- Có thể kết hợp với Google Sheets để lưu trữ lịch sử các sự kiện

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý lịch họp hàng tuần. Với việc tự động hóa toàn bộ quá trình từ lấy dữ liệu đến gửi email, các sếp có thể tập trung vào công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!