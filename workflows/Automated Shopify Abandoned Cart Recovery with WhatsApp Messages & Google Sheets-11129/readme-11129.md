---
title: "🚀 Tự động thu hồi giỏ hàng bỏ quên trên Shopify qua WhatsApp & Google Sheets"
description: "Workflow n8n tự động lấy danh sách giỏ hàng bỏ quên trên Shopify, xác thực số điện thoại và gửi tin nhắn WhatsApp nhắc nhở, đồng thời lưu trạng thái vào Google Sheets."
slug: "tu-dong-thu-ho-gio-hang-bo-quen-shopify-whatsapp-google-sheets"
tags: [n8n, automation, no-code, Shopify, WhatsApp, GoogleSheets]
keywords: [n8n workflow, tự động hóa, Shopify, WhatsApp, abandoned cart, Google Sheets]
---

# 🚀 Tự động thu hồi giỏ hàng bỏ quên trên Shopify qua WhatsApp & Google Sheets

Bạn có bao giờ lo lắng vì khách hàng bỏ giỏ hàng trên Shopify mà không nhận được bất kỳ phản hồi nào?  
Việc theo dõi thủ công, gửi email hoặc tin nhắn từng khách một không chỉ tốn thời gian mà còn dễ bỏ sót, dẫn đến mất doanh thu.  

**Workflow này** sẽ tự động:

1. Lấy danh sách **abandoned checkouts** từ Shopify mỗi giờ.  
2. Lấy thông tin khách hàng (số điện thoại) và **xác thực** qua Rapiwa.  
3. Gửi **tin nhắn WhatsApp** nhắc nhở mua hàng.  
4. Ghi lại trạng thái **Verified / Sent** hoặc **Unverified / Not Sent** vào Google Sheets để bạn dễ dàng theo dõi và phân tích.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn thao tác thủ công, workflow chạy tự động mỗi giờ.  
- **Tăng tỷ lệ chuyển đổi**: Nhắc nhở khách qua WhatsApp – kênh có tỷ lệ mở cao.  
- **Độ chính xác cao**: Số điện thoại được xác thực trước khi gửi, giảm lỗi gửi sai.  
- **Báo cáo rõ ràng**: Trạng thái gửi được lưu trong Google Sheets, dễ dàng phân tích KPI.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Shopify Admin API credentials** (API key & password) để gọi các endpoint `/admin/api/2023-07/checkout.json`.  
- **Rapiwa API credentials** (API key & secret) để xác thực số và gửi tin nhắn WhatsApp.  
- **Google Account** có quyền tạo và chỉnh sửa Google Sheet; tạo **Google Sheets credential** trong n8n.  
- **WhatsApp Business number** đã được đăng ký và liên kết với Rapiwa.  
- **n8n** (phiên bản mới nhất) được cài đặt và có ít nhất 2 GB RAM để chạy các node batch.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Import from JSON** và tải file `shopify-abandoned-cart-whatsapp.json` (được cung cấp trong mục **Resources** của bài viết).  
3. Hoặc **Copy/Paste** toàn bộ JSON vào ô **Paste JSON** và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và hướng dẫn cấu hình chi tiết:

| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **Schedule Trigger** | `scheduleTrigger` | Đặt **Cron**: `0 * * * *` (mỗi giờ) hoặc tùy chỉnh thời gian chạy. |
| **Get All Abandoned checkouts** | `httpRequest` | - **Method**: `GET` <br> - **URL**: `https://{shop}.myshopify.com/admin/api/2023-07/checkouts.json?status=abandoned` <br> - **Authentication**: **Basic Auth** → nhập **API key** (username) và **Password** (password). |
| **Loop Over Items** | `splitInBatches` | **Batch Size**: `10` (để tránh rate‑limit). |
| **Get customer info** | `httpRequest` | - **Method**: `GET` <br> - **URL**: `https://{shop}.myshopify.com/admin/api/2023-07/customers/{{ $json.customer_id }}.json` <br> - **Authentication**: dùng cùng **Basic Auth** như trên. |
| **If** | `if` | Kiểm tra **phone number** tồn tại: `{{$json.phone != null}}`. |
| **Rapiwa (verify number)** | `n8n-nodes-rapiwa.rapiwa` | - **Operation**: `Verify Number` <br> - **Phone Number**: `{{$json.phone}}` <br> - **Credentials**: chọn **Rapiwa API** đã tạo. |
| **Rapiwa (sent message)** | `n8n-nodes-rapiwa.rapiwa` | - **Operation**: `Send Message` <br> - **Phone Number**: `{{$json.phone}}` <br> - **Message**: `Xin chào {{ $json.first_name }}, bạn đã để lại giỏ hàng chưa hoàn tất trên {{ $json.shop_name }}. Nhấn vào link để hoàn tất: {{ $json.checkout_url }}` <br> - **Credentials**: Rapiwa. |
| **Wait** | `wait` | Đặt **Delay**: `5 seconds` (để tránh spam quá nhanh). |
| **Store State of Rows in Verified & Sent** | `googleSheets` | - **Operation**: `Append` <br> - **Spreadsheet ID**: ID của sheet “Verified & Sent”. <br> - **Range**: `A1:E1` (hoặc tùy cấu trúc). <br> - **Values**: `{{$json.customer_id}}, {{$json.email}}, {{$json.phone}}, Verified, Sent`. |
| **Store State of Rows in Unverified & Not Sent** | `googleSheets` | Tương tự, nhưng **Range** và **Values** ghi `Unverified, Not Sent`. |
| **Code in JavaScript** | `code` | Dùng để **format dữ liệu** trước khi ghi vào Google Sheets (ví dụ: chuyển đổi timestamp, tạo link checkout). |
| **Split Out / Split Out1** | `splitOut` | Tách mảng kết quả thành các item riêng để xử lý tuần tự. |
| **Loop Over Items1** | `splitInBatches` | Batch cho **Rapiwa verification & send** (độ sâu 5‑10). |
| **Sticky Note** | `stickyNote` | Chỉ dùng để ghi chú, không cần cấu hình. |

> **Lưu ý:** Mọi node **httpRequest** và **Rapiwa** đều phải **chọn Credentials** tương ứng. Nếu chưa tạo, vào **Credentials → New Credential** → chọn loại và nhập API key/secret.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu để kiểm tra dữ liệu mẫu.  
2. Kiểm tra **Google Sheet** xem có dòng “Verified & Sent” hoặc “Unverified & Not Sent” được thêm không.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải) để workflow chạy tự động theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Dùng node `Slack` hoặc `Telegram` để gửi báo cáo tổng hợp mỗi ngày vào kênh nội bộ.  
- **Lưu log chi tiết**: Kết nối `n8n-nodes-base.mongodb` hoặc `PostgreSQL` để lưu toàn bộ payload, giúp debug nhanh khi có lỗi.  
- **Gửi ưu đãi**: Khi số điện thoại được xác thực, có thể chèn **mã giảm giá** vào tin nhắn WhatsApp để tăng tỷ lệ chuyển đổi.  
- **Phân đoạn khách hàng**: Dùng node `If` bổ sung để chỉ gửi tin nhắn tới khách hàng chưa mua trong 30 ngày hoặc có giá trị giỏ hàng > $100.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động thu hồi giỏ hàng bỏ quên** trên Shopify, **tăng doanh thu** và **giảm tải công việc** chỉ trong vài phút thiết lập. Hãy import ngay, cấu hình các credential, bật Active và để n8n làm việc cho bạn 24/7! 🚀