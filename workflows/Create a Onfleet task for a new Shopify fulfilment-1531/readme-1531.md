---
title: "🚀 Tự động tạo nhiệm vụ Onfleet cho đơn hàng mới trên Shopify"
description: "Kết nối Shopify và Onfleet, tự động tạo task giao hàng ngay khi có fulfillment mới, giảm thao tác thủ công và tăng độ chính xác."
slug: "tu-dong-tao-nhiem-vu-onfleet-cho-shopify"
tags: [n8n, automation, no-code, Shopify, Onfleet, logistics]
keywords: [n8n workflow, tự động hóa, Onfleet, Shopify, fulfillment]
---

# 🚀 Tự động tạo nhiệm vụ Onfleet cho đơn hàng mới trên Shopify

Khi các sếp phải xử lý hàng nghìn đơn hàng mỗi ngày, việc **tạo task giao hàng trên Onfleet thủ công** sau khi Shopify tạo fulfillment là một công việc tẻ nhạt, mất thời gian và dễ gây sai sót.  
Workflow này sẽ **kết nối trực tiếp Shopify → Onfleet**, tự động tạo nhiệm vụ giao hàng ngay khi có fulfillment mới, giúp các sếp **tiết kiệm thời gian, giảm lỗi nhập liệu và duy trì quy trình giao hàng 24/7** mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tạo task ngay khi fulfillment xuất hiện.  
- **Độ chính xác cao**: Dữ liệu địa chỉ, tên người nhận được truyền thẳng từ Shopify, không còn nhập tay.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc của nhân viên.  
- **Dễ mở rộng**: Có thể thêm thông báo Slack, lưu log, hoặc tạo báo cáo định kỳ.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Shopify** với **API key** (cần cấp quyền đọc fulfillment).  
- **Tài khoản Onfleet** với **API key** (có quyền tạo task).  
- **n8n** đã được cài đặt và có quyền truy cập internet để gọi API của cả hai dịch vụ.  
- (Tùy chọn) Kết nối internet ổn định nếu chạy trên VPS.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n.  
2. Vào **Workflows → Import**.  
3. Chọn **Upload JSON** và tải file `Create a Onfleet task for a new Shopify fulfilment.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
4. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
**Node 1 – Shopify Trigger**  
- **Tên node:** `Shopify Trigger`  
- **Type:** `shopifyTrigger`  
- **Credentials:** Chọn credential `shopifyApi` đã tạo trước đó.  
- **Event:** Chọn **Fulfilment Created** (hoặc **Fulfilment Updated** tùy nhu cầu).  
- **Store:** Chọn cửa hàng Shopify muốn theo dõi.  

**Node 2 – Onfleet**  
- **Tên node:** `Onfleet`  
- **Type:** `onfleet`  
- **Credentials:** Chọn credential `onfleetApi`.  
- **Operation:** Đặt thành **Create** (đã được thiết lập sẵn trong `keyParameters`).  
- **Fields cần map:**  
  - **Task name:** `{{$json["name"]}}` hoặc tự đặt tên như `Giao hàng - {{ $json["order_id"] }}`.  
  - **Destination address:** Dùng dữ liệu `shipping_address` từ payload của Shopify (`{{$json["shipping_address"]["address1"]}}`, `{{$json["shipping_address"]["city"]}}`, …).  
  - **Recipient name:** `{{$json["shipping_address"]["name"]}}`.  
  - **Recipient phone:** `{{$json["shipping_address"]["phone"]}}`.  
  - **Notes (tùy chọn):** Thêm thông tin sản phẩm, mã đơn hàng, v.v. (`{{$json["line_items"]}}`).  

> **Lưu ý:** Đảm bảo các trường bắt buộc của Onfleet (address, name, phone) được điền đầy đủ, nếu thiếu sẽ gây lỗi khi tạo task.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** và tạo một fulfillment mẫu trên Shopify để kiểm tra.  
2. Kiểm tra trong bảng điều khiển Onfleet xem task đã được tạo thành công chưa.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram:** Thêm một node Slack hoặc Telegram ngay sau node Onfleet để gửi tin nhắn “Task #{{ $json["task_id"] }} đã được tạo”.  
- **Lưu log vào Google Sheets:** Dùng node Google Sheets để ghi lại mỗi lần tạo task (order ID, task ID, thời gian).  
- **Xử lý lỗi:** Thêm node **Error Trigger** để gửi email hoặc Slack khi có lỗi API (ví dụ: quota hết, địa chỉ không hợp lệ).  
- **Báo cáo định kỳ:** Kết hợp node **Cron** + **Google Sheets** để tổng hợp số task tạo được trong ngày/tuần.

### 📌 Kết luận
Với workflow chỉ **2 node** này, các sếp đã có thể **tự động hoá quy trình giao hàng** từ Shopify sang Onfleet, giảm thiểu công việc lặp lại và tăng độ tin cậy cho hệ thống logistics. Hãy **import ngay**, cấu hình credential và bật hoạt động – để doanh nghiệp của các sếp luôn “đi trước một bước” trong thời đại tự động hoá!