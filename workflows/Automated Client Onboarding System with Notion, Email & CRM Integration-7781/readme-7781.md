---
title: "🚀 Hệ thống Onboarding Khách hàng Tự động với Notion, Email & CRM"
description: "Giải pháp tự động hoá quy trình tiếp nhận khách hàng, tạo hồ sơ trong Notion, gửi email chào mừng và đồng bộ vào CRM chỉ với một workflow n8n."
slug: "onboarding-khach-hang-tu-dong"
tags: [n8n, automation, no-code, crm, notion, email]
keywords: [n8n workflow, tự động hóa, onboarding khách hàng, CRM, Notion]
---

# 🚀 Hệ thống Onboarding Khách hàng Tự động với Notion, Email & CRM

Bạn đang mất hàng giờ mỗi ngày để xử lý thủ công dữ liệu khách hàng mới, tạo hồ sơ trong Notion, gửi email chào mừng và đồng bộ vào CRM?  
Workflow này sẽ **đưa mọi thao tác vào một chuỗi tự động 100% không cần code**, giúp các sếp tiết kiệm thời gian, giảm sai sót và tăng tính cá nhân hoá trong giao tiếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ xử lý thủ công xuống dưới 5 phút cho mỗi khách hàng mới.  
- **Chính xác & nhất quán**: Tất cả dữ liệu được đồng bộ vào Notion, CRM và lịch một cách tự động, tránh lỗi nhập liệu.  
- **Tự động hoá toàn diện**: Gửi email chào mừng, thông báo Telegram, tạo dòng trong Airtable và đặt lịch hold ngay lập tức.  
- **Dễ dàng mở rộng**: Thêm Slack, Telegram, Zapier, hoặc lưu trữ log chỉ với vài dòng cấu hình.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ | Credential | Mô tả |
|---------|------------|-------|
| **Notion** | `Notion API Key` | Kết nối tới database “Clients” (định danh ID). |
| **HubSpot** | `HubSpot API Key` | Tạo contact mới trong HubSpot. |
| **Airtable** | `Airtable API Key` + `Base ID` | Tạo dòng mới trong bảng “Clients”. |
| **Telegram** | `Telegram Bot Token` + `Chat ID` | Gửi thông báo tới owner. |
| **Email** | `SMTP Host`, `Port`, `User`, `Password` | Gửi email chào mừng. |
| **Google Calendar** | `OAuth2 Credentials` | Tạo sự kiện hold. |
| **Webhook** | - | Định nghĩa endpoint cho intake và opt‑in. |
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/7781> hoặc copy nội dung JSON.  
2. Mở n8n Editor → **Import** → **Import from JSON** → dán JSON.  
3. Kiểm tra lại tên workflow và lưu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên thực tế | Cấu hình cần thiết |
|------|-------------|---------------------|
| **Client Intake Webhook** | `Client Intake Webhook` | Đặt URL endpoint, chọn `HTTP Method` (POST). |
| **Set: User Config** | `Set: User Config` | Định nghĩa các biến mặc định (ví dụ: `enableTelegram`, `enableAirtable`, `enableHubSpot`, `enableCalendar`). |
| **Function: Simulate Intake** | `Function: Simulate Intake` | Chỉ dùng khi thử nghiệm; bỏ qua khi dùng webhook thực. |
| **Function: Map Intake** | `Function: Map Intake` | Map dữ liệu từ webhook sang cấu trúc Notion. |
| **Function: Score Lead** | `Function: Score Lead` | Tính điểm lead (đánh giá mức độ quan tâm). |
| **Notion: Create Client** | `Notion: Create Client` | Chọn `Database ID` của “Clients”. |
| **Function: Build Welcome Email** | `Function: Build Welcome Email` | Tạo nội dung email dựa trên dữ liệu khách hàng. |
| **Email: Send Welcome** | `Email: Send Welcome` | Chọn credential SMTP, điền `To`, `Subject`, `Body`. |
| **If: Telegram Enabled?** | `If: Telegram Enabled?` | Kiểm tra biến `enableTelegram`. |
| **Telegram: Notify Owner** | `Telegram: Notify Owner` | Chọn credential Telegram, điền `Chat ID`. |
| **If: Airtable Enabled?** | `If: Airtable Enabled?` | Kiểm tra biến `enableAirtable`. |
| **Airtable: Create Row** | `Airtable: Create Row` | Chọn `Base ID`, `Table ID`. |
| **If: HubSpot Enabled?** | `If: HubSpot Enabled?` | Kiểm tra biến `enableHubSpot`. |
| **HubSpot: Create Contact** | `HubSpot: Create Contact` | Chọn credential HubSpot, map trường. |
| **If: Calendar Hold Enabled?** | `If: Calendar Hold Enabled?` | Kiểm tra biến `enableCalendar`. |
| **Function: Hold Times** | `Function: Hold Times` | Tính thời gian hold (ví dụ: 30 phút). |
| **Google Calendar: Create Hold** | `Google Calendar: Create Hold` | Chọn credential Google Calendar, map tiêu đề, thời gian. |
| **Opt-in Confirm Webhook** | `Opt-in Confirm Webhook` | Endpoint nhận xác nhận opt‑in. |
| **Function: Parse Optin** | `Function: Parse Optin` | Phân tích payload opt‑in. |
| **Notion: Find by Token** | `Notion: Find by Token` | Tìm client theo token trong Notion. |
| **Function: Pick Page** | `Function: Pick Page` | Chọn trang Notion phù hợp. |
| **Notion: Set Consent + Status** | `Notion: Set Consent + Status` | Cập nhật trạng thái & đồng ý. |
| **On Error → Email Owner** | `On Error → Email Owner` | Gửi email cảnh báo khi workflow gặp lỗi. |

> **Lưu ý**: Mỗi node “If” cần cấu hình đúng điều kiện (`enableX`) và chọn đúng credential. Nếu không bật tính năng, node “If” sẽ bỏ qua.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm “Execute Workflow”). Kiểm tra logs, xác nhận mọi bước thực thi đúng.  
2. **Bật Active**: Đánh dấu workflow là “Active” để tự động chạy khi webhook nhận dữ liệu.  
3. **Kiểm tra**: Gửi request tới endpoint `Client Intake Webhook` (có thể dùng Postman) và theo dõi các bước: tạo Notion, gửi email, thông báo Telegram, v.v.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack**: Thêm node `Slack: Send Message` trong “If: Slack Enabled?” để nhận thông báo nhanh hơn.  
- **Lưu log vào Google Sheets**: Sử dụng node `Google Sheets: Append Row` để ghi lại lịch sử onboarding.  
- **Báo cáo định kỳ**: Dùng `Cron` node để gửi báo cáo hàng tuần về số lượng khách hàng mới, điểm lead trung bình.  
- **Tự động gửi follow‑up**: Thêm node `Delay` + `Email: Send Follow‑up` để nhắc nhở khách hàng sau 3 ngày.  

### 📌 Kết luận
Workflow “Automated Client Onboarding System with Notion, Email & CRM Integration” là công cụ **đơn giản nhưng mạnh mẽ** giúp các sếp tập trung vào chiến lược kinh doanh thay vì quản lý dữ liệu.  
Hãy **tải về, cấu hình credential và bật workflow ngay hôm nay** – bạn sẽ thấy quy trình onboarding trở nên mượt mà, chính xác và tiết kiệm thời gian hơn bao giờ hết.  

Chúc các sếp thành công và “đưa khách hàng vào vòng quay” nhanh hơn!