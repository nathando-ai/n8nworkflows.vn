---
title: "🤖 Tự Động Xử Lý Tài Liệu Phức Tập với Chunking Tự Động: Google Drive + OpenAI + Gemini RAG"
description: "Workflow tự động hóa 100% không code giúp các sếp xử lý, tóm tắt và tra cứu thông tin từ tài liệu PDF/TEXT trên Google Drive bằng AI, tiết kiệm 80% thời gian so với cách làm thủ công. Kết quả: dữ liệu được phân tích, lưu trữ vector và trả lời câu hỏi thông minh bằng Gemini AI."
slug: "tieu-ly-tai-lieu-voi-chunking-ai"
tags: [n8n, automation, ai-rag, google-drive, openai, gemini, vector-database]
keywords: [tự động hóa xử lý tài liệu, chunking tài liệu pdf, google drive + ai, gemini rag n8n, tự động tóm tắt tài liệu, tra cứu thông tin bằng ai]
---

# 🚀 **Tự Động Xử Lý & Tra Cứu Tài Liệu Phức Tập với AI (Chunking + RAG)**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp thường phải:
- **Tốn thời gian vô cùng** để đọc, tóm tắt và tra cứu thông tin từ hàng trăm tài liệu PDF, báo cáo, hoặc văn bản dài.
- **Mất mát thông tin quan trọng** khi không có hệ thống lưu trữ thông minh, dẫn đến quyết định sai lầm.
- **Khó tra cứu nhanh** khi cần tìm kiếm thông tin cụ thể trong một tài liệu dài (ví dụ: hợp đồng, báo cáo tài chính, nghiên cứu khoa học).
- **Phải làm thủ công** việc phân tích và tổng hợp dữ liệu, gây ra sự chậm trễ trong quá trình làm việc.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động tải và xử lý** tất cả tài liệu mới trên Google Drive.
✅ **Phân tích và tóm tắt** nội dung bằng AI (OpenAI + Gemini).
✅ **Lưu trữ thông minh** bằng Vector Database (Supabase) để tra cứu nhanh.
✅ **Trả lời câu hỏi thông minh** bằng RAG (Retrieval-Augmented Generation), kết hợp Gemini AI và OpenAI.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công: AI tự động xử lý tài liệu trong vài phút thay vì giờ.
- **Tra cứu thông tin nhanh chóng** bằng cách hỏi như người thường: *"Hãy cho tôi biết điểm chính trong hợp đồng này?"* hoặc *"Tóm tắt phần 3 của báo cáo tài chính?"*
- **Lưu trữ thông minh** với Vector Database, giúp AI hiểu ngữ cảnh và trả lời chính xác hơn.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu trữ tài liệu và kích hoạt trigger tự động).
2. **API Key OpenAI** (để sử dụng GPT-4o-mini và Embeddings).
3. **Tài khoản Supabase** (để lưu trữ vector embeddings).
4. **Tài khoản Google Cloud (Google Gemini API)** (nếu muốn sử dụng Gemini AI).
5. **n8n Self-hosted** (để workflow chạy 24/7 ổn định).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/5521](https://n8n.io/workflows/5521) và import vào n8n Editor.
- **Copy/Paste JSON** từ link trên vào n8n Editor (tab "Import").

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **3 phần chính**:
- **Phần 1: Xử lý tài liệu (Document Ingestion & Processing)**
  - **Google Drive Trigger** (cần cấu hình OAuth2 của Google Drive).
  - **Switch** (chọn loại file: PDF hoặc TEXT).
  - **Extract from PDF/TEXT** (tách nội dung ra).
  - **Recursive Splitter** (phân chia tài liệu thành chunks logic, không chỉ theo ký tự).

- **Phần 2: Tạo Embeddings & Lưu Trữ (Embedding & Storage)**
  - **OpenAI Embeddings** (tạo vector từ chunks).
  - **Supabase Vector Store** (lưu embeddings + metadata).
  - **Summarize** (tóm tắt tài liệu bằng AI).

- **Phần 3: Tra Cứu & Trả Lời Câu Hỏi (Query Processing)**
  - **Manual Trigger** (bắt đầu khi người dùng nhấn "Execute").
  - **AI Agent** (orchestrate tra cứu bằng vector + keyword).
  - **Google Gemini Chat** (trả lời câu hỏi bằng ngữ cảnh từ tài liệu).

##### **Cấu hình chi tiết các node quan trọng:**
| **Node**               | **Lưu Ý Cần Chỉnh**                                                                 | **Tham Số Cần Điền**                          |
|------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **Google Drive Trigger** | Chọn folder Google Drive cần theo dõi.                                            | Folder ID, OAuth2 Google Drive.               |
| **OpenAI Chat Model**   | Chọn model `gpt-4o-mini` (miễn phí và hiệu quả).                                    | API Key OpenAI.                               |
| **Embeddings OpenAI**   | Chọn model embeddings phù hợp (ví dụ: `text-embedding-ada-002`).                     | API Key OpenAI.                               |
| **Supabase Vector Store** | Cấu hình URL và API Key của Supabase.                                             | URL Supabase, API Key, Table Name (ví dụ: `documents`). |
| **Google Gemini Chat**  | Nếu muốn sử dụng Gemini, cần API Key từ Google Cloud.                              | API Key Google Cloud.                         |
| **Recursive Splitter**  | Node này **không thể bỏ qua** vì nó phân chia tài liệu thành chunks logic.          | Cần chỉnh code trong node (xem phần **Mẹo nâng cao**). |

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một tài liệu mẫu (PDF hoặc TEXT) để kiểm tra:
   - AI có tóm tắt đúng không?
   - Embeddings có lưu vào Supabase không?
   - Gemini có trả lời câu hỏi chính xác không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu Recursive Splitter**
   - Node này sử dụng **code custom** để phân chia tài liệu thành chunks logic (không chỉ theo ký tự).
   - **Lưu ý:** Nếu không muốn chỉnh code, có thể thay thế bằng `textSplitterCharacterTextSplitter` (nhưng hiệu quả kém).
   - **Mẫu code tham khảo** (nếu cần chỉnh sửa):
     ```javascript
     // Chỉnh trong node "Recursive Splitter" (type: code)
     const chunks = [];
     const currentChunk = { text: "", metadata: {} };
     let lastSentenceEnd = 0;

     // Logic phân chia dựa trên câu và ngữ cảnh (cần tối ưu)
     // Ví dụ: Phân chia khi gặp từ kết thúc câu (., !, ?)
     // ...
     return chunks;
     ```

2. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack/Telegram Webhook** để nhận thông báo khi có tài liệu mới được xử lý.
   - Ví dụ: *"Tài liệu [Tên File] đã được tóm tắt và lưu vào Vector DB!"*

3. **Lưu Log & Báo Cáo Định Kỳ**
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử xử lý tài liệu.
   - Tự động gửi báo cáo hàng tuần về số lượng tài liệu được xử lý.

4. **Sử dụng Gemini AI cho Trả Lời Tự Động**
   - Nếu không muốn sử dụng Gemini, có thể thay thế bằng **OpenAI Chat Model** để trả lời câu hỏi.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần:
✔ **Tự động hóa xử lý tài liệu** (PDF, TEXT) từ Google Drive.
✔ **Tra cứu thông tin nhanh** bằng cách hỏi AI như người thường.
✔ **Lưu trữ thông minh** với Vector Database (Supabase).
✔ **Tiết kiệm thời gian** và giảm thiểu sai lầm trong quyết định.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với một tài liệu mẫu** để đảm bảo hoạt động.
3. **Bật Active** và bắt đầu tự động hóa!

---
**💡 Cần hỗ trợ thêm?**
- **Join Cộng Đồng n8n Việt Nam** tại [Facebook Group](https://www.facebook.com/groups/n8nvietnam).
- **Đăng ký VPS n8n** với mã giảm giá **VPSN8N** để workflow chạy ổn định 24/7.