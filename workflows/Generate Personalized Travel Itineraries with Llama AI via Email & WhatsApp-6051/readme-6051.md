---
title: "🚀 Tự động tạo lịch trình du lịch cá nhân hóa với Llama AI, Email và WhatsApp bằng n8n"
description: "Xây dựng hệ thống AI tự động đọc yêu cầu du lịch qua Email hoặc WhatsApp, sử dụng Llama 3.2 để lên lịch trình chi tiết và gửi trả kết quả tự động 100%."
slug: "tao-lich-trinh-du-lich-voi-llama-ai-email-whatsapp"
tags: [n8n, automation, ai-agent, llama, whatsapp, email]
keywords: [n8n workflow, tự động hóa du lịch, Llama AI, Ollama, WhatsApp trigger, Email IMAP SMTP, AI chatbot]
---

# 🚀 Tự động tạo lịch trình du lịch cá nhân hóa với Llama AI, Email và WhatsApp

Các sếp đang vận hành dịch vụ du lịch, lữ hành hay đơn giản là muốn xây dựng một trợ lý ảo thông minh để tự động lên kế hoạch vi vu? Việc phải ngồi đọc từng tin nhắn của khách hàng ("Tôi muốn đi Dubai 5 ngày với bạn bè..."), tra cứu thông tin rồi soạn thảo một lịch trình chi tiết thủ công tốn rất nhiều thời gian và dễ gây quá tải.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ từ **Oneclick AI Squad**. Hệ thống này sẽ tự động nhận yêu cầu từ **Email** hoặc **WhatsApp**, phân tích qua mô hình **Llama AI** (chạy cục bộ qua Ollama) để tạo ra một lịch trình du lịch chi tiết từng ngày, kèm theo gợi ý hoạt động, phương tiện di chuyển, khách sạn, sau đó tự động gửi trả lại đúng kênh mà khách hàng đã nhắn tin đến!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý AI và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đa kênh:** Xử lý yêu cầu thông suốt từ cả Email (IMAP/SMTP) và WhatsApp mà không cần nhân sự can thiệp thủ công.
- **AI thông minh, cá nhân hóa:** Sử dụng Llama 3.2 để hiểu ngữ cảnh, tạo ra lịch trình chi tiết, giọng văn thân thiện, tự nhiên như chuyên gia tư vấn thực thụ.
- **Tiết kiệm 90% thời gian:** Khách hàng nhận được lịch trình chỉ trong vài giây sau khi gửi yêu cầu.
- **Hoạt động 24/7:** Phục vụ khách hàng xuyên ngày đêm, gia tăng tỷ lệ chuyển đổi và chăm sóc khách hàng chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyến nghị bản Self-hosted để kết nối mượt mà với Ollama).
- **Ollama:** Đã cài đặt Ollama chạy mô hình `llama3.2-16000:latest` (hoặc model tương đương).
- **Tài khoản Email (IMAP/SMTP):** Dùng để nhận yêu cầu và gửi phản hồi qua email.
- **WhatsApp Business API / WhatsApp Trigger API:** Tài khoản Meta Business hoặc cấu hình WhatsApp API để nhận/gửi tin nhắn tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Get Query from Email (`emailReadImap`) & Sending Itinery from Email (`emailSend`):**
  - Cấu hình thông tin đăng nhập IMAP (để đọc mail đến) và SMTP (để gửi mail đi).
  - Đảm bảo hòm thư kết nối hoạt động ổn định và có quyền truy cập ứng dụng kém bảo mật hoặc App Password (nếu dùng Gmail).
- **Get Query from WhatsApp (`whatsAppTrigger`) & Send Itinery from message (`whatsApp`):**
  - Kết nối `whatsAppTriggerApi` và `whatsAppApi` bằng cách điền thông số từ Meta for Developers (Access Token, Phone Number ID, Webhook Verify Token).
- **Agent (`lmOllama`):**
  - Chọn credentials kết nối đến Ollama server của các sếp.
  - Tại mục `model`, điền chính xác tên model đang chạy, ví dụ: `llama3.2-16000:latest`.
- **Itinerary Creator Agent (`chainLlm`):**
  - Thiết lập Prompt hệ thống (System Prompt) để hướng dẫn AI cách đóng vai trò là một chuyên gia tư vấn du lịch nhiệt tình, xuất ra định dạng rõ ràng (Ngày 1, Ngày 2, Địa điểm, Khách sạn...).
- **Check Proper Data (`set`) & Check where to send Answer (`if`):**
  - Kiểm tra logic điều kiện để phân luồng dữ liệu: Nếu yêu cầu đến từ Email thì kích hoạt node gửi Email, nếu đến từ WhatsApp thì điều hướng sang node gửi tin nhắn WhatsApp tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một email hoặc tin nhắn WhatsApp giả lập với nội dung kiểu: *"Mình muốn đi Bangkok 4 ngày với người yêu, ngân sách tầm trung"*.
- Kiểm tra xem AI có sinh ra lịch trình chuẩn xác không và hệ thống có tự động gửi trả lại đúng kênh hay không.
- Nếu mọi thứ mượt mà, hãy bật công tắc **Active** góc trên cùng bên phải để workflow chính thức chạy tự động 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ lịch sử khách hàng:** Kết nối thêm node **Google Sheets** hoặc **Supabase** ngay sau bước nhận yêu cầu để lưu lại thông tin khách hàng, phục vụ cho việcRemarketing sau này.
- **Tích hợp thêm kênh chat khác:** Có thể mở rộng workflow bằng cách gắn thêm trigger của Telegram hoặc Facebook Messenger, đưa dữ liệu vào chung một Agent xử lý.
- **Gửi kèm file PDF:** Sử dụng node chuyển đổi văn bản sang PDF để gửi kèm lịch trình sang trọng hơn qua email cho khách hàng.

### 📌 Kết luận
Workflow tạo lịch trình du lịch tự động với Llama AI, Email và WhatsApp là mảnh ghép hoàn hảo giúp các doanh nghiệp lữ hành tối ưu hóa quy trình chăm sóc khách hàng và bán hàng thời đại số. Hãy triển khai ngay hôm nay để biến trợ lý ảo thành "vũ khí bí mật" gia tăng doanh thu cho các sếp!