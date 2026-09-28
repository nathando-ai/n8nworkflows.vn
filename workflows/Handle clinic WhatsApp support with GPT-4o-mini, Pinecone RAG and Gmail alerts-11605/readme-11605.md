---
title: "🚀 Xây dựng Trợ lý ảo WhatsApp Y tế thông minh với GPT-4o-mini, Pinecone RAG và Google Sheets CRM"
description: "Hướng dẫn chi tiết thiết lập hệ thống tự động chăm sóc khách hàng phòng khám qua WhatsApp: xử lý tin nhắn đa phương tiện, tích hợp AI RAG và đồng bộ CRM."
slug: "huong-dan-tro-ly-ao-whatsapp-y-te-n8n-gpt-4o-mini"
tags: [n8n, automation, ai, openai, whatsapp, pinecone, crm]
keywords: [n8n workflow, trợ lý ảo whatsapp, gpt-4o-mini, pinecone rag, crm google sheets, tự động hóa y tế]
---

# 🚀 Xây dựng Trợ lý ảo WhatsApp Y tế thông minh với GPT-4o-mini, Pinecone RAG và Google Sheets CRM

Các sếp đang vận hành phòng khám hoặc dịch vụ tư vấn chắc chắn hiểu cảm giác quá tải khi hàng trăm tin nhắn WhatsApp đổ về mỗi ngày: khách hỏi lịch khám, giá dịch vụ, gửi hình ảnh kết quả xét nghiệm hay file tài liệu, yêu cầu gọi điện hỗ trợ gấp... Việc trả lời thủ công không chỉ chậm trễ mà còn dễ bỏ sót khách hàng tiềm năng.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code (No-code) sử dụng **n8n**, kết hợp trí tuệ nhân tạo **GPT-4o-mini**, cơ sở tri thức **Pinecone RAG** và hệ thống lưu trữ **Google Sheets CRM**. Bài viết này sẽ hướng dẫn các sếp cách triển khai workflow toàn diện này.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7**: Tự động xử lý tin nhắn dạng văn bản, ghi âm (Audio), hình ảnh (Image) và tài liệu (PDF) từ khách hàng qua WhatsApp.
- **Tư vấn chuẩn xác với RAG**: Tra cứu tài liệu, quy trình, bảng giá phòng khám được lưu trên Google Docs thông qua Pinecone Vector Store.
- **Tự động hóa Đặt lịch & CRM**: Trích xuất thông tin đặt lịch, phân loại khách hàng, lưu trữ vào Data Table và đồng bộ tự động sang Google Sheets mỗi phút.
- **Cảnh báo nhân sự kịp thời**: Tự động gửi Email thông báo và đẩy vào hàng chờ (Human Escalation) khi khách hàng cần sự can thiệp của nhân viên y tế.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (bản Self-hosted hoặc Cloud).
- **Tài khoản OpenAI API**: Sử dụng cho GPT-4o-mini, Whisper (transcribe audio), Vision (analyze image) và Embeddings.
- **WhatsApp Cloud API**: Token và Phone Number ID từ Meta Business.
- **Pinecone Account**: Vector database để lưu trữ dữ liệu RAG.
- **Google Account**: Sử dụng Gmail (gửi thông báo), Google Sheets (CRM) và Google Docs (tài liệu kiến thức).
- **n8n Data Tables**: Hệ thống bảng dữ liệu nội bộ của n8n để lưu trữ memory, lịch hẹn, lead và hàng chờ human.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn JSON từ nguồn cấp.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 60 nodes được chia thành 8 section chính. Các sếp cần tập trung cấu hình các điểm sau:
- **WhatsApp Webhook & Send via WhatsApp**: Cấu hình Webhook URL nhận sự kiện từ Meta và kết nối `httpBearerAuth` với Token của WhatsApp Cloud API.
- **OpenAI Nodes (OpenAI Chat Model, Transcribe Audio, Analyze image, Embeddings)**: Thêm credentials `openAiApi` cho toàn bộ các node liên quan đến OpenAI. Kiểm tra model mặc định là `gpt-4o-mini`.
- **Pinecone Vector Store**: Cấu hình API Key và index/namespace tương ứng để hệ thống RAG có thể truy vấn dữ liệu từ Google Docs đã nạp.
- **Google Sheets & Gmail Nodes**: Kết nối tài khoản Google OAuth2 cho các node Google Sheets (`Append or update slot`, `Append or update lead`...) và Gmail (`Send Email with attachment`, `Send Email Notification If Human is called`). Tham khảo cấu trúc mẫu tại [Google Sheets Template](https://docs.google.com/spreadsheets/d/1HCl3CvMnzILIrcjnFK-AwLqWuKfMwezM1yXWkJ4KG9Q/edit?usp=sharing).
- **n8n Data Tables**: Đảm bảo các Data Tables lưu trữ lịch sử chat (`Insert Row Memory`, `Get History`), lịch hẹn (`Booked Appointment`), lead (`Get lead`, `Insert Lead`) và hàng chờ nhân sự (`Add row for Human Call`) đã được tạo và liên kết đúng tên bảng trong node.

#### 3. Kích hoạt ⚡️
- Thực hiện chạy thử (Test run) với một vài tin nhắn mẫu (văn bản hoặc file) để kiểm tra luồng xử lý từ Webhook qua AI Agent đến WhatsApp.
- Sau khi kiểm tra mọi thứ chạy mượt mà, gạt công tắc sang **Active** để đưa trợ lý ảo vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack**: Bổ sung node gửi thông báo qua Telegram hoặc Slack bên cạnh Gmail để nhân viên phòng khám nhận được cảnh báo `needs_human` nhanh chóng hơn.
- **Mở rộng RAG**: Định kỳ cập nhật tài liệu hướng dẫn dịch vụ, bác sĩ trực trên Google Docs để trợ lý ảo luôn cung cấp thông tin mới nhất.
- **Báo cáo định kỳ**: Thiết lập thêm một nhánh workflow chạy hàng ngày bằng `Schedule Trigger` để tổng hợp số lượng khách hàng đặt lịch và gửi báo cáo qua email cho quản lý.

### 📌 Kết luận
Việc tự động hóa chăm sóc khách hàng và đặt lịch hẹn qua WhatsApp với AI và RAG không chỉ giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn nâng tầm chuyên nghiệp cho phòng khám của các sếp. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành!