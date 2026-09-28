---
title: "🚀 Chuyển đổi trường markdown dạng rich text từ Airtable sang HTML tự động"
description: "Workflow n8n tự động lấy nội dung markdown từ Airtable, chuyển thành HTML và cập nhật lại, hỗ trợ xử lý một bản ghi hoặc toàn bộ bảng."
slug: "chuyen-doi-airtable-markdown-sang-html"
tags: [n8n, automation, no-code, airtable, markdown, html]
keywords: [n8n workflow, tự động hóa, Airtable markdown, chuyển đổi HTML, no-code]
---

# 🚀 Chuyển đổi trường markdown dạng rich text từ Airtable sang HTML tự động

Khi làm việc với Airtable, nhiều team thường lưu nội dung mô tả dưới dạng **markdown** để dễ soạn thảo. Tuy nhiên, các công cụ hiển thị (website, email, CMS…) lại yêu cầu **HTML**. Việc chuyển đổi thủ công từng bản ghi gây tốn thời gian, dễ sai sót và không đồng bộ.  
Workflow này sẽ **tự động**:

1. Lấy markdown từ một trường trong Airtable.  
2. Chuyển đổi sang HTML bằng node Markdown của n8n.  
3. Cập nhật lại bản ghi (hoặc toàn bộ bảng) với trường HTML mới.  

Tất cả chỉ cần một webhook kích hoạt, không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải copy‑paste và chuyển đổi thủ công.  
- **Độ chính xác 100%**: HTML luôn phản ánh đúng markdown gốc.  
- **Tự động hoá toàn bộ**: Có thể chạy 24/7, xử lý một bản ghi hoặc toàn bộ bảng.  
- **Dễ mở rộng**: Kết hợp với Slack, Email hay Zapier để thông báo sau khi cập nhật.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Airtable** với **API Token** (có quyền `read` và `write`).  
- **Base ID** và **Table Name** chứa trường markdown và trường HTML.  
- **Tên trường markdown** (ví dụ: `Description_md`).  
- **Tên trường HTML** (ví dụ: `Description_html`).  
- **n8n** đã được cài đặt và có thể truy cập webhook công cộng.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n > Workflows > Import**.  
2. Tải file JSON của workflow (được cung cấp ở phần cuối tài liệu) hoặc **Copy/Paste** toàn bộ JSON vào ô import.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình:

| Node | Loại | Mô tả | Cấu hình cần chỉnh |
|------|------|------|--------------------|
| **Airtable sync video description** | Webhook | Đầu vào duy nhất, kích hoạt workflow khi nhận request. | - `Path`: `848644e5-6b1d-42b3-9259-5828c29780a8` (không thay đổi). <br> - Đảm bảo webhook được **public** (n8n Cloud hoặc reverse proxy). |
| **Check if it's 1 record or all records - Airtable** | IF | Kiểm tra payload `recordId` có tồn tại → quyết định xử lý một bản ghi hay toàn bộ. | - Điều kiện: `{{ $json["recordId"] ? true : false }}`. |
| **Get single record from airtable** | Airtable (Get) | Lấy một bản ghi dựa trên `recordId`. | - **Credentials**: Airtable API Token. <br> - **Base ID**, **Table Name**. <br> - **Record ID**: `{{ $json["recordId"] }}`. |
| **Get all records from airtable** | Airtable (Search) | Lấy toàn bộ bản ghi trong bảng. | - **Credentials**, **Base ID**, **Table Name**. <br> - **View** (nếu muốn giới hạn). |
| **Convert markdown to HTML1** | Markdown | Chuyển markdown của **bản ghi đơn** sang HTML. | - **Input**: `{{ $json["fields"]["Description_md"] }}` (đặt đúng tên trường markdown). |
| **Convert markdown to HTML2** | Markdown | Chuyển markdown của **các bản ghi đa** sang HTML (dùng trong Loop). | - **Input**: `{{ $json["fields"]["Description_md"] }}`. |
| **Update single record in airtable** | Airtable (Update) | Cập nhật trường HTML cho một bản ghi. | - **Record ID**: `{{ $json["id"] }}` (từ node Get single). <br> - **Fields**: `{ "Description_html": "{{ $json["html"] }}" }`. |
| **Update all records in airtable** | Airtable (Update) | Cập nhật trường HTML cho từng bản ghi trong vòng lặp. | - **Record ID**: `{{ $json["id"] }}` (từ node Get all). <br> - **Fields**: `{ "Description_html": "{{ $json["html"] }}" }`. |

**Lưu ý quan trọng**  
- Đảm bảo **tên trường** trong Airtable khớp chính xác (case‑sensitive).  
- Node Markdown trả về `html` trong `{{ $json["html"] }}`; dùng giá trị này để cập nhật.  
- Nếu bảng có **tỷ lệ record > 100**, bật tùy chọn **Pagination** trong node Airtable để lấy hết dữ liệu.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một request POST tới webhook, body JSON: `{ "recordId": "recXXXXXXXXXXXX" }` để xử lý một bản ghi, hoặc `{}` để xử lý toàn bộ.  
2. Kiểm tra log của các node **Markdown** và **Airtable Update** để chắc chắn HTML đã được ghi lại.  
3. Khi mọi thứ ổn, bật **Active** ở góc trên bên phải của workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack/Telegram sau node Update để gửi tin “✅ Đã chuyển đổi X bản ghi”.  
- **Lưu log vào Google Sheet**: Dùng node Google Sheets để ghi lại `recordId`, thời gian chạy, và trạng thái.  
- **Xử lý định kỳ**: Kết hợp với **Cron** node để tự động chạy mỗi giờ/ngày mà không cần webhook.  
- **Bảo mật**: Đặt **IP whitelist** cho webhook nếu chạy trên server nội bộ.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động** chuyển đổi mọi nội dung markdown trong Airtable sang HTML chỉ bằng một cú click hoặc một request webhook. Không còn lo lắng về lỗi chuyển đổi thủ công, không cần viết code, và có thể mở rộng dễ dàng cho các kịch bản thông báo hay báo cáo. Hãy **import ngay**, cấu hình vài thông tin và để n8n làm phần còn lại! 🚀