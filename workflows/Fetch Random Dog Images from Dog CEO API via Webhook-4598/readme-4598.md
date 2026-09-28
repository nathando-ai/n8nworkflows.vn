---
title: "🚀 Tự động lấy ảnh chú cún ngẫu nhiên qua Webhook với Dog CEO API trong n8n"
description: "Hướng dẫn xây dựng workflow n8n cực kỳ đơn giản để tạo một API trả về ảnh chó ngẫu nhiên bằng cách kết hợp Webhook và Dog CEO API."
slug: "lay-anh-cun-ngau-nhien-qua-webhook-n8n"
tags: [n8n, automation, no-code, webhook, api-integration, dog-ceo]
keywords: [n8n workflow, tự động hóa n8n, dog ceo api, webhook n8n, http request n8n, api lay anh cho]
---

# 🚀 Tự động lấy ảnh chú cún ngẫu nhiên qua Webhook với Dog CEO API trong n8n

Các sếp có bao giờ cần một nguồn dữ liệu hình ảnh động vật (cụ thể là những chú cún đáng yêu) để tích hợp vào ứng dụng, chatbot hoặc hệ thống giải trí nội bộ nhưng lại ngại việc phải code từ đầu chưa? Thay vì xây dựng cả một backend phức tạp, chúng ta hoàn toàn có thể dựng nhanh một API endpoint trả về ảnh chó ngẫu nhiên chỉ trong vòng chưa đầy 2 phút với n8n!

Workflow này sẽ giúp các sếp tạo ra một Webhook nhận request, tự động gọi sang **Dog CEO API** công khai và trả về URL hình ảnh ngay lập tức. Giải pháp không-cần-code (no-code) 100% giúp tiết kiệm thời gian và cực kỳ dễ triển khai.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo Custom API riêng biệt:** Sở hữu ngay một Webhook URL có thể nhận request từ bất kỳ hệ thống nào (frontend, Telegram bot, Slack...).
- **Tích hợp dữ liệu mượt mà:** Tự động gọi bên thứ ba (Dog CEO API) và phản hồi dữ liệu JSON chuẩn chỉnh.
- **Nền tảng mở rộng:** Dễ dàng phát triển thêm các tính năng như tải ảnh về, lưu trữ Cloudinary, hoặc gửi ảnh cún vào nhóm chat mỗi sáng.
- **Hoạt động 24/7:** Không lo gián đoạn nếu triển khai trên hạ tầng VPS chuẩn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động (Cloud hoặc Self-hosted đều được).
- **Dog CEO API** hoàn toàn miễn phí và **không yêu cầu API Key**, các sếp chỉ cần bật workflow lên là chạy ngay!
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ JSON của workflow hoặc sử dụng tính năng import có sẵn để đưa 3 nodes cốt lõi vào màn hình làm việc:
- `Trigger Webhook` (Webhook)
- `Fetch Random Dog Image` (HTTP Request)
- `Respond with Image URL` (Respond to Webhook)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này rất gọn nhẹ chỉ gồm 3 nodes, các sếp hãy lưu ý cấu hình từng phần như sau:

- **Node `Trigger Webhook` (Webhook):**
  - Node này lắng nghe các yêu cầu HTTP POST gửi đến. 
  - Đường dẫn (Path) mặc định là `get-dog-image`. Các sếp có thể đổi lại tùy ý (ví dụ: `random-dog`). Không cần truyền thêm body data nào vì mục đích chỉ là lấy ngẫu nhiên.
  
- **Node `Fetch Random Dog Image` (HTTP Request):**
  - Cấu hình phương thức gọi là **GET**.
  - URL gọi API: `https://dog.ceo/api/breeds/image/random`.
  - API này sẽ trả về một JSON object chứa thuộc tính `message` (chính là đường dẫn URL của bức ảnh chú cún).

- **Node `Respond with Image URL` (Respond to Webhook):**
  - Node này nhận dữ liệu từ node HTTP Request phía trước và đẩy kết quả trả về cho người gọi webhook ban đầu. Các sếp có thể tùy biến response dạng JSON hoặc plain text tùy theo nhu cầu tích hợp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và dùng công cụ như Postman, cURL hoặc trình duyệt để bắn thử một request vào Test URL của Webhook.
- Kiểm tra kết quả trả về xem đã nhận được JSON chứa link ảnh chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang chế độ **Active** để đưa workflow vào trạng thái chạy chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "lợi hại" hơn, các sếp có thể mở rộng bằng cách:
1. **Gửi vào Telegram/Slack:** Thêm một node Telegram phía sau để bot tự động gửi ảnh cún vào nhóm làm việc mỗi khi có lệnh `/dog`.
2. **Lưu trữ tự động:** Chèn thêm node Google Drive hoặc S3 để tải bức ảnh đó về lưu trữ thay vì chỉ lấy URL thuần túy.
3. **Bổ sung xác thực:** Thêm Header Authentication vào Webhook để tránh việc endpoint bị các bên khác spam request linh tinh.

### 📌 Kết luận
Một workflow siêu gọn nhẹ nhưng lại cực kỳ hữu ích để làm quen với cơ chế xử lý Webhook và HTTP Request trong n8n. Hãy áp dụng ngay vào hệ thống của các sếp để tự động hóa các tác vụ liên quan đến API bên thứ ba nhé!