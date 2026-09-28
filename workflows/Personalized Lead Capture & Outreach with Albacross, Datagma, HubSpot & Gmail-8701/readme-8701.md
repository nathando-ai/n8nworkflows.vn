---
title: "🚀 Tự động Thu thập Lead & Gửi Email Cá nhân hoá với Albacross, Datagma, HubSpot & Gmail"
description: "Workflow n8n giúp tự động thu thập khách hàng tiềm năng từ Albacross, làm giàu dữ liệu qua Datagma, đồng bộ vào HubSpot và gửi email cá nhân hoá qua Gmail – hoàn toàn không cần code."
slug: "tự-động-thu-đập-lead-gửi-email-cá-nhân-hoá"
tags: [n8n, automation, no-code, albacross, datagma, hubspot, gmail, lead-generation]
keywords: [n8n workflow, tự động hóa, lead capture, email outreach, CRM integration]
---

# 🚀 Tự động Thu thập Lead & Gửi Email Cá nhân hoá với Albacross, Datagma, HubSpot & Gmail

Bạn đang mất hàng giờ mỗi ngày để theo dõi khách hàng tiềm năng, làm giàu dữ liệu và gửi email? Workflow này sẽ biến quy trình thủ công thành một chuỗi tự động 100% – giảm thiểu sai sót, tăng tốc độ phản hồi và nâng cao chất lượng lead.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và làm giàu dữ liệu, không cần thao tác thủ công.
- **Chính xác & nhất quán**: Dữ liệu được lấy từ API chính thức, đồng bộ ngay vào HubSpot.
- **Cá nhân hoá**: Email được tạo động dựa trên thông tin thực tế của khách hàng.
- **Hoạt động liên tục**: Workflow chạy theo lịch, không phụ thuộc vào giờ làm việc.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | API Key / Credential | Ghi chú |
|---------|----------------------|---------|
| **Albacross** | `ALBACROSS_API_KEY` | Đăng ký tại <https://www.albacross.com/> |
| **Datagma** | `DATAGMA_API_KEY` | Đăng ký tại <https://datagma.io/> |
| **HubSpot** | `HUBSPOT_APP_TOKEN` | Tạo App Token trong HubSpot → Settings → Integrations → API Key |
| **Gmail** | `GMAIL_OAUTH2` | Cài đặt OAuth2 trong Gmail → Settings → Apps & Services |
| **n8n** | N/A | Đảm bảo n8n đang chạy và có quyền truy cập các node trên |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ <https://n8n.io/workflows/8701> hoặc copy toàn bộ JSON.
2. Mở **n8n Editor**, chọn **Import** → **Import from file** hoặc **Paste JSON**.
3. Nhấn **Import** để tải workflow vào workspace.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Tham số cần cấu hình | Credential | Ghi chú |
|------|----------|----------------------|------------|---------|
| 1 | ⏰ **Schedule Trigger** | `Cron Expression` (ví dụ: `0 * * * *` để chạy hàng giờ) | N/A | Đặt lịch phù hợp với khối lượng lead |
| 2 | 🌐 **Albacross Website Visitor** | `Endpoint: https://api.albacross.com/v1/visitors`<br>`Headers: Authorization: Bearer <API_KEY>` | `ALBACROSS_API_KEY` | Trả về danh sách visitor, lấy `company`, `domain`, `industry`, `employees` |
| 3 | 🔍 **Enrich Lead Data** | `Endpoint: https://api.datagma.io/v1/lookup`<br>`Params: domain=<domain>`<br>`Headers: Authorization: Bearer <API_KEY>` | `DATAGMA_API_KEY` | Trả về `fullName`, `title`, `email`, `phone`, `linkedin` |
| 4 | 📇 **Create/Update HubSpot Contact** | `Properties: email, firstname, lastname, company, jobtitle, phone, linkedin, leadStatus=NEW` | `hubspotAppToken` | Đặt `Object Type: Contact` |
| 5 | ✍️ **Generate Personalized Message** | **Code**: Sử dụng `{{$json["fullName"]}}`, `{{$json["company"]}}`, `{{$json["industry"]}}` để tạo nội dung. | N/A | Đảm bảo node trả về `message` trong `return { message: ... }` |
| 6 | 📧 **Send Personalized Email** | `To: {{$json["email"]}}`<br>`Subject: Hi {{fullName}}, let’s talk about {{industry}}`<br>`Body: {{$node["Generate Personalized Message"].json.message}}` | `gmailOAuth2` | Kiểm tra quyền gửi email |
| 7 | 📝 **Log Email Activity in HubSpot** | `Engagement Type: EMAIL`<br>`Properties: hs_email_subject, hs_email_body, hs_email_to` | `hubspotAppToken` | Đảm bảo `resource: engagement` đã được khai báo |

> **Tip**: Trong node **Code**, bạn có thể viết JavaScript như sau:
> ```js
> const { fullName, company, industry } = $json;
> return {
>   message: `Hi ${fullName},\n\nI noticed your company ${company} operates in the ${industry} sector. I believe our solution can help you achieve X. Let’s schedule a quick call!`,
> };
> ```

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm **Execute Workflow**).
2. Kiểm tra logs: Đảm bảo không có lỗi và email đã được gửi.
3. Khi mọi thứ ổn, bật **Active** (đánh dấu nút **Active**).
4. Theo dõi HubSpot → **Engagements** để xác nhận email đã được ghi lại.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi thông báo khi email được gửi thành công.
- **Lưu log**: Sử dụng node **Google Sheets** hoặc **MongoDB** để lưu lại lịch sử email và phản hồi.
- **Báo cáo định kỳ**: Thêm node **Schedule Trigger** khác để gửi báo cáo hàng ngày/tuần về số lead mới, email mở, click.
- **AI Personalization**: Thay vì code đơn giản, dùng **OpenAI** node để tạo nội dung email dựa trên prompt tùy chỉnh.

## 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các doanh nghiệp muốn tự động hóa quy trình thu thập lead, làm giàu dữ liệu và gửi email cá nhân hoá mà không cần viết code. Hãy thử ngay, điều chỉnh lịch và tham số phù hợp với quy mô của bạn, và cảm nhận sự khác biệt trong tốc độ và chất lượng lead!