---
title: "🚀 Xây dựng Trợ lý Bán hàng WhatsApp thông minh tích hợp GPT-4, Supabase và Product Catalog"
description: "Tự động hóa toàn bộ quy trình chăm sóc khách hàng và bán hàng trên WhatsApp bằng AI Agent. Xử lý tin nhắn văn bản, hình ảnh, ghi âm và tra cứu danh mục sản phẩm 24/7."
slug: "tro-ly-ban-hang-whatsapp-gpt-4-supabase"
tags: [n8n, ai-chatbot, whatsapp, gpt-4, supabase, automation]
keywords: [n8n workflow, whatsapp chatbot ai, gpt-4 sales agent, supabase vector store, tu dong hoa ban hang whatsapp]
---

# 🚀 Xây dựng Trợ lý Bán hàng WhatsApp thông minh tích hợp GPT-4, Supabase và Product Catalog

Các doanh nghiệp kinh doanh online thường xuyên đối mặt với tình trạng quá tải tin nhắn từ khách hàng trên WhatsApp. Việc phải trả lời thủ công các câu hỏi về giá cả, thông số sản phẩm, hay xử lý hình ảnh và tin nhắn thoại khiến đội ngũ sales mệt mỏi, dễ bỏ lỡ khách hàng tiềm năng ngoài giờ làm việc.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code/Low-code), đóng vai trò như một **Sales AI Agent** chuyên nghiệp trên WhatsApp. Hệ thống có khả năng tiếp nhận tin nhắn đa định dạng (văn bản, hình ảnh, giọng nói), tra cứu thông tin sản phẩm từ kho dữ liệu Supabase và danh mục n8n, sau đó tư vấn, chốt đơn tự động cho khách hàng 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đa định dạng:** Xử lý mượt mà cả tin nhắn văn bản, file ghi âm giọng nói (Voice notes qua OpenAI Audio) và hình ảnh sản phẩm do khách gửi lên.
- **Tra cứu thông tin chính xác:** Kết nối trực tiếp với RAG pipeline trên Supabase Vector Store và n8n Data Table để trả lời đúng giá, đúng thông số sản phẩm.
- **Phản hồi thông minh với GPT-4.1-mini:** Tư vấn bán hàng tự nhiên, cá nhân hóa, kèm theo hình ảnh sản phẩm thực tế gửi trực tiếp qua WhatsApp.
- **Hoạt động 24/7 không nghỉ:** Không bao giờ bỏ lỡ một khách hàng tiềm năng nào, tăng tỷ lệ chốt đơn và giảm thiểu chi phí vận hành nhân sự.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **WhatsApp Business API** (Cấu hình qua Meta for Developers với Webhook và Credentials).
- **OpenAI API Key** (Dùng cho GPT-4, Whisper cho Audio và Embeddings).
- **Supabase Account** (Cấu hình Vector Store làm cơ sở tri thức - Knowledge Base).
- **SerpAPI Key** (Dùng cho tính năng tìm kiếm web mở rộng của AI Agent nếu cần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:
- **WhatsApp Trigger & Send nodes (`WhatsApp Trigger`, `Send text message`, `Send media&caption message`,...):** Kết nối đúng tài khoản WhatsApp Business API credentials, cài đặt Webhook nhận tin nhắn từ số điện thoại doanh nghiệp.
- **Supabase Vector Store (`Knowledgebase`, `Supabase Vector Store`):** Kết nối credentials Supabase, thiết lập bảng vector với kích thước embedding dimension chuẩn (1536 cho OpenAI).
- **OpenAI & LLM (`the brain`, `Embeddings OpenAI1`,...):** Chọn model `gpt-4.1-mini` cho node `the brain` và cấu hình OpenAI API key đầy đủ.
- **Product Catalog (`search_products_inventory`):** Trỏ dữ liệu tới bảng danh mục sản phẩm của các sếp (bao gồm SKU, giá, mô tả, và link hình ảnh sản phẩm).
- **Code Node (`Response_validation`):** Node này có nhiệm vụ trích xuất và làm sạch URL hình ảnh từ kết quả của AI để định dạng chuẩn trước khi gửi kèm tin nhắn Media qua WhatsApp.

#### 3. Kích hoạt ⚡️
- Gửi thử tin nhắn văn bản, hình ảnh hoặc voice note vào số WhatsApp Business đã kết cấu hình.
- Kiểm tra kết quả trả về trên WhatsApp và theo dõi luồng chạy (Execution logs) trên n8n.
- Khi mọi thứ hoạt động ổn định, bật nút **Active** để hệ thống chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM/Google Sheets:** Mở rộng workflow để tự động lưu thông tin khách hàng và đơn hàng vào Google Sheets hoặc HubSpot CRM sau khi khách chốt mua.
- **Thêm chuyển tiếp Human-agent:** Thiết lập điều kiện (If node) để nếu khách hàng yêu cầu gặp nhân viên tư vấn người thật, hệ thống sẽ tự động bắn thông báo sang Slack hoặc Telegram cho đội ngũ sale.
- **Tùy chỉnh Prompt theo ngành hàng:** Mặc dù workflow được thiết kế tối ưu cho ngành nội thất, các sếp hoàn toàn có thể tinh chỉnh system prompt của AI Agent để bán mỹ phẩm, thời trang, thiết bị điện tử,...

### 📌 Kết luận
Trợ lý bán hàng WhatsApp tích hợp AI và Vector Database là "vũ khí tối tân" giúp các doanh nghiệp tối ưu hóa quy trình chăm sóc khách hàng trong kỷ nguyên số. Hãy cài đặt ngay hôm nay để bứt phá doanh số tự động!