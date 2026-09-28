---
title: "🚀 Xây dựng Chatbot WhatsApp Thương mại Điện tử thông minh với Whapi, WooCommerce, RAG và Gmail"
description: "Hướng dẫn chi tiết thiết lập hệ thống chăm sóc khách hàng tự động qua WhatsApp tích hợp AI Agent, tra cứu đơn hàng WooCommerce, kho kiến thức RAG và chuyển tiếp cho nhân sự qua Gmail."
slug: "chatbot-whatsapp-thuong-mai-dien-tu-rag-woo-woocommerce-n8n"
tags: [n8n, automation, whatsapp, ai-agent, woocommerce, rag]
keywords: [n8n workflow, chatbot whatsapp, woocommerce automation, rag qdrant, ai customer support]
---

# 🚀 Xây dựng Chatbot WhatsApp Thương mại Điện tử thông minh với Whapi, WooCommerce, RAG và Gmail

Trong thời đại mua sắm trực tuyến phát triển, tốc độ phản hồi khách hàng chính là yếu tố quyết định tỷ lệ chốt đơn. Việc để khách hàng phải chờ đợi giải đáp về tình trạng đơn hàng, chính sách đổi trả hay thông tin sản phẩm sẽ làm giảm uy tín doanh nghiệp. Tuy nhiên, việc túc trực 24/7 để trả lời hàng trăm tin nhắn WhatsApp là một gánh nặng lớn.

Workflow này giải quyết triệt để vấn đề trên bằng cách xây dựng một **Trợ lý AI chăm sóc khách hàng tự động trên WhatsApp**. Hệ thống hoạt động 24/7, tự động tra cứu dữ liệu đơn hàng từ WooCommerce, tìm kiếm tài liệu công ty qua công nghệ RAG (Qdrant + Google Drive), áp dụng bộ lọc an toàn (Guardrails) và tự động chuyển tiếp yêu cầu khó sang email nhân sự (Gmail) khi cần thiết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7**: Khách hàng nhận được câu trả lời chính xác ngay lập tức qua WhatsApp bất kể ngày đêm.
- **Tích hợp sâu WooCommerce**: AI có thể tự động kiểm tra trạng thái đơn hàng, thông tin khách hàng và danh mục sản phẩm theo thời gian thực.
- **Kiến thức thông minh (RAG)**: Đọc hiểu tài liệu, chính sách từ Google Drive để tư vấn chuẩn xác như nhân viên kỳ cựu.
- **Chuyển giao thông minh (Escalation)**: Tự động gửi email qua Gmail cho đội ngũ hỗ trợ con người khi gặp các ca khó hoặc khi khách hàng yêu cầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản Whapi.cloud**: Để kết nối WhatsApp API (Có thể [Đăng ký Whapi miễn phí tại đây](https://panel.whapi.cloud/partner_registration/n3w) với 7 ngày dùng thử).
- **OpenAI API Key** (hoặc Google Gemini API Key): Dùng cho LLM và Embeddings.
- **Qdrant Vector Database**: Lưu trữ dữ liệu vector cho RAG (có thể dùng Qdrant Cloud miễn phí).
- **Google Drive**: Lưu trữ tài liệu, FAQ, chính sách công ty để vector hóa.
- **WooCommerce Store**: Website WordPress bán hàng có bật REST API.
- **Google Gmail Account**: Cấp quyền OAuth2 để gửi email escalation.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ nguồn.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau:

- **STEP 1 - Create Qdrant Collection & STEP 2 - Vectorization**:
  - Kết nối node `Qdrant Vector Store` bằng thông tin API của bạn.
  - Trỏ node `Get folder` tới thư mục chứa tài liệu/FAQ trên **Google Drive**.
  - Cấu hình `Embeddings OpenAI` với OpenAI API key.
  - Chạy thủ công luồng này một lần để nạp dữ liệu tài liệu vào Qdrant.

- **STEP 3 - WhatsApp Whapi Webhook (`Get WhatsApp`)**:
  - Sao chép Webhook URL từ node này và cấu hình vào phần **Webhook Settings** trên trang quản trị Whapi.cloud của bạn.
  - Đảm bảo các node `Send WhatsApp`, `Only text avaiable`, `Bad message` được cấu hình đúng HTTP Bearer Token từ Whapi.

- **Configure AI Agent (`E-Commerce Customer Support AI Agent`)**:
  - Cấu hình System Prompt cho AI Agent (định hình tính cách, ngôn ngữ và quy tắc trả lời).
  - Kết nối Model (`OpenAI Chat Model1` hoặc `Google Gemini Chat Model`).
  - Kiểm tra các công cụ (Tools) đã được gắn vào Agent:
    - `get_order`, `get_orders`, `get_user`, `get_product`, `get_many_products`: Nhập thông tin xác thực WooCommerce của bạn.
    - `rag_search`: Kết nối với vector store Qdrant.
    - `Calculator`: Hỗ trợ tính toán giá tiền/phí ship.
    - `get_human_support`: Kết nối tài khoản Gmail để gửi email escalation.
  - Kiểm tra bộ lọc `Guardrails` để đảm bảo nội dung chat luôn an toàn và đúng chuẩn.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** hoặc gửi một tin nhắn mẫu qua WhatsApp để kiểm tra hệ thống phản hồi.
- Bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Kết hợp thêm node Telegram hoặc Slack để đội ngũ sale nhận được thông báo ngay lập tức khi có ca escalation từ Gmail.
- **Lưu lịch sử hội thoại**: Tận dụng node `Window Buffer Memory` kết hợp lưu trữ vào Google Sheets hoặc Database để phân tích hành vi khách hàng sau này.
- **Tối ưu Prompt**: Thêm các ví dụ (Few-shot prompting) vào System Prompt của AI Agent để chatbot hiểu rõ văn phong thương hiệu của các sếp hơn.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một hệ thống chăm sóc khách hàng tự động hóa đỉnh cao kết hợp giữa AI và dữ liệu thương mại điện tử thực tế. Hãy triển khai ngay hôm nay để tối ưu hóa chi phí vận hành và tăng tỷ lệ chuyển đổi đơn hàng!