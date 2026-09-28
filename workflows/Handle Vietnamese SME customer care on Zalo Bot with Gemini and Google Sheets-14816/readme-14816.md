---
title: "🚀 Xây dựng Chatbot Chăm sóc Khách hàng Zalo tự động cho SME Việt Nam với Gemini AI và Google Sheets"
description: "Tự động hóa hoàn toàn quy trình chăm sóc khách hàng trên Zalo OA/Bot sử dụng n8n, Google Gemini AI và Google Sheets CRM mà không cần code."
slug: "chatbot-cskh-zalo-gemini-google-sheets-n8n"
tags: [n8n, automation, zalo-bot, google-gemini, google-sheets, ai-chatbot]
keywords: [n8n workflow, zalo bot ai, chăm sóc khách hàng zalo, gemini ai n8n, google sheets crm, tự động hóa zalo]
---

# 🚀 Xây dựng Chatbot Chăm sóc Khách hàng Zalo tự động cho SME Việt Nam với Gemini AI và Google Sheets

Các doanh nghiệp SME Việt Nam thường gặp khó khăn khi số lượng tin nhắn từ khách hàng trên Zalo ngày càng tăng cao. Việc phản hồi thủ công chậm trễ dễ khiến khách hàng bỏ đi, trong khi việc thuê đội ngũ trực chat 24/7 tốn kém chi phí. 

Workflow n8n này từ **THE NEXOVA** chính là giải pháp tự động hóa 100% không cần code, giúp doanh nghiệp tích hợp Zalo Bot với trí tuệ nhân tạo Google Gemini và Google Sheets CRM để chăm sóc khách hàng chuyên nghiệp, thông minh và tiết kiệm tối đa nguồn lực.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và hỗ trợ cài đặt các community node, các sếp nên cài n8n trên VPS riêng (Self-hosted). Lưu ý rằng workflow này sử dụng community node nên **không thể chạy trên n8n Cloud**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7:** Phản hồi tin nhắn của khách hàng tức thì bất kể ngày đêm, kể cả ngoài giờ hành chính.
- **Cá nhân hóa thông minh:** Tự động nhận diện khách hàng mới, gửi lời chào kèm sticker và lưu thông tin vào Google Sheets CRM.
- **AI hiểu tiếng Việt sắc bén:** Sử dụng Google Gemini để giải đáp các câu hỏi phức tạp bằng ngữ cảnh tự nhiên, thân thiện.
- **Chuyển giao nhân sự (Escalation):** Tự động nhận diện khi khách hàng cần gặp người thật và ghi log để nhân viên xử lý kịp thời.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Self-hosted instance** (bắt buộc để cài community node).
- **Zalo Bot Token** (tạo qua Zalo Bot Manager trong ứng dụng Zalo).
- **Google AI Studio API Key** (tạo tài khoản miễn phí để dùng Google Gemini).
- **Google Sheets Template** (sử dụng mẫu CRM được cung cấp sẵn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON dán vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 20 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình các phần sau:

- **Cài đặt Community Node:** Vào **Settings > Community Nodes** trên n8n và cài đặt gói `n8n-nodes-zalo-platform`.
- **Receive Zalo Message (`n8n-nodes-zalo-platform.zaloBotTrigger`):** Kết nối với tài khoản Zalo Bot thông qua `zaloBotApi` credentials.
- **Set Configuration (`set`):** Điền `googleSheetId` của sếp, cùng với cấu hình tên doanh nghiệp, URL ảnh sản phẩm, bảng giá và số hotline.
- **Lookup Customer in CRM, Append New Customer, Log Escalation, Log Conversation (`googleSheets`):** Kết nối bằng Google Sheets credentials (`googleApi`) và trỏ tới file CRM chuẩn.
- **Google Sheets CRM Template:** 
  - Truy cập [Google Sheets CRM Template](https://docs.google.com/spreadsheets/d/1e9155FKWikWTADXWssAdYvOq7g8l3N4NvhnxQXo9EFc/edit?usp=sharing) và chọn **File > Make a copy**.
  - Copy Sheet ID từ URL (đoạn nằm giữa `/d/` và `/edit`) dán vào node **Set Configuration**.
  - Template đã có sẵn 2 tab: `Customers` (quản lý thông tin khách hàng) và `Conversations` (lưu lịch sử chat, intent và phản hồi của AI/bot).
- **Gemini AI Reply (`googleGemini`):** Cấu hình Google Palm/Gemini API key để AI xử lý các câu hỏi nằm ngoài danh sách từ khóa cố định.

#### 3. Kích hoạt ⚡️
- Gửi tin nhắn test thử nghiệm qua Zalo Bot để kiểm tra luồng nhận tin, ghi CRM và phản hồi từ Gemini.
- Bật công tắc **Active** để workflow chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kịch bản:** Bổ sung thêm các nhánh trong node **Detect Intent** (như đặt lịch hẹn, kiểm tra đơn hàng, chính sách đổi trả).
- **Tích hợp thông báo:** Kết nối thêm node Telegram hoặc Slack để gửi cảnh báo ngay lập tức cho đội ngũ sales khi có khách hàng yêu cầu gặp nhân viên (`human_escalation`).
- **Nâng cấp AI:** Dễ dàng thay thế Google Gemini bằng OpenAI GPT-4o hoặc Anthropic Claude tùy theo nhu cầu và ngân sách của doanh nghiệp.

### 📌 Kết luận
Việc tự động hóa chăm sóc khách hàng trên Zalo chưa bao giờ dễ dàng đến thế với sự kết hợp của n8n, Gemini AI và Google Sheets. Hãy áp dụng ngay workflow này để tối ưu hóa vận hành và bứt phá doanh số cho doanh nghiệp SME của các sếp!