---
title: "🚀 Tự động hóa xử lý và leo thang yêu cầu bảo trì quá hạn với GPT-4o, Google Sheets và Slack"
description: "Xây dựng hệ thống tự động theo dõi SLA bảo trì, phân loại mức độ khẩn cấp bằng AI và tự động leo thang các yêu cầu chưa được giải quyết."
slug: "tu-dong-hoa-xu-ly-yeu-cau-bao-tri-gpt-4o-google-sheets-slack"
tags: [n8n, automation, no-code, ai, google-sheets, slack, gpt-4o]
keywords: [n8n workflow, tự động hóa bảo trì, gpt-4o ai, google sheets automation, slack alert, sla tracking]
---

# 🚀 Tự động hóa xử lý và leo thang yêu cầu bảo trì quá hạn với GPT-4o, Google Sheets và Slack

Các đội ngũ quản lý bất động sản, vận hành cơ sở vật chất hay dịch vụ kỹ thuật thường xuyên đối mặt với cơn ác mộng: Các yêu cầu bảo trì từ khách thuê hoặc nhân sự bị bỏ quên, xử lý chậm trễ dẫn đến phàn nàn và mất uy tín. Việc theo dõi thủ công bằng bảng biểu hay kiểm tra tin nhắn liên tục tốn rất nhiều thời gian mà vẫn dễ sót việc.

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: Tiếp nhận yêu cầu qua Webhook, sử dụng AI (GPT-4o) để phân loại độ khẩn cấp, lưu trữ vào Google Sheets, theo dõi thời hạn SLA, và tự động cảnh báo qua Slack hoặc Email khi có yêu cầu chưa được xử lý đúng hạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn SLA:** Theo dõi thời gian xử lý yêu cầu và tự động kích hoạt leo thang khi quá hạn mà không cần con người can thiệp.
- **Phân loại thông minh bằng AI:** GPT-4o tự động đọc nội dung yêu cầu bảo trì và đánh giá mức độ khẩn cấp (High, Medium, Low) một cách chính xác.
- **Minh bạch dữ liệu:** Mọi yêu cầu đều được ghi nhận tập trung lên Google Sheets để dễ dàng kiểm tra trạng thái (Resolved / Unresolved).
- **Cảnh báo đa kênh:** Tức tốc gửi tin nhắn cảnh báo qua Slack và Email cho quản lý đối với các ca quá hạn mức độ cao.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để sử dụng node GPT-4o phân loại độ khẩn cấp.
- **Google Sheets Account:** Tạo sẵn một trang tính (Google Sheet) để lưu log các yêu cầu bảo trì và kiểm tra trạng thái.
- **Slack Workspace:** Cài đặt Slack Integration để gửi thông báo cảnh báo.
- **Email/SMTP Service:** Tài khoản gửi email (Gmail OAuth2 hoặc SMTP) để gửi thông báo cho quản lý và báo cáo tổng hợp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau để workflow chạy mượt mà:
- **Maintenance Request Webhook**: Nhận endpoint URL để kết nối với form đặt trên website hoặc cổng thông tin khách thuê (Tenant Portal).
- **Classify Urgency with AI**: Kết nối với credential **OpenAI API** của các sếp. Viết prompt hướng dẫn GPT-4o cách phân loại mức độ khẩn cấp dựa trên mô tả yêu cầu bảo trì.
- **Log Request to Sheets** & **Check Request Status** & **Get Unresolved Requests**: Kết nối tài khoản **Google Sheets OAuth2**, chọn file Google Sheet và chỉ định Sheet Name tương ứng dùng để lưu trữ dữ liệu.
- **Wait for SLA Window**: Cấu hình khoảng thời gian chờ phù hợp với chính sách SLA của doanh nghiệp (ví dụ: chờ 4 tiếng hoặc 24 tiếng trước khi kiểm tra lại trạng thái).
- **Send Slack Alert (High)** / **Send Slack Alert (Medium)**: Chọn kênh Slack (Channel) muốn nhận tin nhắn cảnh báo khi yêu cầu bị trễ hạn.
- **Email Manager (High)** & **Send Daily Summary Email**: Cấu hình tài khoản gửi email và điền địa chỉ email của quản lý hoặc bộ phận vận hành.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request mẫu qua Webhook để test luồng chạy từ đầu đến cuối.
- Kiểm tra kết quả trên Google Sheets, Slack và Email.
- Nếu mọi thứ chạy trơn tru, hãy bật công tắc **Active** ở góc trên bên phải để workflow chính thức hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Zalo:** Thay thế hoặc bổ sung node Slack bằng node Telegram để nhận thông báo tức thời trên điện thoại cá nhân của kỹ thuật viên.
- **Tự động phân công công việc:** Kết hợp thêm logic gán trực tiếp thợ sửa chữa dựa trên khu vực hoặc loại sự cố (điện, nước, điều hòa...).
- **Báo cáo định kỳ:** Tận dụng node **Daily Summary Schedule** để gửi báo cáo tổng kết cuối ngày về các đầu việc chưa hoàn thành vào email của giám đốc vận hành.

### 📌 Kết luận
Workflow này là một "vũ khí" đắc lực giúp các đội ngũ quản lý bất động sản loại bỏ hoàn toàn tình trạng sót việc, tối ưu hóa thời gian phản hồi và nâng cao sự hài lòng của khách thuê. Hãy thiết lập ngay hôm nay để hệ thống vận hành trơn tru không cần tốn sức!