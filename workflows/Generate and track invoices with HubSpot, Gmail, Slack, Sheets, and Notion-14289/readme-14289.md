---
title: "🚀 Tự động tạo & theo dõi hoá đơn với HubSpot, Gmail, Slack, Sheets & Notion"
description: "Workflow n8n tự động tạo hoá đơn PDF khi Deal trong HubSpot chuyển sang Closed Won, lưu vào Google Sheets & Notion, gửi email cho khách và nhắc nhở thanh toán."
slug: "tu-dong-hoa-hoa-don-hubspot-gmail-slack-sheets-notion"
tags: [n8n, automation, no-code, invoice, hubspot, gmail, slack, notion, google-sheets]
keywords: [n8n workflow, tự động hóa hoá đơn, hubspot integration, gmail invoice, slack notification, notion database, google sheets]
---

# 🚀 Tự động tạo & theo dõi hoá đơn với HubSpot, Gmail, Slack, Sheets & Notion

Doanh nghiệp thường phải **tạo hoá đơn thủ công**, sao chép dữ liệu từ HubSpot sang Google Sheets, đính kèm PDF, gửi email và cuối cùng mới theo dõi việc thanh toán.  
Quá trình này tốn thời gian, dễ sai sót và khiến đội ngũ bán hàng mất tập trung vào việc chốt deal.

**Workflow này** giải quyết toàn bộ chuỗi công việc trên **100 % không cần viết code**:
- Khi một Deal trong HubSpot chuyển sang **Closed Won**, hệ thống tự động lấy thông tin Deal & Contact.  
- Tạo hoá đơn dạng HTML, chuyển thành PDF, lưu vào Google Sheets & Notion.  
- Gửi PDF qua Gmail, đồng thời thông báo trên Slack.  
- Theo dõi trạng thái thanh toán, tự động nhắc nhở và escalade nếu quá hạn.  

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút xuống còn vài giây mỗi hoá đơn.  
- **Độ chính xác 100 %**: Dữ liệu đồng bộ trực tiếp từ HubSpot, không còn nhập tay.  
- **Nhắc nhở tự động**: Không còn lo khách chưa thanh toán, hệ thống gửi reminder và escalade.  
- **Báo cáo liên tục**: Tất cả hoá đơn được ghi lại trong Google Sheets & Notion, dễ dàng truy xuất.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **HubSpot**: API Key hoặc OAuth token, quyền truy cập Deals & Contacts.  
- **HTML2PDF API** (hoặc bất kỳ dịch vụ chuyển HTML → PDF nào): API Key.  
- **Google Sheets**: Tài khoản Google, ID Spreadsheet và quyền chỉnh sửa.  
- **Notion**: Integration token và ID Database để lưu hoá đơn.  
- **Gmail**: Tài khoản Gmail được kết nối với n8n.  
- **Slack**: Token Bot và kênh (hoặc webhook) để nhận thông báo.  
- **n8n**: Đã cài đặt và có quyền tạo/đọc credentials cho các dịch vụ trên.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ link gốc: https://n8n.io/workflows/14289).  
2. Vào n8n → **Workflows** → **Import** → Chọn file JSON hoặc **Copy/Paste** nội dung JSON vào ô import.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là danh sách các node quan trọng và hướng dẫn cấu hình chi tiết:

| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| 🎯 **HubSpot - Deal Trigger** | Kích hoạt khi Deal thay đổi stage. | Chọn **HubSpot credentials**, **Object = Deal**, **Trigger on stage change**, **Stage ID = Closed Won** (cập nhật ID thực tế). |
| 🔀 **IF - Is Deal Closed Won?** | Kiểm tra stage của Deal. | Điều kiện: `{{$json["properties"]["dealstage"]}}` **equals** `<Closed Won stage ID>`. |
| 🏷️ **HTTP - Get Deal Details** | Lấy chi tiết Deal (giá trị, ngày, v.v.). | URL: `https://api.hubapi.com/crm/v3/objects/deals/{{ $json["id"] }}?properties=...` <br> Header: `Authorization: Bearer <HubSpot API Key>` (sử dụng **httpHeaderAuth**). |
| 🔗 **HTTP - Get Deal Associations** | Lấy danh sách Contact liên quan. | URL: `https://api.hubapi.com/crm/v3/objects/deals/{{ $json["id"] }}/associations/contact` <br> Header tương tự. |
| ⚙️ **Code - Extract Contact ID** | Trích xuất Contact ID từ kết quả associations. | Không cần thay đổi, chỉ đảm bảo `return { contactId: ... }`. |
| 👤 **HTTP - Get Contact Details** | Lấy thông tin Contact (email, tên). | URL: `https://api.hubapi.com/crm/v3/objects/contacts/{{ $json["contactId"] }}?properties=email,firstname,lastname` |
| 📄 **Code - Build Invoice + HTML** | Tạo dữ liệu hoá đơn và HTML template. | **Tuỳ chỉnh** phần HTML nếu muốn thay đổi logo, màu sắc, hoặc thêm trường tùy chỉnh. |
| 🖨️ **HTTP - Generate PDF** | Chuyển HTML → PDF. | URL: endpoint của dịch vụ HTML2PDF, body: `{ "html": "<HTML string>", "options": {...} }` <br> Header: `x-api-key: <HTML2PDF API Key>`. |
| 📊 **Google Sheets - Log Invoice** | Ghi dữ liệu hoá đơn vào Sheet. | Chọn **Google Sheets credentials**, **Spreadsheet ID**, **Sheet Name**, **Operation = Append**, map các trường (Invoice No, Amount, Client, Date, Link PDF). |
| 📓 **Notion - Create Invoice Record** | Tạo bản ghi hoá đơn trong Notion DB. | Chọn **Notion credentials**, **Database ID**, **Operation = Create**, map các thuộc tính (Tên, Số tiền, Trạng thái, Link PDF). |
| 📧 **Gmail - Send Invoice Email** | Gửi PDF cho khách hàng. | Chọn **Gmail credentials**, **To = {{$json["contact"]["email"]}}**, **Subject**, **Body** (có thể dùng HTML), **Attachments** = PDF URL hoặc binary. |
| 💬 **Slack - Invoice Sent Alert** | Thông báo nội bộ khi hoá đơn được gửi. | Chọn **Slack credentials**, **Channel**, **Message**: “✅ Hoá đơn #{{invoiceNo}} đã gửi cho {{contactName}}”. |
| ⏳ **Wait - 7 Day Payment Window** | Đợi 7 ngày để khách thanh toán. | Thời gian **7 days** (có thể thay đổi). |
| 🔍 **HTTP - Recheck Deal Stage** | Kiểm tra lại stage của Deal sau 7 ngày. | URL tương tự node “Get Deal Details”. |
| 🔀 **IF - Payment Received?** | Kiểm tra xem Deal đã chuyển sang stage thanh toán chưa. | Điều kiện: `{{$json["properties"]["dealstage"]}}` **equals** `<Payment Received stage ID>`. |
| ✅ **Slack - Payment Confirmed** | Thông báo thanh toán thành công. | Channel nội bộ, nội dung “💰 Thanh toán cho hoá đơn #{{invoiceNo}} đã được xác nhận”. |
| 📧 **Gmail - Follow-up Email #1** | Nhắc nhở thanh toán lần 1 (nếu chưa nhận). | Đặt **To**, **Subject**, **Body** (có link PDF). |
| ⏳ **Wait - 5 More Days** | Đợi thêm 5 ngày trước lần nhắc cuối. | Thời gian **5 days**. |
| 🔍 **HTTP - Final Payment Check** | Kiểm tra lần cuối trạng thái thanh toán. | Gọi API HubSpot giống node “Recheck Deal Stage”. |
| 🔀 **IF - Still Unpaid? (Escalate)** | Nếu vẫn chưa thanh toán → escalade. | Điều kiện: stage **