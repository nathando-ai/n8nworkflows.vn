---
title: "🚀 Tự động làm giàu thông tin khách hàng Intercom mới với ExactBuyer trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt sự kiện người dùng mới từ Intercom, quét thông tin chi tiết từ ExactBuyer và cập nhật lại hồ sơ."
slug: "tu-dong-lam-giau-thong-tin-khach-hang-intercom-exactbuyer"
tags: [n8n, automation, intercom, exactbuyer, crm, sales, enrichment]
keywords: [n8n workflow, intercom exactbuyer integration, lam giau thong tin khach hang, tu dong hoa intercom]
---

# 🚀 Tự động làm giàu thông tin khách hàng Intercom mới với ExactBuyer

Khi có một người dùng mới đăng ký hoặc tạo tài khoản trên hệ thống của bạn và được đồng bộ vào Intercom, thông tin ban đầu thường rất ít ỏi (chỉ có email hoặc tên). Việc tra cứu thủ công thông tin mạng xã hội, số điện thoại, hay vị trí địa lý của từng khách hàng tốn rất nhiều thời gian của đội ngũ Sales và Support.

Workflow n8n này sẽ giải quyết bài toán đó hoàn toàn tự động! Ngay khi có sự kiện người dùng mới xuất hiện trên Intercom, hệ thống sẽ gọi API sang ExactBuyer để lấy toàn bộ thông tin chi tiết (số điện thoại, mạng xã hội, vị địa lý...) và tự động cập nhật ngược lại hồ sơ Intercom. Giúp các sếp luôn có bức tranh toàn diện về khách hàng mà không cần tốn một phút làm thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hồ sơ khách hàng phong phú:** Tự động điền số điện thoại, mạng xã hội, vị trí và thông tin công ty vào Intercom.
- **Tiết kiệm thời gian:** Đội ngũ Sales và Support không phải tra cứu thông tin thủ công trên các công cụ bên ngoài.
- **Cá nhân hóa trải nghiệm:** Biết rõ khách hàng đến từ đâu và là ai ngay từ những tương tác đầu tiên.
- **Hoạt động 24/7:** Quy trình chạy ngầm thời gian thực (real-time) ngay khi có user mới tạo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Intercom:** Quyền quản trị để cấu hình Webhook và API Credentials.
- **Tài khoản ExactBuyer:** Lấy API Key để sử dụng dịch vụ tra cứu thông tin liên hệ (Contact Enrichment).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Node `On Webhook event from Intercom` (Webhook):** 
  - Lấy URL từ node này và cấu hình trong bảng điều khiển Webhooks của Intercom.
  - Đảm bảo sự kiện `contact.user.created` được bật (enabled) để hệ thống nhận tín hiệu khi có user mới.
- **Node `set key fields` & `massage data` (Set / Code):** 
  - Trích xuất địa chỉ email của user mới từ payload của Intercom làm định danh chính để gửi sang ExactBuyer.
- **Node `Enrich user from ExactBuyer` (HTTP Request):** 
  - Sử dụng API Key của ExactBuyer. 
  - Thiết lập request dùng email làm trường định danh (identifier) theo [tài liệu API của ExactBuyer](https://docs.exactbuyer.com/contact-enrichment/enrichment).
- **Node `Update data in Intercom` hoặc `Intercom` (HTTP Request / Intercom Node):** 
  - Cấu hình thông tin xác thực (Credentials) cho Intercom.
  - Sử dụng chuẩn [Intercom REST API (Contacts/UpdateContact)](https://developers.intercom.com/docs/references/rest-api/api.intercom.io/Contacts/UpdateContact/) để ghi đè các thông tin đã làm giàu vào profile khách hàng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** hoặc **Test workflow** bằng cách tạo một user giả lập trên Intercom để kiểm tra dữ liệu trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau bước cập nhật thành công để bắn thông báo về channel nội dung: *"Vừa enrich thành công thông tin cho khách hàng [Tên khách hàng] ([Email])!"*.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để cảnh báo nếu ExactBuyer không tìm thấy thông tin hoặc API Intercom gặp sự cố.
- **Lưu log vào Google Sheets:** Lưu lại lịch sử các user đã được enrich để đội ngũ Marketing dễ dàng theo dõi và phân tích data.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" giúp tự động hóa khâu nghiên cứu khách hàng (Data Enrichment) ngay từ giây phút đầu tiên họ đăng ký. Hãy triển khai ngay để tối ưu hóa hiệu suất làm việc cho đội ngũ Sales và Support của các sếp nhé!