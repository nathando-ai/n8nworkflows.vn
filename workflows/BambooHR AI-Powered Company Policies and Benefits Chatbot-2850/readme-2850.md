---
title: "🤖 Chatbot AI Tự Động Trả Lời Về Chính Sách & Lợi Ích Công Ty BambooHR - Tiết Kiệm 200h/năm Cho HR"
description: "Workflow tự động hóa AI tích hợp BambooHR + OpenAI + Supabase giúp chatbot trả lời mọi câu hỏi về chính sách, lợi ích công ty và liên lạc nhân viên 24/7, giảm thiểu công việc lặp lại cho bộ phận HR. Đáp ứng 90% yêu cầu thông tin nhân viên mà không cần can thiệp thủ công."
slug: "chatbot-ai-bamboohr-policies-benefits"
tags: [n8n, automation, hr, ai-chatbot, bamboohr, openai, supabase, no-code]
keywords: [n8n workflow bamboohr, chatbot hr tự động hóa, tự động trả lời chính sách công ty, ai chatbot nhân sự, giảm thời gian làm việc cho hr, tự động hóa bộ phận nhân sự]
---

# 🚀 **Chatbot AI Tự Động Trả Lời Chính Sách & Lợi Ích Công Ty BambooHR**

### **Giải pháp AI hoàn toàn tự động hóa cho bộ phận HR**
Công việc của các sếp HR thường bị "chìm" trong hàng trăm cuộc gọi, email và tin nhắn từ nhân viên về chính sách công ty, lợi ích, hoặc cách liên lạc với đồng nghiệp. Thậm chí, nhiều câu hỏi này lại lặp đi lặp lại như:
- *"Lợi ích y tế mới nhất là gì?"*
- *"Làm thế nào để liên lạc với trưởng phòng?"*
- *"Điều kiện nghỉ phép năm nay có thay đổi không?"*

**Workflow này giúp:**
✅ **Tự động trả lời 90% câu hỏi** về chính sách, lợi ích và liên lạc nhân viên **không cần can thiệp thủ công**.
✅ **Tiết kiệm 200+ giờ/năm** cho bộ phận HR bằng cách loại bỏ công việc lặp lại.
✅ **Cung cấp thông tin chính xác** từ nguồn dữ liệu BambooHR và tài liệu công ty.
✅ **Hỗ trợ nhân viên 24/7** qua Slack, Telegram, hoặc email (cần cấu hình thêm).
✅ **Tích hợp AI OpenAI** để phân tích và trả lời thông minh, thậm chí tìm kiếm thông tin từ tài liệu PDF trong BambooHR.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 80% thời gian trả lời câu hỏi lặp lại (từ 5-10 phút/câu hỏi xuống còn <1 phút).
- **Chính xác 100%**: Thông tin trả lời luôn cập nhật từ BambooHR và tài liệu chính thức.
- **Trải nghiệm nhân viên nâng cao**: Nhân viên nhận được câu trả lời nhanh chóng và chi tiết, giảm sự chờ đợi.
- **Hoạt động liên tục**: Chatbot hoạt động 24/7, không cần nhân viên trực ca.
- **Tích hợp AI thông minh**: Hiểu ngữ cảnh và trả lời phù hợp với từng trường hợp (ví dụ: tìm kiếm nhân viên cụ thể, giải thích chính sách chi tiết).
:::

---

### 🔧 **Yêu cầu cần thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản BambooHR** với quyền truy cập API:
   - API Key (tạo tại **Admin > Settings > API**).
   - Credential trong n8n với tên `bambooHrApi`.
2. **Tài khoản OpenAI** (API Key):
   - Tạo tại [OpenAI Platform](https://platform.openai.com/).
   - Credential trong n8n với tên `openAiApi`.
3. **Tài khoản Supabase** (miễn phí):
   - Đăng ký tại [Supabase](https://supabase.com/).
   - Credential trong n8n với tên `supabaseApi` (cấu hình database và vector store).
4. **Tài liệu chính sách công ty** (PDF):
   - Tải lên BambooHR và đảm bảo chúng thuộc danh mục "company_files" để workflow có thể đọc.
5. **Node LangChain** (n8n Community):
   - Cài đặt từ [n8n Community](https://community.n8n.io/) (cần cài đặt trước).

---
:::note[Lưu ý quan trọng]
- Workflow **không tự động hóa việc tạo/đổi chính sách**, mà chỉ **trả lời thông tin hiện có**.
- Để tối ưu, các sếp nên **cập nhật thường xuyên** tài liệu trong BambooHR.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/2850](https://n8n.io/workflows/2850).
- **Cách 1**: Nhấn **Import** trong n8n Editor và chọn file JSON.
- **Cách 2**: Copy toàn bộ JSON và nhấn **Paste JSON** trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **3 phần chính**:
- **Phần 1: Chuẩn bị dữ liệu** (tải tài liệu từ BambooHR, xử lý thành vector store).
- **Phần 2: Tìm kiếm thông tin** (sử dụng AI OpenAI để phân tích và trả lời).
- **Phần 3: Trả lời nhân viên** (tích hợp với chatbot hoặc email).

##### **A. Cấu hình BambooHR**
1. **Node "GET all files"**:
   - Đảm bảo credential `bambooHrApi` được cấu hình với API Key.
   - **Lưu ý**: Workflow sẽ tải tất cả file thuộc danh mục "company_files". Nếu có file không liên quan, cần **lọc bằng node "Filter out files from undesired categories"**.

2. **Node "GET all employees"**:
   - Credential `bambooHrApi` phải có quyền đọc danh sách nhân viên.
   - **Lưu ý**: BambooHR không hỗ trợ tìm kiếm theo tên, nên workflow sẽ tải toàn bộ danh sách và lọc sau.

##### **B. Cấu hình OpenAI**
- **Tất cả node `lmChatOpenAi`** đều cần credential `openAiApi`.
- **Lưu ý**:
  - Đặt **ngân sách API** hợp lý để tránh bị giới hạn.
  - Cấu hình **model** (ví dụ: `gpt-4` hoặc `gpt-3.5-turbo`) trong node `OpenAI Chat Model`.

##### **C. Cấu hình Supabase**
1. **Node "Supabase Vector Store"**:
   - Cấu hình credential `supabaseApi` với URL và key của database Supabase.
   - **Bước 1**: Tạo database Supabase và table `documents`.
   - **Bước 2**: Cài đặt extension `pgvector` (nếu chưa có).
   - **Bước 3**: Cấu hình trong n8n:
     ```
     URL: https://<your-project-ref>.supabase.co
     Key: <your-supabase-key>
     Database: postgresql
     ```

2. **Node "Supabase Vector Store Retrieval"**:
   - Sử dụng cùng credential `supabaseApi`.
   - **Lưu ý**: Đảm bảo table `documents` đã được tạo và chứa vector embeddings từ tài liệu PDF.

##### **D. Cấu hình AI Agent**
- **Node "HR AI Agent"**:
  - Đây là **cốt lõi** của workflow, kết hợp nhiều công cụ (OpenAI, BambooHR, Supabase).
  - **Lưu ý**:
    - Đảm bảo **tất cả credential** (`openAiApi`, `bambooHrApi`, `supabaseApi`) được cấu hình chính xác.
    - **Không bật tùy chọn "simplify"** trong node `Employee Lookup Tool` để AI có thể phân tích chi tiết.

##### **E. Test và kích hoạt**
1. **Nhấn "Test workflow"** để chạy với dữ liệu mẫu.
2. **Kiểm tra các node quan trọng**:
   - "Embeddings OpenAI" → Đảm bảo tài liệu được chuyển thành vector.
   - "OpenAI Chat Model" → Trả lời có logic không?
   - "Employee Lookup Tool" → Có tìm được nhân viên không?
3. **Bật "Active"** khi tất cả node hoạt động bình thường.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng node `n8n-nodes-slack` hoặc `n8n-nodes-telegram` để chatbot trả lời trên kênh nhóm.
   - **Cách làm**:
     - Thêm node `Slack/Telegram Webhook` sau node `HR AI Agent`.
     - Cấu hình credential và gửi tin nhắn phản hồi.

2. **Gửi báo cáo định kỳ**:
   - Thêm node `n8n-nodes-email` hoặc `n8n-nodes-google-sheets` để gửi báo cáo về:
     - Số lượng câu hỏi được trả lời.
     - Thời gian phản hồi trung bình.
     - Top 5 câu hỏi phổ biến.

3. **Cập nhật tài liệu tự động**:
   - Sử dụng **webhook** từ BambooHR để khi có file mới được tải lên, workflow tự động cập nhật vector store.

4. **Tối ưu chi phí OpenAI**:
   - Sử dụng **model `gpt-3.5-turbo`** thay vì `gpt-4` để giảm chi phí.
   - **Lọc câu hỏi** trước khi gửi đến AI bằng node `Text Classifier`.

5. **Lưu log hoạt động**:
   - Thêm node `n8n-nodes-base.set` để lưu lịch sử câu hỏi và trả lời vào database hoặc Google Sheets.

---
### 📌 **Kết luận**
Chatbot AI này không chỉ **giải phóng thời gian** cho bộ phận HR mà còn **cải thiện trải nghiệm nhân viên** bằng cách cung cấp thông tin nhanh chóng và chính xác. Với **tự động hóa 90% công việc lặp lại**, các sếp có thể tập trung vào những nhiệm vụ chiến lược hơn.

**Bắt đầu ngay!**
1. Import workflow và cấu hình credential.
2. Test với dữ liệu mẫu.
3. Bật hoạt động và chia sẻ với nhân viên qua Slack/email.

**Nếu gặp vấn đề**, liên hệ với tác giả [Ludwig Gerdes](https://www.linkedin.com/in/ludwiggerdes/) hoặc cộng đồng n8n để hỗ trợ.

---
**💡 Mẹo cuối**: Để workflow chạy ổn định, các sếp nên **cập nhật tài liệu BambooHR định kỳ** và **monitor log** trong n8n để phát hiện lỗi sớm.