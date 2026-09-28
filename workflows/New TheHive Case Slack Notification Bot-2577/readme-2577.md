---
title: "🚀 Tự động hóa SOC: Tích hợp TheHive với Slack Notification Bot"
description: "Hướng dẫn xây dựng workflow n8n giúp SOC analysts quản lý, cập nhật trạng thái, mức độ nghiêm trọng và giao việc cho các case trong TheHive trực tiếp từ Slack mà không cần đổi tab."
slug: "tich-hop-thehive-slack-notification-bot-n8n"
tags: [n8n, automation, cybersecurity, thehive, slack, devops]
keywords: [n8n workflow, thehive slack bot, soc automation, tu dong hoa thehive, quan ly su co bao mat]
h1: "🚀 Tự động hóa SOC: Tích hợp TheHive với Slack Notification Bot"
---

# 🚀 Tự động hóa SOC: Tích hợp TheHive với Slack Notification Bot

Trong các đội ngũ An toàn thông tin (SOC), việc liên tục chuyển đổi ngữ cảnh giữa công cụ quản lý sự cố (**TheHive**) và nền tảng chat (**Slack**) làm giảm đáng kể tốc độ phản ứng. Các phân tích viên phải mất nhiều thời gian để cập nhật trạng thái, gán việc hay thay đổi mức độ nghiêm trọng của các case thủ công.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% hai chiều: đẩy thông báo case mới từ TheHive lên Slack với các nút tương tác (Interactive Buttons) và modal popup, cho phép các sếp xử lý sự cố trực tiếp ngay trong Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tốc phản ứng sự cố (Incident Response):** Xử lý case, thay đổi TLP, PAP, Severity hoặc đóng case giả mạo (False Positive) ngay trong Slack chỉ bằng 1 cú click.
- **Loại bỏ thao tác thủ công:** Không cần mở giao diện TheHive để cập nhật trạng thái, giảm thiểu sai sót dữ liệu.
- **Đồng bộ hóa thời gian thực:** Mọi thay đổi trên Slack sẽ lập tức cập nhật vào hệ thống TheHive và làm mới tin nhắn gốc trên Slack.
- **Quản lý task tiện lợi:** Hỗ trợ mở Modal Popup trong Slack để thêm task, phân công nhiệm vụ trực tiếp vào case của TheHive.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **TheHive (v5+):** Tài khoản quản trị để cấu hình Webhook và API Key (`theHiveProjectApi`).
- **Slack Workspace & App:** Đã tạo Slack App với các quyền cấu hình Event Subscriptions, Bot Token, và cấu hình tương tác (Interactivity & Shortcuts) để nhận webhook từ n8n (`slackApi`).
- **Lưu ý quan trọng về Email:** Email của tài khoản người dùng trong **TheHive** và **Slack** **PHẢI TRÙNG KHỚP** nhau để tính năng gán việc (Assignee) hoạt động chính xác.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n template hoặc copy đoạn mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** / **Paste Workflow JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node cốt lõi sau:
- **TheHive Trigger:** Cấu hình URL webhook nhận từ TheHive (vào Cài đặt của TheHive 5 để thêm webhook trỏ về URL của node này).
- **Receive Button Press (Webhook):** Cấu hình đường dẫn endpoint (`slackthehivewebhook`) để nhận sự kiện khi người dùng click vào các nút tương tác trên Slack.
- **Credentials Slack (`slackApi` & `theHiveProjectApi`):** Kết nối tài khoản Slack Bot Token và TheHive API Key của các sếp vào các node tương ứng (`Post New Case To Slack`, `Update Status in TheHive`, `Add a task to TheHive`,... đa số sử dụng các credentials này).
- **Nhóm node xử lý Modal & HTTP Request:** Node `Task Modal` gọi đến API `https://slack.com/api/views.open` yêu cầu cấu hình đúng Slack Bot Scope (`chat:write`, `commands`, `users:read`,...).

#### 3. Kích hoạt ⚡️
- Nhấp vào **Execute Workflow** và gửi một thử nghiệm (test event) từ TheHive để kiểm tra luồng dữ liệu.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm các node như Telegram hoặc Microsoft Teams nếu đội ngũ của các sếp sử dụng đa nền tảng chat.
- **Tạo bảng Log kiểm toán:** Thêm node Google Sheets hoặc cơ sở dữ liệu (PostgreSQL/MySQL) để lưu lại lịch sử tương tác của từng SOC analyst trên Slack phục vụ cho việc đánh giá hiệu suất.
- **Cảnh báo lỗi phân công:** Thêm node `If` kiểm tra xem email nhận từ Slack có tồn tại trong hệ thống TheHive hay không để tránh việc workflow bị lỗi dừng đột ngột khi email không khớp.

### 📌 Kết luận
Tích hợp TheHive và Slack thông qua n8n là một bước tiến lớn giúp tối ưu hóa quy trình vận hành SOC, giúp đội ngũ tiết kiệm từng giây quý giá trong việc xử lý các mối đe dọa an ninh mạng. Hãy áp dụng ngay vào hệ thống của các sếp để cảm nhận sự khác biệt!