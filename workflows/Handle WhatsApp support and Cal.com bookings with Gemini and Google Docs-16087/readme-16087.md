---
title: "🚀 Tự động hóa hỗ trợ khách hàng WhatsApp & Đặt lịch Cal.com với Gemini AI và n8n"
description: "Xây dựng trợ lý ảo thông minh trên WhatsApp tích hợp Google Docs, Cal.com và Gemini AI giúp tự động giải đáp thắc mắc và đặt lịch hẹn 24/7."
slug: "tu-dong-hoa-whatsapp-cal-com-gemini-n8n"
tags: [n8n, automation, no-code, whatsapp, ai-agent, gemini, cal-com]
keywords: [n8n workflow, whatsapp chatbot, cal.com integration, gemini ai n8n, tu dong hoa whatsapp, ai support agent]
---

# 🚀 Tự động hóa hỗ trợ khách hàng WhatsApp & Đặt lịch Cal.com với Gemini AI và n8n

Các sếp có đang gặp tình trạng quá tải tin nhắn trên WhatsApp? Khách hàng liên tục hỏi những câu hỏi lặp đi lặp lại về sản phẩm, dịch vụ và việc đặt lịch hẹn thủ công khiến đội ngũ sales mất quá nhiều thời gian? 

Giải pháp hoàn hảo đây rồi! Workflow n8n này sẽ giúp các sếp xây dựng một **Trợ lý AI thông minh trên WhatsApp** hoạt động 24/7. Hệ thống tự động kiểm tra khung thời gian tin nhắn, tra cứu tài liệu công ty từ Google Docs, trò chuyện thông minh bằng Google Gemini AI, tự động trích xuất thông tin đặt lịch và đẩy thẳng lên Cal.com, đồng thời lưu log tương tác chi tiết vào Google Sheets. Tất cả diễn ra hoàn toàn tự động mà không cần nhân sự can thiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7:** Khách hàng không phải chờ đợi, tăng tỷ lệ chuyển đổi và giữ chân khách hàng trên WhatsApp.
- **Tự động hóa đặt lịch hẹn:** AI tự động phân tích ý định đặt lịch, kiểm tra thông tin và tạo lịch hẹn thành công trên Cal.com.
- **Kiến thức chính xác:** Trả lời dựa trên tài liệu thực tế của công ty (Google Docs), tránh tình trạng AI tự bịa thông tin (hallucination).
- **Quản lý và theo dõi dễ dàng:** Mọi tương tác đều được ghi log tự động vào Google Sheets để báo cáo và chăm sóc lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Meta WhatsApp Cloud API** (Credentials cho Trigger, Send Message và Template Reopen).
- **Google Cloud Account / OAuth2** (Truy cập Google Docs và Google Sheets).
- **Google Gemini API Key** (Cho các node AI Agent và Chat Model).
- **Cal.com API Key / Headers** (Để tạo booking tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ n8n.
- Mở giao diện n8n Editor, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> **Import from File** hoặc **Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các thông số quan trọng sau đây:

- **When WhatsApp Message Received & Send WhatsApp Response:** Cấu hình WhatsApp Cloud API Credentials. Đảm bảo cài đặt đúng template mở lại khung chat 24 giờ (`Send WhatsApp Reopen Message`) khi khách hàng nhắn tin ngoài khung giờ cho phép.
- **Retrieve Company Knowledge (Google Docs):** Kết nối tài khoản Google Docs và trỏ tới file tài liệu chứa kiến thức doanh nghiệp (FAQ, thông tin dịch vụ, chính sách...).
- **Google Chat Model (Booking) & Google Chat Model (Support):** Thêm Google Gemini API Credentials cho 2 mô hình AI Agent (`Booking Information Agent` và `General Support Agent`).
- **Post Cal Booking (HTTP Request):** Cấu hình API Key/Headers của Cal.com, kiểm tra lại payload gửi đi (event type, attendee fields, múi giờ time zone).
- **Append Log to Google Sheets:** Kết nối Google Sheets Credentials và chọn đúng file Google Sheet dùng để lưu log tương tác của khách hàng.
- **Các Code Nodes xử lý dữ liệu:** Kiểm tra lại các đoạn code (`Normalize Message Input`, `Extract Booking Details`, `Normalize Date and Time`...) để đảm bảo định dạng dữ liệu đầu vào/đầu ra khớp với payload thực tế từ WhatsApp và Cal.com.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tin nhắn mẫu qua WhatsApp để test luồng chạy.
- Kiểm tra kết quả trên Google Sheets và Cal.com.
- Nếu mọi thứ hoạt động mượt mà, hãy gạt công tắc sang **Active** để đưa hệ thống vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo nội bộ:** Kết nối thêm node Slack hoặc Telegram để bắn thông báo cho đội ngũ Sales ngay khi có khách hàng đặt lịch thành công qua WhatsApp.
- **Gửi email xác nhận:** Tự động gửi email cảm ơn và lịch hẹn chi tiết cho khách hàng sau khi Cal.com ghi nhận booking thành công.
- **Lưu trữ lịch sử chat dài hạn:** Kết hợp database như PostgreSQL hoặc Supabase thay vì chỉ dùng `Store Simple Memory` để lưu trữ lịch sử hội thoại chi tiết hơn cho từng khách hàng.

### 📌 Kết luận
Việc tự động hóa chăm sóc khách hàng và đặt lịch hẹn trên WhatsApp chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và Gemini AI. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công và mang lại trải nghiệm chuyên nghiệp nhất cho khách hàng của các sếp!