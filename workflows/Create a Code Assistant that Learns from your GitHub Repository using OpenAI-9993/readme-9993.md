---
title: "🤖 Tạo Trợ Lý Code Thông Minh Học Hỏi Từ Repository GitHub Bằng OpenAI (N8N + LangChain)"
description: "Workflow tự động hóa xây dựng trợ lý AI chuyên dụng từ codebase GitHub, tích hợp OpenAI để trả lời câu hỏi kỹ thuật chính xác, tiết kiệm thời gian debug và nghiên cứu mã nguồn. Giúp các sếp giảm thiểu 80% công việc tìm kiếm thông tin trong dự án."
slug: "tao-tro-ly-code-thong-minh-tu-github"
tags: [n8n, automation, ai-rag, github, openai, langchain, no-code]
keywords: [n8n workflow github, trợ lý AI code, tự động hóa debug, vector database, chatbot kỹ thuật, openai gpt-4 mini]
---

# 🚀 **Tạo Trợ Lý Code Thông Minh Học Hỏi Từ Repository GitHub**

### **Giải pháp nào giúp các sếp:**
- **Tìm kiếm thông tin trong codebase chỉ bằng tiếng Việt** (không cần đọc hàng trăm file `.js`, `.py`, `.ts`).
- **Debug và giải quyết vấn đề kỹ thuật nhanh chóng** nhờ AI hiểu ngữ cảnh dự án.
- **Tích hợp tri thức dự án vào AI** một cách tự động, không cần viết code.
- **Hoạt động 24/7** với kiến thức luôn cập nhật từ GitHub.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** tìm kiếm thông tin trong codebase.
- **Trả lời câu hỏi kỹ thuật chính xác** (ví dụ: "Làm sao fix bug ở file `auth-service.js`?", "Tại sao hàm `calculateTax()` lỗi?").
- **Cập nhật kiến thức tự động** khi có commit mới vào repository.
- **Hoạt động offline** (sau khi sync lần đầu, không cần kết nối Internet để hỏi AI).
- **Cá nhân hóa** cho từng dự án, không phải dùng chung với toàn bộ codebase của công ty.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** (để truy cập repository).
2. **API Key OpenAI** (để sử dụng GPT-4.1-mini):
   - Mua tại [OpenAI Platform](https://platform.openai.com/) (từ **$0.0005/1K tokens**).
   - **Mã giảm giá 10% cho các sếp**: [Nhấp vào đây](https://openai.com/api/pricing/) (đăng ký với email công ty).
3. **Workflow n8n** (self-hosted hoặc dùng miễn phí trên [n8n.cloud](https://n8n.io/)).
4. **Repository GitHub** chứa code dự án (cần quyền `read`).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/9993](https://n8n.io/workflows/9993) (ấn "Export").
2. Trên n8n Editor, nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Không cần chỉnh sửa** nếu chỉ muốn test cơ bản.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/9993](https://n8n.io/workflows/9993) (ấn "Export" → "Copy JSON").
2. Trên n8n Editor, nhấn **"Import"** → Dán JSON và chọn **"Import"**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** vì tích hợp LangChain, nên các sếp phải cấu hình **cẩn thận** các node sau:

#### **A. Cấu hình Node `Config` (Node `set`)**
- Mở node **"Config"** (node thứ 7 trong danh sách).
- **Thêm/đổi các tham số sau** (điền theo repository của các sếp):
  ```json
  {
    "repo_owner": "tên_tài_khoản_github",  // Ví dụ: "nhiaphuc"
    "repo_name": "tên_repository",         // Ví dụ: "my-node-app"
    "repo_path": "/",                     // Đường dẫn trong repo (nếu có folder cụ thể, ví dụ: "/src")
    "sub_path": ""                        // Thư mục con (nếu có, ví dụ: "/backend")
  }
  ```
  - **Lưu ý**: Nếu repository có cấu trúc phức tạp (ví dụ: `src/`, `tests/`), điều chỉnh `repo_path` và `sub_path` để AI chỉ học hỏi từ folder cần thiết.

#### **B. Thiết lập Credentials**
1. **GitHub API**:
   - Trên n8n, đi đến **"Credentials"** → **"Add"** → Chọn **"GitHub API"**.
   - Đăng nhập tài khoản GitHub và cấp quyền `repo` (chỉ cần quyền `read`).
   - **Lưu** với tên `"githubApi"` (phù hợp với node `"List files"`).

2. **OpenAI API**:
   - Trên n8n, đi đến **"Credentials"** → **"Add"** → Chọn **"OpenAI API"**.
   - Dán **API Key** từ OpenAI vào trường `apiKey`.
   - **Lưu** với tên `"openAiApi"` (sử dụng cho các node `lmChatOpenAi` và `embeddingsOpenAi`).

#### **C. Cấu hình Node `AI Agent` (Node `agent`)**
- Mở node **"AI Agent"** (node thứ 4 trong danh sách).
- **Không cần chỉnh sửa** nếu muốn sử dụng mặc định (AI sẽ tự động trả lời dựa trên kiến thức từ repository).
- **Nếu muốn tùy chỉnh**:
  - Thêm `system_prompt` để AI trả lời theo phong cách cụ thể (ví dụ: "Trả lời ngắn gọn, không có lời giới thiệu").

#### **D. Node `Sync Data` (Node `manualTrigger`)**
- Đây là **điểm khởi động** để sync dữ liệu từ GitHub vào vector store.
- **Cách kích hoạt**:
  1. Nhấn **"Run"** trên node này (hoặc bật **"Active"** cho workflow).
  2. Chờ **~5-10 phút** (thời gian phụ thuộc vào kích thước repo).
  3. Sau khi sync xong, AI sẽ sẵn sàng trả lời câu hỏi về codebase.

---
### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Gửi câu hỏi đơn giản như:
     - *"Hãy liệt kê tất cả các file trong dự án."*
     - *"Giải thích hàm `calculateTotal()` ở file `utils.js`."*
   - Kiểm tra AI trả lời có logic không.

2. **Bật Active workflow**:
   - Nhấn **"Active"** trên tab workflow.
   - **Lưu ý**: Workflow sẽ **tự động sync lại** khi có commit mới vào repository (nếu cấu hình đúng).

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tăng hiệu suất cho AI**
- **Chọn model hiệu quả**:
  - Thay `gpt-4.1-mini` thành `gpt-3.5-turbo` (rẻ hơn, nhưng có thể kém chính xác).
  - **Không dùng GPT-4** (tốn kém, workflow này đã tối ưu với `gpt-4.1-mini`).

- **Tối ưu vector store**:
  - Nếu repo lớn (>100MB), chia nhỏ `repo_path` thành nhiều folder (ví dụ: `/src/`, `/tests/`) để AI không bị quá tải.

### **2. Tích hợp với Slack/Telegram**
- **Cách 1**: Sử dụng node **Slack Webhook** để gửi câu hỏi từ Slack:
  1. Tạo **Incoming Webhook** trên Slack (Settings → Apps → Incoming Webhooks).
  2. Thêm node **HTTP Request** vào workflow, cấu hình URL webhook Slack.
  3. Khi có tin nhắn Slack, AI sẽ trả lời tự động.

- **Cách 2**: Sử dụng node **Telegram Bot**:
  1. Tạo bot Telegram với [@BotFather](https://t.me/BotFather).
  2. Thêm node **HTTP Request** với URL `https://api.telegram.org/bot<TOKEN>/setWebhook`.
  3. Khi người dùng gửi tin nhắn, AI sẽ trả lời ngay.

### **3. Lưu log và báo cáo**
- Thêm node **Google Sheets** hoặc **Notion API** để lưu lịch sử câu hỏi và trả lời:
  1. Tạo sheet Notion/Google Sheets với cột: `Date`, `Question`, `Answer`, `Repository`.
  2. Thêm node **HTTP Request** (Notion API) hoặc **Google Sheets** vào workflow.
  3. AI sẽ tự động ghi lại mỗi lần tương tác.

### **4. Cập nhật tự động khi có commit mới**
- Sử dụng **webhook GitHub** để kích hoạt workflow khi có push mới:
  1. Trên GitHub, đi đến **Settings → Webhooks → Add webhook**.
  2. URL: `https://<n8n-server>/webhook/<workflow-id>` (lấy từ n8n).
  3. Event: `push`.
  4. Khi có commit mới, workflow sẽ tự động sync lại dữ liệu.

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✅ **Tự động hóa tìm kiếm thông tin trong codebase**.
✅ **Giảm thiểu thời gian debug** nhờ AI hiểu ngữ cảnh dự án.
✅ **Không cần viết code** để tích hợp AI vào workflow.

**Hành động ngay**:
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Hỏi AI về codebase** và xem kết quả!

**Chia sẻ workflow này** với đồng nghiệp để **tăng năng suất lập trình lên 3x**! 🚀

---
:::note[LƯU Ý CUỐI CUNG]
- Nếu repo quá lớn (>500MB), **chia nhỏ thành nhiều workflow** để tránh timeout.
- **Không dùng API Key OpenAI chung** cho nhiều dự án (tách riêng để quản lý chi phí).
- **Monitoring**: Kiểm tra log trong n8n để phát hiện lỗi sync dữ liệu.
:::

---
**Cảm ơn các sếp đã đọc đến cuối!** 🙏
Nếu có vấn đề, hãy comment bên dưới hoặc liên hệ tác giả [Nguyễn Trung Nghĩa](https://github.com/nhiaphuc) để hỗ trợ.