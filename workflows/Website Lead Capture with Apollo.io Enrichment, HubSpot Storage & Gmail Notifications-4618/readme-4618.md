---
title: "🚀 Tự động thu thập Lead website, làm giàu dữ liệu Apollo, lưu HubSpot & gửi Gmail thông báo"
description: "Workflow n8n nhận lead từ website, enrich bằng Apollo.io, tạo contact trên HubSpot và tự động gửi email cảm ơn + thông báo cho đội ngũ."
slug: "tu-dong-lead-capture-apollo-hubspot-gmail"
tags: [n8n, automation, no-code, sales, lead-generation, crm]
keywords: [n8n workflow, tự động hóa, lead capture, Apollo enrichment, HubSpot integration, Gmail notifications]
---

# 🚀 Tự động thu thập Lead website, làm giàu dữ liệu Apollo, lưu HubSpot & gửi Gmail thông báo

Khi các sếp phải thu thập lead từ website bằng cách copy‑paste vào bảng tính, rồi mới vào HubSpot tạo contact, rồi mới gửi email cảm ơn – **công việc tốn thời gian, dễ sai sót và mất tính cá nhân hoá**.  
Workflow này giải quyết toàn bộ chuỗi:  
1️⃣ Nhận lead ngay khi khách truy cập gửi form (Webhook).  
2️⃣ Gửi email “Cảm ơn” tự động tới khách hàng.  
3️⃣ Gọi API Apollo.io để enrich thông tin (công ty, quy mô, ngành...).  
4️⃣ Tạo contact mới trên HubSpot với dữ liệu đã enrich.  
5️⃣ Gửi email thông báo cho đội sales/kỹ thuật ngay lập tức.  

Tất cả chỉ cần **cài một lần, chạy 24/7, không viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với quy trình thủ công.  
- **Dữ liệu chuẩn xác, đầy đủ** nhờ enrichment Apollo.io.  
- **Tự động tạo contact** trong HubSpot ngay lập tức, không bỏ lỡ lead.  
- **Gửi email cảm ơn & thông báo** ngay trong giây lát, tăng trải nghiệm khách hàng và tốc độ phản hồi đội ngũ.  
- **Hoạt động 24/7** không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (OAuth2) – dùng cho cả email cảm ơn và email thông báo.  
- **API Key Apollo.io** – để gọi endpoint enrich dữ liệu.  
- **HubSpot App Token** – quyền tạo contact.  
- **Domain hoặc sub‑domain** để cấu hình Webhook (ví dụ: `https://yourdomain.com/webhook/lead-intake`).  
- **n8n** đã được cài đặt (Self‑hosted hoặc n8n.cloud).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Editor.  
2. Nhấn **Import** → **Upload JSON** và chọn file `lead-capture-apollo-hubspot-gmail.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **Webhook - Collect Lead** | - **Path**: `lead-intake` (đảm bảo trùng với URL bạn sẽ cung cấp cho form).<br>- **HTTP Method**: `POST`. | URL cuối cùng sẽ là `https://yourdomain.com/webhook/lead-intake`. |
| **Enrich Data from Apollo** (HTTP Request) | - **Method**: `GET` hoặc `POST` tùy API.<br>- **URL**: `https://api.apollo.io/v1/mixed_people/search` (hoặc endpoint enrich).<br>- **Headers**: `Authorization: Bearer <YOUR_APOLLO_API_KEY>`.<br>- **Query Parameters**: truyền email/phone từ webhook để Apollo trả về thông tin công ty. | Đảm bảo **Apollo API Key** được lưu trong **Credentials → API Key** để không lộ trong workflow. |
| **HubSpot - Create Contact** | - **Authentication**: chọn **hubspotAppToken**.<br>- **Properties**: map các trường từ webhook + dữ liệu Apollo (email, firstName, lastName, company, industry, size, …). | Kiểm tra **property names** trong HubSpot để tránh lỗi “property not found”. |
| **Gmail - Send Thank You** | - **Authentication**: chọn **gmailOAuth2** (tài khoản gửi email cảm ơn).<br>- **To**: `{{$json["email"]}}` (email của lead).<br>- **Subject** & **Body**: tùy chỉnh nội dung cảm ơn, có thể dùng biến `{{$json["firstName"]}}`. | Đặt **From** là địa chỉ công ty để tăng độ tin cậy. |
| **Gmail - Notify Team** | - **Authentication**: cùng **gmailOAuth2** (hoặc tài khoản khác).<br>- **To**: danh sách email nội bộ (ví dụ: `sales@yourcompany.com`).<br>- **Subject**: “New Lead from Website – {{$json["email"]}}”.<br>- **Body**: bao gồm toàn bộ thông tin lead + dữ liệu Apollo. | Có thể thêm **CC/BCC** hoặc **attachments** (ví dụ: PDF lead summary). |

> **Lưu ý quan trọng:** Sau khi chỉnh xong, nhấn **Execute Node** từng node để kiểm tra dữ liệu đầu ra, đặc biệt node `Enrich Data from Apollo` – nếu API trả về lỗi, kiểm tra lại **API Key** và **quota** của Apollo.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một POST request mẫu tới webhook (dùng Postman hoặc curl) với payload JSON chứa `email`, `firstName`, `lastName`, … để xác nhận toàn bộ chuỗi hoạt động.  
2. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  
3. Kiểm tra **Execution Log** để chắc chắn không có lỗi.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node Slack để gửi tin nhắn nhanh tới kênh sales mỗi khi có lead mới.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để ghi lại mọi lead, giúp tạo báo cáo định kỳ.  
- **Chạy định kỳ cleanup**: Thêm node **Cron** để xóa các lead trùng lặp hoặc không đủ thông tin sau 30 ngày.  
- **A/B testing email**: Tạo 2 mẫu email cảm ơn, dùng node **IF** dựa trên `utm_source` để gửi phiên bản phù hợp.  

### 📌 Kết luận
Với workflow này, các sếp sẽ **biến quy trình thu thập lead thành một chuỗi tự động, nhanh chóng và chính xác** – từ lúc khách hàng điền form tới khi contact được tạo trên HubSpot và đội ngũ nhận thông báo ngay lập tức. Đừng để thời gian và lỗi con người làm mất cơ hội bán hàng; hãy **cài ngay** và trải nghiệm hiệu quả tăng gấp bội! 🚀