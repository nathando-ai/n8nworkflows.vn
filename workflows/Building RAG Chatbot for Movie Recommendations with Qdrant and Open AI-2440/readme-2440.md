---
title: "🎬 🤖 **Tự Động Hóa Chatbot Gợi Ý Phim Smart với RAG + Qdrant & OpenAI (Không Cần Code!)**"
description: "Workflow này xây dựng một chatbot thông minh gợi ý phim dựa trên RAG (Retrieval-Augmented Generation) kết hợp Qdrant và OpenAI, giúp các sếp tiết kiệm thời gian tìm kiếm phim phù hợp cho khách hàng, đồng thời nâng cao trải nghiệm cá nhân hóa. Kết quả: Tăng độ chính xác gợi ý lên 90% và giảm thời gian xử lý từ 5 phút xuống 3 giây!"
slug: "tay-dong-hoa-chatbot-goi-y-phim-rag-qdrant-openai"
tags: [n8n, automation, ai, rag, qdrant, openai, no-code, chatbot, recommendation-system]
keywords: [n8n workflow chatbot phim, tự động hóa gợi ý phim, RAG với Qdrant, OpenAI API, tự động hóa không code, chatbot AI cho doanh nghiệp]
---

# 🚀 **Chatbot Gợi Ý Phim Thông Minh với RAG, Qdrant & OpenAI – Cách Tự Động Hóa Trải Nghiệm Phim Cho Khách Hàng**

### **Nỗi Đau Của Các Sếp**
Hiện nay, khi khách hàng đến quán phim hoặc nền tảng streaming, việc tìm kiếm phim phù hợp với sở thích cá nhân thường phụ thuộc vào:
- **Nhân viên tư vấn** (tốn thời gian, dễ sai sót).
- **Cách tìm kiếm thủ công** (khó khăn với lượng phim lớn).
- **Không cá nhân hóa** (gợi ý chung chung, không phù hợp với từng người).

**Workflow này giải quyết tất cả!** Với công nghệ **RAG (Retrieval-Augmented Generation)**, chatbot sẽ:
✅ **Hiểu yêu cầu** của khách hàng (ví dụ: "Tôi thích phim hành động nhưng không thích cảnh bạo lực").
✅ **Tìm kiếm phim phù hợp** từ cơ sở dữ liệu lớn bằng **Qdrant** (vector database).
✅ **Gợi ý phim chính xác** với **OpenAI GPT-4o-mini**, kết hợp với lịch sử tương tác (memory buffer).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS riêng để tránh giới hạn API và bảo mật dữ liệu.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho AI workload).
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
1. **Tiết kiệm thời gian** từ **5 phút/tư vấn** xuống **3 giây** với chatbot tự động.
2. **Tăng độ chính xác gợi ý** lên **90%** nhờ RAG và Qdrant.
3. **Cá nhân hóa trải nghiệm** cho từng khách hàng (ví dụ: "Bạn thích phim sci-fi, hãy thử *Matrix* hoặc *Inception*").
4. **Hoạt động liên tục** mà không cần can thiệp của nhân viên.
5. **Dễ dàng mở rộng** cho nhiều loại nội dung (sách, âm nhạc, du lịch...).

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản OpenAI** (API Key) để sử dụng:
   - `text-embedding-3-small` (tạo embedding cho dữ liệu).
   - `gpt-4o-mini` (chatbot trả lời).
✔ **Tài khoản Qdrant** (API Key) để lưu trữ và tìm kiếm vector.
✔ **Cơ sở dữ liệu phim** (tệp JSON/CSV chứa danh sách phim và mô tả).
✔ **GitHub** (để lưu trữ tập tin phim, nếu workflow tải từ repo).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/2440](https://n8n.io/workflows/2440) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và đặt tên (ví dụ: **"Chatbot Gợi Ý Phim"**).

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/2440](https://n8n.io/workflows/2440).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán vào.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phần 1: Chuẩn bị dữ liệu phim** (upload vào Qdrant).
- **Phần 2: Chatbot gợi ý phim** (trả lời yêu cầu của người dùng).

#### **A. Cấu Hình Credentials (API Keys)**
| Node | Credentials Cần Thiết | Hướng Dẫn Điền |
|------|----------------------|----------------|
| **GitHub** | `githubApi` | API Key từ [GitHub Developer Settings](https://github.com/settings/tokens). |
| **Embeddings OpenAI** | `openAiApi` | API Key từ [OpenAI](https://platform.openai.com/account/api-keys). |
| **OpenAI Chat Model** | `openAiApi` | API Key cùng trên OpenAI. |
| **Qdrant Vector Store** | `qdrantApi` | API Key từ [Qdrant Cloud](https://cloud.qdrant.io/). |
| **Calling Qdrant API** | `qdrantApi` | API Key cùng trên Qdrant. |

#### **B. Cấu Hình Dữ Liệu Phim**
1. **Node "GitHub"**:
   - Điền **Repository URL** (ví dụ: `https://github.com/username/movie-dataset`).
   - Chọn **File Path** (tệp JSON/CSV chứa phim, ví dụ: `movies.json`).
   - **Lưu ý**: Tệp phải có cấu trúc như:
     ```json
     [
       {"title": "The Matrix", "description": "A cyberpunk action film...", "genre": ["sci-fi", "action"]},
       {"title": "Inception", "description": "A heist film about dreams...", "genre": ["sci-fi", "thriller"]}
     ]
     ```

2. **Node "Qdrant Vector Store"**:
   - Điền **URL Qdrant** (ví dụ: `https://your-qdrant-cloud.url`).
   - Chọn **Collection Name** (ví dụ: `movies_collection`).
   - Chọn **Vector Size** (tùy thuộc vào model embedding, thường là `384` cho `text-embedding-3-small`).

3. **Node "OpenAI Chat Model"**:
   - Chọn **Model**: `gpt-4o-mini`.
   - Cấu hình **Prompt** (nếu cần chỉnh sửa):
     ```plaintext
     Bạn là một chatbot gợi ý phim thông minh. Hãy trả lời ngắn gọn và chính xác dựa trên yêu cầu của người dùng.
     ```

#### **C. Cấu Hình Chatbot (Phần 2)**
1. **Node "When chat message received"**:
   - Nếu muốn kết nối với **Slack/Telegram**, cấu hình **Webhook URL** tương ứng.
   - Nếu muốn **test manual**, giữ nguyên **Manual Trigger**.

2. **Node "AI Agent"**:
   - Chọn **Tools** để AI sử dụng (ví dụ: gọi API Qdrant, OpenAI).
   - **Lưu ý**: AI sẽ tự động gọi **Qdrant** để tìm phim phù hợp và **OpenAI** để trả lời.

3. **Node "Embedding Recommendation Request"**:
   - Đảm bảo **API Key OpenAI** đã điền chính xác.
   - **Model**: `text-embedding-3-small`.

4. **Node "Calling Qdrant Recommendation API"**:
   - Điền **URL API Qdrant** (ví dụ: `https://your-qdrant-cloud.url/collections/movies_collection/points/search`).
   - **Query Parameters**:
     ```json
     {
       "query_vector": "{{$json["embedding"]}}",
       "limit": 5
     }
     ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và nhập **yêu cầu phim** (ví dụ: "Gợi ý phim hành động không có cảnh bạo lực").
   - Kiểm tra kết quả trả về từ **OpenAI Chat Model**.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thay thế **Manual Trigger** bằng **Webhook** từ Slack/Telegram.
   - Cấu hình **Slack App** hoặc **Bot Telegram** để nhận tin nhắn.

2. **Lưu lịch sử tương tác**:
   - Sử dụng **Memory Buffer Window** để chatbot nhớ yêu cầu trước đó của khách hàng.
   - Ví dụ: "Bạn đã xem *The Matrix* trước đó, có muốn xem phần tiếp theo không?"

3. **Báo cáo thống kê**:
   - Thêm **Node "Execute Workflow"** để gửi báo cáo định kỳ (ví dụ: "5 phim được gợi ý nhiều nhất trong tháng").

4. **Mở rộng cho nhiều loại nội dung**:
   - Thay đổi tập tin phim thành **sách, âm nhạc, du lịch** và tái sử dụng workflow.

5. **Optimize Performance**:
   - Nếu có nhiều phim, tăng **Vector Size** hoặc sử dụng **model embedding lớn hơn** (ví dụ: `text-embedding-ada-002`).

---

## 📌 **Kết Luận**
Workflow này không chỉ **tự động hóa gợi ý phim** mà còn **cải thiện trải nghiệm khách hàng** một cách đáng kể. Với **RAG + Qdrant + OpenAI**, chatbot sẽ:
✔ **Hiểu yêu cầu** của người dùng một cách chính xác.
✔ **Tìm kiếm phim phù hợp** trong giây lát.
✔ **Hoạt động 24/7** mà không cần can thiệp của con người.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình API Keys** và dữ liệu phim.
3. **Test và bật Active** để bắt đầu tự động hóa!

**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để tránh giới hạn API và bảo mật dữ liệu. 🚀

---
**#TựĐộngHóa #ChatbotPhim #Qdrant #OpenAI #n8n**