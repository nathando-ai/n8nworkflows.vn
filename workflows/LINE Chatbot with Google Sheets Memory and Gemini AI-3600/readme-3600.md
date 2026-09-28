---
title: "🚀 Xây dựng LINE Chatbot thông minh với Bộ nhớ Google Sheets và Gemini AI"
description: "Hướng dẫn xây dựng LINE Chatbot tự động trả lời tin nhắn sử dụng Google Gemini AI kết hợp Google Sheets làm bộ nhớ lịch sử trò chuyện dài hạn qua n8n."
slug: "line-chatbot-google-sheets-gemini-ai"
tags: [n8n, automation, no-code, line-chatbot, google-sheets, google-gemini, ai-agent]
keywords: [n8n workflow, line chatbot, google sheets memory, gemini ai, tu dong hoa chat, ai agent n8n]
---

# 🚀 Xây dựng LINE Chatbot thông minh với Bộ nhớ Google Sheets và Gemini AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải trả lời những câu hỏi lặp đi lặp lại từ khách hàng trên ứng dụng nhắn tin LINE? Việc phải túc trực 24/7 để chăm sóc khách hàng không chỉ tốn thời gian mà còn làm gián đoạn các công việc chiến lược khác. 

Hôm nay, em xin giới thiệu một giải pháp tự động hóa 100% không cần code (No-Code): **LINE Chatbot tích hợp Google Gemini AI và Google Sheets**. Bot này không chỉ thông minh nhờ AI mà còn có "trí nhớ" để ghi nhớ ngữ cảnh trò chuyện trước đó của khách hàng, giúp cuộc hội thoại trở nên tự nhiên như người thật!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa chăm sóc khách hàng 24/7**: Phản hồi tin nhắn trên LINE Official Account ngay lập tức bất kể ngày đêm.
- **Trí nhớ dài hạn thông minh**: Bot đọc và lưu lịch sử chat vào Google Sheets, giúp AI hiểu được ngữ cảnh các câu hỏi trước đó.
- **Tiết kiệm 80% thời gian**: Giảm tải áp lực cho đội ngũ support, tập trung vào các khách hàng tiềm năng cao.
- **Vận hành trơn tru, không cần code**: Dễ dàng chỉnh sửa kịch bản, prompt của AI theo ý muốn chỉ với vài thao tác kéo thả trong n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **LINE Official Account (LINE OA)** và Developer Console để lấy Channel Access Token và Webhook URL.
- **Google Cloud Account** để lấy API Key cho **Google Gemini (Google Palm API)**.
- **Google Sheets** chứa sẵn một file định dạng sẵn để làm bộ nhớ lưu lịch sử chat.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình. Workflow bao gồm 9 nodes chính phối hợp nhịp nhàng với nhau.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Node Webhook**: 
  - Cấu hình đường dẫn (Path) ví dụ: `guitarpa` với phương thức `POST`. Đây là điểm nhận dữ liệu từ LINE Official Account gửi tới.
- **Node Get History (Google Sheets)**: 
  - Kết nối tài khoản `Google Sheets OAuth2 API`.
  - Chọn đúng file Google Sheets và Sheet lưu lịch sử trò chuyện của người dùng.
- **Node Prepare Prompt (Edit Fields) & Split History (Code)**: 
  - Xử lý dữ liệu đầu vào từ LINE, làm sạch và chuẩn bị câu lệnh (Prompt) kết hợp với lịch sử chat cũ (`"{{ $json.Prompt }}"`) để gửi cho AI.
- **Node AI Agent & Google Gemini Chat Model**: 
  - Chọn credentials `Google Palm API` cho Gemini.
  - Thiết lập vai trò (System Prompt) cho AI Agent để chatbot phản hồi đúng văn phong thương hiệu của các sếp.
- **Node Save History (Google Sheets)**: 
  - Sử dụng tính năng `appendOrUpdate` để lưu lại câu hỏi của khách hàng và câu trả lời của AI vào Google Sheets, làm cơ sở cho lần chat tiếp theo.
- **Node HTTP Request**: 
  - Cấu hình gửi phản hồi ngược lại về API của LINE Official Account để tin nhắn hiển thị đến thiết bị của khách hàng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một tin nhắn thử nghiệm qua LINE OA để kiểm tra luồng dữ liệu.
- Sau khi test thành công, bật công tắc **Active** để chatbot chính thức đi vào hoạt động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo**: Nối thêm node Telegram hoặc Slack để nhận thông báo mỗi khi có khách hàng VIP nhắn tin cho chatbot.
- **Ghi log nâng cao**: Lưu trữ thêm thông tin phân tích cảm xúc (Sentiment Analysis) của khách hàng vào một sheet riêng để đội ngũ sales nắm bắt tâm lý.
- **Cá nhân hóa nội dung**: Tùy biến prompt của Gemini AI để chatbot nói chuyện theo các phong cách khác nhau (hài hước, trang trọng, chuyên gia tư vấn...).

### 📌 Kết luận
Việc tích hợp LINE Chatbot với Gemini AI và Google Sheets qua n8n là một bài toán tự động hóa cực kỳ hiệu quả, giúp nâng tầm trải nghiệm khách hàng với chi phí tối thiểu. Chúc các sếp "lên đồ" thành công và hẹn gặp lại ở các bài hướng dẫn tiếp theo!