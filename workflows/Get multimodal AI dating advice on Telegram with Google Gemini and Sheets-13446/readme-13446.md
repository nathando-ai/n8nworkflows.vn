---
title: "🚀 Trợ lý AI Hẹn hò Đa phương thức trên Telegram với Google Gemini & Google Sheets"
description: "Xây dựng bot Telegram thông minh sử dụng Google Gemini Vision & Audio để phân tích ảnh chụp màn hình chat, tin nhắn thoại và gợi ý câu trả lời tán tỉnh đỉnh cao."
slug: "tro-ly-ai-hen-ho-telegram-google-gemini-sheets"
tags: [n8n, automation, ai-agent, telegram, google-gemini, google-sheets]
keywords: [n8n workflow, ai dating assistant, telegram bot gemini, google sheets crm, tự động hóa n8n, multimodal ai]
---

# 🚀 Trợ lý AI Hẹn hò Đa phương thức trên Telegram với Google Gemini & Google Sheets

Việc nhắn tin và tìm kiếm cơ hội hẹn hò trên các ứng dụng đôi khi khiến các sếp đau đầu vì không biết phải trả lời thế nào cho duyên dáng, tinh tế mà vẫn giữ được cá tính. Làm sao để phân tích nhanh một bức ảnh chụp màn hình đoạn chat Tinder hoặc nghe một tin nhắn thoại dài dằng dặc từ "crush" mà vẫn đưa ra lời khuyên chiến lược ngay lập tức? 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, biến Telegram bot thành một "quân sư tình yêu" (Wingman) thực thụ, tích hợp AI đa phương thức (xem ảnh, nghe âm thanh), ghi nhớ ngữ cảnh trò chuyện và quản lý danh sách đối tượng (Leads) qua Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phân tích đa phương thức thông minh:** Bot có thể "nhìn" ảnh chụp màn hình chat, "nghe" tin nhắn thoại và "đọc" tin nhắn văn bản gửi tới Telegram.
- **Gợi ý chiến lược đỉnh cao:** Tự động tạo ra 3 lựa chọn trả lời khác nhau (Thoải mái, Hóm hỉnh, Táo bạo) dựa trên phong cách hẹn hò cá nhân hóa của bạn.
- **Bộ nhớ ngữ cảnh & CRM tích hợp:** Ghi nhớ lịch sử trò chuyện và tự động quản lý thông tin đối tượng (Leads) trực tiếp trên Google Sheets.
- **Hoạt động 24/7:** Phản hồi ngay lập tức mọi lúc mọi nơi trực tiếp trên ứng dụng Telegram quen thuộc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Self-hosted hoặc n8n Cloud).
- **Telegram Bot Token:** Tạo bot thông qua `@BotFather` trên Telegram.
- **Google Gemini API Key:** Lấy khóa API từ Google AI Studio để cấp quyền cho các node Google Gemini.
- **Google Sheets Template:** Bản sao Google Sheets quản lý người dùng và leads.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn mã JSON của workflow này và paste trực tiếp vào trình soạn thảo n8n của các sếp, hoặc import file JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số quan trọng sau trong workflow:

- **Telegram Trigger & Send a text message (và các node Telegram khác):** Kết nối với Telegram API Credential sử dụng Bot Token đã tạo từ `@BotFather`.
- **Google Gemini Chat Model & Analyze nodes (Analyze image, Analyze voice message):** Thêm Google Palm/Gemini API Key vào phần Credentials của các node AI này.
- **Get Rizzler Profile & Google Sheets Tools (`create_rizzler_profile`, `search_leads`, `get_lead_history`, `create_new_lead`, `update_profile`, `update_lead`, `Append Log`):** 
  - Copy [Google Sheets Template mẫu tại đây](https://docs.google.com/spreadsheets/d/1JxoahgYNHc6nuWJ-VOsHlEzaKYxnksGFeYA0TKE4lWo/edit?usp=sharing).
  - Kết nối tài khoản Google Sheets OAuth2.
  - Cập nhật lại **Sheet ID** chuẩn của các sếp vào node `Get Rizzler Profile` và các công cụ trong Agent.

#### 3. Kích hoạt ⚡️
- Gửi tin nhắn thử nghiệm (text, ảnh chụp màn hình, hoặc voice note) tới Bot Telegram của bạn.
- Kiểm tra kết quả phản hồi từ AI trên Telegram.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Kết nối thêm node Slack hoặc Telegram channel riêng để log lại các cuộc trò chuyện thú vị hoặc báo cáo thống kê hàng ngày.
- **Tùy chỉnh System Prompt:** Tinh chỉnh prompt trong AI Agent ("Rizz AI") để bot có phong cách trò chuyện hài hước, châm biếm hoặc lịch thiệp hơn theo đúng cá tính của bạn.
- **Mở rộng lưu trữ:** Lưu trữ thêm log tương tác vào cơ sở dữ liệu như PostgreSQL hoặc Airtable để phân tích sâu hơn.

### 📌 Kết luận
Workflow này là minh chứng tuyệt vời cho việc ứng dụng AI Agent đa phương thức vào đời sống hàng ngày và tự động hóa quy trình cá nhân. Hãy triển khai ngay để có một "quân sư tình yêu" AI luôn sẵn sàng hỗ trợ các sếp 24/7 trên Telegram!