---
title: "🤖 **Tự Động Hóa Chat AI với Tài Liệu Google Drive: RAG + GPT-5 + Supabase (Không Cần Code!)**"
description: "Workflow này tự động tải tài liệu từ Google Drive, xử lý bằng OCR, lưu trữ dưới dạng vector trong Supabase, và cho phép chat AI thông minh với GPT-5 thông qua Slack, Telegram, WhatsApp hoặc Gmail. Giúp các sếp tiết kiệm thời gian tìm kiếm thông tin và tăng cường hiệu suất công việc 24/7."
slug: "tieu-dong-hoa-chat-ai-voi-tai-lieu-google-drive"
tags: [n8n, automation, ai, rag, google-drive, supabase, openai, gpt-5, slack, telegram, whatsapp, gmail]
keywords: [n8n workflow chat ai, tự động hóa tài liệu google drive, rag với gpt-5, supabase vector database, chatbot doanh nghiệp, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Chat AI với Tài Liệu Google Drive: RAG + GPT-5 + Supabase**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất nhiều thời gian để tìm kiếm thông tin trong các tài liệu PDF, Word, hoặc hình ảnh từ Google Drive. Thậm chí, khi cần tra cứu thông tin cụ thể, họ phải mở từng file một và đọc kỹ – điều này không chỉ tốn thời gian mà còn dễ gây lỗi nhầm lẫn. **Workflow này giải quyết vấn đề này bằng cách:**
✅ **Tự động tải và xử lý** tất cả tài liệu từ Google Drive.
✅ **Chuyển đổi văn bản thành vector** và lưu trữ trong **Supabase Vector Database** (không cần cơ sở dữ liệu phức tạp).
✅ **Cho phép chat AI thông minh** với GPT-5 (hoặc các mô hình khác) thông qua **Slack, Telegram, WhatsApp, hoặc Gmail**.
✅ **Hỗ trợ OCR** để xử lý tài liệu dạng hình ảnh (PDF, scan).
✅ **Lưu trữ lịch sử chat** trong PostgreSQL để các sếp có thể tiếp tục trò chuyện mà không mất bối cảnh.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS riêng. N8n chạy tốt nhất trên máy chủ có **RAM 4GB+** và **CPU đa nhân**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công trong hàng trăm tài liệu.
- **Trả lời chính xác**: AI hiểu ngữ cảnh và trả lời dựa trên **tài liệu thực tế** (không phải giả thuyết).
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp.
- **Tích hợp nhiều kênh**: Chat qua **Slack, Telegram, WhatsApp, hoặc Gmail** – tùy chọn theo nhu cầu.
- **Lưu trữ thông minh**: Dữ liệu được **vector hóa** và lưu trong **Supabase**, tối ưu hóa tốc độ tra cứu.
- **Hỗ trợ OCR**: Xử lý được **tài liệu hình ảnh** (PDF scan, ảnh chụp).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (để tải tài liệu).
✔ **API Key OpenAI** (để sử dụng GPT-5 và Embeddings).
✔ **Supabase Project** (để lưu trữ vector database).
✔ **PostgreSQL Database** (để lưu trữ lịch sử chat).
✔ **Credentials cho các kênh chat**:
   - **Slack**: Token OAuth và Channel ID.
   - **Telegram**: Token Bot và ID Chat.
   - **WhatsApp**: Số điện thoại và mã xác minh (nếu sử dụng).
   - **Gmail**: Tài khoản và OAuth 2.0.
✔ **Mistral AI API Key** (nếu sử dụng OCR).

---
:::note[Lưu ý quan trọng]
- **Không cần cài đặt OpenAI API** trên máy chủ n8n (sử dụng proxy API).
- **Supabase và PostgreSQL** phải được cấu hình trước khi chạy workflow.
- **Tài liệu trong Google Drive** phải được chia sẻ với tài khoản n8n (hoặc là tài khoản cá nhân).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import từ file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/7308](https://n8n.io/workflows/7308).
2. Trong **n8n Editor**, nhấn **Import Workflow** và chọn file JSON.
3. Hoặc **copy toàn bộ JSON** và dán vào **Import Workflow** (tab **JSON**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **2 phần chính**:
- **Phần 1: Xử lý tài liệu (Google Drive → Supabase)**
- **Phần 2: Chat AI (Slack/Telegram/WhatsApp/Gmail → GPT-5)**

##### **A. Cấu Hình Phần Xử Lý Tài Liệu**
| **Node**               | **Cần Chỉnh Gì?**                                                                 | **Lưu Ý** |
|------------------------|----------------------------------------------------------------------------------|------------|
| **Google Drive Trigger** | Chọn **Folder** muốn tải tài liệu.                                               | Chọn **Folder Shareable** để n8n có quyền truy cập. |
| **Download File**      | Chọn **File ID** từ Google Drive.                                                | Nếu là file PDF hình ảnh, cần **OCR** (sử dụng Mistral AI). |
| **OCR (Mistral AI)**   | Điền **API Key Mistral** và chọn **Model** (nếu có).                          | Chỉ cần thiết nếu tài liệu là **hình ảnh/PDF scan**. |
| **Character Text Splitter** | Cấu hình **chunk size** (ví dụ: 500 từ/chunk).                                  | Lớn hơn → AI trả lời chi tiết hơn, nhưng tốn dung lượng. |
| **Embeddings OpenAI**  | Điền **API Key OpenAI** và chọn **Model** (ví dụ: `text-embedding-ada-002`).    | Đảm bảo **API Key** có đủ quota. |
| **Supabase Vector Store** | Điền **URL Supabase** và **API Key Supabase**.                                   | Cần tạo **Table** trong Supabase với cấu trúc phù hợp. |

##### **B. Cấu Hình Phần Chat AI**
| **Node**               | **Cần Chỉnh Gì?**                                                                 | **Lưu Ý** |
|------------------------|----------------------------------------------------------------------------------|------------|
| **Chat Trigger**       | Chọn **kênh chat** (Slack/Telegram/WhatsApp/Gmail).                                | Nếu dùng **Gmail**, cần cấu hình **OAuth 2.0**. |
| **GPT-5 (lmChatOpenAi)** | Điền **API Key OpenAI** và chọn **Model** (`gpt-5` hoặc `gpt-4`).                | **GPT-5** hiện chưa được hỗ trợ toàn cầu, có thể thay bằng **GPT-4**. |
| **RAG Agent**          | Cấu hình **Prompt** để AI trả lời dựa trên **tài liệu trong Supabase**.           | Có thể chỉnh sửa **system prompt** để phù hợp với ngành nghề. |
| **Slack/Telegram/WhatsApp/Gmail** | Điền **Credentials** (Token, Channel ID, số điện thoại, tài khoản Gmail). | **WhatsApp** cần **số điện thoại** và **mã xác minh**. |

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một **tài liệu mẫu** (ví dụ: PDF Word).
2. **Gửi tin nhắn** qua **Slack/Telegram/WhatsApp/Gmail** để kiểm tra AI trả lời.
3. **Bật Active** workflow khi đã kiểm tra xong.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Notion/Confluence**
   - Sử dụng **n8n-nodes-notion** để tự động **tạo bài viết** từ kết quả chat AI.

2. **Lưu Log Chat**
   - Sử dụng **n8n-nodes-base.stickyNote** để lưu **lịch sử chat** vào **Google Sheets** hoặc **Airtable**.

3. **Báo Cáo Định Kỳ**
   - Sử dụng **n8n-nodes-base.email** để **gửi báo cáo** về **số lượng query** và **thời gian phản hồi**.

4. **Sử Dụng GPT-4 Thay Vì GPT-5**
   - Nếu **GPT-5** không khả dụng, thay bằng **GPT-4** trong node `lmChatOpenAi`.

5. **Tối Ưu Hiệu Suất Supabase**
   - **Tạo Index** cho **Table Vector** trong Supabase để tăng tốc độ tra cứu.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp bằng cách **tự động hóa tìm kiếm thông tin** và **cung cấp AI chat thông minh** dựa trên tài liệu thực tế. **Không cần code**, chỉ cần **cấu hình đúng credentials** là có thể sử dụng ngay.

**Hãy áp dụng ngay và làm việc hiệu quả hơn!** 🚀
Nếu cần **hỗ trợ custom hóa**, liên hệ với **Paul (n8n Power User)** qua [n8n Community](https://community.n8n.io/).

---
**🔗 [Tải Workflow Mẫu](https://n8n.io/workflows/7308)** | **📌 [Cài Đặt n8n Self-Hosted](https://docs.n8n.io/)**