---
title: "🚀 Tự động tạo khách hàng & hóa đơn Stripe 100% không code"
description: "Giải pháp tự động kiểm tra khách hàng, tạo mới nếu chưa tồn tại và lập hóa đơn ngay lập tức, giúp doanh nghiệp tiết kiệm thời gian và giảm sai sót."
slug: "tua-dong-tao-khach-hang-va-hoa-don-stripe"
tags: [n8n, automation, no-code, stripe, finance]
keywords: [n8n workflow, tự động hóa, Stripe, invoice, khách hàng]
---

# 🚀 Tự động tạo khách hàng & hóa đơn Stripe 100% không code

Bạn đang phải nhập liệu thủ công từng khách hàng, tạo hóa đơn, và gửi cho khách hàng qua email? Điều này không chỉ tốn thời gian mà còn dễ gây lỗi. Workflow “Create or Find Stripe Customers and Automatically Generate Invoices” giúp bạn **tự động** kiểm tra khách hàng trên Stripe, tạo mới nếu chưa có, và lập hóa đơn ngay lập tức – hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút nhập liệu thủ công thành vài giây tự động.
- **Chính xác 100%**: Dữ liệu được lấy trực tiếp từ Stripe, tránh lỗi nhập tay.
- **Tự động hóa liên tục**: Khi có sự kiện mới (ví dụ: webhook), workflow sẽ chạy ngay mà không cần can thiệp.
- **Dễ dàng mở rộng**: Thêm các bước gửi email, Slack, hoặc lưu log vào Google Sheet chỉ vài click.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Stripe API Key** (Secret key) – cần thiết cho các node `httpRequest` tương tác với Stripe.
- **Webhook URL** (nếu muốn kích hoạt tự động từ Stripe) – có thể dùng node `manualTrigger` để test.
- **Thông tin hóa đơn** (ví dụ: item name, amount, currency) – sẽ được cấu hình trong node `Set invoice data`.
- **Cấu hình Stripe**: Đảm bảo tài khoản Stripe đã được bật API và có quyền tạo khách hàng, hóa đơn.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ link gốc: <https://n8n.io/workflows/3723> hoặc copy nội dung JSON.
2. Mở **n8n Editor**, chọn **Import Workflow** → **Upload JSON** hoặc **Paste JSON**.
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Thông số cần cấu hình |
|------|-------|-----------------------|
| **Get Stripe Customer** | Gọi API `GET /v1/customers?email={email}` để tìm khách hàng | `Stripe API Key` trong Credentials, `email` lấy từ input |
| **Customer exists?** | Kiểm tra phản hồi của node trước | Không cần cấu hình thêm |
| **Create customer** | Gọi API `POST /v1/customers` nếu khách hàng chưa tồn tại | `Stripe API Key`, `email`, `name`, v.v. |
| **Set customer id** | Lưu `customer.id` vào dữ liệu tiếp theo | `customer.id` từ node `Create customer` |
| **Set invoice data** | Định nghĩa nội dung hóa đơn (items, amount, currency) | `customer.id`, `items`, `amount`, `currency` |
| **Create invoice** | Gọi API `POST /v1/invoices` | `Stripe API Key`, `customer.id`, `items` |
| **Add item to invoice** | Thêm item vào invoice đã tạo | `invoice.id`, `item details` |
| **Finalize invoice** | Gọi API `POST /v1/invoices/{invoice_id}/finalize` | `Stripe API Key`, `invoice.id` |
| **When clicking ‘Test workflow’** | Trigger thủ công để test | Không cần cấu hình |

> **Tip**: Đối với các node `httpRequest`, hãy chọn **Credentials** → **Stripe** (đã tạo trước). Nếu chưa có, tạo mới bằng cách điền `Stripe API Key`.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn nút **Execute Workflow** trong n8n Editor, nhập dữ liệu mẫu (email, item, amount) và xem log.
2. Kiểm tra phản hồi từ Stripe (đảm bảo khách hàng được tạo/không, hóa đơn được lập).
3. Khi mọi thứ ổn, bật **Active** cho workflow.
4. Nếu muốn tự động, tạo webhook trong Stripe (đến URL của node `manualTrigger`) hoặc sử dụng trigger khác.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi email xác nhận**: Thêm node `Send Email` sau khi `Finalize invoice` để gửi hóa đơn cho khách hàng.
- **Slack notification**: Kết nối với Slack để nhận thông báo khi hóa đơn được tạo.
- **Lưu log vào Google Sheet**: Dùng node `Google Sheets` để ghi lại ID khách hàng, invoice, thời gian.
- **Tích hợp với Zapier**: Nếu cần, xuất dữ liệu sang Zapier để tiếp tục quy trình marketing.

## 📌 Kết luận

Workflow này giúp các sếp **tự động hóa hoàn toàn** quy trình tạo khách hàng và lập hóa đơn trên Stripe, giảm thiểu công sức, tránh lỗi và tăng tính linh hoạt. Hãy thử ngay, tùy chỉnh theo nhu cầu và mở rộng thêm các bước khác để tối ưu hoá quy trình kinh doanh của bạn!