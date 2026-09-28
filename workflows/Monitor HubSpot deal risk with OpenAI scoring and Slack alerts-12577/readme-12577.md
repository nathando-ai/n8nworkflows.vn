---
title: "🚀 Tự động giám sát rủi ro deal HubSpot bằng AI chấm điểm và cảnh báo Slack"
description: "Giải pháp tự động hóa giúp đội ngũ sales phát hiện sớm các deal có nguy cơ thất bại trên HubSpot bằng OpenAI, lưu log Google Sheets và gửi cảnh báo tức thì qua Slack."
slug: "giam-sat-rui-ro-deal-hubspot-openai-slack"
tags: [n8n, automation, no-code, hubspot, openai, slack, crm]
keywords: [n8n workflow, tự động hóa hubspot, chấm điểm deal openai, cảnh báo slack crm, quản lý rủi ro sales]
keywords: [n8n workflow, tự động hóa, giám sát deal hubspot, openai scoring, slack alerts]
---

# 🚀 Tự động giám sát rủi ro deal HubSpot bằng AI chấm điểm và cảnh báo Slack

Các sếp có bao giờ đau đầu vì các deal lớn trên CRM cứ "lặn mất tăm" mà sales quên không cập nhật, hay đến phút chót mới phát hiện khách hàng quay lưng? Việc kiểm tra thủ công hàng trăm deal mỗi ngày là ác mộng tốn thời gian và rất dễ bỏ sót các dấu hiệu cảnh báo sớm.

Đừng lo, workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Hệ thống sẽ tự động quét danh sách deal trên HubSpot, sử dụng AI thông minh từ OpenAI để phân tích và chấm điểm rủi ro, lưu lịch sử vào Google Sheets, đồng thời bắn cảnh báo ngay lập tức lên Slack để đội ngũ sales kịp thời can thiệp. Toàn bộ quy trình diễn ra hoàn toàn tự động 24/7 mà không cần tốn một phút thao tác thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện rủi ro tức thì:** AI phân tích sâu dữ liệu deal và đưa ra điểm số rủi ro chính xác giúp team sales đánhúng trọng tâm.
- **Không bỏ sót deal quan trọng:** Tự động hóa lịch trình quét dữ liệu định kỳ, cảnh báo trực diện qua kênh Slack của team.
- **Quản lý dữ liệu minh bạch:** Lưu trữ toàn bộ lịch sử phân tích rủi ro vào Google Sheets để dễ dàng báo cáo và đánh giá lại.
- **Tối ưu hóa thời gian:** Giải phóng đội ngũ quản lý khỏi việc phải đi kiểm tra từng deal thủ công trên CRM.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản HubSpot** (với quyền truy cập API/CRM Deals).
- **Tài khoản OpenAI API** (để sử dụng Langchain Agent / Chat Model chấm điểm deal).
- **Không gian làm việc Slack** (để nhận tin nhắn cảnh báo).
- **Google Sheets** (để lưu trữ log dữ liệu deal).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cung cấp hoặc copy toàn bộ mã JSON, sau đó paste trực tiếp vào giao diện n8n Editor của mình thông qua tính năng **New Workflow** -> **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần cấu hình chính xác các kết nối (credentials) và tham số sau:
- **Schedule Trigger:** Thiết lập thời gian chạy định kỳ (ví dụ: mỗi ngày một lần vào sáng sớm) để hệ thống tự động quét deal.
- **HubSpot Node:** Kết nối tài khoản HubSpot của doanh nghiệp, cấu hình lấy danh sách các deal đang mở (Open Deals) cùng thông tin chi tiết liên quan.
- **OpenAI / Langchain Agent & LM Chat OpenAI:** Nhập OpenAI API Key, thiết lập Prompt chi tiết để AI hiểu rõ tiêu chí đánh giá rủi ro (ví dụ: thời gian dừng ở một stage quá lâu, giá trị deal lớn, thiếu hoạt động tương tác...).
- **Google Sheets Node:** Chọn đúng file Spreadsheet và Sheet Name dùng để lưu log kết quả phân tích điểm rủi ro.
- **Slack Node:** Kết nối với Workspace Slack và chọn Channel nhận thông báo cảnh báo khi phát hiện deal có rủi ro cao.
- **If / Code Nodes:** Tinh chỉnh điều kiện lọc (ví dụ: chỉ gửi cảnh báo Slack nếu điểm rủi ro vượt ngưỡng cho phép).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với dữ liệu mẫu để kiểm tra từng node từ HubSpot -> OpenAI -> Google Sheets -> Slack xem có lỗi phát sinh không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chính thức hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Email/Telegram:** Ngoài Slack, các sếp có thể gắn thêm node Telegram hoặc Gmail để gửi trực tiếp cảnh báo đến người phụ trách deal (Sales Owner) cụ thể.
- **Lưu lịch sử chat/ghi chú:** Cập nhật ngược lại kết quả đánh giá rủi ro của AI vào thẳng phần ghi chú (Notes) của deal trên HubSpot để sales dễ theo dõi.
- **Dashboard quản trị:** Dùng Google Sheets kết hợp với Looker Studio để vẽ biểu đồ theo dõi xu hướng rủi ro các deal theo tuần/tháng.

### 📌 Kết luận
Việc kiểm soát rủi ro trong phễu bán hàng chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy cài đặt ngay workflow này để bảo vệ doanh thu của doanh nghiệp và giúp đội ngũ sales chủ động hơn trong mọi tình huống!