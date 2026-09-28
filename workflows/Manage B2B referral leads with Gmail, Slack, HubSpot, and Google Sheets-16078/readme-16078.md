---
title: "🚀 Tự động hóa toàn bộ quy trình quản lý B2B Referral với n8n, Gmail, Slack, HubSpot và Google Sheets"
description: "Xây dựng hệ thống tự động hóa giới thiệu khách hàng (B2B Referral) từ A-Z: xác thực form, gửi email cảm ơn, thông báo Slack, đồng bộ HubSpot CRM, chuỗi email nuôi dưỡng và ghi log Google Sheets."
slug: "quan-ly-b2b-referral-tu-dong-voi-n8n-hubspot-slack"
tags: [n8n, automation, no-code, hubspot, crm, lead-generation]
keywords: [n8n workflow, b2b referral automation, hubspot crm n8n, tu dong hoa lead, quan ly gioi thiệu khách hàng]
---

# 🚀 Tự động hóa toàn bộ quy trình quản lý B2B Referral với n8n, Gmail, Slack, HubSpot và Google Sheets

Các sếp có đang gặp tình trạng chương trình giới thiệu khách hàng (Referral Program) bị "rơi rớt" dữ liệu, quên gửi email cảm ơn người giới thiệu, sales tiếp nhận chậm trễ hoặc quên mất lịch follow-up lead tiềm năng sau vài ngày? Làm thủ công những việc này vừa tốn thời gian, vừa thiếu chuyên nghiệp.

Đừng lo, workflow n8n được thiết kế bởi chuyên gia **Avkash Kakdiya** sẽ giúp các sếp giải quyết triệt để bài toán này một cách tự động 100%, không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% từ đầu đến cuối**: Từ lúc khách điền form giới thiệu đến khi tạo deal trên CRM và gửi email chăm sóc.
- **Trải nghiệm chuyên nghiệp**: Người giới thiệu nhận được email cảm ơn tức thì; lead mới nhận được email chào mừng cá nhân hóa có nhắc tên người giới thiệu.
- **Tăng tốc độ phản hồi của Sales**: Đội ngũ sales nhận thông báo real-time qua Slack ngay khi có referral mới.
- **Nuôi dưỡng lead thông minh**: Tự động kiểm tra phản hồi sau 3 ngày và gửi email follow-up nếu khách chưa trả lời, tránh bỏ sót cơ hội chốt sale.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản kết nối sau:
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Tài khoản Gmail** (để gửi email cảm ơn, nurture email và check reply).
- **Workspace Slack** (để tạo kênh nhận thông báo sales và error log).
- **HubSpot CRM** (để check trùng lặp, tạo Contact và Deal).
- **Google Sheets** (để lưu trữ dữ liệu báo cáo tracking).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này (hoặc tải file từ n8n template Hub) và dán trực tiếp vào n8n Editor của mình. Workflow gồm 19 nodes được sắp xếp logic theo từng giai đoạn rõ ràng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Referral Form Webhook**: Lấy Webhook URL để kết nối với form trên website của các sếp (Webflow, WordPress, Tally, Typeform...).
- **Gmail Nodes (`Thank You Email to Referrer`, `Send Nurture Email to Lead`, `Check for Lead Reply`, `Send Follow-Up Email`)**: Kết nối tài khoản Gmail cá nhân hoặc Google Workspace để gửi và quét email.
- **Slack Nodes (`Slack Alert — Sales Team`, `Slack Alert — Error Channel`)**: Chọn đúng credentials của Slack workspace và cấu hình tên kênh nhận thông báo (ví dụ: `#referrals` và `#errors`).
- **HubSpot Nodes (`Check Lead in HubSpot`, `Create HubSpot Contact`, `Create HubSpot Deal`)**: Xác thực tài khoản HubSpot qua API/OAuth2 và map các trường dữ liệu (Name, Email, Phone, Company) cho khớp với CRM của công ty.
- **Google Sheets Node (`Log Referral to Google Sheet`)**: Trỏ tới file Google Sheet quản lý referral của các sếp, chọn đúng Sheet Name và map các cột dữ liệu tương ứng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách gửi một dữ liệu mẫu qua Webhook.
- Kiểm tra xem email đã gửi đi, dữ liệu đã vào HubSpot và Google Sheets chưa.
- Bật công tắc **Active** để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo**: Ngoài Slack, các sếp có thể nhân bản node thông báo sang Telegram để đội ngũ sales nhận tin nhắn trên điện thoại nhanh hơn.
- **Thêm AI (OpenAI/Anthropic Node)**: Dùng AI để phân tích nội dung lời nhắn giới thiệu (Referral Notes) và tự động chấm điểm chất lượng lead (Lead Scoring) trước khi đưa vào HubSpot.
- **Báo cáo định kỳ**: Kết hợp thêm một trigger Cron (Schedule) chạy vào thứ Hai hàng tuần để tổng hợp số liệu từ Google Sheets và gửi báo cáo tổng kết qua email cho Ban Giám Đốc.

### 📌 Kết luận
Hệ thống B2B Referral tự động này không chỉ giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn đảm bảo không một khách hàng tiềm năng nào bị bỏ quên. Hãy cài đặt ngay hôm nay để tối ưu hóa phễu bán hàng của các sếp nhé!