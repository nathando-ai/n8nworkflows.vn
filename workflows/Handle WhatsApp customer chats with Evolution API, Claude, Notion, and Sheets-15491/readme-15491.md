---
title: "🚀 Xây dựng Trợ lý WhatsApp AI tự động hoàn chỉnh với Evolution API, Claude & Notion CRM"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa chăm sóc khách hàng trên WhatsApp 24/7 bằng AI Claude, tích hợp Notion CRM, Google Sheets và Telegram."
slug: "whatsapp-ai-chatbot-evolution-api-claude-notion"
tags: [n8n, automation, no-code, whatsapp, ai-chatbot, notion, claude]
keywords: [n8n workflow, tự động hóa whatsapp, evolution api, claude ai, notion crm, chatbot thông minh]
---

# 🚀 Xây dựng Trợ lý WhatsApp AI tự động hoàn chỉnh với Evolution API, Claude & Notion CRM

Các sếp kinh doanh, dịch vụ hoặc agency chắc chắn hiểu cảm giác mệt mỏi khi phải túc trực 24/7 để trả lời tin nhắn WhatsApp của khách hàng. Việc trả lời thủ công không chỉ tốn thời gian mà còn dễ bỏ lỡ khách hàng tiềm năng vào ban đêm hay giờ nghỉ. 

Giải pháp ư? Sử dụng ngay workflow n8n cực đỉnh này để biến số WhatsApp Business của các sếp thành một trợ lý AI thực thụ: xử lý cả **tin nhắn văn bản lẫn tin nhắn thoại**, tự động tra cứu khách hàng trong **Notion CRM**, tạo câu trả lời thông minh bằng **Claude**, tự động chuyển giao cho nhân viên qua **Telegram** khi cần, và đồng bộ dữ liệu mượt mà. Tất cả hoàn toàn tự động và không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi 24/7 tức thì:** Khách nhắn tin là AI trả lời ngay lập tức dựa trên kho tri thức (FAQs, Sản phẩm) có sẵn.
- **Xử lý cả tin nhắn thoại:** Tự động chuyển đổi file ghi âm thành văn bản (nhờ Whisper) để AI đọc và phản hồi.
- **Quản lý CRM tự động:** Tự động tạo lead mới trên Notion hoặc cập nhật trạng thái tương tác của khách hàng cũ.
- **Chuyển giao thông minh (Handoff):** Khi gặp khách hàng khó tính hoặc có ý định mua hàng cao, bot tự động dừng và báo cáo qua Telegram để nhân viên tiếp quản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Evolution API Instance:** (URL + API Key) để kết nối WhatsApp.
- **Anthropic API Key:** Dùng mô hình Claude Haiku cho AI xử lý ngữ cảnh và tạo phản hồi.
- **OpenAI API Key:** Dùng cho mô hình Whisper để transcribe tin nhắn thoại (có thể bỏ qua nếu không dùng voice).
- **Google Sheets:** Lưu trữ kho tri thức (Business Info, Products, FAQs) và log hội thoại.
- **Notion API:** Quản lý CRM và trạng thái của Bot (`WA ChatBot Status`).
- **Telegram Bot Token & Chat ID:** Nhận thông báo khi cần chuyển giao cho người thật.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp (hoặc copy toàn bộ JSON và paste trực tiếp vào không gian làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 38 nodes được sắp xếp logic qua 5 giai đoạn chính. Các sếp cần cấu hình kỹ các điểm sau:

- **Evolution Webhook1:** Cấu hình Webhook URL `https://YOUR-N8N-DOMAIN/webhook/evo-inbound`. Đảm bảo cấu hình sự kiện `MESSAGES_UPSERT` và bật `Webhook Base64` để hỗ trợ tin nhắn thoại.
- **Transcribe Audio1 & Sentiment Analysis1 / Generate Response1:** Kết nối tài khoản OpenAI (cho Whisper) và Anthropic (cho Claude Haiku).
- **Read Business Info1, Read Products1, Read FAQs1, Log Conversation1:** Kết nối tài khoản Google Sheets OAuth của các sếp và trỏ đến [Google Sheets knowledge base template](https://docs.google.com/spreadsheets/d/1O1hSVLTL-yfugolm_y22-67lV0i59R0sRM0UPPq2Dlk/edit?usp=sharing) (gồm 3 tab: `Business_Info`, `Products`, `FAQs`).
- **Check Leads1, Create a New Lead1, Update LeadStatus1, Pause ChatBot1:** Kết nối Notion API và liên kết với [Notion CRM template](https://cifral.gumroad.com/l/notion-crm-template) để hệ thống tự động đọc/ghi dữ liệu khách hàng.
- **Send WhatsApp Reply (Evolution)1:** Trỏ URL đến instance Evolution API của các sếp dạng `https://YOUR-EVOLUTION-DOMAIN/message/sendText/YOUR-INSTANCE-NAME` và điền Header `apikey`.
- **Alert Owner (Telegram)1:** Kết nối Bot Telegram để nhận cảnh báo khi khách hàng cần hỗ trợ từ con người.

#### 3. Kích hoạt ⚡️
- Thực hiện test thử một tin nhắn mẫu qua WhatsApp để kiểm tra luồng chạy từ Nhận tin nhắn -> Xử lý AI -> Gửi phản hồi -> Lưu Log.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải màn hình n8n.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy biến System Prompt:** Trong node `Generate Response1`, hãy tinh chỉnh lại System Prompt để bot nói chuyện đúng văn phong, ngôn ngữ thương hiệu của công ty các sếp.
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Telegram, các sếp có thể kết nối thêm node Slack hoặc Discord để đội ngũ sales nhận thông báo lead mới ngay lập tức.
- **Quản lý trạng thái Bot:** Nếu muốn bot tiếp tục trò chuyện với một khách hàng đã bị pause trước đó, chỉ cần đổi trạng thái `WA ChatBot Status` trong Notion về lại `Active`.

### 📌 Kết luận
Với workflow này, các sếp đã sở hữu một hệ thống chăm sóc khách hàng tự động hóa đỉnh cao trên WhatsApp, tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần và không bao giờ bỏ lỡ bất kỳ cơ hội chốt đơn nào nữa. Triển khai ngay thôi các sếp ơi!