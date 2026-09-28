---
title: "🚀 Xây Dựng Chatbot Hỗ Trợ Khách Hàng WhatsApp Tích Hợp CRM & AI"
description: "Hướng dẫn chi tiết xây dựng chatbot WhatsApp thông minh bằng n8n, OpenAI và Evolution API. Tự động hóa tra cứu đơn hàng, điểm tích lũy và xử lý khiếu nại qua CRM."
slug: "chatbot-whatsapp-ai-crm-n8n"
tags: [n8n, automation, no-code, whatsapp-bot, ai-chatbot, crm-integration]
keywords: [n8n workflow, chatbot whatsapp, tự động hóa hỗ trợ khách hàng, tích hợp crm, openai agent]
---

# 🚀 Xây Dựng Chatbot Hỗ Trợ Khách Hàng WhatsApp Tích Hợp CRM & AI

Việc trả lời hàng trăm tin nhắn WhatsApp mỗi ngày về đơn hàng, điểm tích lũy hay khiếu nại là một gánh nặng lớn cho đội ngũ CSKH. Làm thủ công không chỉ tốn thời gian mà còn dễ dẫn đến sai sót thông tin, gây trải nghiệm khách hàng kém.

Workflow này là giải pháp "chốt hạ" cho vấn đề đó. Sử dụng sức mạnh của **n8n**, **OpenAI (LangChain Agent)** và **Evolution API**, các sếp có thể tự động hóa 100% quy trình hỗ trợ khách hàng. Chatbot không chỉ trả lời câu hỏi chung chung mà còn **tra cứu trực tiếp dữ liệu từ CRM** (đơn hàng, chi nhánh, danh mục sản phẩm) để đưa ra câu trả lời chính xác, cá nhân hóa và chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Chatbot xử lý tin nhắn 24/7, không cần nhân viên trực.
- **Dữ liệu chính xác**: AI Agent trực tiếp gọi API CRM để tra cứu đơn hàng, điểm tích lũy, tránh trả lời "mù" hay sai thông tin.
- **Phân loại thông minh**: Workflow tự động phân loại tin nhắn (Đơn hàng, Khiếu nại, Menu, Chi nhánh) và áp dụng prompt phù hợp.
- **Trải nghiệm liền mạch**: Tích hợp Evolution API để gửi/nhận tin nhắn WhatsApp mượt mà, hỗ trợ ghi nhớ ngữ cảnh hội thoại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n**: Bản Self-hosted hoặc Cloud.
2. **Tài khoản OpenAI**: API Key để sử dụng mô hình ngôn ngữ (GPT-3.5/4).
3. **Evolution API**: Instance Evolution API đã được cài đặt và kết nối với số điện thoại WhatsApp.
4. **Hệ thống CRM/Backend**: Các endpoint API RESTful cho phép:
   - Tìm kiếm khách hàng/đơn hàng (`crm_search_tool`).
   - Lưu bản ghi mới (`save_crm_record_tool`).
   - Tra cứu điểm tích lũy (`get_loyalty_points_tool`).
   - Tìm kiếm sản phẩm/danh mục/chi nhánh (`items_search_tool`, `categories_search_tool`, `branches_search_tool`).
5. **Webhook URL**: Địa chỉ webhook từ Evolution API để nhận tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải xuống file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Sau khi import, các sếp sẽ thấy một workflow phức tạp với 22 nodes, bao gồm các Agent AI, công cụ HTTP Request và node Evolution API.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Workflow này sử dụng kiến trúc **AI Agent** với nhiều công cụ (Tools), vì vậy cần cấu hình kỹ:

*   **Cấu hình Evolution API (2 Nodes)**:
    *   **`Webhook: Receive WhatsApp message`**: Đảm bảo URL webhook này khớp với cấu hình trong Evolution API để nhận tin nhắn từ khách hàng.
    *   **`Send WhatsApp Greeting`** & **`Send Answer to User's WhatsApp`**: Chọn đúng **Credential** của Evolution API. Kiểm tra trường `instanceName` (tên instance WhatsApp) và `to` (số điện thoại người nhận) được ánh xạ đúng từ dữ liệu đầu vào.

*   **Cấu hình OpenAI (3 Nodes)**:
    *   **`OpenAI Chat Model`**, **`OpenAI Chat Model1`**, **`OpenAI Chat Model2`**: Chọn đúng **OpenAI Credential**. Các sếp có thể chọn model khác nhau cho từng tác vụ (ví dụ: dùng GPT-4o cho Agent chính để tăng độ chính xác, GPT-3.5-turbo cho Router để tiết kiệm chi phí).

*   **Cấu hình AI Agents (2 Nodes)**:
    *   **`AI Agent Router: Classify msg`**: Agent này dùng để phân loại tin nhắn đầu vào. Kiểm tra **Structured Output Parser** đảm bảo định dạng JSON trả về đúng các trường như `intent` (orders, complaints, branches, menu).
    *   **`AI Agent`**: Đây là "bộ não" chính. Kiểm tra **System Prompt** (có thể nằm trong các node `Set` như `Orders System Prompt`, `Complaints System Prompt`...). Đảm bảo prompt hướng dẫn AI cách sử dụng các tools đã định nghĩa.

*   **Cấu hình HTTP Request Tools (6 Nodes)**:
    *   Các node `crm_search_tool`, `save_crm_record_tool`, `get_loyalty_points_tool`, `items_search_tool`, `branches_search_tool`, `categories_search_tool` đều là các **HTTP Request Tool**.
    *   **BẮT BUỘC**: Các sếp phải thay thế URL API mẫu bằng **URL thực tế** của hệ thống CRM/Backend của mình.
    *   Kiểm tra **Headers** (API Key, Authorization) và **Body** (tham số gửi đi) cho đúng với API documentation của hệ thống backend.
    *   Ví dụ: `crm_search_tool` cần gửi `phone_number` hoặc `customer_id` để tìm kiếm.

*   **Cấu hình Memory (2 Nodes)**:
    *   **`Simple Memory`** & **`Simple Memory-2`**: Đảm bảo cấu hình đúng `sessionKey` (thường là số điện thoại người dùng) để AI nhớ ngữ cảnh hội thoại giữa các tin nhắn.

*   **Cấu hình Switch Node**:
    *   Node **`Switch`** sẽ nhận kết quả từ `AI Agent Router` và phân luồng đến các System Prompt tương ứng. Kiểm tra điều kiện (conditions) khớp với các intent đã định nghĩa.

#### 3. Kích hoạt ⚡️
1. **Test Run**: Gửi một tin nhắn mẫu từ số điện thoại đã kết nối với Evolution API đến số WhatsApp của bot.
2. Kiểm tra log trong n8n:
   - Tin nhắn có được nhận qua Webhook không?
   - Router có phân loại đúng intent không?
   - Agent có gọi đúng tool (ví dụ: `crm_search_tool`) không?
   - Kết quả từ API có được trả về và AI có tổng hợp thành câu trả lời hợp lý không?
   - Tin nhắn có được gửi đi qua `Send Answer to User's WhatsApp` không?
3. Nếu mọi thứ ổn, bật **Active** workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Slack/Telegram**: Thêm node Slack hoặc Telegram để gửi thông báo cho đội ngũ CSKH khi có khiếu nại nghiêm trọng (intent = complaints) mà AI không xử lý được.
- **Lưu log hội thoại**: Thêm node Google Sheets hoặc Database để lưu lại toàn bộ cuộc hội thoại, giúp phân tích dữ liệu và cải thiện prompt.
- **Cá nhân hóa hơn**: Sử dụng dữ liệu từ CRM (tên khách hàng, lịch sử mua hàng) để chèn vào prompt, giúp AI gọi tên khách hàng và gợi ý sản phẩm phù hợp.
- **Giới hạn tốc độ (Rate Limiting)**: Thêm node Delay hoặc Rate Limiter để tránh bị chặn bởi WhatsApp nếu có nhiều tin nhắn spam.

### 📌 Kết luận
Với workflow này, các sếp không chỉ có một chatbot "chát" đơn thuần mà là một **trợ lý ảo thông minh** có khả năng truy cập dữ liệu doanh nghiệp. Đây là bước tiến lớn trong việc tự động hóa CSKH, giảm tải cho nhân viên và nâng cao trải nghiệm khách hàng. Hãy bắt đầu triển khai ngay hôm nay để tận dụng sức mạnh của AI trong vận hành!