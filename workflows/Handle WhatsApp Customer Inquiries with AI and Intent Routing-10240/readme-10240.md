---
title: "🚀 Xây dựng Chatbot WhatsApp CSKH thông minh với AI và Intent Routing trên n8n"
description: "Tự động hóa chăm sóc khách hàng qua WhatsApp với mô hình Hybrid thông minh: kết hợp phản hồi có sẵn và AI Agent giúp tiết kiệm 80% chi phí."
slug: "chatbot-whatsapp-cskh-ai-intent-routing-n8n"
tags: [n8n, automation, whatsapp, ai-chatbot, google-gemini, customer-support]
keywords: [n8n workflow, whatsapp chatbot, ai agent, intent routing, tự động hóa cskh, google gemini]
---

# 🚀 Xây dựng Chatbot WhatsApp CSKH thông minh với AI và Intent Routing

Các sếp có đang đau đầu vì lượng tin nhắn hỏi giá, sản phẩm và hỗ trợ trên WhatsApp gửi đến mỗi ngày quá tải, khiến nhân viên sales phải trả lời mỏi tay mà vẫn chậm trễ? Việc thuê đội ngũ trực chat 24/7 thì tốn kém, nhưng bỏ lỡ khách hàng thì mất doanh thu.

Giải pháp ở đây là **Workflow n8n Tự động hóa CSKH trên WhatsApp kết hợp AI và Intent Routing**. Đây là một hệ thống hybrid cực kỳ thông minh: xử lý tự động các câu hỏi quen thuộc bằng kịch bản có sẵn (nhanh và miễn phí), đồng thời dùng AI Agent (Google Gemini) để giải quyết các yêu cầu phức tạp. Giúp doanh nghiệp tiết kiệm đến **80% chi phí vận hành AI** mà vẫn giữ được chất lượng chăm sóc khách hàng đỉnh cao!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 24/7:** Tiếp nhận và phản hồi tin nhắn WhatsApp của khách hàng ngay lập tức bất kể ngày đêm.
- **Tiết kiệm 80% chi phí AI:** Phân loại thông minh (80% câu hỏi chung đi qua kịch bản dựng sẵn, 20% câu hỏi khó mới gọi AI Agent).
- **Cá nhân hóa cao:** Nhớ ngữ cảnh trò chuyện (Conversation Memory), đưa ra gợi ý sản phẩm, giá cả chính xác theo danh mục cửa hàng của bạn.
- **Hoạt động đa ngành:** Áp dụng hoàn hảo cho thời trang, điện tử, F&B, nội thất, làm đẹp...
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **WhatsApp Business API:** Tài khoản kết nối qua Meta, Twilio hoặc 360Dialog (để nhận/gửi tin nhắn).
- **Google Gemini API Key:** Sử dụng cho mô hình AI xử lý các truy vấn phức tạp.
- **Google Docs (Tùy chọn):** Nếu muốn AI đọc catalog sản phẩm trực tiếp từ tài liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste toàn bộ cấu trúc nodes.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để chatbot hoạt động đúng với cửa hàng của các sếp, cần cấu hình các node quan trọng sau:
- **WhatsApp Trigger - Receive Messages & Send WhatsApp Response:** Kết nối tài khoản WhatsApp Business API thông qua credentials tương ứng (`whatsAppTriggerApi` và `whatsAppApi`).
- **Classify User Intent:** Chỉnh sửa logic phân loại intent trong node code này để phù hợp với các danh mục sản phẩm/dịch vụ của doanh nghiệp (ví dụ: sản phẩm, giá cả, liên hệ, hỗ trợ, chào hỏi...).
- **Generate Product Response & Generate Contact Info Response:** Cập nhật thông tin chi tiết về sản phẩm, giá cả, và thông tin liên hệ/giờ mở cửa của cửa hàng bạn.
- **Build AI System Prompt & Google Gemini Chat Model:** Điền thông tin chi tiết về doanh nghiệp, chính sách vào System Prompt và kết nối Google Gemini API Key (`googlePalmApi`).
- **Google Docs - Product Catalog (Optional):** Liên kết tài liệu Google Docs chứa catalog sản phẩm nếu muốn AI tra cứu dữ liệu trực tiếp.

#### 3. Kích hoạt ⚡️
- Gửi tin nhắn test từ số cá nhân tới số WhatsApp Business để kiểm tra luồng nhận/gửi.
- Kiểm tra các nhánh Switch xem dữ liệu có đi đúng hướng (Pre-built vs AI Agent) hay không.
- Bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo nội bộ:** Thêm node Telegram/Slack vào nhánh hỗ trợ (Support) để tự động bắn thông báo cho nhân viên human-agent nhảy vào chốt đơn khi khách cần hỗ trợ trực tiếp.
- **Lưu trữ dữ liệu khách hàng:** Kết nối thêm Google Sheets hoặc CRM (Hubspot/Notion) sau node nhận tin nhắn để lưu thông tin lead.
- **Xử lý Media:** Mở rộng node Parse WhatsApp Message Data để hỗ trợ nhận hình ảnh/voice từ khách hàng.

### 📌 Kết luận
Workflow "WhatsApp Customer Inquiries with AI and Intent Routing" là vũ khí tối tân giúp tự động hóa toàn bộ khâu chăm sóc khách hàng trên nền tảng nhắn tin phổ biến nhất thế giới. Hãy cài đặt ngay hôm nay để tối ưu hóa nhân sự và gia tăng tỷ lệ chuyển đổi cho cửa hàng của các sếp!