---
title: "🚀 Tự động đặt bàn & đặt món qua giọng nói với VAPI + PostgreSQL"
description: "Giải pháp tự động hoá 100% cho nhà hàng: nhận đặt bàn, đặt món và cung cấp thông tin qua giọng nói, lưu trữ dữ liệu ngay trong cơ sở dữ liệu PostgreSQL."
slug: "assistant-voi-vapi-postgresql-booking-orders"
tags: [n8n, automation, no-code, chatbot, voice-assistant, postgres]
keywords: [n8n workflow, tự động hóa, chatbot, voice assistant, PostgreSQL, VAPI]
---

# 🚀 Tự động đặt bàn & đặt món qua giọng nói với VAPI + PostgreSQL

Bạn đang quản lý nhà hàng, quán ăn và muốn khách hàng có thể đặt bàn, đặt món chỉ bằng giọng nói mà không cần phải nhập dữ liệu thủ công? Workflow này sẽ giúp bạn:

- Nhận yêu cầu đặt bàn/đặt món qua VAPI (Voice API).
- Lưu trữ thông tin vào bảng **Booking** hoặc **Orders** trong PostgreSQL.
- Trả lời khách hàng ngay lập tức với xác nhận đặt bàn/đặt món.
- Cung cấp thông tin chi tiết về nhà hàng khi khách yêu cầu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập dữ liệu thủ công, giảm lỗi nhập liệu.  
- **Chính xác**: Dữ liệu được lưu trực tiếp vào PostgreSQL, tránh mất mát.  
- **Cá nhân hóa**: Gửi xác nhận và thông tin chi tiết ngay lập tức qua giọng nói.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào con người.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **VAPI**: Tài khoản, API Key, và cấu hình webhook (đường dẫn dưới đây).  
- **PostgreSQL**: Cơ sở dữ liệu đã có bảng `Booking` và `Orders` (hoặc tạo mới).  
- **n8n**: Phiên bản mới nhất, cài đặt trên VPS hoặc Docker.  
- **Credentials**:  
  - `postgres` – kết nối tới DB.  
  - `VAPI` – credentials cho webhook và respondToWebhook.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/5847).  
2. Trong n8n Editor, chọn **Import** → **Import from File** → chọn file JSON.  
3. Hoặc copy toàn bộ JSON vào **Editor** → **Paste** → **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên thực tế | Thông tin cần cấu hình | Ghi chú |
|------|-------------|------------------------|---------|
| **Trigger: Voice Request (VAPI)** | `webhook` | `path: 9f6b9125-0b75-41c2-87a9-1b6746c89e2e` <br> `httpMethod: POST` | Đặt URL webhook trong VAPI (điền vào VAPI dashboard). |
| **Update Data (Table Booking / Orders)** | `postgres` | `operation: upsert` <br> `table: Booking` hoặc `Orders` <br> `primaryKey: id` | Đảm bảo bảng có cột `id` (auto-increment). |
| **Respond: Booking/Order Confirmation (VAPI)** | `respondToWebhook` | `response: <text>` | Dùng dữ liệu từ node trước để tạo tin nhắn xác nhận. |
| **Wait For Response** | `wait` | `waitTime: 5s` (hoặc tùy chỉnh) | Đợi phản hồi từ khách trước khi tiếp tục. |
| **Wait For Response1** | `wait` | `waitTime: 5s` | Đợi thêm nếu cần. |
| **Trigger: Info Request (VAPI)** | `webhook` | `path: efe2c13f-1ba5-46e1-9996-57bdc6041973` | Đặt URL webhook cho yêu cầu thông tin. |
| **Get Restaurant Info (Postgres)** | `postgres` | `operation: select` <br> `table: RestaurantInfo` | Lấy thông tin nhà hàng (địa chỉ, giờ mở cửa, menu). |
| **Respond: Restaurant Details (VAPI)** | `respondToWebhook` | `response: <text>` | Trả lời chi tiết cho khách. |

> **Lưu ý**: Mỗi node `respondToWebhook` cần được cấu hình **Credentials** VAPI. Nếu chưa có, vào **Credentials** → **New Credential** → chọn `VAPI` → nhập API Key.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với dữ liệu mẫu (đăng ký webhook, gửi POST từ Postman hoặc VAPI).  
2. Kiểm tra log trong n8n để xác nhận dữ liệu đã được upsert vào DB.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` để gửi báo cáo đặt bàn hàng ngày.  
- **Lưu log**: Dùng node `Postgres` để ghi log các yêu cầu và phản hồi.  
- **Báo cáo định kỳ**: Sử dụng node `Cron` + `Postgres` để gửi thống kê đặt bàn hàng tuần qua email.  
- **Tùy chỉnh prompt**: Nếu sử dụng LLM, thêm node `OpenAI` để tạo câu trả lời tự nhiên hơn.  

## 📌 Kết luận

Workflow này giúp các sếp nhà hàng tiết kiệm thời gian, giảm lỗi và nâng cao trải nghiệm khách hàng bằng cách tự động hoá toàn bộ quy trình đặt bàn, đặt món và cung cấp thông tin qua giọng nói. Hãy thử ngay, cài đặt trên VPS và trải nghiệm sự tiện lợi mà công nghệ mang lại!