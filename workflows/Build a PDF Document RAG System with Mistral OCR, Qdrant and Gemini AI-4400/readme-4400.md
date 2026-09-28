---
title: "📄 **Tự Động Xây Dựng Hệ Thống RAG PDF với Mistral OCR, Qdrant & Gemini AI – Không Cần Code!**"
description: "Workflow này tự động quét, vector hóa và trả lời câu hỏi từ tài liệu PDF bằng AI, tiết kiệm thời gian nghiên cứu lên đến 80%. Hỗ trợ doanh nghiệp tìm kiếm thông tin chính xác trong hàng ngàn trang tài liệu chỉ với một câu hỏi."
slug: "tự-dộng-xây-dựng-he-thong-rag-pdf-mistral-qdrant-gemini"
tags: [n8n, automation, AI, RAG, vector-database, Mistral, Qdrant, Gemini, Google Drive, no-code]
keywords: [n8n workflow RAG, tự động hóa AI PDF, Mistral OCR n8n, Qdrant vector store, Gemini AI trả lời câu hỏi, tự động hóa nghiên cứu tài liệu]
---

# 🚀 **Tự Động Xây Dựng Hệ Thống RAG PDF với Mistral OCR, Qdrant & Gemini AI**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Tìm kiếm thông tin trong hàng ngàn trang tài liệu PDF** (sách, báo cáo, hợp đồng) bằng cách copy-paste và tra cứu thủ công.
- **Mất thời gian nghiên cứu** để tổng hợp ý tưởng từ nhiều nguồn khác nhau.
- **Không đảm bảo độ chính xác** vì con người dễ bỏ sót hoặc hiểu sai thông tin quan trọng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Quét và chuyển đổi PDF thành văn bản** bằng Mistral OCR.
✅ **Vector hóa và lưu trữ thông tin** vào Qdrant (vector database).
✅ **Trả lời câu hỏi từ tài liệu** bằng Gemini AI với độ chính xác cao.
✅ **Tổng hợp tóm tắt nội dung** cho các tài liệu dài.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian nghiên cứu** lên đến **80%** so với cách làm thủ công.
- **Trả lời câu hỏi chính xác** từ tài liệu PDF chỉ trong giây lát.
- **Tự động tổng hợp tóm tắt** cho các báo cáo dài.
- **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.
- **Hỗ trợ nhiều loại tài liệu** (PDF, hình ảnh quét).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản API** của các dịch vụ sau:
- **Mistral Cloud API** (để OCR và xử lý văn bản).
- **OpenAI API** (để tạo embedding cho vector store).
- **Qdrant API** (để lưu trữ và quản lý vector database).
- **Google Drive API** (để truy cập và tải xuống PDF).
- **Google Gemini API** (để trả lời câu hỏi bằng AI).

✔ **File PDF** cần xử lý (có thể là báo cáo, sách, hoặc tài liệu nội bộ).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4400](https://n8n.io/workflows/4400).
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào ô **"Import Workflow"** trong Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **3 bước chính** (xem hướng dẫn trên canvas). Dưới đây là các node **quan trọng nhất** cần cấu hình:

##### **🔹 Bước 1: Tạo Collection Qdrant**
- **Node: "Create collection"** (HTTP Request)
  - **Tham số cần thay đổi:**
    - `QDRANTURL`: URL của server Qdrant (ví dụ: `http://localhost:6333`).
    - `COLLECTION`: Tên collection muốn tạo (ví dụ: `pdf_documents`).
  - **Lưu ý:** Nếu collection đã tồn tại, có thể bỏ qua bước này.

##### **🔹 Bước 2: Vector hóa Tài liệu với Qdrant & Google Drive**
- **Node: "Search PDFs"** (Google Drive)
  - **Tham số cần thiết:**
    - **Folder ID** trong Google Drive chứa PDF cần xử lý.
  - **Node: "Get PDF"** (Google Drive)
    - **Chọn file PDF** từ folder đã chỉ định.
  - **Node: "Mistral DOC OCR"** (HTTP Request)
    - **Sử dụng API Mistral** để quét và chuyển đổi PDF thành văn bản.
    - **Lưu ý:** Đảm bảo đã cấu hình `mistralCloudApi` trong credentials.

- **Node: "Embeddings OpenAI"** (OpenAI)
  - **Tham số cần thiết:**
    - **API Key OpenAI** (đã cấu hình trong `openAiApi`).
    - **Model embedding** (ví dụ: `text-embedding-ada-002`).

- **Node: "Qdrant Vector Store"** (Vector Store Qdrant)
  - **Tham số cần thay đổi:**
    - `QDRANTURL`: URL của Qdrant.
    - `COLLECTION`: Tên collection đã tạo ở bước 1.
    - **Lưu ý:** Đảm bảo `qdrantApi` đã cấu hình trong credentials.

##### **🔹 Bước 3: Test RAG & Cấu Hình Tóm Tắt (Tùy Chọn)**
- **Node: "When chat message received"** (Chat Trigger)
  - **Cấu hình để nhận câu hỏi** từ người dùng (ví dụ: qua Slack, Telegram, hoặc form).
- **Node: "Question and Answer Chain"** (Chain Retrieval QA)
  - **Sử dụng Gemini AI** để trả lời câu hỏi từ dữ liệu vector đã lưu.
- **Node: "Summarization Chain"** (Tùy chọn)
  - **Nếu muốn tóm tắt nội dung** thay vì trả lời câu hỏi chi tiết, thay thế node **"Set page"** bằng **"Summarization Chain"**.

##### **🔹 Các Node Khác Cần Lưu Ý**
- **Node: "Loop Over Items"** → Đảm bảo **batch size** phù hợp (không quá tải server).
- **Node: "Wait"** → Thêm thời gian chờ nếu API chậm.
- **Node: "Execute Workflow"** → Nếu muốn chạy workflow phụ (ví dụ: gửi báo cáo).

#### **3. Kích Hoạt ⚡️**
- **Test run** với **1-2 file PDF mẫu** để kiểm tra kết quả.
- **Bật Active workflow** khi đã cấu hình xong.
- **Kiểm tra log** trong n8n để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**
   - Sử dụng **node Slack/Telegram** để nhận câu hỏi từ nhóm công việc.
   - **Cấu hình Webhook** để n8n phản hồi kết quả ngay lập tức.

2. **Lưu Log & Báo Cáo**
   - Sử dụng **node Set** + **Google Sheets** để lưu lịch sử câu hỏi và trả lời.
   - **Tự động gửi báo cáo hàng tuần** về hoạt động RAG.

3. **Optimize Performance**
   - **Chia nhỏ batch** khi xử lý nhiều file PDF cùng lúc.
   - **Sử dụng cache** cho embedding OpenAI để tiết kiệm chi phí API.

4. **Mở rộng với nhiều nguồn dữ liệu**
   - **Kết hợp với Notion, Airtable** để lấy dữ liệu từ các nền tảng khác.
   - **Sử dụng node Webhook** để nhận file từ form trực tuyến.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tìm kiếm và tổng hợp thông tin thủ công. Bằng cách **tự động hóa RAG với Mistral OCR, Qdrant và Gemini AI**, doanh nghiệp có thể:
✔ **Tìm kiếm thông tin nhanh chóng** trong hàng ngàn trang tài liệu.
✔ **Tăng độ chính xác** so với cách làm thủ công.
✔ **Hoạt động 24/7** mà không cần can thiệp của con người.

**🚀 Hãy áp dụng ngay workflow này và bắt đầu tự động hóa nghiên cứu tài liệu của mình!**
Nếu có vấn đề, **hãy liên hệ với tác giả Davide** qua [LinkedIn](https://www.linkedin.com/in/davideboizza/) hoặc email **info@n3w.it**.

---
**💡 Lưu ý:** Để workflow chạy ổn định, **hãy sử dụng VPS riêng** (không dùng phiên bản miễn phí của n8n.io). Các sếp có thể tham khảo gói **VPS Xeon 4GB chỉ 50k/tháng** từ [BNIX](https://my.bnix.one/aff.php?aff=172) để đảm bảo hiệu suất tối ưu!