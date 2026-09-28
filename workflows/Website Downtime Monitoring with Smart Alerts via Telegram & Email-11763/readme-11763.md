---
title: "🚀 Giám sát downtime website tự động với cảnh báo thông minh qua Telegram & Email"
description: "Hướng dẫn tự động hóa giám sát website, phát hiện downtime và gửi cảnh báo qua Telegram và Email bằng n8n. Tiết kiệm thời gian và nâng cao hiệu suất vận hành hệ thống."
slug: "giam-sat-downtime-website-tu-dong-voi-n8n"
tags: [n8n, automation, no-code, devops, monitoring]
keywords: [n8n workflow, tự động hóa, giám sát website, cảnh báo downtime, telegram, email]
---

# 🚀 Giám sát downtime website tự động với cảnh báo thông minh qua Telegram & Email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện downtime ngay lập tức**: Kiểm tra website theo lịch trình và thông báo ngay khi có sự cố.
- **Cảnh báo đa kênh**: Nhận thông báo qua cả Telegram và Email để đảm bảo không bỏ lỡ bất kỳ sự cố nào.
- **Tiết kiệm thời gian**: Tự động hóa quy trình giám sát thay vì phải kiểm tra thủ công.
- **Dễ dàng cấu hình**: Workflow được thiết kế đơn giản, chỉ cần nhập danh sách website và thông tin liên lạc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Danh sách website cần giám sát**: Danh sách các URL của website cần theo dõi.
- **Thông tin Telegram**:
  - Token của bot Telegram (hướng dẫn tạo bên dưới).
  - Chat ID của người nhận thông báo (hướng dẫn lấy bên dưới).
- **Thông tin Email**:
  - Thông tin tài khoản SMTP (ví dụ: Gmail, Outlook).
  - Địa chỉ email nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/11763](https://n8n.io/workflows/11763) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.
3. Hoặc, copy toàn bộ nội dung JSON từ trang web và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Cấu hình lịch trình kiểm tra website (ví dụ: mỗi 5 phút).

2. **Node "Perform Site Test"**:
   - Đảm bảo URL của website cần giám sát được nhập chính xác.

3. **Node "Config"**:
   - Nhập danh sách website cần giám sát vào trường **websites**.
   - Nhập **telegram_chat_id** của người nhận thông báo.

4. **Node "Send a text message"**:
   - Tạo mới credentials cho Telegram:
     - Nhấn vào **Credentials** → **Create New** → **Telegram Bot API**.
     - Nhập **bot token** đã tạo từ BotFather.
   - Đảm bảo **telegram_chat_id** đã được nhập chính xác.

5. **Node "Send email"**:
   - Tạo mới credentials cho SMTP:
     - Nhấn vào **Credentials** → **Create New** → **SMTP**.
     - Nhập thông tin tài khoản SMTP (ví dụ: Gmail, Outlook).
   - Nhập địa chỉ email nhận thông báo vào trường **to**.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Nhấn vào nút **Execute Workflow** để kiểm tra workflow hoạt động đúng.
2. **Bật Active workflow**:
   - Nhấn vào nút **Activate Workflow** để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node Slack để nhận thông báo trên kênh Slack.
- **Lưu log giám sát**: Thêm node Google Sheets để lưu log giám sát.
- **Cảnh báo nâng cao**: Thêm node LLM để phân tích nguyên nhân downtime và gửi báo cáo chi tiết.
- **Gửi báo cáo định kỳ**: Thêm node Email để gửi báo cáo trạng thái website hàng ngày.

### 📌 Kết luận
Workflow "Website Downtime Monitoring with Smart Alerts via Telegram & Email" giúp các sếp tự động hóa quá trình giám sát website, phát hiện downtime ngay lập tức và nhận cảnh báo đa kênh. Với việc cấu hình đơn giản và hiệu suất cao, workflow này là giải pháp hoàn hảo cho việc nâng cao hiệu suất vận hành hệ thống. Hãy áp dụng ngay để tiết kiệm thời gian và đảm bảo hệ thống luôn hoạt động ổn định!

---
## Hướng dẫn tạo Telegram bot và lấy chat ID

1. **Tạo Telegram bot**
   1. Mở Telegram và trò chuyện với **@BotFather**.
   2. Gửi `/newbot` và làm theo hướng dẫn để chọn **tên** và **username** cho bot (phải kết thúc bằng “bot”).
   3. Sao chép **bot token** được trả về bởi BotFather.

2. **Bắt đầu cuộc trò chuyện & lấy chat ID**
   1. Trong Telegram, tìm bot bằng username (ví dụ: `@my_alert_bot`) và gửi tin nhắn (ví dụ: `/start`).
   2. Trong trình duyệt, truy cập:
      ```
      https://api.telegram.org/bot<Token>/getUpdates
      ```
   3. Tìm `"chat":{"id":123456789}` trong JSON và sao chép số đó làm **chat_id**.

3. **Thêm cài đặt Telegram trong n8n**
   - Trong workflow, nhấn vào node **Telegram**.
   - Tại **Credentials**, chọn **Create New** → **Telegram Bot API**, và dán **bot token**.
   - Tại trường **telegram_chat_id** trong node **Config**, nhập **chat_id** đã lấy được.

---
## Tác giả
# Muntasir Mubin
### Founder & CEO của WebDextro Ltd, một công ty phát triển Web & App nổi tiếng tại Vương quốc Anh.

📧 mubin@webdextro.org
📞 [Theo dõi trên Facebook](https://fb.me/the.mubiin)
💼 [Kết nối trên Linkedin](https://www.linkedin.com/in/mubiiin/)