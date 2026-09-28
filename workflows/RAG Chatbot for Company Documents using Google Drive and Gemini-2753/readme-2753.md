---
title: "🤖 **Chatbot AI Tự Động Trả Lời Với Tài Liệu Công Ty (RAG) - Sử Dụng Google Drive + Gemini Pro**"
description: "Tự động hóa việc tạo chatbot AI trả lời câu hỏi dựa trên tài liệu công ty (PDF, DOCX, PPTX...) bằng cách kết nối Google Drive và Gemini Pro. Giúp các sếp tiết kiệm thời gian tìm kiếm thông tin, tăng độ chính xác và cá nhân hóa hỗ trợ khách hàng/nhân viên."
slug: "chatbot-ai-rag-google-drive-gemini"
tags: [n8n, automation, ai, rag, google-drive, gemini-pro, no-code, vector-database]
keywords: [n8n workflow rag, tự động hóa chatbot ai, gemini pro n8n, vector store pinecone, google drive automation, hỏi đáp tài liệu công ty]
---

# 🚀 **Chatbot AI Trả Lời Bằng Tài Liệu Công Ty (RAG) - Cách Sử Dụng Google Drive + Gemini Pro**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp và nhân viên phải mất thời gian quét qua hàng trăm tài liệu (PDF, DOCX, PPTX...) trên Google Drive để tìm câu trả lời cho các câu hỏi liên quan đến:
- **Quy trình nội bộ** (ví dụ: quy trình phê duyệt, chính sách nhân sự).
- **Thông tin khách hàng** (đơn hàng, hợp đồng, lịch sử tương tác).
- **Báo cáo tài chính** hoặc **dữ liệu dự án**.
- **Câu hỏi pháp lý** (hợp đồng, quy định mới).

**Kết quả?** Thời gian tìm kiếm lâu, dễ sai sót, và không thể hỗ trợ 24/7. **Giải pháp?** **Chatbot AI RAG** (Retrieval-Augmented Generation) tự động hóa việc trả lời dựa trên tài liệu công ty, kết hợp **Google Drive** và **Gemini Pro** của Google.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công trên Google Drive.
✅ **Trả lời chính xác**: AI trả lời dựa trên nội dung tài liệu thực tế (không tưởng tượng).
✅ **Hỗ trợ 24/7**: Chatbot hoạt động liên tục, trả lời ngay khi có câu hỏi.
✅ **Cá nhân hóa**: Hỗ trợ khách hàng/nhân viên với thông tin chính xác từ tài liệu công ty.
✅ **Tự động cập nhật**: Khi tài liệu mới được thêm vào Google Drive, chatbot tự động cập nhật kiến thức.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **Thao Tác Cần Thực Hiện**                                                                 | **Liên Kết**                          |
|---------------------------|-------------------------------------------------------------------------------------------|----------------------------------------|
| **Google Cloud Project**  | Tạo một dự án mới trên [Google Cloud Console](https://console.cloud.google.com/).          | [Tạo dự án mới](https://console.cloud.google.com/) |
| **Vertex AI API**         | Bật **Vertex AI API** trong dự án (để sử dụng Gemini Pro).                              | [Cài đặt API](https://cloud.google.com/vertex-ai/docs/general/enable-api) |
| **Google AI API Key**      | Tạo **API Key** từ [Google AI Studio](https://aistudio.google.com/) (dùng cho Gemini Pro). | [Tạo API Key](https://aistudio.google.com/) |
| **Pinecone**              | Tạo tài khoản miễn phí và **API Key** từ [Pinecone](https://www.pinecone.io/).             | [Đăng ký Pinecone](https://www.pinecone.io/signup/) |
| **Google Drive**          | Tạo một **folder riêng** để lưu tài liệu công ty (ví dụ: `company-documents`).           | [Google Drive](https://drive.google.com/) |

### **2. Cấu Hình Pinecone**
- **Tạo Index**: Trong Pinecone, tạo một **index mới** tên là `company-files` (dùng để lưu trữ vector của tài liệu).
- **Chọn Vector Size**: Chọn `text-embedding-004` (phù hợp với Gemini Pro).

### **3. Cấu Hình n8n**
Các sếp cần **cấu hình credentials** trong n8n:
- **Google Drive OAuth2** (để đọc/tải tài liệu từ Google Drive).
- **Google Gemini (PaLM) API** (điền **API Key** từ Google AI Studio).
- **Pinecone API** (điền **API Key** từ Pinecone).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Import từ File JSON**
1. Tải workflow từ [n8n.io/workflows/2753](https://n8n.io/workflows/2753) (chọn **Download JSON**).
2. Trong n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Import All** để thêm workflow vào n8n.

#### **Phương Pháp 2: Copy/Paste JSON**
1. Tải file JSON từ [đây](https://n8n.io/workflows/2753) và mở ra.
2. Trong n8n Editor, nhấn **Import** → Chọn **Paste JSON** và dán nội dung file vào.
3. Nhấn **Import** để hoàn tất.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phần 1**: **Tải tài liệu từ Google Drive → Chuyển thành vector → Lưu vào Pinecone**.
- **Phần 2**: **Chatbot trả lời câu hỏi dựa trên vector đã lưu**.

#### **A. Cấu Hình Google Drive Trigger**
- **Node**: `Google Drive File Created` và `Google Drive File Updated`.
- **Cần chỉnh**:
  - **Folder ID**: Điền **ID của folder** bạn tạo trên Google Drive (lấy từ đường link folder, ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Mime Types**: Chọn `application/pdf, application/vnd.openxmlformats-officedocument.wordprocessingml.document, application/vnd.ms-powerpoint` (để hỗ trợ PDF, DOCX, PPTX).

#### **B. Cấu Hình Pinecone Vector Store**
- **Node**: `Pinecone Vector Store` và `Pinecone Vector Store (Retrieval)`.
- **Cần chỉnh**:
  - **API Key**: Điền **API Key** từ Pinecone.
  - **Index Name**: Điền `company-files` (index bạn tạo trước).
  - **Dimension**: Chọn `768` (phù hợp với model Gemini Pro).

#### **C. Cấu Hình Google Gemini API**
- **Node**: `Embeddings Google Gemini`, `Google Gemini Chat Model`, `Google Gemini Chat Model (retrieval)`.
- **Cần chỉnh**:
  - **API Key**: Điền **API Key** từ Google AI Studio.
  - **Model**: Chọn `gemini-pro` (hoặc `gemini-pro-vision` nếu cần xử lý hình ảnh).

#### **D. Cấu Hình AI Agent & Memory**
- **Node**: `AI Agent` và `Window Buffer Memory`.
- **Lưu ý**:
  - **AI Agent** sẽ tự động kết hợp **vector retrieval** và **chat model** để trả lời.
  - **Memory Buffer** giúp chatbot nhớ lịch sử câu hỏi (nếu cần).

#### **E. Cấu Hình Chat Trigger (Nếu Muốn Chatbot Trả Lời Trực Tiếp)**
- **Node**: `When chat message received`.
- **Lưu ý**:
  - Nếu muốn chatbot hoạt động trên **Slack/Telegram**, cần thêm **node Webhook** hoặc **node Slack/Telegram**.
  - Ví dụ: Sử dụng **node `n8n-nodes-base.slack`** để nhận tin nhắn từ Slack.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với một tài liệu mẫu:
   - Tải một file PDF/DOCX vào folder Google Drive.
   - Chờ workflow tự động **tải file → chuyển thành vector → lưu vào Pinecone**.
   - Kiểm tra **node `Pinecone Vector Store`** để xác nhận vector đã được tạo.
2. **Bật Active**:
   - Nhấn **Active** trên workflow để kích hoạt tự động hóa.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với Slack/Telegram**
- **Thêm node `n8n-nodes-base.slack`** hoặc `n8n-nodes-base.telegram` sau `chatTrigger` để nhận câu hỏi từ Slack/Telegram.
- **Cấu hình**:
  - Điền **Token Slack** hoặc **Token Telegram**.
  - Chọn **channel/room** muốn chatbot hoạt động.

### **2. Lưu Log & Báo Cáo**
- **Thêm node `n8n-nodes-base.set`** sau `Google Gemini Chat Model` để lưu **câu hỏi + câu trả lời** vào một **Google Sheet** hoặc **database**.
- **Cách làm**:
  ```json
  {
    "operation": "create",
    "values": {
      "question": "{{$node["Google Gemini Chat Model"].json["question"]}}",
      "answer": "{{$node["Google Gemini Chat Model"].json["answer"]}}",
      "timestamp": "{{$node["Google Gemini Chat Model"].date}}"
    }
  }
  ```

### **3. Cập Nhật Tài Liệu Định Kỳ**
- **Thêm node `n8n-nodes-base.schedule`** để **tải lại tất cả tài liệu** mỗi ngày (ví dụ: 00:00).
- **Cấu hình**:
  - Chọn **cron job** như `0 0 * * *` (lúc 00:00 hàng ngày).
  - Kết nối với **Google Drive** để tải lại tất cả file.

### **4. Sử Dụng Model Gemini Pro Vision (Nếu Có Hình Ảnh)**
- Nếu tài liệu có **hình ảnh** (ví dụ: báo cáo PowerPoint), thay đổi **model** trong `Google Gemini Chat Model` thành `gemini-pro-vision`.

---

## 📌 **Kết Luận**
**Chatbot AI RAG** là giải pháp **tự động hóa hoàn hảo** để các sếp:
✔ **Tiết kiệm thời gian** tìm kiếm thông tin trong tài liệu.
✔ **Trả lời chính xác** dựa trên dữ liệu thực tế.
✔ **Hỗ trợ 24/7** mà không cần nhân viên.

**Bước đầu tiên**: **Import workflow**, **cấu hình Google Drive & Pinecone**, và **bật Active**!
**Bước tiếp theo**: **Kết nối với Slack/Telegram** và **tự động hóa báo cáo** để tối ưu hóa hơn.

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên **self-host n8n** trên **VPS** thay vì dùng phiên bản miễn phí.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

**Hãy thử ngay và tự động hóa việc trả lời câu hỏi từ tài liệu công ty!** 🚀