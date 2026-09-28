---
title: "🚀 Tự động chuyển tiếp Email quan trọng từ Gmail sang Telegram Chat với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động lọc và chuyển tiếp email quan trọng từ Gmail (như Urgent, Server Down) trực tiếp đến Telegram chat theo thời gian thực."
slug: "tu-dong-chuyen-tiep-email-gmail-sang-telegram-n8n"
tags: [n8n, automation, no-code, gmail, telegram, it-ops]
keywords: [n8n workflow, tự động hóa gmail, gửi email qua telegram, lọc email quan trọng, n8n gmail trigger]
---

# 🚀 Tự động chuyển tiếp Email quan trọng từ Gmail sang Telegram Chat

Các sếp có bao giờ cảm thấy mệt mỏi vì phải liên tục mở hộp thư Gmail để kiểm tra xem có email khẩn cấp từ khách hàng, cảnh báo từ hệ thống server hay không? Việc kiểm tra thủ công này vừa tốn thời gian, vừa dễ bỏ lỡ các thông tin cốt lõi giữa hàng trăm email rác mỗi ngày.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: Lắng nghe hộp thư Gmail, lọc ra các email có chứa từ khóa quan trọng (như "Urgent", "Server Down", "Lỗi hệ thống"...), và bắn ngay một tin nhắn được định dạng đẹp mắt trực tiếp vào Telegram chat của các sếp hoặc đội ngũ kỹ thuật. Không cần code phức tạp, setup một lần chạy mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cảnh báo tức thì (Real-time):** Nhận ngay thông báo qua Telegram ngay khi email quan trọng vừa đến hộp thư.
- **Lọc bỏ nhiễu:** Chỉ nhận các email thực sự cần thiết dựa trên từ khóa tùy chỉnh, tránh bị spam thông báo.
- **Tiết kiệm thời gian:** Không cần túc trực trên ứng dụng email, tập trung tối đa cho công việc chuyên môn.
- **Bảo mật & Chủ động:** Dữ liệu chạy trực tiếp trên hệ thống của các sếp thông qua n8n self-hosted.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Tài khoản Google (Gmail):** Để cấp quyền OAuth2 cho n8n đọc email.
- **Telegram Bot:** Tạo một Bot thông qua `@BotFather` trên Telegram để lấy **Bot Token** và biết **Chat ID** nhận tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác 3 nodes sau:

- **Incoming Email Monitor (`gmailTrigger`):**
  - Kết nối tài khoản Gmail của các sếp bằng **Gmail OAuth2**.
  - Thiết lập các bộ lọc cơ bản (nếu muốn) để n8n chỉ bắt những email chưa đọc hoặc từ một gửi cụ thể.

- **Email Validation Check (`if`):**
  - Cấu hình điều kiện kiểm tra tiêu đề email (Subject) hoặc nội dung.
  - Ví dụ: Đặt điều kiện nếu Subject chứa từ khóa `"Urgent"` hoặc `"Server Down"` thì nhánh điều kiện sẽ đi tiếp sang bước gửi tin nhắn.

- **Send Telegram Message (`telegram`):**
  - Kết nối **Telegram Bot Credentials** (điền Bot Token đã lấy từ BotFather).
  - Điền **Chat ID** của cá nhân hoặc nhóm Telegram muốn nhận thông báo.
  - Tùy chỉnh nội dung tin nhắn (Message) bằng cách kéo thả các biến từ node Gmail sang như: Người gửi (`Sender`), Tiêu đề (`Subject`), và Nội dung tóm tắt (`Snippet/Body`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Node** ở từng bước để test thử với dữ liệu email mẫu gần nhất.
- Khi mọi thứ đã chạy mượt mà, gạt công tắc sang **Active** để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Telegram, các sếp có thể gắn thêm node Slack, Discord hoặc Zalo ZNS để gửi thông báo đa kênh cùng lúc cho đội ngũ.
- **Lưu trữ lịch sử:** Thêm một node Google Sheets hoặc Notion ở cuối luồng để lưu lại toàn bộ các email khẩn cấp đã được xử lý, tiện cho việc thống kê báo cáo cuối tuần.
- **Gắn nhãn tự động:** Thêm node Gmail ở bước cuối để tự động đánh dấu "Đã xử lý" hoặc gán nhãn màu đỏ cho các email khẩn cấp đó.

### 📌 Kết luận
Chỉ với 3 nodes đơn giản trong n8n, các sếp đã xây dựng thành công một hệ thống cảnh báo thông minh, giúp không bao giờ bỏ lỡ các email quan trọng từ khách hàng hay hệ thống. Chúc các sếp cài đặt thành công và tối ưu hóa quy trình làm việc!