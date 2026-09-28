---
title: "🚀 Xây dựng Lễ tân khách sạn AI trên WhatsApp với n8n, Gemini, Redis và Google Sheets"
description: "Tự động hóa hoàn toàn quy trình chăm sóc khách hàng khách sạn qua WhatsApp bằng AI Agent, kết nối cơ sở dữ liệu MySQL, Google Sheets và phân phối tải thông minh với Redis."
slug: "le-tan-khach-san-ai-whatsapp-gemini-redis-google-sheets"
tags: [n8n, automation, ai-chatbot, whatsapp, google-gemini, redis, mysql]
keywords: [n8n workflow, chatbot khách sạn, whatsapp ai agent, google gemini model switching, redis n8n, tự động hóa khách sạn]
---

# 🚀 Xây dựng Lễ tân khách sạn AI trên WhatsApp với n8n, Gemini, Redis và Google Sheets

Các sếp làm trong ngành khách sạn, lưu trú chắc hẳn luôn đau đầu với việc khách hàng nhắn tin hỏi phòng trống, giá cả, giờ check-in/check-out liên tục 24/7. Trả lời thủ công thì tốn nhân sự, mà chậm trễ một chút là mất khách vào tay đối thủ. 

Giải pháp tuyệt vời cho các sếp đây: một hệ thống **Lễ tân khách sạn AI chạy tự động 100% trên WhatsApp**, kết hợp sức mạnh của AI Agent (Google Gemini), cơ sở dữ liệu MySQL, Google Sheets và hệ thống phân tải thông minh bằng Redis. Không cần code phức tạp, các sếp chỉ cần import workflow n8n này và "lên đồ" là hệ thống tự động chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý mượt mà các cuộc trò chuyện của khách hàng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7:** Khách hỏi lúc nửa đêm hay sáng sớm đều nhận được câu trả lời chính xác trong tích tắc qua WhatsApp.
- **Tối ưu chi phí & Tải hệ thống:** Ứng dụng Redis để phân phối người dùng qua nhiều mô hình Gemini khác nhau, giúp giảm quá tải API và tiết kiệm chi phí vận hành.
- **Dữ liệu thời gian thực:** AI tự động tra cứu tình trạng phòng trống, thông tin đặt phòng từ MySQL và bảng giá từ Google Sheets cực kỳ chính xác.
- **Bảo mật & An toàn:** Hệ thống chỉ cho phép truy vấn dữ liệu (Read-only SQL), tuyệt đối không lo bị ghi đè hay xóa nhầm dữ liệu doanh nghiệp.
:::

### 🇾êu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Meta WhatsApp Business API** (Node WhatsApp Trigger & Send message).
- **Google Cloud / Google AI Studio API Key** (Cho Google Gemini Chat Model).
- **Redis Server** (Để lưu trữ phiên làm việc và phân phối model cho người dùng).
- **MySQL Database** (Lưu trữ thông tin phòng, đặt phòng, check-in của khách).
- **Google Sheets** (Lưu bảng giá phòng, dịch vụ đi kèm).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo một workflow mới và copy/paste toàn bộ mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node cốt lõi sau đây để kết nối hệ thống của mình:

- **WhatsApp Trigger & Send message:** Kết nối tài khoản WhatsApp Business API chính chủ của khách sạn để nhận tin nhắn từ khách và gửi tin nhắn phản hồi tự động.
- **Google Gemini Chat Model & Google Gemini Chat Model1:** Thêm Google AI API Key để cung cấp "bộ não" thông minh cho AI Agent.
- **Check User Number & Store User Number (Redis Nodes):** Cấu hình kết nối Redis để hệ thống lưu trữ và theo dõi xem khách hàng đang được gán cho mô hình AI nào (Model 0 hoặc Model 1) với thờiGian sống (TTL) là 1 giờ.
- **Execute a SQL query in MySQL (MySQL Tool):** Kết nối tới cơ sở dữ liệu MySQL của khách sạn. *Lưu ý: Thiết lập quyền truy vấn an toàn (chỉ cho phép câu lệnh `SELECT`).*
- **Pricing (Google Sheets Tool):** Kết nối tài khoản Google Sheets và trỏ tới file Google Sheet chứa thông tin bảng giá phòng của khách sạn.
- **Model Decider & Choose Model:** Kiểm tra logic chuyển đổi mô hình AI để phân phối tải người dùng hiệu quả.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử dùng tài khoản WhatsApp cá nhân nhắn tin test thử (ví dụ: *"Bên mình còn phòng trống loại Deluxe vào cuối tuần này không?"*).
- Kiểm tra kết quả trả về và sau khi mọi thứ mượt mà, hãy bật nút **Active** để hệ thống chính thức hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo nhân sự:** Thêm node gửi cảnh báo qua Telegram/Slack cho quản lý khách sạn khi có một booking lớn thành công hoặc khi khách có yêu cầu đặc biệt.
- **Ghi log cuộc trò chuyện:** Lưu trữ lịch sử chat của khách hàng vào một Google Sheet riêng hoặc cơ sở dữ liệu để phục vụ việc phân tích nhu cầu và chăm sóc khách hàng sau lưu trú.
- **Đa ngôn ngữ:** Cấu hình thêm prompt cho AI Agent để tự động nhận diện ngôn ngữ của khách (Tiếng Anh, Trung, Hàn, Nhật...) và phản hồi tương ứng.

### 📌 Kết luận
Workflow "Hotel Receptionist with WhatsApp, Gemini Model-Switching, Redis & Google Sheets" là một giải pháp tự động hóa toàn diện, giúp nâng tầm trải nghiệm dịch vụ khách sạn lên một đẳng cấp mới với chi phí tối ưu nhất. Hãy cài đặt ngay hôm nay để tối ưu hóa vận hành cho khách sạn của các sếp!