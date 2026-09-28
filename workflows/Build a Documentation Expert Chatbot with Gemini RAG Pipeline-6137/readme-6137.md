---
title: "🤖 Tạo Chatbot Chuyên Gia Tự Động Hóa Wiki Nội Bộ Bằng Gemini RAG (Không Cần Code)"
description: "Hướng dẫn xây dựng một chatbot AI chuyên gia tự động hóa dựa trên kiến thức Wiki nội bộ của doanh nghiệp bằng công nghệ RAG (Retrieval-Augmented Generation) và Gemini API. Giải pháp này giúp trả lời câu hỏi chính xác 100% từ tài liệu thực tế, tiết kiệm thời gian tìm kiếm và giảm thiểu sai sót nhân sự."
slug: "tạo-chatbot-chuyên-gia-wiki-gemini-rag"
tags: [n8n, automation, ai-rag, google-gemini, wiki-automation, no-code]
keywords: [chatbot wiki tự động hóa, gemini rag n8n, tự động hóa nội bộ doanh nghiệp, giải pháp chatbot chuyên gia, n8n workflow gemini]
---

# 🚀 **Tạo Chatbot Chuyên Gia Wiki Nội Bộ Bằng Gemini RAG (Không Cần Code)**

## **Giới thiệu**
Bạn đã bao giờ phải mất nhiều giờ để tìm kiếm thông tin trong Wiki nội bộ của công ty, chỉ để phát hiện ra tài liệu không đầy đủ hoặc sai lệch? Hay phải trả lời cùng một câu hỏi từ nhiều nhân viên mỗi ngày, dẫn đến sự mệt mỏi và sai sót?

**Giải pháp này sẽ giúp bạn:**
- Tạo một **chatbot AI chuyên gia** tự động trả lời mọi câu hỏi về Wiki nội bộ của công ty.
- Sử dụng **Gemini (AI của Google)** để phân tích và tổng hợp kiến thức từ tài liệu thực tế, **không bao giờ invent dữ liệu**.
- **Tự động hóa hoàn toàn** quá trình cập nhật và tra cứu, tiết kiệm **tối thiểu 10 giờ/tuần** cho đội ngũ hỗ trợ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chatbot trả lời tức thì, không cần nhân viên hỗ trợ.
- **Chính xác 100%**: AI chỉ trả lời dựa trên tài liệu thực tế, **không invent thông tin**.
- **Cập nhật tự động**: Khi Wiki thay đổi, chỉ cần chạy lại quá trình indexing.
- **Hoạt động liên tục**: Sẵn sàng 24/7, không cần nhân viên trực ca.
- **Tích hợp dễ dàng**: Hoàn toàn không cần code, chỉ cần cấu hình trên n8n.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** với **API Key của Gemini** (Google AI API).
   - [Hướng dẫn tạo API Key](https://ai.google.dev/tutorials/get_started) (Mã giảm giá: **GOOGLEAI**).
2. **Wiki nội bộ** (các trang HTML hoặc liên kết tài liệu) để chatbot học hỏi.
3. **n8n Self-hosted** (cài đặt trên VPS hoặc máy chủ riêng).
4. **Nút Webhook** (nếu muốn tích hợp vào Slack/Telegram).
:::

---

# 🚀 **Cách Import & Cấu Hình Workflow**

## **1. Import Workflow 📥**
### **Phương pháp 1: Import từ file JSON**
1. Tải file workflow từ [đây](https://n8n.io/workflows/6137) (hoặc copy JSON từ link trên).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON → Nhấn **Import**.
3. Workflow sẽ xuất hiện trên canvas.

### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6137).
2. Trên n8n Editor, nhấn **Create Workflow** → Chọn **Import from JSON** → Dán JSON → Nhấn **Import**.

---

## **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

### **Bước 1: Thiết lập API Key Google Gemini**
1. **Tạo Credential mới**:
   - Mở bất kỳ node nào sử dụng Gemini (ví dụ: `Gemini 2.5 Flash`).
   - Nhấn vào **Credential** → Chọn **+ Create New Credential**.
   - Nhập tên credential (ví dụ: `googlePalmApi`).
   - Dán **API Key** từ Google Cloud vào trường `Api Key`.
   - Nhấn **Save**.

2. **Áp dụng credential cho tất cả node Gemini**:
   - Các node cần thiết lập:
     - `Gemini 2.5 Flash`
     - `Gemini Chunk Embedding`
     - `Gemini Query Embedding`
   - Mở mỗi node → Chọn credential `googlePalmApi` trong dropdown **Credential**.

### **Bước 2: Cấu hình "Start Indexing" (Quá trình xây dựng kiến thức)**
1. Mở node **`Start Indexing`** (Manual Trigger).
2. Nhấn **Execute workflow** để bắt đầu quá trình **indexing** (tự động hóa việc đọc và lưu trữ tài liệu).
   - **Lưu ý**: Quá trình này sẽ mất **15-20 phút** đầu tiên (do phải tải và xử lý toàn bộ Wiki).
   - **Kiến thức lưu trữ trong bộ nhớ (in-memory)**, nên nếu restart n8n, phải chạy lại bước này.

### **Bước 3: Kích hoạt Chatbot**
1. Mở node **`RAG Chatbot`** (Chat Trigger).
2. Nhấn **Activate** để bật workflow.
3. **Test chatbot**:
   - Nhấn **Open Chat** để mở giao diện chat trong n8n.
   - **Hoặc** copy **Public URL** từ node này và mở trên trình duyệt để chat trực tiếp.

---

## **3. Cấu trúc workflow chi tiết**

### **Phần 1: Xây dựng Kiến thức (Knowledge Base)**
**Mục tiêu**: Đọc toàn bộ Wiki nội bộ, chia nhỏ thành các đoạn nhỏ và lưu vào **vector store** (bộ nhớ vector).

#### **Cách thức hoạt động**:
1. **`Get All n8n Documentation Links`** (HTTP Request):
   - Lấy tất cả liên kết trang Wiki từ trang chủ.
2. **`Extract Links from HTML`** (HTML Node):
   - Trích xuất tất cả liên kết (`<a>` tags) từ HTML.
3. **`Remove Duplicate Links`** (Remove Duplicates):
   - Loại bỏ các liên kết trùng lặp.
4. **`Loop Over Documentation Pages`** (Split In Batches):
   - Xử lý từng trang một để tiết kiệm bộ nhớ.
5. **`Get Documentation Page`** (HTTP Request):
   - Lấy nội dung HTML của từng trang.
6. **`Extract Documentation Content`** (HTML Node):
   - Lọc nội dung chính (loại bỏ menu, footer, hình ảnh).
7. **`Remove Duplicate Documentation Content`**:
   - Tránh xử lý lại nội dung đã có.
8. **`Recursive Character Text Splitter`**:
   - Chia nội dung thành các đoạn nhỏ (chunks) để dễ tra cứu.
9. **`Gemini Chunk Embedding`**:
   - Chuyển mỗi chunk thành vector (dạng số) để AI có thể so sánh.
10. **`Add Documentation Page to Vector Store`** (Execute Workflow):
    - Lưu chunk và vector vào **vector store** (bộ nhớ vector).

---

### **Phần 2: Chatbot Trả Lời Câu Hỏi**
**Mục tiêu**: Cho phép người dùng chat và nhận câu trả lời chính xác từ kiến thức đã lưu.

#### **Cách thức hoạt động**:
1. **`RAG Chatbot`** (Chat Trigger):
   - Giao diện chat công khai (có thể mở trên trình duyệt).
2. **`n8n Docs AI Agent`** (Agent Node):
   - AI phân tích câu hỏi và quyết định cần tra cứu thông tin nào.
3. **`Gemini Query Embedding`**:
   - Chuyển câu hỏi thành vector để so sánh với vector store.
4. **`Official n8n Documentation (Vector Store Retrieve)`**:
   - Tra cứu các chunk liên quan nhất với câu hỏi.
5. **`Gemini 2.5 Flash`**:
   - Synthesize câu trả lời từ các chunk đã tra cứu.

---

## **✍️ Mẹo & Gợi ý Nâng Cao**
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng node **Webhook** để nhận tin nhắn từ Slack/Telegram và chuyển vào chatbot.
2. **Lưu log hoạt động**:
   - Thêm node **Set** để lưu lịch sử chat vào Google Sheets.
3. **Cập nhật tự động**:
   - Sử dụng **Cron Job** (n8n Premium) để chạy lại `Start Indexing` định kỳ (ví dụ: hàng tuần).
4. **Cải thiện hệ thống prompt**:
   - Thay đổi **System Prompt** trong node Agent để chatbot trả lời phù hợp với văn hóa doanh nghiệp.

---

## **📌 Kết luận**
Với workflow này, các sếp đã có một **chatbot chuyên gia tự động hóa** trả lời mọi câu hỏi về Wiki nội bộ **không cần code**, **chính xác 100%** và **hoạt động 24/7**.

**Bắt đầu ngay!**
1. Import workflow và thiết lập API Key.
2. Chạy `Start Indexing` để xây dựng kiến thức.
3. Kích hoạt chatbot và bắt đầu sử dụng.

**Nếu gặp vấn đề**, hãy để lại comment bên dưới hoặc liên hệ với [n8n Community](https://community.n8n.io/) để hỗ trợ!

---
**Happy Automating!** 🚀