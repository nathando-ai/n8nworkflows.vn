---
title: "🚀 Hệ Thống RAG Tự Động Xây Dựng Tài Liệu với Kimi-K2, Gemini Embeddings & Qdrant - Giảm Thiểu Chi Phí Token"
description: "Workflow tự động hóa hoàn toàn không code để xây dựng hệ thống RAG (Retrieval-Augmented Generation) từ tài liệu PDF lớn như Quy định Lái Xe Anh (Highway Code), sử dụng Kimi-K2 (unlimited tokens trên Featherless.ai) và Gemini Embeddings để tối ưu hóa độ chính xác và giảm chi phí token. Phù hợp cho doanh nghiệp cần giải quyết vấn đề tra cứu thông tin phức tạp từ tài liệu dài."
slug: "huong-dan-rag-system-kimi-k2-gemini-qdrant"
tags: [n8n, automation, ai-rag, document-extraction, featherless-ai, qdrant, gemini-embeddings]
keywords: [n8n workflow rag, tự động hóa tài liệu pdf, kimik2 featherless, gemini embeddings, qdrant vector store, giải pháp tra cứu thông tin tự động]
---

# 🚀 **Xây Dựng Hệ Thống RAG Tự Động từ Tài Liệu PDF với Kimi-K2, Gemini & Qdrant**

## **Giới Thiệu: Giải Pháp Tra Cứu Thông Tin Tự Động cho Doanh Nghiệp**
Các sếp đang gặp khó khăn khi phải tra cứu thông tin từ tài liệu dài như **Quy định Lái Xe Anh (Highway Code)** hay các tài liệu pháp lý, kỹ thuật? Hay phải mất thời gian thủ công để tổng hợp thông tin từ nhiều trang PDF? **Workflow này giải quyết vấn đề đó bằng cách tự động hóa toàn bộ quy trình:**
✅ **Xây dựng hệ thống RAG (Retrieval-Augmented Generation)** từ tài liệu PDF lớn.
✅ **Tối ưu hóa độ chính xác** bằng cách sử dụng **Contextual Summaries** (tóm tắt bối cảnh) thay vì chunking đơn giản.
✅ **Giảm chi phí token** với **Kimi-K2 trên Featherless.ai** (unlimited tokens từ $10/tháng).
✅ **Tra cứu thông tin nhanh chóng** bằng **Gemini Embeddings + Qdrant Vector Store**.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trong hàng trăm trang PDF.
- **Độ chính xác cao**: Bằng cách sử dụng **Contextual Summaries**, hệ thống hiểu bối cảnh của từng trang thay vì chỉ dựa vào chunking đơn giản.
- **Giảm chi phí token**: Sử dụng **Featherless.ai** với mô hình **unlimited tokens** (từ $10/tháng).
- **Hoạt động tự động**: Cập nhật và tra cứu thông tin liên tục mà không cần can thiệp.
- **Phù hợp với nhiều ngành**: Từ luật sư, giáo viên, đến nhân viên HR tra cứu quy định nội bộ.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Featherless.ai** (đăng ký [tại đây](https://featherless.ai/register?referrer=HJUUTA6M)) với **API Key** để sử dụng **Kimi-K2** (model `moonshotai/Kimi-K2-Instruct`).
2. **Tài khoản Google Cloud** (để sử dụng **Gemini Embeddings 001**) với **API Key** (đăng ký [tại đây](https://aistudio.google.com/app/apikey)).
3. **Qdrant Vector Store** (miễn phí hoặc self-hosted) để lưu trữ embeddings.
4. **Tài liệu PDF lớn** (ví dụ: [Quy định Lái Xe Anh](https://www.highwaycodeuk.co.uk/uploads/3/2/9/2/3292309/the_official_highway_code_-_10-04-2025_2.pdf)) để xây dựng hệ thống.
5. **N8n Self-hosted** (không dùng phiên bản cloud để tránh giới hạn token).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
Các sếp có thể tải workflow từ [đây](https://n8n.io/workflows/6574) hoặc sử dụng file JSON đã cung cấp:
```bash
# Cách import từ UI n8n:
1. Mở n8n Editor.
2. Nhấp vào **Import** (icon "cloud upload").
3. Chọn file JSON và nhấn **Import**.
```

### **2. Các Bước Cấu Hình Quan Trọng (BẮT BUỘC ĐIỀN)**
Workflow gồm **25 node**, nhưng các bước sau đây là **cốt lõi** cần chú ý:

#### **🔹 Cấu Hình Credentials (API Keys)**
| **Node** | **Credentials Cần Điền** | **Ghi Chú** |
|----------|--------------------------|-------------|
| **Kimi-K2 (Featherless)** | `featherlessApi` | API Key từ [Featherless.ai](https://featherless.ai/register?referrer=HJUUTA6M) |
| **Gemini Embeddings** | `googlePalmApi` | API Key từ [Google Cloud](https://aistudio.google.com/app/apikey) |
| **Qdrant** | `qdrantRestApi` | URL và API Key của Qdrant (self-hosted hoặc cloud) |

#### **🔹 Cấu Hình Node "Extract from File" (Trích Xuất PDF)**
- **Operation**: Chọn `pdf` (đã mặc định).
- **File Input**: Các sếp có thể:
  - **Tải trực tiếp** từ URL (ví dụ: [Quy định Lái Xe Anh](https://www.highwaycodeuk.co.uk/uploads/3/2/9/2/3292309/the_official_highway_code_-_10-04-2025_2.pdf)).
  - **Kết nối với Google Drive** (sử dụng node `Google Drive` để push file tự động).
  - **Sử dụng node `httpRequest`** để tải file từ URL.

#### **🔹 Cấu Hình Node "Retrieval Vectors with Gemini Embeddings"**
- **API Endpoint**: Sử dụng **HTTP Request** (không dùng node embeddings mặc định của n8n vì Gemini Embeddings 001 yêu cầu cấu hình đặc biệt).
- **Tham Số Quan Trọng**:
  ```json
  {
    "output_dimensionality": 768,  // Giảm kích thước vector để tiết kiệm token
    "task_type": "RETRIEVAL_DOCUMENT"  // Tối ưu hóa cho tra cứu tài liệu
  }
  ```

#### **🔹 Cấu Hình Node "Add Docs To Qdrant Vector Store"**
- **Operation**: `upsertPoints` (thêm hoặc cập nhật embeddings).
- **Collection Name**: Tự định nghĩa (ví dụ: `highway_code_rag`).
- **Payload**:
  ```json
  {
    "vector": $json["embeddings"],  // Vector từ Gemini
    "payload": {
      "summary": $json["summary"],  // Tóm tắt bối cảnh từ Kimi-K2
      "page": $json["page"]        // Trang gốc
    }
  }
  ```

#### **🔹 Cấu Hình Node "Query Docs from Qdrant Vector Store"**
- **Operation**: `search` (tra cứu embeddings).
- **Query Vector**: Sẽ được tạo từ **câu hỏi** của người dùng (ví dụ: *"Làm thế nào để đổi hướng xe trên đường cao tốc?"*).
- **Kết quả**: Trả về **top-k embeddings** phù hợp nhất.

#### **🔹 Cấu Hình Node "Highway Code Expert" (Agent)**
- **Tool Workflows**: Kết nối với **subworkflow** để gọi API Kimi-K2 và Gemini.
- **Prompt**: Cấu hình để **Kimi-K2** trả lời dựa trên kết quả tra cứu từ Qdrant.

---
### **3. Kích Hoạt Workflow**
1. **Test Run**:
   - Nhấn **Execute Workflow** để chạy thử với tài liệu mẫu.
   - Kiểm tra **Qdrant** để xác nhận embeddings đã được lưu trữ.
2. **Bật Active**:
   - Chuyển trạng thái workflow sang **Active**.
   - **Lưu ý**: Nếu sử dụng **manual trigger**, các sếp phải nhấn nút **Run** mỗi khi muốn xử lý tài liệu mới.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tự Động Hóa với Google Drive**
- Sử dụng workflow [Push Notifications for Google Drive](https://n8n.io/workflows/6106) để **push file PDF mới** tự động vào hệ thống RAG.
- **Cách làm**:
  ```mermaid
  googleDrive -> extractFromFile -> [Cấu hình như trên]
  ```

### **2. Thêm Log & Monitoring**
- Sử dụng **node `Set`** để lưu **log** mỗi khi xử lý thành công/lỗi.
- **Gợi ý**: Kết nối với **Slack/Telegram** để báo cáo kết quả:
  ```json
  {
    "message": "Tài liệu [FILE_NAME] đã được xử lý thành công!",
    "attachments": [{
      "text": "Trang: $node["Split Pages"].json["page"]"
    }]
  }
  ```

### **3. Tối Ưu Hóa Embeddings**
- **Sparse Vectors**: Các sếp có thể thêm **sparse vectors** để cải thiện độ chính xác (hiện chưa có trong template).
- **Multi-stage Query**: Tra cứu **đồng thời** từ embeddings và metadata (ví dụ: tên chương, trang).

### **4. Mở Rộng cho Nhiều Tài Liệu**
- **Kết nối với API nội bộ**: Thay vì chỉ PDF, các sếp có thể trích xuất từ **Word, Excel, hoặc API REST**.
- **Cập Nhật Định Kỳ**: Sử dụng **node `Schedule`** để tự động cập nhật tài liệu mới.

---
## **📌 Kết Luận: Áp Dụng Ngay để Tiết Kiệm Thời Gian & Chi Phí**

Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp cần:
✔ **Tra cứu thông tin nhanh chóng** từ tài liệu dài.
✔ **Giảm chi phí token** với mô hình **unlimited tokens** của Featherless.ai.
✔ **Tự động hóa hoàn toàn** mà không cần code.

**Hành động ngay:**
1. **Đăng ký VPS** để self-host n8n (không giới hạn token):
   👉 [VPS TinoHost (Mã giảm: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
   👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Cấu hình workflow** theo hướng dẫn trên.
3. **Kết nối với tài liệu của doanh nghiệp** và bắt đầu tra cứu tự động!

---
### **💡 Cần Hỗ Trợ?**
- **Join Discord n8n**: [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Forum Cộng Đồng**: [https://community.n8n.io/](https://community.n8n.io/)

**Happy Hacking!** 🚀