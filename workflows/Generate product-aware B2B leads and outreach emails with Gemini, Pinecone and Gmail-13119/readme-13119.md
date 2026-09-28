---
title: "🚀 Tự động hóa tạo Lead B2B & Gửi email cá nhân hóa với Gemini, Pinecone và Gmail"
description: "Xây dựng hệ thống Sales tự động hoàn toàn (Autonomous Sales) từ tìm kiếm doanh nghiệp, nghiên cứu khách hàng đến gửi email cá nhân hóa bằng n8n, AI Gemini và Vector DB Pinecone."
slug: "tu-dong-hoa-tao-lead-b2b-gemini-pinecone-gmail"
tags: [n8n, automation, ai-agent, lead-generation, gemini, pinecone, gmail]
keywords: [n8n workflow, ai lead generation, b2b sales automation, gemini rag n8n, pinecone vector store]
---

# 🚀 Hệ thống Tự động hóa Tìm kiếm Lead B2B & Gửi Email Cá nhân hóa bằng AI

Chào các sếp! Việc đi tìm kiếm khách hàng tiềm năng (Lead Generation), nghiên cứu từng công ty và soạn email outreach thủ công thường ngốn rất nhiều thời gian của đội ngũ sales nhưng tỷ lệ chuyển đổi lại thấp do thiếu sự cá nhân hóa. 

Bài viết này sẽ hướng dẫn các sếp triển khai một hệ thống **Autonomous Sales Department (Phòng Sales tự động)** chạy ngầm 24/7 thông qua n8n. Workflow này kết hợp sức mạnh của RAG (Retrieval-Augmented Generation), AI Gemini, Pinecone Vector Database, Serper Web Search, Hunter.io và Gmail để tự động hóa toàn bộ phễu bán hàng từ A-Z.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% phễu Sales:** Từ việc cập nhật tài liệu sản phẩm, tìm kiếm công ty, lọc rác web, tìm người ra quyết định (Decision-makers) đến gửi email.
- **Cá nhân hóa cực cao:** Email gửi đi không phải là template rập khuôn mà dựa trên phân tích chuyên sâu về thách thức, tin tức của từng công ty mục tiêu.
- **Tiết kiệm chi phí & thời gian:** Thay vì tốn hàng chục giờ lướt web thủ công, AI tự động sàng lọc và chỉ đưa vào database những doanh nghiệp thực sự phù hợp.
- **Chống trùng lặp thông minh:** Sử dụng SHA256 hashing kết hợp Google Sheets Record Manager và PostgreSQL để loại bỏ hoàn toàn việc spam hoặc xử lý trùng lead.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản self-hosted hoặc cloud).
- **Google Drive & Google Sheets:** Lưu trữ tài liệu sản phẩm và quản lý trạng thái file (Record Manager).
- **Pinecone Account:** Tạo Vector Database để lưu trữ kiến thức sản phẩm (Knowledge Base).
- **Google Gemini API (Google Palm API):** Dùng cho mô hình ngôn ngữ lớn (LLM) và Embeddings.
- **Serper.dev API:** API tìm kiếm web chuyên dụng cho AI Agents.
- **PostgreSQL Database:** Lưu trữ thông tin công ty và danh sách leads.
- **Hunter.io API:** Tìm kiếm và xác thực email chuyên nghiệp từ domain công ty.
- **Gmail Account:** Tài khoản gửi email outreach tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n Editor chọn **Add workflow** -> **Import from File** và tải file JSON lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 giai đoạn chính (tương ứng với 4 khối xử lý logic trên canvas):

- **Giai đoạn 1: Context Creation (Đồng bộ tài liệu sản phẩm)**
  - Các node `Search files and folders`, `Download file`: Kết nối tài khoản Google Drive qua `googleDriveOAuth2Api` và trỏ tới thư mục chứa tài liệu sản phẩm của sếp.
  - Các node `Pinecone Vector Store`, `KB - Lead Criteria`, `KB - Research`, `KB - Email`: Cấu hình `pineconeApi`, tạo index và trỏ đúng namespace.
  - Các node `Add to Record Manger`, `Update the RecordManger`, `searchRecordManger`: Cấu hình `googleSheetsOAuth2Api` và chọn file Google Sheet quản lý trạng thái hashing file.

- **Giai đoạn 2: Lead Generation (Tìm kiếm công ty mục tiêu)**
  - Node `Lead Criteria Agent` & `Gemini`: Cấu hình `googlePalmApi`. Agent này sẽ đọc kiến thức sản phẩm từ Pinecone để tự động sinh ra tiêu chí chân dung khách hàng lý tưởng (ICP) và câu lệnh tìm kiếm.
  - Node `Web Search - Serper`: Cấu hình `httpHeaderAuth` với API key của Serper.dev để thực hiện search web.
  - Các node `Get Existing Leads`, `Insert Companies`: Kết nối cơ sở dữ liệu `PostgreSQL` để lưu trữ và kiểm tra trùng lặp domain công ty.

- **Giai đoạn 3: Contact Generation (Nghiên cứu sâu & Tìm người liên hệ)**
  - Node `Company Research Agent`: Phân tích sâu về công ty bằng AI Gemini kết hợp Web Search và Pinecone.
  - Node `Hunter`: Cấu hình `hunterApi` để quét email và thông tin LinkedIn của các "decision-makers" tại doanh nghiệp đó.
  - Node `Insert Lead` & `Update Company Status`: Lưu thông tin người liên hệ vào bảng `leads` trên PostgreSQL và đánh dấu trạng thái công ty đã xử lý xong.

- **Giai đoạn 4: Email Outreach (Soạn & Gửi email cá nhân hóa)**
  - Node `Email Personalization Agent`: Sử dụng Gemini để viết email chuẩn sales chuyên nghiệp (150-200 từ), nhắc đến các điểm đau (pain points) thực tế của công ty đó.
  - Node `Send Gmail`: Kết nối `gmailOAuth2` để gửi email trực tiếp từ tài khoản Google Workspace/Gmail của sếp.
  - Node `Update Lead`: Cập nhật ngày gửi (`sent_date`) và nội dung email vào PostgreSQL để tracking.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`When clicking ‘Execute workflow’`) cho từng phân đoạn để đảm bảo các API kết nối thành công và dữ liệu trả về đúng định dạng JSON.
- Bật công tắc **Active** tại các node `Schedule Trigger` để hệ thống tự động chạy ngầm hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo về kênh chat riêng mỗi khi hệ thống tìm được một Lead chất lượng cao hoặc gửi thành công một email outreach.
- **Theo dõi tỷ lệ phản hồi (Reply Tracking):** Kết hợp thêm node kiểm tra IMAP/Gmail để quét phản hồi từ khách hàng, tự động dừng chuỗi email nếu khách hàng đã reply.
- **Tối ưu Prompt AI:** Các sếp có thể tinh chỉnh lại System Prompt trong các Agent Gemini để văn phong email phù hợp hơn với văn hóa công ty hoặc thị trường mục tiêu (B2B SaaS, Agency, Logistics...).

### 📌 Kết luận
Với workflow n8n cực kỳ mạnh mẽ này, các sếp đã sở hữu ngay một hệ thống tự động hóa marketing và sales chuẩn AI, hoạt động không mệt mỏi 24/7. Hãy import ngay vào n8n, kết nối các API cần thiết và tối ưu hóa quy trình kinh doanh của mình ngay hôm nay!