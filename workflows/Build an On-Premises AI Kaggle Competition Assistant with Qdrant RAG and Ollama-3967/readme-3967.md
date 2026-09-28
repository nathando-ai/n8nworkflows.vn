---
title: "🤖 Tự Động Hóa Trợ Lý Tham Gia Cuộc Thi Kaggle On-Premises Với AI, Qdrant RAG & Ollama (N8n)"
description: "Workflow này tự động hóa việc tải, xử lý, tóm tắt và lưu trữ dữ liệu Kaggle thành vector để hỗ trợ AI trả lời câu hỏi chuyên sâu về dữ liệu. Giúp các sếp tiết kiệm 80% thời gian phân tích thủ công và cải thiện chất lượng dự báo."
slug: "tay-dong-hoa-tro-ly-kaggle-ai-qdrant-ollama"
tags: [n8n, automation, ai, machine-learning, qdrant, ollama, no-code, data-processing]
keywords: [n8n workflow Kaggle, tự động hóa AI on-premises, RAG với Ollama, xử lý dữ liệu Kaggle, vector store Qdrant, chatbot dữ liệu khoa học]
---

# 🚀 **Trợ Lý AI Tự Động Tham Gia Cuộc Thi Kaggle On-Premises: Xử Lý Dữ Liệu Khổng Lồ Với Qdrant RAG & Ollama**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp và nhà khoa học dữ liệu thường phải:
- **Tải và xử lý hàng ngàn file Kaggle** (CSV, JSON, Excel) thủ công.
- **Tóm tắt và phân tích dữ liệu** để chuẩn bị cho cuộc thi, mất nhiều giờ.
- **Tra cứu thông tin trong dữ liệu** một cách không hiệu quả, dẫn đến sai sót.
- **Không có hệ thống lưu trữ tri thức** để AI có thể tham khảo khi trả lời câu hỏi chuyên sâu.

Workflow này **giải quyết tất cả** bằng cách tự động hóa toàn bộ quy trình từ tải file đến tạo vector store cho AI, giúp các sếp **tiết kiệm thời gian, tăng độ chính xác và tối ưu hóa dự báo**.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động tải và xử lý tất cả file Kaggle** (CSV, JSON, Excel) khi chúng được thêm vào thư mục.
✅ **Tóm tắt và vector hóa nội dung** để AI có thể truy xuất thông tin nhanh chóng (RAG - Retrieval Augmented Generation).
✅ **Trả lời câu hỏi chuyên sâu** về dữ liệu bằng AI Ollama (Qwen3) với độ chính xác cao.
✅ **Lưu trữ tri thức** trong Qdrant, giúp AI học hỏi từ dữ liệu cũ và cải thiện dần.
✅ **Hoạt động 24/7** trên máy chủ riêng (Self-hosted), không phụ thuộc vào cloud.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Máy chủ VPS** (Self-hosted n8n) để chạy 24/7.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Cài đặt các dịch vụ sau**:
   - **Ollama** (cài đặt [trên máy chủ](https://ollama.com/)) với các mô hình:
     - `mxbai-embed-large:latest` (Embeddings)
     - `ALIENTELLIGENCE/contentsummarizer:latest` (Tóm tắt văn bản)
     - `qwen3:8b` (Chatbot AI)
   - **Qdrant** (cài đặt [trên máy chủ](https://qdrant.tech/documentation/quick-start/)) để lưu trữ vector.
     - **API Key Qdrant** (để n8n kết nối).
     - **URL Qdrant** (ví dụ: `http://localhost:6333`).

3. **Thư mục lưu file Kaggle**:
   - Thiết lập thư mục `C:\ipynb\loadme` (hoặc thay đổi trong node **Local File Trigger**).
   - Đặt các file Kaggle (CSV, JSON, Excel) vào thư mục này.

4. **Credentials trong n8n**:
   - **`ollamaApi`**: API key Ollama (để n8n kết nối với Ollama).
   - **`qdrantApi`**: API key Qdrant (để n8n lưu/truy xuất vector).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3967](https://n8n.io/workflows/3967).
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Create Workflow** → **Import from JSON**.
  - Chọn file JSON đã tải và nhấn **Import**.

:::note[LƯU Ý]
- Nếu import từ link trực tiếp, **không sao chép/paste JSON** vì có thể mất cấu hình.
- **Không cần chỉnh sửa node** nếu đã cài đặt Ollama và Qdrant đúng yêu cầu.
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Node "Local File Trigger"**
- **Path**: Đảm bảo đường dẫn `C:\ipynb\loadme` **trùng khớp** với thư mục thực tế trên máy chủ.
  - Nếu dùng Linux/Mac, thay đổi thành `/home/user/loadme`.
- **Test**: Đặt 1 file Kaggle vào thư mục → workflow sẽ tự động kích hoạt.

#### **B. Cấu Hình Ollama & Qdrant**
1. **Node `Embeddings Ollama` & `Ollama Chat Model`**:
   - **Model**: Đã mặc định là `mxbai-embed-large:latest` và `qwen3:8b`.
   - **Credentials**: Chọn `ollamaApi` (đã tạo trước).
   - **Test**: Chạy node này với 1 đoạn văn bản mẫu để kiểm tra Ollama hoạt động.

2. **Node `Qdrant Vector Store`**:
   - **Credentials**: Chọn `qdrantApi`.
   - **URL**: Nếu Qdrant chạy trên localhost, để trống hoặc nhập `http://localhost:6333`.
   - **Collection Name**: Mặc định là `default` (có thể đổi).
   - **Test**: Chạy node này với 1 vector mẫu để kiểm tra Qdrant kết nối.

#### **C. Cấu Hình AI Agent (Chat Trigger)**
- **Node `When chat message received`**:
  - Đây là **điểm kích hoạt AI** khi người dùng gửi câu hỏi.
  - **Test**: Gửi 1 câu hỏi về dữ liệu Kaggle (ví dụ: *"Hãy phân tích trend giá nhà ở New York trong dataset này"*).
  - **Kết quả**: AI sẽ trả lời dựa trên vector store Qdrant + mô hình Qwen3.

#### **D. Cấu Hình Tóm Tắt & Vector Store**
- **Node `Summarization Chain`**:
  - Sử dụng mô hình `ALIENTELLIGENCE/contentsummarizer` để tóm tắt văn bản.
  - **Test**: Chạy node này với 1 file Kaggle để kiểm tra tóm tắt có logic không.
- **Node `Vector Store Tool`**:
  - Kết nối với Qdrant để lưu vector của văn bản đã tóm tắt.
  - **Test**: Kiểm tra Qdrant có thêm collection mới không.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Chọn **Run Workflow** và chọn 1 file Kaggle trong thư mục `loadme`.
   - Kiểm tra từng node có hoạt động không (đặc biệt là **Embeddings**, **Qdrant**, **AI Agent**).
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang **ON**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa AI Agent**
- **Cài đặt mô hình lớn hơn**: Thay `qwen3:8b` bằng `qwen2:72b` (nếu Ollama hỗ trợ) để AI trả lời chính xác hơn.
- **Cấu hình prompt**: Thêm **câu hỏi mẫu** vào node `AI Agent` để AI trả lời theo định dạng nhất định (ví dụ: "Trả lời bằng tiếng Việt và có ví dụ").

### **2. Lưu Log & Báo Cáo**
- **Thêm node `Markdown`** sau `AI Agent` để lưu kết quả vào file log.
- **Gửi báo cáo định kỳ** (ví dụ: hàng tuần) qua **Slack/Email** bằng node `n8n-nodes-base.email` hoặc `n8n-nodes-slack`.

### **3. Kết Hợp Với Slack/Telegram**
- **Thêm node `Slack`** để thông báo khi có file mới được tải hoặc AI trả lời câu hỏi.
- **Cài đặt bot Telegram** để các sếp hỏi AI thông qua chatbot.

### **4. Xử Lý File Lớn**
- Nếu file Kaggle quá lớn (>100MB), chia nhỏ bằng **node `Text Splitter`** trước khi vector hóa.
- **Optimize Qdrant**: Sử dụng **HNSW** (Hyperbolic Navigation Search) để tăng tốc độ truy xuất.

---
## **📌 Kết Luận**
Workflow này **đem lại cách mạng** cho cách các sếp làm việc với dữ liệu Kaggle:
✔ **Tự động hóa 100%** từ tải file đến trả lời câu hỏi AI.
✔ **Tăng tốc độ phân tích** từ ngày thành giờ.
✔ **Cải thiện chất lượng dự báo** nhờ RAG và mô hình Ollama Qwen3.
✔ **Hoạt động 24/7** trên máy chủ riêng, không phụ thuộc vào cloud.

**Hành động ngay!**
1. **Cài đặt VPS** và Ollama/Qdrant theo hướng dẫn.
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test với 1 file Kaggle** và bắt đầu tự động hóa!

🚀 **Các sếp sẵn sàng tự động hóa dữ liệu Kaggle chưa?** 🚀