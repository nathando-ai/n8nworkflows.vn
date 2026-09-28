---
title: "🚀 Tự động cảnh báo website sập đa kênh qua UptimeRobot, Slack, WhatsApp & Notion bằng n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động phát hiện sự cố website và bắn cảnh báo tức thì qua Slack, WhatsApp, Email đồng thời tạo task trên Notion để team kỹ thuật xử lý ngay lập tức."
slug: "tu-dong-canh-bao-website-sap-da-kenh-n8n"
tags: [n8n, automation, devops, uptimerobot, slack, whatsapp, notion]
keywords: [n8n workflow, cảnh báo website sập, downtime alert, uptimerobot n8n, tự động hóa devops]
---

# 🚀 Tự động cảnh báo website sập đa kênh qua UptimeRobot, Slack, WhatsApp & Notion

Các sếp có bao giờ rơi vào cảnh website "bỗng dưng mất tích" giữa đêm, khách hàng thì la ó, còn team kỹ thuật thì hoàn toàn mù tịt vì không nhận được thông báo kịp thời? Việc kiểm tra thủ công hoặc chỉ dựa vào một kênh thông báo đơn lẻ (như email dễ bị trôi) thường mang lại rủi ro rất lớn cho doanh nghiệp.

Được phát triển bởi **Oneclick AI Squad**, workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp doanh nghiệp thiết lập một hệ thống ứng phó sự cố (Incident Management) đa kênh chuyên nghiệp. Ngay khi website gặp sự cố, hệ thống sẽ lập tức bắn thông tin đến mọi "mặt trận" quan trọng và tạo task xử lý giao việc tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và không bỏ lỡ bất kỳ sự cố downtime nào của hệ thống, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sự cố tức thì**: Nhận tín hiệu từ UptimeRobot qua Webhook chỉ trong vài mili-giây kể từ khi website "ngỏm".
- **Phủ sóng thông báo đa kênh**: Đồng thời gửi cảnh báo khẩn cấp đến **Slack**, **WhatsApp** và **Email** của đội ngũ vận hành.
- **Tự động hóa quản lý task**: Tự động tạo một task khắc phục sự cố (Incident Ticket) trong **Notion** kèm theo thông tin chi tiết để kỹ sư phụ trách xử lý ngay.
- **Hoạt động 24/7 không nghỉ**: Đảm bảo không có sự cố nào bị bỏ sót dù là ban ngày hay nửa đêm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- Một instance **n8n** đang hoạt động (Self-hosted hoặc Cloud).
- Tài khoản **UptimeRobot** đã thiết lập Monitor cho website kèm tính năng Webhook Alerts.
- Tài khoản và quyền kết nối API của các nền tảng:
  - **Slack Workspace** (để cấu hình Webhook/Bot gửi tin nhắn).
  - **WhatsApp Business API** hoặc nhà cung cấp dịch vụ tin nhắn WhatsApp.
  - **SMTP Server** (Gmail, SendGrid, Resend...) để gửi email.
  - **Notion Workspace** với một Database chuyên quản lý Task/Sự cố.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm góc trên bên phải -> **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình các node quan trọng sau đây:

- **UptimeRobot Webhook Trigger (`webhook`)**:
  - Node này sẽ cung cấp một URL Webhook Production. Các sếp cần copy URL này và dán vào phần cài đặt Webhook Alert của dịch vụ UptimeRobot để hệ thống bắn dữ liệu về khi website chuyển sang trạng thái "Down".
- **Send Slack Alert (`slack`)**:
  - Chọn hoặc tạo mới `slackApi` credentials.
  - Chọn Channel hoặc User nhận tin nhắn cảnh báo khẩn cấp.
- **Send WhatsApp Alert (`whatsApp`)**:
  - Cấu hình credentials `whatsAppApi` và điền số điện thoại nhận thông báo cùng mẫu tin nhắn (template) phù hợp.
- **Send Email Alert (`emailSend`)**:
  - Điền thông tin cấu hình `smtp` credentials (Host, Port, User, Pass) và thiết lập danh sách email nhận cảnh báo (DevOps team, CTO...).
- **Create Notion Task (`notion`)**:
  - Kết nối tài khoản qua `notionApi`.
  - Chọn đúng **Database ID** trong Notion của các sếp để hệ thống tự động thêm tiêu đề task, trạng thái (Status) và phân công kỹ sư phụ trách mỗi khi có sự cố xảy ra.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request test giả lập từ UptimeRobot để kiểm tra luồng chạy.
- Sau khi mọi thứ hoạt động trơn tru, hãy gạt công tắc sang trạng thái **Active** để hệ thống chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Các sếp có thể tích hợp thêm node **Telegram** hoặc **Discord** để đa dạng hóa kênh tiếp cận đội ngũ kỹ thuật.
- **Tự động phục hồi (Auto-resolve)**: Thiết lập thêm một nhánh xử lý khi UptimeRobot báo trạng thái website "Up" trở lại, từ đó tự động đóng task trên Notion và nhắn tin thông báo "Đã fix xong" lên Slack.
- **Lưu lịch sử sự cố**: Kết nối thêm Google Sheets hoặc Airtable để lưu lại toàn bộ lịch sử downtime nhằm phục vụ việc đo lường SLA sau này.

### 📌 Kết luận
Việc phụ thuộc vào cảnh báo thủ công hay đơn kênh không chỉ làm giảm uy tín dịch vụ mà còn kéo dài thời gian downtime của hệ thống. Với workflow n8n tích hợp UptimeRobot, Slack, WhatsApp và Notion này, các sếp sẽ xây dựng được một quy trình ứng phó sự cố chuyên nghiệp, tự động hóa hoàn toàn và cực kỳ hiệu quả. Hãy cài đặt ngay hôm nay để bảo vệ doanh nghiệp của mình!