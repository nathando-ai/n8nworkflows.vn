---
title: "🚀 Tự động hóa quy trình chăm sóc Deal HubSpot với Gmail, Slack và Google Sheets"
description: "Xây dựng chuỗi follow-up deal tự động 100% từ HubSpot, tích hợp Gmail gửi email cá nhân hóa, kiểm tra phản hồi, thông báo qua Slack và đồng bộ Google Sheets."
slug: "tu-dong-hoa-cham-soc-hubspot-deal-gmail-slack-google-sheets"
tags: [n8n, automation, hubspot, gmail, slack, crm]
keywords: [n8n workflow, hubspot automation, chăm sóc khách hàng tự động, tich hop gmail hubspot, slack notification n8n]
---

# 🚀 Tự động hóa quy trình chăm sóc Deal HubSpot với Gmail, Slack và Google Sheets

Các sếp có bao giờ gặp tình trạng deal mới vừa đổ về HubSpot nhưng đội ngũ sales lại bận rộn quên mất việc gửi email chào mừng (intro email), dẫn đến việc khách hàng nguội lạnh? Hoặc việc theo dõi lịch trình gửi email follow-up thủ công cực kỳ tốn thời gian và dễ bỏ sót?

Workflow n8n này chính là giải pháp tự động hóa toàn diện giúp các sếp giải quyết triệt để vấn đề đó. Ngay khi có một deal mới được tạo trên HubSpot, hệ thống sẽ tự động xác thực thông tin, gửi chuỗi email chăm sóc theo kịch bản có sẵn, phát hiện phản hồi của khách hàng, cập nhật trạng thái CRM, bắn thông báo về Slack cho sales và ghi log chi tiết vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì:** Gửi email giới thiệu ngay lập tức khi deal vừa được tạo, tăng tỷ lệ chốt đơn.
- **Nuôi dưỡng tự động (Nurturing):** Chuỗi 3 email (Intro -> Follow-up -> Breakup email) được tự động hóa hoàn toàn với các mốc thời gian chờ chuẩn xác (2 ngày, 3 ngày).
- **Cập nhật CRM thời gian thực:** Trạng thái deal trên HubSpot tự động thay đổi từ *New* sang *Contacted*, *Meeting Booked* hoặc *Closed Lost*.
- **Báo cáo minh bạch:** Mọi hoạt động, kể cả dữ liệu lỗi hay phản hồi của khách, đều được ghi log tự động vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **HubSpot CRM** (đã cấp quyền OAuth2).
- Tài khoản **Gmail** để gửi email tự động.
- Workspace **Slack** và một channel chuyên nhận thông báo lead (ví dụ: `#sales-alerts`).
- **Google Sheets** đã tạo sẵn một bảng tính dùng để log dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các credentials và tham số quan trọng sau cho từng node:

- **HubSpot Trigger – New Deal & Get Deal Details / Get Contact Details:** Kết nối tài khoản HubSpot của các sếp qua OAuth2. Node Trigger sẽ lắng nghe sự kiện khi có deal mới phát sinh.
- **Valid Contact & Email? (Node IF):** Kiểm tra xem deal có gắn kèm contact và email hợp lệ hay không. Nếu không, hệ thống sẽ chuyển hướng sang node **Log Invalid – Skip**.
- **Send Intro Email & Send Follow-Up Email & Send Breakup Email (Node Gmail):** Chọn tài khoản Gmail cá nhân hoặc email doanh nghiệp để gửi chuỗi email chăm sóc. Cấu hình tiêu đề và nội dung template phù hợp với sản phẩm của công ty.
- **Wait 2 Days & Wait 3 More Days (Node Wait):** Thiết lập khoảng thời gian chờ giữa các lần gửi email (mặc định là chờ 2 ngày cho follow-up đầu tiên và thêm 3 ngày trước khi kiểm tra phản hồi).
- **Slack Alert – Contact Replied (Node Slack):** Kết nối tài khoản Slack, chọn Channel nhận thông báo (ví dụ: `#sales-leads`) để nhân viên sales kịp thời nắm bắt khi khách hàng phản hồi email.
- **Log Invalid – Skip, Log to Sheet – Replied, Log to Sheet – No Reply (Node Google Sheets):** Kết nối tài khoản Google Drive/Sheets và trỏ tới file Google Sheet chuẩn bị sẵn với các cột: `Date`, `Deal Name`, `Contact Name`, `Contact Email`, `Sequence Status`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với một deal mẫu trên HubSpot để kiểm tra toàn bộ luồng chạy từ Gmail, Slack đến Google Sheets.
- Sau khi test thành công, gạt công tắc sang trạng thái **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI (OpenAI/Anthropic):** Thay vì dùng email template cứng nhắc, các sếp có thể chèn thêm một node LLM để tự động viết nội dung email chào mừng dựa trên thông tin ngành nghề và quy mô công ty của khách hàng trên HubSpot.
- **Mở rộng kênh thông báo:** Ngoài Slack, có thể kết nối thêm Telegram Bot để gửi thông báo trực tiếp về điện thoại cá nhân cho sales.
- **Báo cáo định kỳ:** Sử dụng thêm một cron trigger để tổng hợp dữ liệu từ Google Sheets gửi báo cáo tuần về kết quả chăm sóc lead qua email.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ mạnh mẽ giúp đội ngũ sales tối ưu hóa quy trình chăm sóc lead từ HubSpot mà không cần tốn một phút thao tác thủ công nào. Hãy áp dụng ngay để tăng tốc độ phản hồi khách hàng và bứt phá doanh số trong tháng này nhé các sếp!