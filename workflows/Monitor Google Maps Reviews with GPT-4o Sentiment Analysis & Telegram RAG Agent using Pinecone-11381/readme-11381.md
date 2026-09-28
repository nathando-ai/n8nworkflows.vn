---
title: "🚀 Tự động giám sát đánh giá Google Maps với GPT-4o và Telegram RAG Agent"
description: "Hướng dẫn xây dựng hệ thống tự động cào đánh giá Google Maps, phân tích cảm xúc bằng GPT-4o và tra cứu thông minh qua Telegram RAG Agent với Pinecone."
slug: "tu-dong-giam-sat-danh-gia-google-maps-gpt-4o-telegram-rag"
tags: [n8n, automation, ai-agent, google-maps, pinecone, telegram]
keywords: [n8n workflow, giám sát google maps, phân tích cảm xúc ai, telegram rag agent, pinecone vector store, openai gpt-4o]
---

# 🚀 Tự động giám sát đánh giá Google Maps với GPT-4o và Telegram RAG Agent

Việc theo dõi thủ công hàng trăm đánh giá trên Google Maps của khách hàng mỗi ngày thực sự là một "cực hình" đối với các chủ doanh nghiệp và đội ngũ chăm sóc khách hàng. Các sếp thường bỏ lỡ các phản hồi tiêu cực quan trọng, dẫn đến việc xử lý khủng hoảng chậm trễ và mất đi cơ hội cải thiện chất lượng dịch vụ.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: từ việc cào dữ liệu đánh giá Google Maps, sử dụng AI (GPT-4o) để phân tích cảm xúc, lưu trữ vào Pinecone Vector Database, ghi log Google Sheets và tích hợp sẵn một Telegram RAG Agent giúp các sếp trò chuyện, tra cứu thông tin đánh giá ngay trên điện thoại cực kỳ tiện lợi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn:** Định kỳ cào và cập nhật đánh giá mới từ Google Maps mà không cần can thiệp thủ công.
- **Phân tích thông minh:** AI tự động đánh giá sắc thái (sentiment), lọc ra các đánh giá tiêu cực và gửi cảnh báo ngay lập tức qua Telegram.
- **Tra cứu thông minh (RAG):** Hỏi đáp trực tiếp với trợ lý ảo trên Telegram về toàn bộ lịch sử đánh giá của khách hàng nhờ tích hợp Pinecone Vector Store.
- **Lưu trữ bài bản:** Tự động đồng bộ toàn bộ dữ liệu vào Google Sheets để làm báo cáo định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- API Key của OpenAI (cho GPT-4o/GPT-4o-mini và Embeddings).
- Tài khoản Pinecone (để lưu trữ vector database cho RAG Agent).
- Bot Telegram (tạo qua BotFather để nhận thông báo và chat với RAG Agent).
- Tài khoản Google Sheets (để lưu log dữ liệu).
- Dịch vụ cào dữ liệu Google Maps (API hoặc bên thứ ba được cấu hình trong HTTP Request nodes).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ nguồn cấp.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node sau để hệ thống chạy mượt mà:
- **Các node `⚠️ CONFIGURATION`, `⚠️ CONFIGURATION1`, `⚠️ CONFIGURATION2` (Set):** Điền các thông số cấu hình chung như từ khóa tìm kiếm Google Maps, ID địa điểm, hoặc thông số định danh bot của các sếp.
- **OpenAI Chat Model & GPT 5 mini / GPT-4o:** Kết nối tài khoản OpenAI Credentials, chọn model phù hợp cho việc phân tích cảm xúc và vận hành AI Agent.
- **Embeddings OpenAI & Pinecone (Pinecone Ingest / Pinecone Search Tool):** Nhập API Key của Pinecone, tạo Index phù hợp với kích thước vector của OpenAI để hệ thống RAG hoạt động chính xác.
- **Send Alert & Send a text message (Telegram):** Kết nối Telegram Bot Token và thiết lập Chat ID của các sếp hoặc nhóm Telegram nhận cảnh báo.
- **Log data (Google Sheets):** Chọn tài khoản Google Drive/Sheets credentials, trỏ tới file Google Sheets chuẩn bị sẵn để ghi nhận log đánh giá.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử công đoạn thủ công (`When clicking "Execute"` hoặc `Trigger at midnight`) để test luồng dữ liệu chạy qua các node `Wait`, `Split In Batches` và `HTTP Request`.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy theo lịch hẹn (`Schedule Trigger`).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Discord để đội ngũ vận hành cùng theo dõi các đánh giá 1 sao, 2 sao ngay lập tức.
- **Báo cáo tuần tự động:** Sử dụng node `Schedule Trigger` (chạy vào Chủ Nhật hàng tuần) kết hợp AI Agent để tổng hợp báo cáo xu hướng cảm xúc khách hàng gửi thẳng vào email quản lý.
- **Tối ưu chi phí:** Sử dụng các model tiết kiệm như `gpt-4o-mini` cho các tác vụ phân tích cảm xúc hàng loạt để tối ưu token OpenAI.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh giúp tự động hóa khâu quảnเสียง danh tiếng thương hiệu trên Google Maps kết hợp công nghệ AI RAG tiên tiến. Hãy triển khai ngay hôm nay để không bỏ lỡ bất kỳ phản hồi nào từ khách hàng!