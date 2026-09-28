---
title: "🤖 Tạo Agent Chat AI Tự Động Học (RAG) với Google Gemini & Qdrant - Tự Động Hóa Trả Lời Chuyên Nghiệp 100% Không Code"
description: "Workflow này tự động phân loại và trả lời các câu hỏi người dùng theo 4 chiến lược khác nhau (Thực tế, Phân tích, Đánh giá, Bối cảnh) bằng Google Gemini và Qdrant, giúp doanh nghiệp tiết kiệm thời gian và nâng cao chất lượng hỗ trợ khách hàng. Đặc biệt phù hợp cho chatbot doanh nghiệp, trung tâm hỗ trợ, hoặc hệ thống tư vấn chuyên sâu."
slug: "tao-agent-rag-google-gemini-qdrant"
tags: [n8n, automation, ai, chatbot, rag, google-gemini, qdrant, no-code]
keywords: [n8n workflow rag, tự động hóa chatbot ai, google gemini qdrant, agent chat tự động học, phân loại câu hỏi tự động, hỗ trợ khách hàng 24/7]
---

# 🚀 **Tạo Agent Chat AI Tự Động Học (RAG) với Google Gemini & Qdrant**
*Giải pháp tự động hóa trả lời câu hỏi chuyên nghiệp, cá nhân hóa và linh hoạt cho doanh nghiệp*

---
## **🔍 Nỗi Đau Của Doanh Nghiệp**
Hiện nay, khi doanh nghiệp triển khai **chatbot hỗ trợ khách hàng** hoặc **hệ thống tư vấn tự động**, họ thường gặp phải những vấn đề sau:
- **Trả lời không chính xác**: Chatbot trả lời chung chung, không phù hợp với ngữ cảnh cụ thể của người dùng.
- **Không linh hoạt**: Không phân biệt được giữa câu hỏi **thực tế** (ví dụ: "Lãi suất vay là bao nhiêu?") và **phân tích** (ví dụ: "So sánh 3 sản phẩm này như thế nào?").
- **Tốn thời gian**: Nhân viên phải thủ công phân loại và trả lời, làm giảm hiệu suất.
- **Không tích hợp tri thức**: Dữ liệu trong cơ sở tri thức (Knowledge Base) không được khai thác tối ưu.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Phân loại tự động** câu hỏi người dùng vào 4 loại: **Thực tế, Phân tích, Đánh giá, Bối cảnh**.
✅ **Tự động hóa trả lời** dựa trên chiến lược phù hợp, sử dụng **Google Gemini** (AI mạnh nhất hiện nay) và **Qdrant** (vector database).
✅ **Tích hợp tri thức** từ cơ sở dữ liệu vector để trả lời **chính xác và chuyên nghiệp**.
✅ **Hoạt động 24/7** mà không cần code, tiết kiệm thời gian và chi phí nhân sự.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Tự động trả lời **90% câu hỏi** của khách hàng, giảm tải cho đội ngũ hỗ trợ.
- **Chính xác cao**: Sử dụng **Google Gemini** để phân tích và trả lời dựa trên **bối cảnh cụ thể**.
- **Cá nhân hóa**: Hệ thống **học từ lịch sử hội thoại** (chat memory) để trả lời phù hợp hơn.
- **Tích hợp tri thức**: Khai thác **cơ sở dữ liệu vector (Qdrant)** để trả lời dựa trên kiến thức chuyên sâu.
- **Linh hoạt**: Phân loại và trả lời theo **4 chiến lược khác nhau** (Thực tế, Phân tích, Đánh giá, Bối cảnh).
- **Mở rộng dễ dàng**: Có thể tích hợp với **Slack, Telegram, hoặc website** để hỗ trợ khách hàng trực tiếp.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để sử dụng **Google Gemini API**):
   - [Đăng ký Google Cloud](https://cloud.google.com/) và tạo **API Key** cho **Generative AI API**.
   - Cài đặt **Google Gemini Embeddings** và **Chat API** trong tài khoản.
   - **Mã API Key** sẽ được sử dụng trong các node `lmChatGoogleGemini` và `embeddingsGoogleGemini`.

2. **Tài khoản Qdrant** (để lưu trữ và truy xuất dữ liệu vector):
   - [Đăng ký Qdrant Cloud](https://cloud.qdrant.io/) hoặc tự host Qdrant trên máy chủ.
   - **Vector Store ID** (ID của collection trong Qdrant) sẽ được sử dụng trong node `vectorStoreQdrant`.
   - **Khóa API** (API Key) của Qdrant (nếu sử dụng phiên bản cloud).

3. **Workflow Trigger**:
   - Workflow có thể được kích hoạt bằng:
     - **Webhook** (để tích hợp với website, Slack, Telegram...).
     - **Chat Interface** (n8n built-in) hoặc **bằng cách gọi từ workflow khác**.

4. **Dữ liệu tri thức (Knowledge Base)**:
   - Các tài liệu cần được **chuyển đổi thành vector embeddings** và lưu vào Qdrant trước khi sử dụng.
   - Có thể sử dụng **LangChain** hoặc **n8n** để chuẩn bị dữ liệu trước.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/5111](https://n8n.io/workflows/5111) (nếu có quyền).
- **Hoặc copy toàn bộ JSON** từ link trên và dán vào **n8n Editor** → **Import Workflow**.

:::note[**Lưu ý khi import**]
- **Không sao chép trực tiếp từ trang web** (do có ký tự đặc biệt), mà nên **tải file JSON** hoặc **sử dụng API của n8n** để lấy workflow.
- Nếu copy từ trang web, **xóa các ký tự không hợp lệ** (nếu có).
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **30 node**, nhưng các sếp cần **cấu hình chính xác** các node sau:

#### **🔹 Node `Combined Fields` (Set)**
- **Chức năng**: Chuẩn hóa input từ **webhook** hoặc **workflow khác**.
- **Cần thiết**: Điền các trường sau:
  - `user_query`: **Câu hỏi của người dùng** (ví dụ: "Lãi suất vay là bao nhiêu?").
  - `chat_memory_key`: **Khóa lưu trữ lịch sử hội thoại** (để AI nhớ các câu hỏi trước đó).
  - `vector_store_id`: **ID của collection Qdrant** (để lấy dữ liệu tri thức).

#### **🔹 Node `Query Classification` (Agent)**
- **Chức năng**: Phân loại câu hỏi vào **4 loại**:
  1. **Factual** (Thực tế): Câu hỏi cần **số liệu chính xác** (ví dụ: "Lãi suất là bao nhiêu?").
  2. **Analytical** (Phân tích): Câu hỏi cần **tóm tắt hoặc so sánh** (ví dụ: "So sánh 3 sản phẩm này").
  3. **Opinion** (Đánh giá): Câu hỏi cần **đánh giá chủ quan** (ví dụ: "Sản phẩm này tốt không?").
  4. **Contextual** (Bối cảnh): Câu hỏi cần **ngữ cảnh cụ thể** (ví dụ: "Tôi muốn mua sản phẩm này cho mục đích gì?").
- **Lưu ý**:
  - Node này sử dụng **Google Gemini** để phân loại.
  - **Không cần chỉnh sửa** nếu đã có **API Key** đúng.

#### **🔹 Node `Switch` (Routing)**
- **Chức năng**: **Chuyển hướng** workflow dựa trên kết quả phân loại.
- **Lưu ý**:
  - Các **4 chiến lược** (Factual, Analytical, Opinion, Contextual) sẽ được xử lý **tùy thuộc vào loại câu hỏi**.

#### **🔹 Các Node Chiến Lược (Agent)**
Mỗi chiến lược có **1 node Agent** riêng:
1. **Factual Strategy** (`Factual Strategy - Focus on Precision`):
   - **Chức năng**: **Tối ưu hóa câu hỏi** để trả lời **chính xác nhất**.
   - **Prompt**: "Tôi cần trả lời câu hỏi này với **số liệu chính xác** và **không sai lệch**."

2. **Analytical Strategy** (`Analytical Strategy - Comprehensive Coverage`):
   - **Chức năng**: **Phân tích sâu** câu hỏi và trả lời **tóm tắt toàn diện**.
   - **Prompt**: "Tôi cần **tóm tắt và so sánh** các khía cạnh của câu hỏi này."

3. **Opinion Strategy** (`Opinion Strategy - Diverse Perspectives`):
   - **Chức năng**: **Trả lời từ nhiều góc độ** (đánh giá chủ quan).
   - **Prompt**: "Tôi cần **đánh giá và đưa ra nhiều quan điểm** về câu hỏi này."

4. **Contextual Strategy** (`Contextual Strategy - User Context Integration`):
   - **Chức năng**: **Hiểu ngữ cảnh** của người dùng để trả lời phù hợp.
   - **Prompt**: "Tôi cần **hiểu ngữ cảnh** của người dùng và trả lời phù hợp với tình huống."

#### **🔹 Node `Gemini Classification` và `Gemini [Strategy]` (lmChatGoogleGemini)**
- **Chức năng**: Sử dụng **Google Gemini** để **tạo câu hỏi mới** hoặc **tối ưu hóa** dựa trên chiến lược.
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu đã có **API Key** và **model** (ví dụ: `gemini-pro`).
  - **Prompt** đã được cấu hình sẵn, nhưng có thể **tùy chỉnh** nếu cần.

#### **🔹 Node `vectorStoreQdrant` (Retrieve Documents)**
- **Chức năng**: **Truy xuất dữ liệu từ Qdrant** dựa trên **vector embeddings**.
- **Cần thiết**:
  - **Điền `vector_store_id`**: ID của collection trong Qdrant.
  - **Điền `apiKey`**: Khóa API của Qdrant (nếu dùng phiên bản cloud).
  - **Prompt**: `={{ $json.prompt }}\n\nUser query: \n{{ $json.output }}`
    *(Prompt này sẽ được tự động thay đổi dựa trên chiến lược.)*

#### **🔹 Node `Gemini Answer` (lmChatGoogleGemini)**
- **Chức năng**: **Tạo câu trả lời cuối cùng** dựa trên:
  - **Dữ liệu từ Qdrant** (đã được truy xuất).
  - **Lịch sử hội thoại** (chat memory).
  - **Chiến lược phù hợp** (Factual, Analytical, Opinion, Contextual).
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu đã có **API Key** và **model** đúng.

#### **🔹 Node `Respond to Webhook`**
- **Chức năng**: **Trả lời người dùng** qua **webhook** (nếu tích hợp với website, Slack, Telegram...).
- **Lưu ý**:
  - Nếu muốn **hiển thị trên chat n8n built-in**, có thể **bỏ qua node này** và sử dụng **node `executeWorkflowTrigger`** để gọi workflow khác.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **dữ liệu mẫu**:
   - Điền vào `user_query`: `"Lãi suất vay là bao nhiêu?"` (ví dụ).
   - Chạy workflow và **kiểm tra kết quả phân loại** (Factual, Analytical, Opinion, Contextual).
   - **Kiểm tra trả lời** có phù hợp không.

2. **Bật Active**:
   - Sau khi **test thành công**, chuyển **Active** để workflow hoạt động liên tục.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**TÍCH HỢP VỚI SLACK/TELEGRAM**]
- **Sử dụng node `Slack` hoặc `Telegram`** để **gửi câu trả lời tự động** cho khách hàng.
- **Cấu hình webhook** từ Slack/Telegram vào node `Respond to Webhook`.

:::info[**LƯU LOG & BÁO CÁO**]
- **Thêm node `Set` + `Google Sheets`** để **lưu lịch sử câu hỏi và trả lời**.
- **Tạo báo cáo định kỳ** bằng **node `Google Sheets`** hoặc **node `Email`**.

:::info[**TỰ ĐỘNG CẬP NHẬT TRI THỨC**]
- **Sử dụng node `HTTP Request`** để **cập nhật dữ liệu mới** vào Qdrant.
- **Kết hợp với node `Schedule`** để **cập nhật tri thức định kỳ**.

:::info[**TÍCH HỢP VỚI ZAPPIER/Make**]
- **Nếu muốn tích hợp với nhiều dịch vụ** (Google Drive, Notion, CRM...), có thể **sử dụng node `HTTP Request`** để gọi API từ **Zapier/Make**.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để **tự động hóa chatbot AI** với **Google Gemini và Qdrant**, giúp doanh nghiệp:
✔ **Tiết kiệm thời gian** và **giảm tải cho nhân viên**.
✔ **Trả lời chính xác** dựa trên **tri thức chuyên sâu**.
✔ **Học từ lịch sử hội thoại** để **cải thiện chất lượng**.
✔ **Hoạt động 24/7** mà **không cần code**.

**🚀 Hãy thử ngay và tự động hóa hệ thống hỗ trợ khách hàng của mình!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow **ổn định 24/7**, các sếp nên **self-host n8n** trên **VPS**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow AI)

---
**💡 Cần hỗ trợ thêm?** Hãy để lại **comment** bên dưới hoặc liên hệ với **Quantra Labs** qua:
- [Twitter](https://www.x.com/quantralabs)
-