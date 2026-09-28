---
title: "🚀 Tự động hóa tạo bản nháp RFP từ Google Drive với Groq AI, Salesforce và Slack"
description: "Hướng dẫn xây dựng quy trình tự động hóa n8n giúp trích xuất yêu cầu RFP, viết bản nháp bằng Groq AI, lưu trữ vào Google Docs & Salesforce và thông báo qua Slack."
slug: "tu-dong-hoa-tao-ban-nhap-rfp-groq-ai-salesforce-slack"
tags: [n8n, automation, groq-ai, salesforce, google-drive, ai-rag]
keywords: [n8n workflow, tự động hóa rfp, groq ai, salesforce automation, slack notification, google docs]
---

# 🚀 Tự động hóa tạo bản nháp RFP từ Google Drive với Groq AI, Salesforce và Slack

Viết hồ sơ thầu (RFP - Request for Proposal) thủ công là nỗi ám ảnh của các công ty tư vấn, dịch vụ IT và agency. Các sếp thường phải mất hàng giờ để đọc tài liệu dài ngoằng, phân tích yêu cầu, tra cứu tài liệu cũ và soạn thảo bản nháp trước khi đưa cho đội ngũ duyệt. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa **100% vòng đời RFP** – từ lúc khách hàng tải file lên Google Drive đến khi phân tích AI, lưu vào Google Docs, tạo Opportunity trên Salesforce và bắn thông báo mượt mà lên Slack!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Giảm từ vài ngày xuống vài phút cho việc đọc hiểu và soạn thảo bản nháp RFP.
- **AI thông minh (Groq + LLaMA):** Trích xuất chính xác yêu cầu, ngân sách, thời hạn và tạo văn bản chuẩn chỉnh.
- **Đồng bộ CRM toàn diện:** Tự động tạo Opportunity và Task kiểm duyệt trên Salesforce.
- **Cộng tác liền mạch:** Lưu bản thảo vào Google Docs và thông báo ngay lập tức cho team qua Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Google Drive & Google Docs:** Thư mục chứa file RFP đầu vào và thư mục lưu Knowledge Base (tài liệu thầu cũ).
- **Groq API Key:** Sử dụng mô hình `llama-3.3-70b-versatile` cực mạnh cho việc phân tích và viết lách.
- **Salesforce Account:** Để tạo Opportunity và Task review.
- **Slack Workspace:** Kênh nhận thông báo khi có RFP mới được xử lý xong.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 18 nodes được chia thành các module rõ ràng. Các sếp cần chú ý cấu hình các node sau:

- **Watch RFP Upload Folder (`googleDriveTrigger`):** Chọn tài khoản Google Drive và trỏ tới thư mục ID nơi khách hàng hoặc team upload file RFP PDF.
- **AI Model – Requirement Extraction & Proposal Writing (`lmChatGroq`):** Nhập `groqApi` credentials và chọn model `llama-3.3-70b-versatile`.
- **Fetch Past Proposals (`httpRequest`):** Kết nối Google Drive để lấy các tài liệu thầu cũ (Knowledge Base) làm ngữ cảnh giúp AI viết trúng "văn phong" của công ty.
- **Create Salesforce Opportunity & Task (`salesforce`):** Kết nối tài khoản Salesforce (`salesforceOAuth2Api`) để hệ thống tự động tạo cơ hội kinh doanh và phân công việc review.
- **Save Proposal to Google Docs (`googleDocs`):** Chọn thư mục đích để lưu bản nháp RFP dưới dạng Google Docs.
- **Notify Team via Slack (`slack`):** Cấu hình kênh Slack nhận thông báo kèm link tài liệu Google Docs và Salesforce.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và upload thử một file PDF RFP mẫu lên Google Drive để test.
- Kiểm tra kết quả trên Google Docs, Salesforce và Slack xem mọi thứ đã "chạy mượt" chưa.
- Gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kho tri thức (RAG):** Kết hợp thêm Vector Store (như Pinecone hoặc Qdrant) thay vì chỉ đọc file thầu cũ qua Google Drive để AI tìm kiếm case study chính xác hơn.
- **Tích hợp Email:** Thêm node Gmail/Outlook ở đầu workflow để tự động bắt file đính kèm RFP từ email của khách hàng gửi tới.
- **Báo cáo định kỳ:** Tạo thêm một nhánh thống kê số lượng RFP nhận được mỗi tuần và gửi báo cáo tổng kết vào kênh Slack của Ban Giám Đốc.

### 📌 Kết luận
Việc tối ưu quy trình xử lý thầu bằng AI không chỉ giúp doanh nghiệp tăng tốc độ phản hồi khách hàng mà còn nâng cao tỷ lệ thắng thầu nhờ sự chuẩn hóa và chuyên nghiệp. Hãy triển khai ngay workflow này để giải phóng sức lao động cho đội ngũ sales và bid management của các sếp nhé!