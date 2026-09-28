---
title: "🤖 Xây Dựng Chatbot Trả Lời Câu Hỏi Bằng Tài Liệu (RAG) Với Supabase Vector Search & OpenRouter - Tự Động Hóa AI Cho Doanh Nghiệp"
description: "Workflow này tự động hóa quá trình tạo chatbot trả lời câu hỏi dựa trên tài liệu PDF bằng công nghệ RAG (Retrieval-Augmented Generation), kết hợp Supabase vector search và mô hình AI OpenRouter. Giúp các sếp tiết kiệm thời gian tra cứu, trả lời chính xác và cá nhân hóa tương tác với khách hàng/nhân viên."
slug: "xay-dung-chatbot-rag-suabase-openrouter"
tags: [n8n, automation, ai-rag, supabase, openrouter, google-drive, no-code]
keywords: [n8n workflow rag, tự động hóa chatbot tài liệu, supabase vector search, openrouter ai, google drive pdf, giải pháp tra cứu thông tin tự động]
---

# 🚀 **Xây Dựng Chatbot Trả Lời Câu Hỏi Bằng Tài Liệu (RAG) Với Supabase & OpenRouter - Giải Pháp AI Cho Doanh Nghiệp**

## **💡 Giới Thiệu: Giải Pháp AI Tự Động Hóa Tra Cứu Tài Liệu**
Hiện nay, các doanh nghiệp thường phải mất nhiều thời gian để tra cứu thông tin trong tài liệu PDF, email, hoặc nội bộ wiki để trả lời câu hỏi của khách hàng hoặc nhân viên. Quá trình này không chỉ tốn thời gian mà còn dễ gây sai sót, đặc biệt khi tài liệu lớn và phân tán.

**Workflow này giúp:**
- **Tự động hóa** quá trình chuyển đổi tài liệu PDF thành dữ liệu vector có thể tra cứu.
- **Trả lời chính xác** dựa trên nội dung tài liệu thực tế (không phải "hư cấu" như AI truyền thống).
- **Cung cấp API webhook** để tích hợp với ứng dụng frontend (Next.js, React, Webflow...) để tạo chatbot AI cá nhân hóa.
- **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian tra cứu:** AI tự động tìm kiếm thông tin trong hàng ngàn tài liệu PDF chỉ trong giây lát.
✅ **Trả lời chính xác & dựa trên dữ liệu:** Không còn lo lắng về thông tin sai lệch như khi sử dụng AI truyền thống.
✅ **Cá nhân hóa tương tác:** Chatbot có thể trả lời câu hỏi cụ thể của từng khách hàng/nhân viên.
✅ **Hoạt động liên tục:** Workflow chạy tự động 24/7 trên VPS, không cần người quản lý.
✅ **Tích hợp dễ dàng:** API webhook hỗ trợ kết nối với bất kỳ ứng dụng frontend nào (Next.js, React, Webflow...).
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị các tài nguyên sau:

### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Thông Tin Cần Thiết**                          | **Lưu Ý** |
|----------------------|--------------------------------------------------|------------|
| **Supabase**         | - URL của dự án Supabase <br> - API Key <br> - Database name (có bảng `documents` và `embeddings`) | - Bật **pgvector** trong Supabase để hỗ trợ vector search. |
| **OpenRouter**       | - API Key (đăng ký tại [OpenRouter](https://openrouter.ai/)) | - Chọn mô hình `deepseek/deepseek-chat-v3-0324` (hoặc tương tự). |
| **Google Drive**     | - OAuth 2.0 API Key <br> - File ID của tài liệu PDF cần upload | - Tài khoản Google Drive phải có quyền truy cập vào folder chứa PDF. |
| **Google Gemini**     | - API Key (đăng ký tại [Google AI Studio](https://makersuite.google.com/)) | - Sử dụng mô hình `embeddings-001` cho việc tạo embedding. |

### **2. Hệ Thống Hosting**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow Từ File JSON**
Các sếp có thể tải workflow từ [đây](https://n8n.io/workflows/15751) hoặc sử dụng file JSON đã cung cấp.

#### **Bước 1: Tải Workflow**
- Tải file JSON từ [n8n.io](https://n8n.io/workflows/15751) hoặc copy toàn bộ JSON từ danh sách nodes dưới đây.
- Mở **n8n Editor** và chọn **Import Workflow** (từ menu bên trái).

#### **Bước 2: Cấu Hình Credentials**
Sau khi import, các sếp cần **cấu hình lại credentials** cho các node quan trọng:

| **Node**                     | **Tham Số Cần Điền**                          | **Lưu Ý** |
|------------------------------|-----------------------------------------------|------------|
| **Chat Request Webhook**     | - Path: `0cad49b7-84e3-434c-8973-500ce6736c2c` <br> - HTTP Method: `POST` | - Đảm bảo webhook này được bật (`Active`). |
| **OpenRouter LLM**           | - Credentials: `openRouterApi` <br> - Model: `deepseek/deepseek-chat-v3-0324` | - Điền API Key vào `openRouterApi` trong **Credentials Manager**. |
| **Supabase Vector Retriever** | - Credentials: `supabaseApi` <br> - Database URL & Key | - Cấu hình trong **Credentials Manager** của n8n. |
| **Supabase Vector Store**    | - Credentials: `supabaseApi` (giống trên) <br> - Table Name: `documents` | - Đảm bảo bảng `documents` có cột `embedding` (loại `vector`). |
| **Gemini Embedding Model**   | - Credentials: `googlePalmApi` <br> - Model: `embeddings-001` | - Điền API Key vào `googlePalmApi`. |
| **Google Drive PDF Downloader** | - Credentials: `googleDriveOAuth2Api` <br> - File ID | - Lấy File ID từ URL Google Drive (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`). |

#### **Bước 3: Kích Hoạt Workflow**
- Sau khi cấu hình xong, **test run** với dữ liệu mẫu:
  ```json
  {
    "question": "Giải thích về quy trình tự động hóa tại công ty?"
  }
  ```
- Nếu trả lời đúng, **bật Active** để workflow chạy liên tục.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Với Frontend (Next.js/React/Webflow)**
Workflow này cung cấp **API webhook** để kết nối với ứng dụng frontend. Ví dụ với **Next.js**:
```javascript
const fetch = async (question) => {
  const response = await fetch('YOUR_N8N_WEBHOOK_URL', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ question })
  });
  return response.json();
};
```

### **2. Lưu Log & Báo Cáo Hàng Ngày**
- Sử dụng **node `stickyNote`** để ghi log các câu hỏi và trả lời.
- Tích hợp với **Slack/Telegram** để thông báo lỗi hoặc cập nhật mới.

### **3. Cập Nhật Tài Liệu Thường Xuyên**
- Sử dụng **Google Drive API** để tự động tải mới tài liệu PDF khi có thay đổi.
- Cập nhật lại **vector embeddings** trong Supabase bằng cách chạy lại **Document Ingestion Pipeline**.

### **4. Optimize Performance**
- **Chia nhỏ tài liệu** hiệu quả bằng `Recursive Text Splitter` (điều chỉnh `chunk_size` và `chunk_overlap`).
- **Lọc kết quả vector** bằng cách điều chỉnh `similarity_threshold` trong Supabase.

---
## **📌 Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Trải Nghiệm Khách Hàng**

Workflow này không chỉ giúp **tự động hóa tra cứu tài liệu** mà còn **cải thiện chất lượng tương tác** với khách hàng/nhân viên bằng cách cung cấp trả lời **chính xác và dựa trên dữ liệu thực tế**.

👉 **Hành động ngay:**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình credentials.
3. **Test run** với câu hỏi mẫu.
4. **Tích hợp với frontend** (Next.js/React/Webflow) để tạo chatbot cá nhân hóa.

**Nếu có bất kỳ thắc mắc, hãy để lại comment bên dưới!** 🚀