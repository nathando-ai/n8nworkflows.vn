---
title: "🚀 Tự Động Tạo Hóa Đơn Shopify → PDF, Lưu Google Drive & Gửi Email"
description: "Workflow n8n tự động nhận đơn hàng Shopify, tạo hóa đơn PDF, lưu trên Google Drive và gửi email cho khách hàng chỉ trong vài giây."
slug: "tu-dong-tao-hoa-don-shopify-pdf-google-drive-email"
tags: [n8n, automation, no-code, Shopify, Google-Drive, Gmail]
keywords: [n8n workflow, tự động hóa, invoice, Shopify, PDF, Google Drive, Gmail]
---

# 🚀 Tự Động Tạo Hóa Đơn Shopify → PDF, Lưu Google Drive & Gửi Email

Bạn đã từng phải **tạo hóa đơn thủ công** cho mỗi đơn hàng Shopify, **điền dữ liệu**, **chuyển sang PDF**, **lưu trữ** và **gửi email** cho khách?  
Quá trình này không chỉ tốn thời gian mà còn dễ gây sai sót, ảnh hưởng đến trải nghiệm khách hàng và hiệu suất bán hàng.

**Workflow này** sẽ **tự động hoá 100%** quy trình trên **không cần viết một dòng code nào**. Khi một đơn hàng được thanh toán thành công, hệ thống sẽ:

✅ Nhận dữ liệu đơn hàng qua webhook Shopify  
✅ Kiểm tra trạng thái thanh toán  
✅ Tạo HTML hóa đơn tùy chỉnh  
✅ Chuyển HTML sang PDF (sử dụng API PDFMunk)  
✅ Lưu PDF vào Google Drive  
✅ Gửi email kèm PDF cho khách hàng  
✅ Trả về phản hồi webhook cho Shopify  

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ vài phút xuống còn vài giây cho mỗi đơn hàng.  
- **Độ chính xác 100 %**: Dữ liệu được lấy trực tiếp từ Shopify, không còn nhập tay.  
- **Lưu trữ tự động**: Hóa đơn PDF luôn được sao lưu trên Google Drive, dễ truy xuất.  
- **Giao tiếp chuyên nghiệp**: Khách hàng nhận được email hóa đơn ngay sau khi thanh toán.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Shopify**: Tạo webhook URL (sẽ được cung cấp sau khi import workflow).  
- **Google Drive**: Tài khoản Google, bật OAuth2 và cấp quyền `drive.file`.  
- **Gmail**: Tài khoản Gmail, bật OAuth2 và cấp quyền `https://mail.google.com/`.  
- **PDFMunk**: API Key từ https://pdfmunk.com (để chuyển HTML → PDF).  
- **n8n**: Đã cài đặt và có quyền tạo/đọc credentials cho Google Drive, Gmail, PDFMunk.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (được cung cấp trong mục “Download”).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào **n8n Editor → New Workflow → Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|---------|--------------------|
| **Shopify Order Webhook** | Nhận dữ liệu đơn hàng từ Shopify | - `Path`: `shopify-webhook` (không thay đổi) <br> - `HTTP Method`: `POST` <br> - **Lưu URL** (n8n URL + `/webhook/shopify-webhook`) và đăng ký trên Shopify > Settings > Notifications > Webhooks (Event: *Order creation*). |
| **Check Payment Status** (IF) | Kiểm tra `financial_status` = `paid` | - Điều kiện: `{{$json["financial_status"]}}` **equals** `paid`. |
| **Format Invoice Data** (Code) | Chuẩn bị dữ liệu line items, tổng tiền, thông tin khách | - Không cần thay đổi nếu cấu trúc Shopify mặc định. Nếu shop có custom fields, chỉnh sửa script trong node. |
| **Generate HTML Invoice** (Code) | Tạo HTML hóa đơn | - Thay đổi **template HTML** (logo, màu sắc, địa chỉ công ty) trong script. |
| **Generate PDF Invoice** (HTML/CSS to PDF) | Chuyển HTML → PDF | - **Credential**: `htmlcsstopdfApi` → Nhập API Key PDFMunk. <br> - Kiểm tra `Page size`, `Margins` nếu cần. |
| **Download File PDF** (HTTP Request) | Lấy file PDF từ API PDFMunk | - `Method`: `GET` <br> - URL: `{{$json["pdfUrl"]}}` (được trả về từ node trước). |
| **Save to Google Drive** | Lưu PDF vào Google Drive | - **Credential**: `googleDriveOAuth2Api`. <br> - `Folder ID`: ID thư mục Google Drive nơi lưu hóa đơn. |
| **Email to Customer** (Gmail) | Gửi email kèm PDF | - **Credential**: `gmailOAuth2`. <br> - `To`: `{{$json["email"]}}` (email khách). <br> - `Subject`: “Hóa đơn mua hàng #{{$json["order_number"]}}”. <br> - `Attachments`: Chọn `Binary Data` → `PDF`. |
| **Send Webhook Response** | Phản hồi thành công cho Shopify | - `Status Code`: `200` <br> - `Body`: `{ "message": "Invoice generated and sent." }` |
| **Response for Unpaid Orders** | Phản hồi khi chưa thanh toán | - `Status Code`: `200` <br> - `Body`: `{ "message": "Order not paid. No invoice generated." }` |

> **Lưu ý:** Đảm bảo **credentials** đã được tạo trong n8n → Credentials trước khi gán vào các node.

#### 3. Kích hoạt ⚡️
1. **Test run**: Tạo một đơn hàng thử trên Shopify (có trạng thái *paid*).  
2. Kiểm tra:  
   - Webhook nhận được dữ liệu.  
   - PDF được tạo, lưu vào Google Drive.  
   - Email có đính kèm PDF.  
   - Shopify nhận phản hồi webhook.  
3. Khi mọi thứ hoạt động ổn, bật **Active** ở góc phải của workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo hàng ngày**: Thêm node **Google Sheets** để ghi log mỗi khi tạo hóa đơn, rồi dùng **Cron** để gửi báo cáo qua Gmail.  
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để nhận thông báo ngay khi có đơn hàng mới hoặc lỗi.  
- **Lưu trữ backup**: Đồng thời sao chép PDF vào **AWS S3** hoặc **Dropbox** để đa nền tảng.  
- **Tùy chỉnh mẫu HTML**: Sử dụng **Handlebars** hoặc **Mustache** trong node Code để tạo mẫu đa ngôn ngữ hoặc đa thương hiệu.  

### 📌 Kết luận
Với workflow **Automated Invoice Generator**, các sếp có thể **loại bỏ hoàn toàn công việc tạo hóa đơn thủ công**, giảm thiểu lỗi, tăng tốc độ phản hồi khách hàng và duy trì hồ sơ bán hàng một cách chuyên nghiệp. Hãy **import ngay**, cấu hình các credentials và để n8n làm phần còn lại – doanh nghiệp của bạn sẽ “cất cánh” nhanh hơn bao giờ hết! 🚀