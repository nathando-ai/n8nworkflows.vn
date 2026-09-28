---
title: "🤖 **Tự Động Học Xếp Loại Bài Đăng LinkedIn: Chất Lượng hay Rác - Với OpenAI & Qdrant (N8N Workflow)**
description: "Workflow tự động phân loại bài đăng LinkedIn thành 'chất lượng' hoặc 'rác' bằng trí tuệ nhân tạo (OpenAI) và cơ sở dữ liệu vector Qdrant, giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả nghiên cứu thị trường. Kết quả: Dữ liệu được phân loại chính xác, cá nhân hóa theo sở thích, và hoạt động liên tục 24/7."
slug: "tieu-dong-hoa-phan-loai-bai-dang-linkedin"
tags: [n8n, automation, ai-rag, openai, qdrant, market-research, no-code]
keywords: [tự động hóa phân loại bài đăng LinkedIn, n8n workflow AI, phân loại nội dung chất lượng, OpenAI Qdrant, nghiên cứu thị trường tự động]
---

# 🚀 **Tự Động Học Xếp Loại Bài Đăng LinkedIn: Chất Lượng hay Rác?**

Hiện nay, các sếp và chuyên gia marketing phải mất hàng giờ mỗi ngày để **lọc rác** trong hàng trăm bài đăng LinkedIn, phân loại chúng thành "chất lượng" hay "rác" để tập trung vào nội dung có giá trị. **Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài giây**, sử dụng trí tuệ nhân tạo (OpenAI) và công nghệ **RAG (Retrieval-Augmented Generation)** để phân loại chính xác và học từ phản hồi của các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công lọc hàng trăm bài đăng mỗi ngày.
- **Chính xác cao**: Dựa trên mô hình OpenAI và học từ phản hồi trước đó.
- **Cá nhân hóa**: Hệ thống tự thích nghi với sở thích của các sếp qua thời gian.
- **Hoạt động liên tục**: Chạy tự động 24/7, không cần can thiệp.
- **Dữ liệu sẵn sàng**: Kết quả phân loại được lưu trữ trong Qdrant để phân tích sau.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI**:
   - API Key từ [OpenAI](https://platform.openai.com/account/api-keys).
   - Đăng ký mô hình `gpt-5.1-chat-latest` (hoặc mô hình khác tương thích).
2. **Tài khoản Qdrant**:
   - API Key từ [Qdrant](https://qdrant.tech/).
   - Tạo **collection** có tên **`stopslopin`** (được sử dụng để lưu trữ bài đăng và đánh giá).
3. **Browser Extension (tùy chọn)**:
   - [StopSlopIn](https://chrome.google.com/webstore/detail/stopslopin/...) (nếu muốn tích hợp trực tiếp với LinkedIn).
4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (không dùng phiên bản cloud để đảm bảo dữ liệu riêng tư).
   - Cài đặt **n8n nodes LangChain** (để sử dụng OpenAI và Qdrant).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15242](https://n8n.io/workflows/15242) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và chọn **"Import"**.
- **Lưu ý**: Nếu import từ file, chọn **"Import from File"** và tải file JSON đã tải xuống.

#### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**
Workflow này có **2 chức năng chính**:
- **`analyze`**: Phân loại bài đăng mới.
- **`vote`**: Lưu đánh giá của các sếp vào Qdrant để hệ thống học.

##### **A. Cấu hình OpenAI**
1. **Tạo Credentials OpenAI**:
   - Trong n8n Editor → **"Credentials"** → **"Add"** → Chọn **"OpenAI API"**.
   - Điền **API Key** từ OpenAI và tên credentials là **`openAiApi`** (để sử dụng trong workflow).
2. **Kiểm tra mô hình**:
   - Trong node **"OpenAI Chat Model"**, mô hình mặc định là `gpt-5.1-chat-latest`. Nếu không có, thay bằng mô hình khác như `gpt-4` (cần cập nhật trong **`keyParameters`** của node).

##### **B. Cấu hình Qdrant**
1. **Tạo Credentials Qdrant**:
   - Trong **"Credentials"** → **"Add"** → Chọn **"Qdrant API"**.
   - Điền **URL** của Qdrant (ví dụ: `https://your-qdrant-url:6333`) và **API Key**.
   - Tên credentials là **`qdrantApi`** (để sử dụng trong workflow).
2. **Kiểm tra collection**:
   - Trong node **"Retrieve similar posts"** và **"Store post"**, đảm bảo **collection name** là **`stopslopin`**.
   - Nếu chưa có, tạo collection này trong Qdrant với cấu trúc:
     ```json
     {
       "vector": [], // Vector embedding
       "metadata": {
         "text": "Nội dung bài đăng",
         "rating": "good" // hoặc "slop"
       }
     }
     ```

##### **C. Cấu hình Webhook**
1. **Bật Webhook**:
   - Node **"Webhook"** đã có **path** mặc định (`0c325586-4a79-46d2-a676-64bcf12621e9`).
   - Sau khi import, **không cần thay đổi path** này.
2. **Test Webhook**:
   - Nhấn **"Test"** trên node **"Webhook"** để kiểm tra.
   - Sau đó, bật **"Active"** cho workflow.

##### **D. Cấu hình Prompt & Logic**
1. **Node **"Analyze posts"** (Chain LLM)**:
   - Prompt mặc định đã được thiết kế để phân loại bài đăng thành **"good"** hay **"slop"**.
   - Nếu muốn thay đổi logic, mở node **"Analyze posts"** → **"Edit"** → **"Chain"** → **"Prompt Template"** và sửa nội dung.
2. **Node **"Filter by similarity score"****:
   - Threshold mặc định là **0.7** (độ tương đồng). Nếu muốn tăng giảm độ chính xác, chỉnh số này trong **`keyParameters`** của node.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một **bài đăng mẫu** (JSON) đến Webhook để kiểm tra:
     ```json
     {
       "action": "analyze",
       "text": "Bài đăng mẫu: 'Tôi vừa thử một công cụ tự động hóa mới và nó làm việc tuyệt vời!'"
     }
     ```
   - Kết quả sẽ trả về JSON như:
     ```json
     {
       "id": "123",
       "rating": "good"
     }
     ```
2. **Bật Workflow**:
   - Sau khi test thành công, bật **"Active"** cho workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng node **"Webhook"** của Slack/Telegram để nhận bài đăng từ kênh và gửi kết quả phân loại về.
   - Ví dụ: Khi có bài đăng mới, Slack gửi tin nhắn đến Webhook của n8n, sau đó n8n trả về kết quả phân loại về Slack.

2. **Lưu log phân loại**:
   - Thêm node **"Set"** sau **"Prepare output"** để lưu kết quả phân loại vào **Google Sheets** hoặc **Notion** để theo dõi lịch sử.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày và gửi báo cáo tổng hợp về **email** hoặc **Slack**.

4. **Thay đổi mô hình AI**:
   - Nếu OpenAI `gpt-5.1-chat-latest` không khả dụng, thay bằng **Claude (Anthropic)** hoặc **Ollama (cài đặt local)** bằng cách:
     - Thay đổi node **"OpenAI Chat Model"** thành **"lmChatClaude"** (nếu cài nodes LangChain hỗ trợ).
     - Cập nhật **credentials** và **mô hình** tương ứng.

5. **Tăng độ chính xác với RAG**:
   - Nếu muốn hệ thống học từ nhiều bài đăng hơn, tăng **similarity threshold** (ví dụ: từ 0.7 lên 0.8) trong node **"Filter by similarity score"**.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc phân loại bài đăng LinkedIn, tiết kiệm thời gian và nâng cao hiệu quả nghiên cứu thị trường. **Bằng cách tích hợp OpenAI và Qdrant**, hệ thống không chỉ phân loại chính xác mà còn **học từ phản hồi của các sếp** qua thời gian.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để đảm bảo dữ liệu an toàn).
2. **Import workflow** và cấu hình OpenAI + Qdrant.
3. **Test với bài đăng mẫu** và bật workflow.
4. **Tích hợp với Slack/Telegram** để tự động hóa hoàn toàn.

👉 **[Tải workflow ngay](https://n8n.io/workflows/15242)** và bắt đầu tự động hóa ngay hôm nay! 🚀