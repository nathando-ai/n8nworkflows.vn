---
title: "🚀 Cảnh báo thay đổi website tự động qua Discord"
description: "Hướng dẫn tự động hóa cảnh báo thay đổi nội dung website qua Discord bằng n8n, tiết kiệm thời gian giám sát thủ công"
slug: "canh-bao-thay-doi-website-tu-dong-qua-discord"
tags: [n8n, automation, no-code, discord, web-scraping]
keywords: [n8n workflow, tự động hóa, cảnh báo website, discord notification, web monitoring]
---

# 🚀 Cảnh báo thay đổi website tự động qua Discord

[Các sếp đang làm việc với nhiều website cần theo dõi nội dung thường xuyên? Bạn mệt mỏi phải kiểm tra thủ công mỗi ngày? Hãy để n8n làm việc thay bạn! Workflow này sẽ tự động kiểm tra thay đổi trên website và gửi cảnh báo ngay lập tức qua Discord.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian giám sát thủ công hàng ngày
- Nhận cảnh báo tức thì khi có thay đổi trên website
- Tự động hóa toàn bộ quá trình theo dõi nội dung
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Kết hợp với Discord để thông báo nhanh chóng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Discord và quyền gửi tin nhắn trong kênh
- URL của website cần theo dõi
- Thời gian kiểm tra định kỳ (ví dụ: mỗi giờ)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: https://n8n.io/workflows/426
3. Hoặc tải file JSON từ link trên và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Cron**:
   - Chỉnh sửa biểu thức cron để đặt thời gian kiểm tra định kỳ (ví dụ: `0 * * * *` để kiểm tra mỗi giờ)

2. **Node HTTP Request**:
   - Thay đổi URL trong node này thành địa chỉ website bạn muốn theo dõi
   - Có thể thêm các header nếu website yêu cầu xác thực

3. **Node Discord**:
   - Tạo một Discord Webhook URL trong kênh Discord của bạn
   - Dán Webhook URL vào node Discord
   - Tùy chỉnh nội dung thông báo theo ý muốn

4. **Node IF**:
   - Điều chỉnh logic so sánh để xác định khi nào cần gửi cảnh báo
   - Có thể thêm các điều kiện phức tạp hơn nếu cần

#### 3. Kích hoạt ⚡️
1. Nhấn "Execute Node" trên node Cron để kiểm tra kết nối
2. Sau khi tất cả các node được cấu hình đúng, nhấn "Activate Workflow"
3. Kiểm tra kênh Discord để đảm bảo nhận được thông báo thử nghiệm

### ✍️ Mẹo & gợi ý nâng cao
- Thêm nhiều website để theo dõi bằng cách sao chép và sửa đổi các node HTTP Request và Discord
- Kết hợp với các dịch vụ khác như Slack hoặc Telegram để nhận thông báo đa kênh
- Thêm node Email để nhận cảnh báo qua email
- Tích hợp với các dịch vụ webhook khác để tự động hóa thêm các tác vụ khác

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi thay đổi trên website và nhận cảnh báo tức thì qua Discord. Với việc cấu hình đơn giản và hoạt động liên tục 24/7, đây là giải pháp hoàn hảo cho việc giám sát nội dung website một cách hiệu quả. Hãy thử ngay và tiết kiệm thời gian quý giá của bạn!