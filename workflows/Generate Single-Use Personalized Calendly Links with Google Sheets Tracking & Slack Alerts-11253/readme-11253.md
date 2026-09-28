---
title: "🚀 Tự Động Tạo Link Calendly Dùng 1 Lần, Lưu Google Sheets & Báo Slack bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo link đặt lịch Calendly dùng 1 lần (single-use), cá nhân hóa thông tin khách hàng, lưu trữ vào Google Sheets và gửi thông báo qua Slack tức thì."
slug: "tu-dong-tao-link-calendly-dung-1-lan-n8n"
tags: [n8n, automation, calendly, google-sheets, slack, crm]
keywords: [n8n workflow, tạo link calendly tự động, calendly api single use link, n8n google sheets slack, tự động hóa bán hàng]
---

# 🚀 Tự Động Tạo Link Calendly Dùng 1 Lần, Lưu Google Sheets & Báo Slack

Trong các chiến dịch sales outreach hoặc chăm sóc khách hàng VIP, việc gửi các link đặt lịch chung chung thường làm giảm tỷ lệ chuyển đổi. Khách hàng thích sự cá nhân hóa. Tuy nhiên, việc phải vào Calendly thủ công để tạo từng link dùng một lần (single-use link) cho mỗi khách hàng là một cực hình tốn rất nhiều thời gian.

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Hệ thống sẽ tự động nhận thông tin khách hàng qua Webhook, kết nối với Calendly API để tạo link đặt lịch độc nhất (chỉ dùng được 1 lần, tự động điền sẵn tên & email), lưu vết toàn bộ vào Google Sheets và bắn thông báo mượt mà về Slack cho đội ngũ Sales nắm bắt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Tạo link Calendly cá nhân hóa ngay lập tức thông qua API mà không cần thao tác tay.
- **Bảo mật & Giới hạn thông minh:** Link tự động hết hạn sau 1 lần đặt lịch hoặc sau 90 ngày nếu không sử dụng, tránh việc link bị chia sẻ bừa bãi.
- **Đồng bộ CRM hoàn hảo:** Tự động ghi nhận thông tin khách hàng, thời gian tạo và link tương ứng vào Google Sheets để dễ dàng tracking.
- **Cảnh báo thời gian thực:** Đội ngũ kinh doanh nhận thông báo ngay qua kênh Slack khi có link mới được khởi tạo cho khách hàng tiềm năng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Calendly** có quyền cấu hình API / OAuth2.
- **Google Sheets** để lưu log dữ liệu khách hàng và link.
- **Slack Workspace** (tùy chọn nếu muốn nhận thông báo qua bot).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ kho lưu trữ n8n (link gốc [tại đây](https://n8n.io/workflows/11253)) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Webhook Trigger:** Đây là điểm đầu vào nhận dữ liệu POST request từ CRM hoặc Landing Page của các sếp với cấu trúc JSON mẫu:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "event_type_uri": "optional"
  }
  ```
- **Get Current User, Get Event Types, Create Single-Use Link:** Các node HTTP Request này bắt buộc phải kết nối với **Calendly OAuth2 API Credentials**. Các sếp cần vào `calendly.com/integrations` -> `API & Webhooks` để thiết lập ứng dụng OAuth2 và liên kết với n8n.
- **Log to Google Sheets:** Cấu hình credentials `Google Sheets OAuth2 API`, trỏ tới file Google Sheet quản lý của sếp (với các cột tiêu đề chuẩn: *Name, Email, Link, Event, Created*), chọn thao tác `Append` ở mục `operation`.
- **Notify via Slack:** Kết nối credential `Slack API` và cấu hình Channel ID cụ thể để bot bắn tin nhắn thông báo mỗi khi có link mới xuất xưởng.
- **Respond to Webhook:** Trả về kết quả JSON cho ứng dụng gọi tới với cấu trúc bao gồm URL đặt lịch và thông tin chi tiết của người nhận.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test workflow** bằng cách gửi một POST request mẫu qua Postman hoặc công cụ cURL tới Webhook URL.
- Kiểm tra kết quả trả về, dữ liệu trên Google Sheets và thông báo trên Slack.
- Nếu mọi thứ chạy mượt mà, hãy bật nút **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Email Marketing:** Kết nối thêm node Gmail hoặc SendGrid ngay sau bước tạo link để hệ thống tự động gửi email mời họp chứa đúng chiếc link cá nhân hóa đó cho khách hàng.
- **Xử lý nhánh điều kiện (If Node):** Phân loại loại sự kiện (Event Type) dựa trên giá trị khách hàng (VIP hay Standard) để tự động chọn loại lịch phù hợp.
- **Báo cáo định kỳ:** Kết hợp thêm node Schedule Trigger để tổng hợp số lượng link đã tạo trong tuần/tháng và gửi báo cáo vào nhóm Slack chung.

### 📌 Kết luận
Việc tự động hóa quy trình tạo link đặt lịch Calendly không chỉ giúp tiết kiệm hàng giờ thao tác thủ công mỗi ngày mà còn mang lại trải nghiệm chuyên nghiệp, mượt mà cho khách hàng ngay từ điểm chạm đầu tiên. Hãy áp dụng ngay vào hệ thống CRM của doanh nghiệp các sếp nhé!