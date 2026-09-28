---
title: "🤖 Tự Động Hóa Chat AI Trực Tuyến Với Tài Liệu Nội Bộ - Ollama + Supabase + Google Drive (Không Cần Code)"
description: "Workflow này giúp các sếp tự động hóa việc chat AI với tài liệu nội bộ (PDF, Excel, Word) bằng Ollama (LLM), Supabase Vector DB và Google Drive. Giải phóng thời gian, tăng hiệu suất tra cứu thông tin và cá nhân hóa hỗ trợ cho nhân viên."
slug: "tieu-dong-hoa-chat-ai-voi-tai-lieu-noi-bo"
tags: [n8n, automation, ollama, supabase, google-drive, ai-rag, no-code]
keywords: [n8n workflow chat ai, tự động hóa tài liệu nội bộ, ollama supabase vector db, chatbot nội bộ không code, tra cứu thông tin từ google drive]
---

# 🚀 **Chat AI Trực Tuyến Với Tài Liệu Nội Bộ - Giải Pháp Tự Động Hóa 100% Không Code**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp và nhân viên phải mất **thời gian quý báu** để:
- **Tra cứu thông tin** trong hàng trăm tài liệu PDF, Excel, hoặc Word trên Google Drive.
- **Tóm tắt hoặc tổng hợp** dữ liệu từ nhiều nguồn khác nhau.
- **Hỗ trợ khách hàng/nhân viên** bằng cách giải thích nội dung phức tạp từ tài liệu nội bộ.
- **Cập nhật thường xuyên** khi tài liệu mới được thêm hoặc sửa đổi.

**Kết quả?** Thời gian phản hồi chậm, sai sót cao, và hiệu suất công việc bị ảnh hưởng.

---
### **🎯 Giải Pháp: Workflow Chat AI Tự Động Hóa**
Workflow này **tích hợp Ollama (LLM), Supabase Vector DB và Google Drive** để:
✅ **Tự động tra cứu và tổng hợp** thông tin từ tất cả tài liệu nội bộ.
✅ **Chat AI trực tiếp** với tài liệu (PDF, Excel, Word) như một trợ lý 24/7.
✅ **Cập nhật tự động** khi có tài liệu mới được thêm hoặc sửa đổi trên Google Drive.
✅ **Giữ lịch sử chat** để hỗ trợ cá nhân hóa cho từng người dùng.
✅ **Không cần viết code** – chỉ cần cấu hình và chạy!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm thiểu 80% thời gian tra cứu và tổng hợp thông tin thủ công.
- **Tính chính xác cao**: AI hiểu và trả lời chính xác từ tài liệu nội bộ.
- **Hỗ trợ 24/7**: Nhân viên có thể chat với AI bất kỳ lúc nào, bất kể giờ làm việc.
- **Cập nhật tự động**: Khi có tài liệu mới, hệ thống tự động cập nhật và sẵn sàng sử dụng.
- **Cá nhân hóa**: Giữ lịch sử chat để AI hiểu rõ hơn về nhu cầu của từng người dùng.
- **Tính bảo mật cao**: Tài liệu chỉ được truy cập trong nội bộ và không bị lộ ra ngoài.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để kết nối và tải tài liệu).
2. **Tài khoản Supabase** (để lưu trữ Vector DB và quản lý embeddings).
   - **Bước 1**: Tạo một **Supabase Project** tại [supabase.com](https://supabase.com/).
   - **Bước 2**: Tạo **API Key** và **Database URL** trong **Project Settings > API**.
3. **Ollama được cài đặt và chạy** trên máy chủ (cần cài đặt mô hình `nomic-embed-text` và `llama3.1`).
   - **Hướng dẫn cài Ollama**:
     ```bash
     curl -fsSL https://ollama.com/install.sh | sh
     ollama pull nomic-embed-text
     ollama pull llama3.1
     ```
4. **n8n Self-hosted** (cài đặt trên VPS hoặc máy chủ riêng).
5. **Credentials trong n8n**:
   - `googleDriveOAuth2Api` (để kết nối Google Drive).
   - `supabaseApi` (để kết nối Supabase).
   - `ollamaApi` (để kết nối Ollama).

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow** từ [n8n.io/workflows/6894](https://n8n.io/workflows/6894) hoặc sử dụng file JSON đã cung cấp.
- **Cách import**:
  - Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
  - **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **3 phần chính**:
- **Tool để thêm tài liệu từ Google Drive vào Vector DB**.
- **RAG AI Agent với giao diện chat**.
- **Cập nhật tự động khi có tài liệu mới**.

##### **A. Cấu Hình Google Drive & Supabase**
1. **Node "File Created" và "File Updated"**:
   - Đảm bảo **credentials `googleDriveOAuth2Api`** đã được cấu hình trong n8n.
   - Chọn **Google Drive Folder** cần theo dõi (nơi chứa tài liệu nội bộ).

2. **Node "Delete Old Doc Rows"**:
   - Cần **Supabase Table** đã được tạo sẵn để lưu embeddings.
   - **SQL Query** trong node này sẽ xóa các bản ghi cũ nếu file đã được cập nhật.

3. **Node "Insert into Supabase Vectorstore"**:
   - **Table Name**: Đặt tên cho bảng lưu trữ embeddings (ví dụ: `documents`).
   - **Column Config**:
     - `id`: UUID (auto-generate).
     - `content`: Text của tài liệu.
     - `embedding`: Vector embeddings từ Ollama.
     - `file_id`: ID của file trong Google Drive.
     - `file_name`: Tên file.

##### **B. Cấu Hình Ollama & AI Chat**
1. **Node "Embeddings Ollama"**:
   - **Model**: `nomic-embed-text:latest` (đã cài sẵn trong Ollama).
   - **Input**: Dữ liệu text từ `Extract Document Text` hoặc `Extract from Excel`.

2. **Node "Ollama Chat Model"**:
   - **Model**: `llama3.1:latest`.
   - **Prompt Template**: Có thể tùy chỉnh để phù hợp với nhu cầu chat (ví dụ: "Tôi là trợ lý hỗ trợ nội bộ, hãy trả lời dựa trên tài liệu đã cung cấp").

3. **Node "RAG AI Agent"**:
   - **Tools**:
     - `User_documents` (truy cập Vector DB trong Supabase).
     - `Ollama Chat Model` (để trả lời).
   - **Prompt**: Có thể chỉnh sửa để AI trả lời chính xác hơn (ví dụ: "Hãy trả lời dựa trên thông tin từ tài liệu, nếu không biết thì nói 'Tôi không có thông tin về điều này'").

##### **C. Webhook & Chat Interface**
1. **Node "Webhook"**:
   - **Path**: `rag-chat` (đặt tên tùy ý).
   - **HTTP Method**: `POST`.
   - **Credentials**: Không cần (hoặc sử dụng Basic Auth nếu cần bảo mật).

2. **Node "When chat message received"**:
   - **Trigger**: Khi có yêu cầu chat từ người dùng (ví dụ: POST JSON `{ "message": "Tôi muốn biết về dự án X" }`).
   - **Output**: Trả về kết quả chat từ AI.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Tải một file mẫu (PDF/Excel) lên Google Drive.
   - Gửi yêu cầu chat đến Webhook (ví dụ: `POST http://<n8n-server>/rag-chat` với body `{ "message": "Giải thích về tài liệu này" }`).
   - Kiểm tra kết quả trả về từ AI.

2. **Bật Active Workflow**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active** trong n8n.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Sử dụng **n8n Slack Node** hoặc **Telegram Bot Node** để người dùng chat với AI qua ứng dụng ưa thích.
   - **Cách làm**:
     - Sau khi AI trả lời, gửi kết quả qua Slack/Telegram bằng **n8n Slack Node** với message:
       ```json
       {
         "text": "Kết quả từ AI: {{ $node["RAG AI Agent"].json["answer"] }}"
       }
       ```

2. **Lưu Log & Báo Cáo**:
   - Sử dụng **n8n Database Node** hoặc **Google Sheets Node** để lưu lịch sử chat.
   - **Ví dụ**:
     - Sau mỗi lần chat, lưu dữ liệu vào Google Sheets với cột: `Người dùng`, `Yêu cầu`, `Trả lời`, `Thời gian`.

3. **Tự động Cập Nhật Tài Liệu**:
   - Nếu có nhiều người chỉnh sửa tài liệu, **n8n sẽ tự động cập nhật** khi file được thay đổi (do node `File Updated`).
   - **Lưu ý**: Đảm bảo **credentials Google Drive** có quyền chỉnh sửa file.

4. **Tùy Chỉnh Prompt cho AI**:
   - Nếu AI trả lời không chính xác, chỉnh sửa **prompt** trong node `RAG AI Agent` để rõ ràng hơn.
   - **Ví dụ**:
     ```plaintext
     Bạn là trợ lý hỗ trợ nội bộ. Hãy trả lời dựa trên thông tin từ tài liệu đã cung cấp.
     Nếu câu hỏi không liên quan, hãy nói: "Tôi không có thông tin về điều này".
     ```

5. **Optimize Performance**:
   - Nếu workflow chạy chậm, giảm **chunk size** trong node `Character Text Splitter` (ví dụ: từ 500 xuống 300 ký tự).
   - **Lưu ý**: Chunk size nhỏ hơn sẽ làm AI trả lời chi tiết hơn nhưng tốn thời gian xử lý.

---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp và nhân viên bằng cách tự động hóa việc tra cứu, tổng hợp và chat với tài liệu nội bộ. **Không cần viết code**, chỉ cần cấu hình và chạy – hoàn toàn phù hợp với mô hình **No-Code Automation**.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n Self-hosted** trên VPS (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình các credentials.
3. **Test với một file mẫu** và bắt đầu sử dụng!

**Câu hỏi thường gặp**:
- **AI trả lời không chính xác**: Kiểm tra lại **prompt** và **tài liệu input**.
- **Workflow không hoạt động**: Đảm bảo **Ollama, Supabase và Google Drive** đều kết nối đúng.
- **Tài liệu không được cập nhật**: Kiểm tra **permissions** của Google Drive và **credentials** trong n8n.

**Chia sẻ và phản hồi**: Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n.io/community](https://n8n.io/community). 🚀