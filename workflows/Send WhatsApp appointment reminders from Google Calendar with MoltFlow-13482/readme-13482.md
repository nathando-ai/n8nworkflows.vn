---
title: "📅 Tự động gửi nhắc lịch hẹn WhatsApp từ Google Calendar với MoltFlow"
description: "Hướng dẫn tự động hóa gửi nhắc lịch hẹn WhatsApp từ Google Calendar trong 5 phút, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng"
slug: "tu-dong-gui-nhac-lich-hen-whatsapp-tu-google-calendar"
tags: [n8n, automation, no-code, whatsapp, google-calendar]
keywords: [n8n workflow, tự động hóa lịch hẹn, nhắc lịch hẹn, whatsapp automation, google calendar]
---

# 📅 Tự động gửi nhắc lịch hẹn WhatsApp từ Google Calendar với MoltFlow

[Các sếp] có biết không? Với việc làm thủ công, mỗi lần gửi nhắc lịch hẹn WhatsApp từ Google Calendar lại tốn thời gian và dễ bỏ sót. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình trong 5 phút, đảm bảo không bỏ sót bất kỳ cuộc hẹn nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhấn nút gửi từng tin nhắn
- **Chính xác 100%**: Không bỏ sót bất kỳ cuộc hẹn nào
- **Cá nhân hóa**: Gửi tin nhắn theo thời gian và nội dung cụ thể
- **Hoạt động liên tục**: Chạy tự động mỗi giờ, không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Calendar đã kích hoạt
- Tài khoản MoltFlow đã kết nối WhatsApp
- API Key từ MoltFlow
- Session ID từ MoltFlow (để định dạng tin nhắn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/13482)
2. Click "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Upcoming Events"**:
   - Chọn credential Google Calendar OAuth2 đã cấu hình
   - Điền Calendar ID (mặc định là "primary")

2. **Node "Format Reminders"**:
   - Thay thế `YOUR_SESSION_ID` bằng Session ID thực tế từ MoltFlow
   - Đảm bảo định dạng tin nhắn phù hợp với yêu cầu của các sếp

3. **Node "Send WhatsApp Reminder"**:
   - Thêm credential HTTP Header Auth
   - Thêm header `X-API-Key` với giá trị là API Key từ MoltFlow

4. **Cấu trúc sự kiện Google Calendar**:
   - Phải có số điện thoại khách hàng trong mô tả sự kiện theo định dạng:
     ```
     Phone: 1234567890
     ```

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" của node "Every Hour" để test
2. Kiểm tra kết quả ở node "Log Results"
3. Nếu mọi thứ ổn, click vào nút "Activate" để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để thông báo kết quả qua các kênh này
2. **Lưu log chi tiết**: Mở rộng node "Log Results" để lưu thêm thông tin chi tiết
3. **Gửi báo cáo định kỳ**: Thêm node để tổng hợp và gửi báo cáo hàng ngày
4. **Xử lý lỗi tự động**: Thêm node để xử lý các trường hợp lỗi và gửi thông báo

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa hoàn toàn việc gửi nhắc lịch hẹn WhatsApp từ Google Calendar. Không chỉ tiết kiệm thời gian mà còn nâng cao trải nghiệm khách hàng với các tin nhắn cá nhân hóa và đúng giờ. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!