---
title: "🚀 Xây dựng Trợ lý AI Thương mại Điện tử đa nền tảng (Shopify & WooCommerce) với GPT-4o, Gemini & RAG trên n8n"
description: "Hướng dẫn chi tiết triển khai workflow n8n tích hợp trợ lý AI thông minh cho cả Shopify và WooCommerce, kết hợp RAG Pinecone và AWS Bedrock."
slug: "tro-ly-ai-thuong-mai-dien-tu-shopify-woocommerce-n8n"
tags: [n8n, automation, ai-agent, shopify, woocommerce, rag]
keywords: [n8n workflow, ai chatbot shopify woocommerce, trợ lý ai n8n, rag pinecone aws bedrock]
keywords: [n8n workflow, trợ lý ai thương mại điện tử, shopify woocommerce automation, rag pinecone]
---

# 🚀 Xây dựng Trợ lý AI Thương mại Điện tử đa nền tảng (Shopify & WooCommerce) với GPT-4o, Gemini & RAG

Các sếp đang kinh doanh đa nền tảng (vừa có cửa hàng trên **Shopify**, vừa chạy hệ thống **WooCommerce**) chắc chắn đang đau đầu về việc hỗ trợ khách hàng thủ công? Khách cứ liên tục hỏi: *"Đơn hàng của tôi đâu rồi?"*, *"Shop còn mẫu áo này size L không?"*, hay các câu hỏi chung chung về chính sách đổi trả? 

Trả lời thủ công thì tốn nhân sự, mà dùng chatbot truyền thống thì cứng nhắc, không thông minh. Giải pháp ở đây là gì? Workflow n8n siêu cấp VIP này sẽ giúp các sếp dựng lên một **Trợ lý AI đa năng** tự động định tuyến câu hỏi, tra cứu dữ liệu đơn hàng/sản phẩm theo thời gian thực từ cả Shopify lẫn WooCommerce, kết hợp mô hình RAG (Pinecone & AWS Bedrock) để trả lời mọi thắc mắc của khách hàng 24/7 mà không cần con người nhúng tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng mà không lo sập nguồn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Tự động phân loại câu hỏi (Shopify, WooCommerce hay câu hỏi chung) và chuyển đến đúng chuyên gia AI xử lý.
- **Tích hợp thời gian thực**: Tra cứu chính xác tình trạng đơn hàng và danh sách sản phẩm trực tiếp từ API của Shopify và WooCommerce.
- **Trí tuệ nhân tạo đỉnh cao**: Sử dụng sức mạnh kết hợp giữa OpenAI (GPT-4o-mini), Google Gemini, và AWS Bedrock Embeddings kết hợp Pinecone Vector Store cho RAG cực mượt.
- **Trải nghiệm khách hàng 5 sao**: Phản hồi tức thì, cá nhân hóa, hoạt động không nghỉ ngơi 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Cho `Router Model` và `GPT-4o-mini`).
- **Google Generative AI API Key / Google Palm API** (Cho `Shopify Chat Model` và `WooCommerce Chat Model`).
- **AWS Credentials** (Cho `Embeddings AWS Bedrock`).
- **Pinecone API Key & Index** (Cho `Pinecone Vector Store`).
- **Shopify Access Token API** (Để kết nối lấy thông tin sản phẩm và đơn hàng).
- **WooCommerce API Credentials** (Consumer Key & Consumer Secret để kết nối WooCommerce).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n chọn **New Workflow**, nhấn tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ hệ thống nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Hệ thống gồm 23 nodes được chia thành các phân đoạn xử lý thông minh. Các sếp cần cấu hình kỹ các điểm sau:

- **Initial Query Router & Router Model (GPT-4o-mini)**: 
  - Chọn credentials OpenAI.
  - Node này đóng vai trò "tổng đài viên", phân tích câu hỏi của khách hàng từ `When chat message received` và đưa ra từ khóa định hướng: `SHOPIFY`, `WOOCOMMERCE`, hoặc `None of them`.
- **Check if Its General query & Route To Shopify or WooCommerce (IF Nodes)**: 
  - Các node điều kiện này sẽ đọc kết quả từ Router để đẩy luồng chạy vào đúng nhánh chuyên gia AI tương ứng hoặc nhánh RAG chung.
- **Shopify Assistant Agent & Tools**: 
  - Kết nối `Shopify Chat Model` (sử dụng Gemini).
  - Cấu hình credentials cho các công cụ: `Fetch All Products`, `Get Order info`, và `GraphQL` để chatbot có quyền truy xuất dữ liệu cửa hàng Shopify của các sếp.
- **WooCommerce Assistant Agent & Tools**: 
  - Kết nối `WooCommerce Chat Model` (sử dụng Gemini).
  - Cấu hình credentials (`wooCommerceApi`) cho các công cụ `Fetch All Products2` và `Fetch Order Details`.
- **General Queries (Agent) & Pinecone Vector Store**: 
  - Cấu hình `Pinecone Vector Store` với API Key và Index chứa tài liệu kiến thức công ty/chính sách.
  - Cấu hình `Embeddings AWS Bedrock` với model `amazon.titan-embed-text-v2:0` và AWS credentials để chuyển đổi vector văn bản.
- **Merge Node**: 
  - Node này gom toàn bộ kết quả từ các nhánh xử lý khác nhau về một đường ống duy nhất trước khi trả phản hồi về cho khách hàng qua khung chat.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách gửi câu hỏi mẫu ở node `When chat message received`.
- Kiểm tra xem luồng có chạy qua đúng Router và trả về kết quả chính xác không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để đưa trợ lý ảo lên sàn giao dịch thực tế!

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử hội thoại**: Tận dụng các node `Simple Memory`, `Memory RAG`, `WooCommerce Memory`, `Shopify Memory` có sẵn để bot nhớ ngữ cảnh trò chuyện trước đó của khách hàng.
- **Tích hợp kênh chat đa dạng**: Thay vì chỉ dùng chat trigger mặc định của n8n, các sếp có thể móc nối thêm webhook từ **Telegram, Facebook Messenger, hoặc Zalo OA** để khách hàng nhắn tin trực tiếp.
- **Báo cáo sự cố tự động**: Thêm node Error Trigger để nếu AI gặp lỗi kết quả trống hoặc lỗi API, hệ thống sẽ tự động bắn tin nhắn cảnh báo về kênh Telegram nội bộ của quản lý.

### 📌 Kết luận
Với workflow n8n tích hợp AI Agent, Shopify, WooCommerce và RAG này, các sếp đã sở hữu ngay một "nhân viên sale và CSKH đa năng" cực kỳ thông minh mà chi phí vận hành cực kỳ tối ưu. Triển khai ngay hôm nay để bứt phá doanh thu thương mại điện tử nào các sếp ơi!