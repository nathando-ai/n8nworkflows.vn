---
title: "🚀 Gửi Email Gmail với Bí Danh (Alias) và Đính Kèm Tệp Tự Động qua API trong n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động hóa việc gửi email từ tài khoản Gmail sử dụng custom alias và đính kèm file linh hoạt thông qua Webhook."
slug: "gui-email-gmail-voi-alias-va-dinh-kem-qua-api-n8n"
tags: [n8n, automation, gmail, api, productivity]
keywords: [n8n workflow, gửi email gmail alias, n8n webhook gmail, tự động hóa gửi email n8n]
keywords: [n8n workflow, gửi email gmail alias, n8n webhook gmail, tự động hóa gửi email n8n]
---

# 🚀 Tự Động Hóa Gửi Email Gmail qua API với Custom Alias và Đính Kèm Tệp

Các sếp có bao giờ gặp khó khăn khi cần tích hợp hệ thống CRM, form website hoặc ứng dụng bên ngoài để gửi email thông qua tài khoản Gmail cá nhân/doanh nghiệp, nhưng lại muốn **sử dụng một địa chỉ email bí danh (Alias)** và **đính kèm file động** không? Mặc dù Gmail Node mặc định rất hữu ích, nhưng việc tùy biến sâu các tham số như Send-as Alias hay xử lý file đính kèm từ URL bên ngoài đôi khi bị giới hạn.

Giải pháp hoàn hảo cho các sếp đây! Workflow n8n này sẽ giúp các sếp nhận yêu cầu qua Webhook, xử lý định dạng payload phức tạp, tải file đính kèm và gửi đi một cách mượt mà thông qua Gmail API.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tùy biến Alias linh hoạt**: Gửi email đi nhưng hiển thị dưới một tên miền hoặc địa chỉ email thay thế đã cấu hình sẵn trong Gmail.
- **Xử lý file đính kèm tự động**: Tự động tải xuống các tệp đính kèm từ URL công khai và mã hóa chuẩn MIME để gửi qua API.
- **Tích hợp API mạnh mẽ**: Nhận trigger từ bất kỳ hệ thống nào (CRM, Webhook, Form) để kích hoạt gửi email ngay lập tức.
- **Hoạt động 24/7**: Đảm bảo mọi thông báo, chiến dịch hoặc email giao dịch được gửi đi chính xác, không bỏ sót.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google (Gmail)** đã được cấp quyền OAuth2 để kết nối với n8n.
- Đã thiết lập sẵn địa chỉ email Alias trong phần cài đặt tài khoản Gmail của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép mã JSON của workflow từ nguồn gốc hoặc sử dụng file JSON được cung cấp, sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes hoạt động phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình các node sau:

- **Webhook Trigger**: 
  - Đóng vai trò là điểm tiếp nhận dữ liệu đầu vào (POST request).
  - Cần lấy URL của Webhook này để cấu hình ở các hệ thống bên ngoài gửi dữ liệu đến.
  - Payload gửi lên cần chứa các trường cơ bản như: `to`, `subject`, `body`, `alias` (địa chỉ email alias), và mảng `attachments` (danh sách URL file đính kèm nếu có).

- **Format Email Payload (Code Node)**: 
  - Node này dùng ngôn ngữ JavaScript để đóng gói dữ liệu đầu vào thành định dạng chuẩn MIME mà Gmail API yêu cầu (bao gồm mã hóa base64URL). Các sếp giữ nguyên code logic tại đây trừ khi muốn tùy chỉnh cấu trúc HTML của email.

- **If Attachments & Split Out Attachments**: 
  - Kiểm tra xem request có kèm theo file nào không. Nếu có, node `Split Out Attachments` sẽ tách từng file để xử lý riêng biệt.

- **Download Attachments (HTTP Request)**: 
  - Thực hiện tải nội dung file từ các URL công khai được truyền vào trong payload.

- **Send Gmail as Alias (HTTP Request)**: 
  - Node quan trọng nhất sử dụng **Gmail OAuth2 Credentials**.
  - Gọi trực tiếp đến Google Gmail API (`users/me/messages/send`) thay vì dùng node Gmail thông thường, cho phép truyền linh hoạt header `From` là email Alias của các sếp.

#### 3. Kích hoạt ⚡️
- Gửi một request mẫu (dùng Postman, cURL hoặc n8n Test node) vào Webhook Trigger để kiểm tra luồng chạy.
- Kiểm tra hộp thư đến xem email đã được gửi đi đúng địa chỉ Alias và nhận kèm file đính kèm chưa.
- Bật công tắc **Active** workflow để chạy tự động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack**: Thêm một node thông báo qua Telegram hoặc Slack mỗi khi email được gửi thành công hoặc gặp lỗi.
- **Lưu Log vào Google Sheets**: Tạo thêm một bước ghi nhận lịch sử gửi email (Người nhận, Tiêu đề, Thời gian) vào Google Sheets để dễ dàng tra cứu.
- **Xử lý lỗi (Error Handling)**: Thêm Error Trigger để bắt sự cố nếu token Gmail hết hạn hoặc link file đính kèm bị lỗi, tránh làm gián đoạn hệ thống.

### 📌 Kết luận
Workflow "Send Gmail Messages with Custom Aliases and Attachments via API" là một giải pháp cực kỳ mạnh mẽ giúp vượt qua các giới hạn thông thường của nợ-code, mang lại khả năng tùy biến email chuyên nghiệp cho doanh nghiệp của các sếp. Hãy cài đặt ngay để tối ưu hóa quy trình vận hành!