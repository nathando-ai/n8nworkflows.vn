---
title: "🚀 Xây dựng IT Support Chatbot thông minh với Google Drive, Pinecone & Gemini trong n8n"
description: "Tự động hóa quy trình xử lý tài liệu từ Google Drive, lưu trữ vector với Pinecone và tạo trợ lý ảo IT Support thông minh sử dụng Gemini qua n8n."
slug: "it-support-chatbot-google-drive-pinecone-gemini-n8n"
tags: [n8n, automation, ai, it-ops, google-drive, pinecone, gemini]
keywords: [n8n workflow, ai agent, google drive trigger, pinecone vector store, gemini ai, it support chatbot]
---

# 🚀 Xây dựng IT Support Chatbot thông minh với Google Drive, Pinecone & Gemini

Các sếp có bao giờ cảm thấy đau đầu khi đội ngũ IT lúc nào cũng phải trả lời đi lặp lại hàng trăm câu hỏi giống nhau từ nhân viên mới về quy trình, tài liệu kỹ thuật hay chính sách công ty? Việc tìm kiếm thông tin thủ công trong các tệp PDF tài liệu trên Google Drive vừa mất thời gian lại kém hiệu quả.

Đừng lo, workflow **IT Support Chatbot with Google Drive, Pinecone & Gemini** do *AI Incarnation* thiết kế sẽ giúp các sếp giải quyết triệt để vấn đề này. Đây là hệ thống tự động hóa 100% không cần code, kết hợp sức mạnh của RAG (Retrieval-Augmented Generation), Google Drive, Pinecone Vector Database và mô hình AI Gemini tiên tiến để tạo ra một trợ lý IT Support thông minh, luôn sẵn sàng giải đáp mọi thắc mắc dựa trên chính tài liệu nội bộ của doanh nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn kho tri thức:** Khi có file PDF mới tải lên Google Drive, hệ thống tự động quét, trích xuất, làm sạch, chia nhỏ và đồng bộ vào Pinecone Vector Database mà không cần đụng tay.
- **Trợ lý AI chính xác tuyệt đối:** Chatbot trả lời câu hỏi dựa trên chính tài liệu nội bộ, hạn chế tối đa việc AI "bịa" thông tin (hallucination).
- **Tiết kiệm thời gian cho đội ngũ IT:** Giảm tải đến 80% các câu hỏi thường gặp (FAQs), giúp nhân sự IT tập trung vào các công việc chuyên sâu hơn.
- **Hoạt động liên tục 24/7:** Phản hồi tức thì mọi thắc mắc của nhân viên bất cứ lúc nào qua giao diện chat tích hợp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Drive Account** (Cấp quyền kết nối OAuth2).
- **Pinecone Account & Index** (Để lưu trữ vector embedding).
- **Google AI / Gemini API Key** (Dùng cho phần Embeddings).
- **OpenRouter API Key** (Dùng để gọi mô hình chat `google/gemini-2.0-flash-exp:free`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ [n8n.io workflows 3192](https://n8n.io/workflows/3192), sau đó copy toàn bộ nội dung JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Monitor Google Drive for New Files (`googleDriveTrigger`):** Kết nối tài khoản Google Drive của sếp và chọn thư mục cần theo dõi (Folder ID) nơi chứa các tài liệu IT/hướng dẫn sử dụng.
- **Download File from Google Drive (`googleDrive`):** Đảm bảo node này sử dụng chung cấu hình OAuth2 với Trigger để tải file về khi có sự kiện file mới xuất hiện.
- **Extract PDF Content & Clean and Normalize PDF Text (`extractFromFile`, `code`):** Node code sẽ giúp làm sạch văn bản thô, loại bỏ các ký tự thừa để tối ưu hóa quá trình embedding.
- **Generate Document Embeddings & Insert Document into Pinecone (`embeddingsGoogleGemini`, `vectorStorePinecone`):** 
  - Cấu hình API Key cho Google Gemini.
  - Kết nối tài khoản Pinecone, điền đúng tên Index và Namespace mà sếp đã tạo sẵn trên dashboard của Pinecone.
- **Retrieve Relevant Documents from Pinecone & OpenRouter Chat Model Interface (`vectorStorePinecone`, `lmChatOpenRouter`):**
  - Node AI Agent sẽ gọi mô hình `google/gemini-2.0-flash-exp:free` thông qua OpenRouter. Đảm bảo sếp đã điền đúng `openRouterApi` credentials.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test Run) bằng cách tải một file PDF mẫu lên thư mục Google Drive đã cấu hình để kiểm tra luồng nạp dữ liệu vào Pinecone.
- Mở **Chat Message Trigger** (`chatTrigger`) để test thử việc hỏi đáp với chatbot.
- Sau khi mọi thứ hoạt động trơn tru, các sếp hãy bấm nút **Active workflow** để đưa hệ thống vào vận hành thực tế!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh chat:** Các sếp có thể thay thế hoặc kết nối thêm node Telegram/Slack vào Chat Trigger để nhân viên có thể hỏi đáp trực tiếp ngay trên nhóm chat công ty.
- **Lưu trữ lịch sử chat:** Thêm node lưu log cuộc hội thoại vào Google Sheets hoặc Database để phân tích những vấn đề nhân viên thường gặp phải nhất.
- **Hỗ trợ đa định dạng:** Ngoài PDF, sếp có thể tùy biến workflow để đọc thêm file Word (.docx) hoặc Google Docs từ Drive.

### 📌 Kết luận
Workflow IT Support Chatbot này là một "vũ khí" cực kỳ lợi hại giúp doanh nghiệp tự động hóa khâu hỗ trợ nội bộ bằng AI thế hệ mới. Hãy áp dụng ngay hôm nay để tối ưu hóa vận hành và mang lại trải nghiệm làm việc hiện đại nhất cho đội ngũ của các sếp nhé!