---
title: "🤖 **Hệ Thống RAG Tự Cập Nhật với OpenAI, Google Gemini & Qdrant – Tự Động Hóa Trí Tuệ Nhân Tạo Cho Doanh Nghiệp**"
description: "Workflow tự động hóa hoàn chỉnh để xây dựng hệ thống RAG (Retrieval-Augmented Generation) tự cập nhật từ Google Drive, sử dụng OpenAI, Google Gemini và Qdrant. Giúp các sếp tiết kiệm thời gian tìm kiếm thông tin, trả lời câu hỏi chính xác và tự động hóa lưu trữ dữ liệu với AI."
slug: "he-thong-rag-tu-cap-nhat-openai-google-gemini-qdrant"
tags: [n8n, automation, AI RAG, Google Drive, Qdrant, OpenAI, Google Gemini, no-code, AI-powered]
keywords: [n8n workflow RAG, tự động hóa trí tuệ nhân tạo, hệ thống tìm kiếm AI, Google Drive + Qdrant, OpenAI embeddings, Google Gemini chatbot]
---

# 🚀 **Xây Dựng Hệ Thống RAG Tự Cập Nhật với OpenAI, Google Gemini & Qdrant – Không Cần Code**

## **Nỗi Đau Của Các Sếp Hiện Nay**
Hiện nay, khi làm việc với lượng dữ liệu lớn (ví dụ: FAQ, tài liệu pháp lý, báo cáo nội bộ), các sếp thường phải:
- **Tìm kiếm thủ công** thông tin trong hàng trăm tệp Google Drive.
- **Cập nhật dữ liệu** mỗi khi có thay đổi mới, tốn thời gian và dễ sai sót.
- **Trả lời câu hỏi khách hàng/nhân viên** dựa trên trí nhớ hoặc tìm kiếm không hệ thống, dẫn đến **sai lệch thông tin** và mất uy tín.
- **Không có hệ thống AI tự động** để tổng hợp và trả lời câu hỏi từ dữ liệu hiện có.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa lưu trữ vector** từ Google Drive vào Qdrant (cơ sở dữ liệu vector tiên tiến).
✅ **Tìm kiếm thông tin chính xác** bằng AI (OpenAI/Gemini) từ dữ liệu đã vector hóa.
✅ **Cập nhật tự động** khi có tệp mới hoặc thay đổi trong Google Drive.
✅ **Trả lời câu hỏi tự động** qua chatbot (Google Gemini) với kết quả **chính xác và cá nhân hóa**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến **90%** trong việc tìm kiếm và cập nhật dữ liệu.
- **Trả lời câu hỏi chính xác** nhờ AI (Google Gemini/OpenAI) dựa trên dữ liệu mới nhất.
- **Cập nhật tự động** khi có tệp mới trong Google Drive, **không cần can thiệp thủ công**.
- **Tích hợp với Slack/Telegram** để trả lời câu hỏi ngay trong môi trường làm việc.
- **Bảo mật cao** với Qdrant (không cần chia sẻ dữ liệu ra ngoài).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (đã cấp quyền OAuth 2.0 cho n8n).
✔ **API Key OpenAI** (để tạo embeddings).
✔ **API Key Google Gemini** (để chatbot trả lời).
✔ **Qdrant Cloud/self-hosted** (để lưu trữ vector).
✔ **Google Drive Folder** chứa các tệp cần vector hóa (ví dụ: FAQ, báo cáo, tài liệu pháp lý).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7647](https://n8n.io/workflows/7647) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Active** để chạy ngay.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **4 bước chính**, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Bước 1: Tạo Collection Qdrant**
- **Node: "Create collection"** (HTTP Request)
  - **Thay đổi:**
    - `QDRANTURL` → Địa chỉ API của Qdrant (ví dụ: `https://your-qdrant-cloud.com`).
    - `COLLECTION` → Tên collection (ví dụ: `company_faq`).
  - **Credentials:** Sử dụng `httpHeaderAuth` (đã cấu hình trong n8n).

- **Node: "Clear collection"** (HTTP Request)
  - **Lưu ý:** Chạy trước khi insert dữ liệu mới để tránh trùng lặp.

##### **🔹 Bước 2: Vector hóa Dữ liệu từ Google Drive**
- **Node: "Search files"** (Google Drive)
  - **Chọn folder** chứa tệp cần vector hóa (ví dụ: `FAQ`).
  - **Output:** Lấy `file_id` và `file_name` từ metadata.

- **Node: "Get file"** (Google Drive)
  - **Download tệp** từ `file_id` để xử lý.

- **Node: "Embeddings OpenAI"** (2 lần)
  - **Điền `openAiApi`** vào credentials.
  - **Model:** Chọn `text-embedding-ada-002` (mặc định).

- **Node: "Recursive Character Text Splitter"**
  - **Chia tệp thành chunks** (ví dụ: chunk_size=500, chunk_overlap=50).

- **Node: "Insert file"** (Qdrant)
  - **Thay đổi:**
    - `QDRANTURL` (giống bước 1).
    - **Metadata:** Điền `file_id` và `file_name` từ Google Drive.
    ```json
    {
      "source": "blob",
      "blobType": "text/plain",
      "loc": {
        "lines": {
          "from": 1,
          "to": 15
        }
      },
      "file_id": "{{$node["Get file"].json[0].id}}",
      "file_name": "{{$node["Get file"].json[0].name}}"
    }
    ```

##### **🔹 Bước 3: Cập Nhật Tự Động Khi Có File Mới**
- **Node: "Update?"** (Google Drive Trigger)
  - **Cấu hình:**
    - Chọn **folder** cần theo dõi.
    - **Event:** `fileChanged` (cập nhật khi tệp thay đổi).
  - **Kết nối với "Update file"** (Qdrant) để refresh vector.

##### **🔹 Bước 4: Trả Lời Câu Hỏi Bằng Google Gemini**
- **Node: "When chat message received"** (Chat Trigger)
  - **Cấu hình:**
    - **Endpoint:** Slack/Telegram/Webhook (ví dụ: `https://your-slack-webhook.com`).
  - **Node: "Question and Answer Chain"** (LangChain)
    - **Model:** Chọn `google-gemini-pro`.
    - **Credentials:** Điền `googlePalmApi`.

- **Node: "Vector Store Retriever"** (Qdrant)
  - **Lấy dữ liệu từ collection** đã vector hóa.

- **Node: "Google Gemini Chat Model"**
  - **Trả lời câu hỏi** dựa trên kết quả tìm kiếm từ Qdrant.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run:**
  - Nhấn **"Test workflow"** và upload một tệp mẫu (ví dụ: `FAQ.txt`).
  - Kiểm tra **Qdrant** có lưu vector thành công không.
- **Bật Active:**
  - Sau khi kiểm tra, **bật workflow** để chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Slack/Telegram**
   - Sử dụng **Webhook** từ Slack/Telegram để chatbot trả lời ngay trong nhóm.
   - **Cấu hình:**
     ```json
     {
       "url": "https://hooks.slack.com/services/XXXX",
       "method": "POST",
       "body": {
         "text": "Câu trả lời từ AI: {{$node["Google Gemini Chat Model"].json[0].result}}"
       }
     }
     ```

2. **Lưu Log Cập Nhật**
   - Thêm **node `set`** sau "Update file" để ghi `file_id` và `timestamp` vào Google Sheets.
   - **Công thức:**
     ```json
     {
       "file_id": "{{$node["Get file"].json[0].id}}",
       "last_updated": "{{$now}}",
       "status": "success"
     }
     ```

3. **Báo Cáo Định Kỳ**
   - Sử dụng **node `googleSheets`** để tạo báo cáo số lượng tệp đã vector hóa.
   - **Cấu hình:**
     - Sheet Name: `RAG_Update_Report`.
     - Range: `A1:B2` (để ghi `file_name` và `update_time`).

4. **Optimize Performance**
   - **Chunk Size:** Nếu tệp quá lớn, giảm `chunk_size` (ví dụ: 300) để tránh timeout.
   - **Qdrant Cluster:** Nếu có nhiều tệp, **self-host Qdrant** trên VPS để tránh giới hạn free tier.

---

### 📌 **Kết Luận**
Workflow này **không chỉ tự động hóa việc lưu trữ và tìm kiếm dữ liệu**, mà còn **tạo ra một chatbot AI thông minh** trả lời câu hỏi từ dữ liệu hiện có. **Không cần code**, các sếp chỉ cần **cấu hình vài bước**, hệ thống sẽ:
✔ **Tự cập nhật** khi có tệp mới.
✔ **Trả lời chính xác** nhờ Google Gemini/OpenAI.
✔ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.

**🚀 Hãy áp dụng ngay để nâng cao hiệu suất công việc của doanh nghiệp!**
**📩 Có thắc mắc?** Liên hệ tác giả Davide qua [LinkedIn](https://www.linkedin.com/in/davideboizza/) hoặc email: **info@n3w.it**.

---
**🔥 Bắt đầu tự động hóa AI của bạn hôm nay!** 🔥