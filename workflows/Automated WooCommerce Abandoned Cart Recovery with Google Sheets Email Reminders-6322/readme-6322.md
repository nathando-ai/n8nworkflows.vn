---
title: "🚀 Tự động thu hồi giỏ hàng bỏ quên WooCommerce với Google Sheets & Email Reminder"
description: "Giải pháp n8n tự động lấy đơn hàng bỏ quên từ WooCommerce, lưu vào Google Sheet và gửi email nhắc nhở, giảm thiểu mất doanh thu."
slug: "tu-dong-thu-hoi-gio-hang-bo-quen-woocommerce-google-sheets-email"
tags: [n8n, automation, no-code, woocommerce, google-sheets, email]
keywords: [n8n workflow, tự động hóa, abandoned cart, WooCommerce, Google Sheets, email reminder]
---

# 🚀 Tự động thu hồi giỏ hàng bỏ quên WooCommerce với Google Sheets & Email Reminder

Khi khách hàng thêm sản phẩm vào giỏ nhưng không hoàn tất thanh toán, **doanh thu** của bạn sẽ bị rò rỉ mà không hề biết. Việc **theo dõi và nhắc nhở** thủ công qua email hoặc spreadsheet tiêu tốn hàng giờ, dễ sai sót và không đồng nhất.  
Workflow **Automated WooCommerce Abandoned Cart Recovery** giúp bạn:

* **Lấy tự động** các đơn hàng đang ở trạng thái “pending” từ WooCommerce.  
* **Ghi lại** chi tiết đơn hàng vào Google Sheet để dễ quản lý và phân tích.  
* **Gửi email nhắc nhở** cá nhân hoá tới khách hàng, kích hoạt lại quá trình mua hàng.  

Tất cả chỉ cần **cài đặt một lần**, chạy 24/7 mà không viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn nhập liệu thủ công, workflow tự động chạy mỗi giờ.  
- **Tăng tỷ lệ chuyển đổi**: Email nhắc nhở kịp thời giúp khách quay lại hoàn tất mua hàng.  
- **Độ chính xác 100 %**: Dữ liệu từ WooCommerce được đồng bộ ngay vào Google Sheet, giảm lỗi nhập tay.  
- **Hoạt động liên tục**: Chạy trên VPS hoặc Docker, không phụ thuộc máy cá nhân.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản WooCommerce** với **REST API** (Consumer Key & Consumer Secret).  
- **Google Cloud Project** đã bật Google Sheets API và tạo **OAuth2 credentials** (hoặc Service Account) để n8n có quyền ghi/đọc sheet.  
- **Tài khoản Email** (SMTP) để n8n gửi email reminder (Gmail, SendGrid, Mailgun, …).  
- **Google Sheet** đã tạo sẵn với các cột: `Order ID`, `Customer Email`, `Created At`, `Status`, `Reminder Sent`.  
- **n8n** đã cài đặt và có ít nhất 1 GB RAM để chạy các node HTTP & Code.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Click **“Import” → “From File”** và tải file JSON của workflow (hoặc **Copy/Paste** JSON vào ô nhập).  
3. Nhấn **“Import”**, workflow sẽ xuất hiện dưới dạng **“Automated WooCommerce Abandoned Cart Recovery”**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách **9 node** cần cấu hình chi tiết:

| Node | Loại | Cấu hình quan trọng cần chỉnh |
|------|------|--------------------------------|
| **Schedule Trigger** | scheduleTrigger | Đặt **Cron**: `0 * * * *` (chạy mỗi giờ) hoặc tùy nhu cầu. |
| **Schedule Trigger1** | scheduleTrigger | Đặt **Cron**: `30 * * * *` (chạy mỗi giờ 30 phút) để tách luồng lấy đơn & gửi email. |
| **Date & Time** | dateTime | Định dạng **Current Date** → `YYYY-MM-DD HH:mm:ss` để ghi thời gian tạo đơn. |
| **HTTP Request1** | httpRequest | - **Method**: `GET` <br> - **URL**: `https://yourstore.com/wp-json/wc/v3/orders` <br> - **Authentication**: **OAuth1** (Consumer Key/Secret) hoặc **Basic Auth**. <br> - **Query Params**: `status=pending&per_page=100`. |
| **Convert data** | code | Script JavaScript để **filter** các đơn có `date_created` > 1 giờ, **map** các trường cần (order_id, email, created_at, status). |
| **Adding orders to Google Sheet** | googleSheets | - **Spreadsheet ID**: ID của sheet lưu đơn. <br> - **Sheet Name**: `Orders`. <br> - **Operation**: **Append**. <br> - **Values**: map từ node **Convert data**. |
| **Get order with pending status** | googleSheets | - **Spreadsheet ID**: cùng sheet. <br> - **Sheet Name**: `Orders`. <br> - **Operation**: **Read Rows**. <br> - **Filter**: `Status = pending` và `Reminder Sent = FALSE`. |
| **Reminder Sent Email Update** | googleSheets | - **Spreadsheet ID**: cùng sheet. <br> - **Sheet Name**: `Orders`. <br> - **Operation**: **Update** (đánh dấu cột `Reminder Sent` = TRUE sau khi email gửi). |
| **Send reminder email** | emailSend | - **SMTP Credentials**: tài khoản email. <br> - **To**: `{{$json["Customer Email"]}}`. <br> - **Subject**: “Bạn còn món hàng trong giỏ hàng – Hoàn tất ngay!”. <br> - **HTML Body**: chèn **order details**, **link** tới giỏ hàng (`{{order_url}}`). |

> **Lưu ý:** Đảm bảo **Credentials** cho mỗi node (WooCommerce, Google Sheets, Email) đã được tạo trong n8n → **Credentials** và được chọn trong trường **Credentials** của node tương ứng.

#### 3. Kích hoạt ⚡️
1. **Test run**: Click **“Execute Workflow”** → kiểm tra log của mỗi node, đặc biệt là **HTTP Request1** và **Send reminder email**.  
2. Nếu mọi thứ ổn, bật **“Active”** (nút toggle ở góc trên bên phải).  
3. Kiểm tra Google Sheet: các đơn “pending” mới sẽ xuất hiện, và sau 1‑2 giờ, email reminder sẽ được gửi và cột `Reminder Sent` sẽ chuyển thành **TRUE**.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: dùng node **Slack** hoặc **Telegram** để gửi thông báo nội bộ mỗi khi có đơn mới hoặc email reminder đã gửi.  
- **Lưu log chi tiết**: tạo một sheet “Logs” và dùng node **Google Sheets → Append** để ghi thời gian, order ID, trạng thái gửi.  
- **Gửi báo cáo tuần**: dùng node **Schedule Trigger** (cron `0 9 * * MON`) + **Google Sheets → Read** + **EmailSend** để gửi báo cáo tổng hợp các đơn bỏ quên đã chuyển đổi.  
- **Tùy chỉnh nội dung email**: dùng node **Code** để tạo **dynamic HTML** dựa trên sản phẩm trong giỏ, tăng tính cá nhân hoá.  
- **Giới hạn gửi**: thêm node **IF** kiểm tra số lần reminder (max 2 lần) để tránh spam.

### 📌 Kết luận
Với workflow **Automated WooCommerce Abandoned Cart Recovery**, các sếp có thể **giảm thiểu mất doanh thu** do giỏ hàng bỏ quên, **tự động hoá** quy trình thu thập dữ liệu và nhắc nhở khách hàng chỉ trong vài phút thiết lập. Hãy **import**, **cấu hình** nhanh chóng và **bật chạy** ngay hôm nay – để doanh thu của bạn luôn “được giữ chặt”!