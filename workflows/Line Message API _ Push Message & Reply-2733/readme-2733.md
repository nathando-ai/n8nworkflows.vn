---
title: "🚀 Tích hợp Line Message API: Tự động trả lời và Gửi tin nhắn (Push & Reply) trong n8n"
description: "Hướng dẫn cấu hình workflow n8n tích hợp Line Messaging API để tự động nhận tin nhắn, phản hồi bằng Reply Token và chủ động gửi tin nhắn (Push Message) tới người dùng."
slug: "tich-hop-line-message-api-push-reply-n8n"
tags: [n8n, automation, line-api, chatbot, messaging, marketing-automation]
keywords: [n8n workflow, line message api, push message, reply message, line chatbot automation, tự động hóa line]
---

# 🚀 Tự động hóa tương tác khách hàng qua Line Messaging API với n8n

Việc quản lý và chăm sóc khách hàng thủ công trên nền tảng nhắn tin Line (đặc biệt phổ biến tại thị trường Đài Loan, Nhật Bản, Thái Lan) tốn rất nhiều thời gian và dễ bỏ sót tin nhắn. Nếu các sếp đang đau đầu vì phải ngồi rep từng tin nhắn của khách hay muốn chủ động gửi thông báo (Push Message) mà chưa biết bắt đầu từ đâu, thì đây chính là "vũ khí" tự động hóa dành cho các sếp.

Workflow n8n này sẽ giúp các sếp xây dựng một hệ thống xử lý tin nhắn từ Line cực kỳ gọn nhẹ: tự động bắt sự kiện người dùng nhắn đến, phân loại sự kiện và phản hồi lại ngay lập tức, đồng thời hỗ trợ chủ động đẩy tin nhắn (Push Message) khi có Line UID của khách hàng. Giải pháp 100% không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và nhận webhook từ Line liên tục, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì (Auto-reply):** Bot tự động nhận tin nhắn từ người dùng và phản hồi lại chính xác nội dung đó (hoặc thông điệp tùy chỉnh) bằng `replyToken`.
- **Chủ động gửi tin nhắn (Push Message):** Hỗ trợ gửi thông báo, ưu đãi trực tiếp tới từng cá nhân thông qua `Line UID` mà không cần chờ khách nhắn trước.
- **Hoạt động 24/7 không gián đoạn:** Tự động lắng nghe sự kiện từ Line Webhook và xử lý mượt mà trên nền tảng n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **Line Developers** và đã tạo một **Messaging API Channel**.
- Lấy được **Channel Access Token** từ Line Developers Console để cấu hình xác thực.
- Cấu hình Webhook URL trong Line Channel trỏ về n8n Webhook Node của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor, hoặc import file JSON thông qua menu *Add workflow -> Import from File*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính được thiết kế sẵn cho 2 luồng: **Reply Message** và **Push Message**. Các sếp cần chú ý cấu hình các điểm sau:

- **Webhook from Line Message (Node Webhook):** 
  - Node này sẽ cung cấp cho các sếp một Webhook URL. Hãy copy URL này dán vào phần **Webhook URL settings** trên trang quản trị Line Developers của các sếp.
  - Đảm bảo kênh Line của các sếp đã bật tính năng nhận sự kiện (Use webhook).
- **If (Node If):**
  - Dùng để lọc sự kiện. Line bắn về rất nhiều loại sự kiện khác nhau (như follow, unfollow, join...), node này giúp lọc ra đúng sự kiện là tin nhắn văn bản từ người dùng (`message`) để xử lý tiếp.
- **Edit Fields (Node Set):**
  - Nơi các sếp tinh chỉnh nội dung dữ liệu chuẩn bị gửi đi (ví dụ: bóc tách `replyToken`, `userId`, và nội dung tin nhắn người dùng vừa gửi).
- **Line : Reply with token (Node HTTP Request):**
  - Cấu hình phương thức `POST` tới endpoint của Line API: `https://api.line.me/v2/bot/message/reply`.
  - Cần thêm **Credentials** loại `httpHeaderAuth` với Header Name là `Authorization` và Header Value là `Bearer [Channel Access Token của các sếp]`.
- **Line : Push Message (Node HTTP Request):**
  - Dùng để gửi tin nhắn chủ động tới UID cụ thể qua endpoint: `https://api.line.me/v2/bot/message/push`.
  - Yêu cầu các sếp phải thu thập được Line UID của khách hàng trước (lưu trong Database hoặc Google Sheets) và điền vào payload JSON của request này.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** và thử nhắn một tin nhắn vào Official Account Line của các sếp để kiểm tra luồng Webhook -> If -> Reply hoạt động chưa.
- Sau khi test ngon lành, gạt công tắc **Active** ở góc trên bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI Chatbot:** Thay vì chỉ reply lại y hệt nội dung khách nhắn, các sếp có thể cắm thêm OpenAI/Claude Node vào giữa để tạo một trợ lý ảo thông minh tư vấn bán hàng trên Line.
- **Lưu thông tin khách hàng:** Kết hợp thêm Google Sheets hoặc Supabase node để lưu lại `Line UID` và lịch sử chat mỗi khi có người nhắn tin đến.
- **Gửi thông báo đơn hàng:** Kết hợp luồng **Push Message** với WooCommerce/Shopify để tự động gửi thông báo trạng thái đơn hàng (đang giao, đã giao) cho khách hàng qua Line.

### 📌 Kết luận
Việc tích hợp Line Messaging API vào n8n mở ra khả năng tự động hóa chăm sóc khách hàng cực kỳ mạnh mẽ trên các ứng dụng nhắn tin mà không tốn chi phí thuê lập trình viên đắt đỏ. Hãy "lên đồ" ngay cho hệ thống của các sếp thôi nào!