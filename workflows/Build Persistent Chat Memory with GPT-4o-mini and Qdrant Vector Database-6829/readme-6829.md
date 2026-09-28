---
title: "🧠 Tự Động Hóa Hệ Thống Nhớ Dài Hạn Cho AI với GPT-4o-mini & Qdrant (RAG Self-Hosted)"
description: "Workflow này xây dựng một hệ thống nhớ dài hạn (long-term memory) cho AI bằng cách kết hợp GPT-4o-mini của OpenAI và cơ sở dữ liệu vector Qdrant, giúp AI nhớ lại lịch sử hội thoại, cải thiện chất lượng tương tác và tiết kiệm chi phí token. Đặc biệt phù hợp cho chatbot doanh nghiệp, trợ lý AI cá nhân hoặc hệ thống quản lý tri thức."
slug: "tieu-dong-hoa-he-thong-nho-dai-han-ai-gpt-4o-mini-qdrant"
tags: [n8n, automation, ai-rag, openai, qdrant, self-hosted, chatbot, no-code]
keywords: [n8n workflow ai nhớ dài hạn, tự động hóa chatbot với qdrant, gpt-4o-mini memory system, rag self-hosted, lưu trữ hội thoại ai, giảm chi phí token ai]
---

# 🚀 **Xây Dựng Hệ Thống Nhớ Dài Hạn Cho AI với GPT-4o-mini & Qdrant (Self-Hosted)**

## **📌 Nỗi Đau Của Doanh Nghiệp & Giải Pháp Tự Động Hóa**
Hiện nay, khi tương tác với AI thông qua chatbot hoặc trợ lý ảo, các sếp thường gặp phải những vấn đề sau:
- **AI quên lịch sử**: Mỗi lần bắt đầu một cuộc hội thoại mới, AI không nhớ được thông tin trước đó → mất thời gian giải thích lại.
- **Trải nghiệm không cá nhân hóa**: AI không hiểu được sở thích, ngữ cảnh cá nhân của người dùng.
- **Chi phí token cao**: AI phải tái xử lý cùng một thông tin nhiều lần → lãng phí ngân sách.
- **Không bảo mật dữ liệu**: Dữ liệu hội thoại thường bị xóa sau mỗi phiên → khó theo dõi và phân tích.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tạo hệ thống nhớ dài hạn (Long-Term Memory)** cho AI, giúp nó nhớ lại toàn bộ lịch sử hội thoại.
✅ **Cải thiện chất lượng tương tác** bằng cách sử dụng **RAG (Retrieval-Augmented Generation)** kết hợp với **Qdrant** (cơ sở dữ liệu vector).
✅ **Giảm chi phí token** lên đến 40% bằng cách tránh tái xử lý thông tin cũ.
✅ **Cá nhân hóa trải nghiệm** cho từng người dùng.
✅ **Bảo mật dữ liệu** bằng cách lưu trữ và quản lý hội thoại một cách chuyên nghiệp.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI không cần giải thích lại lịch sử → người dùng tiết kiệm 30-50% thời gian tương tác.
- **Chất lượng cao hơn**: AI trả lời chính xác, liên quan và cá nhân hóa dựa trên lịch sử.
- **Giảm chi phí**: Tối ưu hóa token usage → tiết kiệm ngân sách AI lên đến **40%**.
- **Hoạt động 24/7**: Hệ thống tự động lưu trữ và phục hồi dữ liệu, không cần can thiệp thủ công.
- **Dễ dàng mở rộng**: Phù hợp cho chatbot doanh nghiệp, trợ lý AI cá nhân, hoặc hệ thống quản lý tri thức.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **API Keys**:
   - **OpenAI API Key** (để sử dụng GPT-4o-mini và text-embedding-3-small).
   - **Cohere API Key** (tùy chọn, để sử dụng **Reranker** cải thiện độ chính xác).
   - **Qdrant API Key** (để kết nối với cơ sở dữ liệu vector).
2. **Cơ sở hạ tầng**:
   - **n8n Self-Hosted** (để chạy workflow 24/7).
   - **Qdrant Instance** (có thể là **Qdrant Cloud** hoặc **self-hosted**).
3. **Dữ liệu đầu vào**:
   - Các cuộc hội thoại mẫu (nếu muốn test trước khi triển khai).
4. **Ngân sách**:
   - **OpenAI**: ~$0.02/1M tokens (embeddings) + ~$0.15-$0.60/1M tokens (chat).
   - **Cohere**: ~$1/1000 re-rankings (nếu sử dụng).
   - **Qdrant**: Miễn phí cho phiên bản cloud (có giới hạn), hoặc ~$0.001/1M vectors (self-hosted).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) để self-host n8n ổn định.
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** cho Qdrant.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/6829](https://n8n.io/workflows/6829) (nếu có quyền).
2. **Nhấn vào "Export"** trên canvas n8n Editor.
3. **Chọn "Export as JSON"** và tải xuống file.
4. **Trên n8n Editor**, nhấn **"Import"** → Chọn file JSON vừa tải.
5. **Xác nhận import** và workflow sẽ được tạo ra.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở file JSON** từ [n8n.io/workflows/6829](https://n8n.io/workflows/6829) (nếu có quyền).
2. **Copy toàn bộ nội dung JSON**.
3. **Trên n8n Editor**, nhấn **"Import"** → Chọn **"Paste JSON"** và dán nội dung.
4. **Xác nhận** và workflow sẽ được tạo.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **13 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

#### **🔹 Node 1: Embeddings OpenAI (text-embedding-3-small)**
- **Mục đích**: Chuyển đổi văn bản thành vector 1024 chiều để lưu trữ trong Qdrant.
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi` (đã cấu hình trước).
  - **Model**: `text-embedding-3-small` (được khuyến nghị vì **tối ưu chi phí & hiệu suất**).
  - **Dimensions**: **1024** (phải khớp với Qdrant).

#### **🔹 Node 2: Default Data Loader**
- **Mục đích**: Chuẩn hóa dữ liệu hội thoại trước khi chia nhỏ.
- **Lưu ý**:
  - Không cần cấu hình thêm, chỉ cần **nối với node Text Splitter** sau.

#### **🔹 Node 3: Recursive Character Text Splitter**
- **Mục đích**: Chia nhỏ văn bản thành các chunk nhỏ (200 ký tự) với **overlap 40%** để bảo toàn ngữ cảnh.
- **Cấu hình**:
  - **Chunk Size**: `200` (tối ưu cho hội thoại).
  - **Overlap**: `40` (giúp AI hiểu liên kết giữa các chunk).

#### **🔹 Node 4: When chat message received (chatTrigger)**
- **Mục đích**: Nhận đầu vào từ người dùng (có thể kết nối với **webhook** hoặc **chat widget**).
- **Cấu hình**:
  - **Credentials**: Không cần (sử dụng mặc định).
  - **Lưu ý**: Sau khi kích hoạt workflow, **webhook URL** sẽ được cung cấp để kết nối với ứng dụng bên ngoài.

#### **🔹 Node 5: Embeddings for Retrieval (text-embedding-3-small)**
- **Mục đích**: Tạo vector cho **câu hỏi mới** để tìm kiếm trong Qdrant.
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **Model**: **Không được thay đổi** (phải giống với node Embeddings OpenAI đầu tiên).

#### **🔹 Node 6: Reranker Cohere (tùy chọn)**
- **Mục đích**: Sắp xếp lại kết quả tìm kiếm theo **độ tương quan cao nhất** (cải thiện độ chính xác).
- **Cấu hình**:
  - **Credentials**: `cohereApi`.
  - **Lưu ý**:
    - Nếu không muốn sử dụng, **bỏ qua node này** để tiết kiệm chi phí (~$1/1000 re-rankings).
    - **Không thể bỏ node này nếu muốn tối ưu hóa chất lượng**.

#### **🔹 Node 7 & 12: RAG_MEMORY & Store Conversation (vectorStoreQdrant)**
- **Mục đích**:
  - **RAG_MEMORY**: Lấy dữ liệu từ Qdrant khi AI cần nhớ lại lịch sử.
  - **Store Conversation**: Lưu hội thoại mới vào Qdrant.
- **Cấu hình**:
  - **Credentials**: `qdrantApi`.
  - **Collection**: `'ltm'` (long-term memory).
  - **Top K**: `20` (số lượng kết quả tìm kiếm tối ưu).
  - **Lưu ý**:
    - **Không được thay đổi tên collection** nếu đã có dữ liệu cũ.
    - **Batch size**: `100` (tối ưu hiệu suất).

#### **🔹 Node 8: OpenAI Chat Model (GPT-4o-mini)**
- **Mục đích**: Sử dụng mô hình **GPT-4o-mini** để trả lời người dùng.
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **Model**: `gpt-4o-mini` (không được thay đổi).
  - **Lưu ý**:
    - **Tối ưu chi phí**: GPT-4o-mini rẻ hơn GPT-4 nhưng vẫn hiệu quả.

#### **🔹 Node 9: Structured Output Parser**
- **Mục đích**: Đảm bảo dữ liệu trả về có **cấu trúc nhất quán** (Session ID, User Input, AI Output, Timestamp).
- **Cấu hình**:
  - **Không cần thay đổi**, chỉ cần **nối với node Format Response**.

#### **🔹 Node 10: Format Response**
- **Mục đích**: Lọc bỏ **metadata** và chỉ giữ lại **nội dung trả lời** cho người dùng.
- **Cấu hình**:
  - **Không cần thay đổi**, chỉ cần **nối với node AI Agent**.

#### **🔹 Node 11: AI Agent**
- **Mục đích**: **Cơ chế trung tâm** điều khiển toàn bộ workflow (tương tác với RAG_MEMORY, xử lý logic).
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **System Prompt**: **Không được chỉnh sửa** (định nghĩa cách AI sử dụng nhớ dài hạn).
  - **Lưu ý**:
    - **Tối ưu hóa chi phí**: AI sẽ **trích xuất thông tin từ Qdrant** trước khi trả lời → giảm token usage.

#### **🔹 Node 13: GPT-4o-mini (Main)**
- **Mục đích**: **Mô hình chính** xử lý yêu cầu cuối cùng.
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **Model**: `gpt-4o-mini` (không được thay đổi).
  - **Lưu ý**:
    - **Không được bỏ node này**, nó là **trái tim** của workflow.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Nhấn **"Run"** trên node **When chat message received**.
   - Gửi một **câu hỏi mẫu** (ví dụ: *"Hôm qua chúng ta đã nói về gì?"*).
   - Kiểm tra **AI có trả lời chính xác không** (nếu không, kiểm tra lại cấu hình Qdrant hoặc API keys).

2. **Bật Active**:
   - Sau khi test thành công, **nhấn "Active"** để workflow chạy liên tục.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Kết Nối với Slack/Telegram**
- **Cách làm**:
  - Sử dụng **node Slack Webhook** hoặc **Telegram Bot** để nhận tin nhắn từ Slack/Telegram.
  - **Nối node này vào node `When chat message received`**.
- **Lợi ích**:
  - AI có thể **trả lời ngay trên Slack/Telegram** mà không cần website riêng.

### **🔹 2. Lưu Log & Báo Cáo Định Kỳ**
- **Cách làm**:
  - Thêm **node `Set`** sau node **Store Conversation** để lưu **log hội thoại** vào Google Sheets.
  - Sử dụng **node `Schedule`** để chạy **báo cáo hàng tuần** về hoạt động của AI.
- **Lợi ích**:
  - **Theo dõi hiệu suất** của AI.
  - **Phân tích dữ liệu** để cải thiện chất lượng.

### **🔹 3. Tối ưu hóa Chi Phí**
- **Cách làm**:
  - **Bỏ node Reranker Cohere** nếu không cần độ chính xác cao.
  - **Sử dụng GPT-4o-mini thay vì GPT-4** (tiết kiệm ~50% chi phí).
  - **Lưu trữ dữ liệu cũ** trong Qdrant theo thời gian (xóa dữ liệu >3 tháng).
- **Lợi ích**:
  - **Giảm chi phí token** lên đến **40%**.

### **🔹 4. Cải Thiện Trải Nghiệm Người Dùng**
- **Cách làm**:
  - Thêm **node `Set`** để **ghi lại phản hồi của người dùng** (ví dụ: "Đáp án không chính xác").
  - Sử dụng **AI Agent** để **học từ phản hồi** và cải thiện tương lai.
- **Lợi ích**:
  - **AI trở nên thông minh hơn** theo thời gian.

### **🔹 5. Self-Host Qdrant**
- **Cách làm**:
  - Cài đặt **Qdrant trên VPS** (sử dụng Docker).
  - **Kết nối Qdrant self-hosted** vào node `vectorStoreQdrant`.
- **Lợi ích**:
  - **Không phụ thuộc vào cloud