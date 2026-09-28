---
title: "🤖 Tạo Chatbot Chính Sách Công Ty Tự Động Hóa với RAG, Pinecone & OpenAI (Không Cần Code)"
description: "Workflow tự động hóa tạo chatbot trả lời câu hỏi về chính sách công ty bằng công nghệ RAG (Retrieval-Augmented Generation), Pinecone Vector Database và OpenAI GPT-4o-mini. Giúp tiết kiệm 80% thời gian hỗ trợ khách hàng và nhân viên, giảm sai sót, đồng thời cung cấp trải nghiệm cá nhân hóa 24/7."
slug: "tao-chatbot-chinh-sach-cong-ty-rag-pinecone-openai"
tags: [n8n, automation, ai-rag, pinecone, openai, chatbot, google-drive, no-code]
keywords: [n8n workflow chatbot chính sách công ty, tự động hóa hỗ trợ khách hàng, RAG với Pinecone và OpenAI, giải pháp AI không code, chatbot trả lời câu hỏi chính sách, vector database cho doanh nghiệp]
---

# 🚀 **Tạo Chatbot Chính Sách Công Ty Tự Động Hóa với RAG, Pinecone & OpenAI**

### **Giải pháp cho nỗi đau "Tôi phải trả lời hàng trăm câu hỏi về chính sách công ty hàng ngày"**
Các sếp đã từng gặp phải tình huống này: Nhân viên hoặc khách hàng liên tục gửi câu hỏi về chính sách công ty, như *"Làm thế nào để xin phép nghỉ phép?"*, *"Chính sách bảo mật dữ liệu như thế nào?"*, hoặc *"Tôi có thể làm việc từ xa bao lâu?"*. Những câu hỏi này thường lặp đi lặp lại, tốn thời gian và dễ gây sai sót nếu trả lời không chính xác. **Workflow này sẽ tự động hóa toàn bộ quy trình**, tạo một chatbot thông minh trả lời mọi câu hỏi về chính sách công ty bằng cách kết hợp:
- **RAG (Retrieval-Augmented Generation)**: Trích xuất thông tin chính xác từ tài liệu chính sách.
- **Pinecone Vector Database**: Lưu trữ và tìm kiếm thông tin nhanh chóng.
- **OpenAI GPT-4o-mini**: Trả lời tự nhiên, cá nhân hóa và logic.

Sau khi triển khai, các sếp sẽ **tiết kiệm 80% thời gian hỗ trợ**, giảm thiểu sai sót, và cung cấp trải nghiệm 24/7 cho nhân viên và khách hàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo tính bảo mật và khả năng mở rộng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 80% thời gian trả lời câu hỏi lặp đi lặp lại.
- **Chính xác 100%**: Trả lời dựa trên tài liệu chính sách chính thức, không sai sót.
- **Cá nhân hóa**: Chatbot hiểu ngữ cảnh và trả lời logic, giống như một chuyên viên HR.
- **Hoạt động 24/7**: Khách hàng và nhân viên có thể hỏi bất kỳ lúc nào.
- **Dễ dàng cập nhật**: Khi chính sách thay đổi, chỉ cần cập nhật tài liệu trên Google Drive là xong.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **OpenAI API Key**: Đăng ký tại [OpenAI](https://platform.openai.com/) và chọn model `gpt-4o-mini`.
   - **Pinecone API Key**: Đăng ký tại [Pinecone](https://www.pinecone.io/) và tạo một index mới.
   - **Google Drive OAuth 2.0**: Tạo một ứng dụng OAuth 2.0 trong [Google Cloud Console](https://console.cloud.google.com/) để truy cập folder chứa tài liệu chính sách.
   - **Folder Google Drive**: Chứa tất cả tài liệu chính sách công ty (PDF, DOCX, TXT...).

2. **Cài đặt Node LangChain**:
   - Workflow sử dụng các node LangChain của n8n. Các sếp cần cài đặt plugin này trong n8n:
     - Mở **n8n Editor** → **Settings (⚙️)** → **Plugins** → Tìm và cài đặt `@n8n/n8n-nodes-langchain`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/7563) (hoặc copy JSON từ link trên).
- Trong **n8n Editor**, nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô **Import Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **15 node** với logic phân thành **2 phần chính**:
- **Data Loader**: Tải và xử lý tài liệu từ Google Drive.
- **Data Retrieval**: Trả lời câu hỏi của người dùng bằng RAG.

##### **A. Cấu hình Data Loader (Tải và xử lý tài liệu)**
1. **Google Drive Trigger**:
   - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước khi import).
   - **Folder ID**: Điền ID của folder chứa tài liệu chính sách (tham khảo [Google Drive API](https://developers.google.com/drive/api/v3/manage-folders)).
   - **Polling Interval**: Đặt thành **60 giây** để kiểm tra thay đổi folder mỗi phút.

2. **Google Drive (Download)**:
   - **Credentials**: Chọn `googleDriveOAuth2Api`.
   - **File ID**: Sẽ tự động lấy từ Google Drive Trigger.

3. **Default Data Loader**:
   - **File Content**: Sẽ nhận từ node Google Drive (Download).
   - **Lưu ý**: Node này sẽ tự động phân tích và chia nhỏ tài liệu thành các chunk nhỏ (dùng cho Pinecone).

4. **Recursive Character Text Splitter**:
   - **Chunk Size**: Đặt thành **1000** (tùy chỉnh theo nhu cầu).
   - **Chunk Overlap**: Đặt thành **200** để đảm bảo liên kết logic giữa các chunk.

5. **Pinecone Vector Store (2 lần)**:
   - **Credentials**: Chọn `pineconeApi`.
   - **Index Name**: Điền tên index Pinecone đã tạo trước đó.
   - **Embedding Model**: Chọn `text-embedding-ada-002` (hoặc model khác của OpenAI).
   - **Vector Store Type**: Chọn `pinecone`.
   - **Lưu ý**: Node này sẽ lưu trữ các chunk tài liệu vào Pinecone để tìm kiếm sau này.

##### **B. Cấu hình Data Retrieval (Trả lời câu hỏi)**
1. **Chat Trigger**:
   - **Credentials**: Chọn `chatTrigger` (node này sẽ kích hoạt khi có tin nhắn mới).
   - **Lưu ý**: Các sếp có thể kết nối với Slack, Telegram, hoặc Webhook tùy chọn.

2. **Vector Store QnA**:
   - **Credentials**: Chọn `pineconeApi`.
   - **Index Name**: Điền tên index Pinecone tương tự như Data Loader.
   - **Query Model**: Chọn `text-embedding-ada-002`.
   - **Top K**: Đặt thành **3** (số lượng chunk trả về cho RAG).

3. **OpenAI Chat Model (2 lần)**:
   - **Credentials**: Chọn `openAiApi`.
   - **Model**: Chọn `gpt-4o-mini`.
   - **Prompt**: Node này sẽ tự động tạo prompt dựa trên kết quả từ Vector Store QnA.
   - **Lưu ý**: Các sếp có thể tùy chỉnh prompt để chatbot trả lời logic hơn.

4. **AI Agent**:
   - **Credentials**: Chọn `openAiApi`.
   - **Tools**: Chọn các tool liên quan (Calculator, Vector Store QnA...).
   - **Lưu ý**: Node này sẽ điều phối các tool để trả lời câu hỏi phức tạp.

5. **Simple Memory**:
   - **Credentials**: Không cần.
   - **Window Size**: Đặt thành **3** (lưu 3 tin nhắn gần nhất để chatbot hiểu ngữ cảnh).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và gửi một câu hỏi mẫu (ví dụ: *"Chính sách nghỉ phép của công ty như thế nào?"*).
   - Kiểm tra kết quả trả lời của chatbot.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để chatbot trả lời trên kênh team.

2. **Lưu log câu hỏi**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại tất cả câu hỏi và trả lời của chatbot.

3. **Báo cáo định kỳ**:
   - Sử dụng node **Google Sheets** hoặc **Email** để gửi báo cáo thống kê về câu hỏi thường gặp.

4. **Cập nhật tài liệu tự động**:
   - Khi có thay đổi chính sách, chỉ cần upload lại file vào Google Drive. Workflow sẽ tự động tải và cập nhật Pinecone.

5. **Tùy chỉnh prompt**:
   - Mở rộng prompt trong node **OpenAI Chat Model** để chatbot trả lời chuyên nghiệp hơn (ví dụ: thêm tone của công ty).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn tự động hóa hỗ trợ khách hàng và nhân viên về chính sách công ty **không cần viết một dòng code**. Với RAG, Pinecone và OpenAI, chatbot không chỉ trả lời nhanh mà còn **chính xác và logic**, giúp các sếp tập trung vào công việc chiến lược hơn.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với câu hỏi mẫu** và điều chỉnh prompt nếu cần.
3. **Bật Active** và chia sẻ với team để trải nghiệm!

Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy liên hệ với [Pramod Kumar Rathoure](https://n8n.io/workflows/7563) (tác giả của workflow) hoặc cộng đồng n8n tại [Discord](https://discord.gg/n8n). **Tự động hóa là tương lai – bắt đầu từ hôm nay!** 🚀