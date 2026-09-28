---
title: "🚀 Tự Động Cảnh Báo Lỗi Jira Độ Ưu Cao (High Priority) Lên Slack, Google Chat & Email"
description: "Hướng dẫn cấu hình workflow n8n tự động phát hiện sự cố Jira mức độ cao và gửi cảnh báo tức thì qua Slack, Google Chat và Email cho quản lý."
slug: "tu-dong-canh-bao-jira-high-priority-slack-google-chat-email"
tags: [n8n, automation, no-code, jira, slack, google-chat, gmail]
keywords: [n8n workflow, jira webhook, cảnh báo jira tự động, slack notification, google chat n8n]
---

# 🚀 Tự Động Cảnh Báo Lỗi Jira Độ Ưu Tiên Cao Lên Slack, Google Chat & Email

Các sếp có bao giờ gặp tình trạng lỗi nghiêm trọng (High Priority) được tạo trên Jira nhưng team kỹ thuật lại bỏ quên vì quá bận, dẫn đến việc khách hàng phàn nàn rồi sếp mới biết chuyện? Việc kiểm tra thủ công bảng Jira liên tục là bất khả thi và gây lãng phí thời gian quý báu.

Giải pháp ở đây là để n8n lo! Workflow này sẽ tự động canh gác Jira 24/7. Ngay khi có một task hoặc bug mức độ **High** (hoặc Critical) xuất hiện, hệ thống sẽ lập tức bắn thông báo đa kênh đến **Slack channel**, **Google Chat space** và gửi một email chi tiết đến quản lý (`emailTo`). Không một sự cố nào có thể lọt lưới!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản ứng tức thì (Real-time):** Giảm thời gian trễ từ lúc lỗi xuất hiện đến lúc team kỹ thuật nhận được thông tin xuống còn 0 giây.
- **Đa kênh đồng bộ (Omnichannel):** Đảm bảo thông tin quan trọng tiếp cận đúng người qua Slack, Google Chat và Gmail cá nhân của quản lý.
- **Cá nhân hóa nội dung:** Tự động build HTML email đẹp mắt kèm theo link trực tiếp dẫn tới ticket Jira để xử lý ngay lập tức.
- **Vận hành tự động 24/7:** Không bỏ sót bất kỳ sự cố khẩn cấp nào kể cả ngoài giờ làm việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và quyền kết nối (Credentials) sau:
- **Jira Software Cloud Account** (để cấu hình Webhook và Trigger).
- **Slack Account** (Workspace có quyền cài đặt app/bot để gửi tin nhắn).
- **Google Chat** (Service Account hoặc Webhook để gửi card thông báo).
- **Gmail Account** (Xác thực OAuth2 để gửi email báo cáo tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON rồi paste trực tiếp vào màn hình n8n Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lần lượt các node cốt lõi sau:

- **Node `ON JIRA ISSUE CREATED` (Jira Trigger):** 
  - Kết nối tài khoản Jira Cloud của công ty.
  - Thiết lập điều kiện lọc (chọn Project Key và chỉ định sự kiện khi có Issue được tạo với Priority = High).
- **Node `CONFIGURATION JIRA DOMAIN + Recipients` (Set):**
  - Điền các biến cấu hình quan trọng vào đây:
    - `JIRA_PROJECT_KEY`: Ví dụ `PROJ`
    - `JIRA_DOMAIN`: Ví dụ `my-company.atlassian.net`
    - `emailTo`: Địa chỉ email của quản lý hoặc team trưởng nhận cảnh báo.
- **Node `BUILD HTML` (Code):** Node này dùng đoạn mã JS để đóng gói thông tin ticket thành một cấu trúc HTML sạch sẽ, sẵn sàng đổ vào nội dung email. (Có thể giữ nguyên nếu không muốn tùy biến giao diện email).
- **Node `SEND SLACK CARD` & `SEND GOOGLE CHAT CARD` & `SEND EMAIL`:**
  - Chọn đúng Credentials đã chuẩn bị ở phần yêu cầu (Slack OAuth2, Google Chat Service Account, Gmail OAuth2).
  - Map các trường dữ liệu từ Jira Trigger sang nội dung tin nhắn (Tiêu đề lỗi, Người tạo, Mô tả, Link Jira...).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và tạo thử một ticket High Priority trên Jira để test xem Slack, Google Chat và Gmail có nhận được thông báo không nhé.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể bổ sung thêm node Telegram hoặc Microsoft Teams nếu công ty các sếp sử dụng các nền tảng chat này.
- **Lưu log vào Google Sheets:** Nối thêm một node Google Sheets để lưu lại lịch sử các sự cố High Priority nhằm phục vụ việc họp kiểm điểm hàng tuần (Weekly Review).
- **Tự động gán người xử lý (Assignee):** Tích hợp thêm bước tự động phân công task cho DevOps hoặc Leader trực tuần dựa trên lịch trực.

### 📌 Kết luận
Việc kiểm soát các sự cố ưu tiên cao trên Jira chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy cài đặt ngay workflow này để nâng cao tốc độ xử lý sự cố của doanh nghiệp, giúp khách hàng luôn hài lòng và sếp thì yên tâm tuyệt đối!