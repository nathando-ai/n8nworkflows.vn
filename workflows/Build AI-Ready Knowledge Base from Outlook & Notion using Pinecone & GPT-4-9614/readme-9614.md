---
title: "🤖 Tự Động Xây Dựng Trữ Liệu AI Sẵn Sàng từ Outlook & Notion với Pinecone & GPT-4 (N8n)"
description: "Workflow tự động hóa 100% không code để thu thập, xử lý và lưu trữ kiến thức từ email Outlook và trang Notion vào Pinecone Vector Database, sau đó sử dụng AI Agent (GPT-4) để trả lời câu hỏi chính xác và cá nhân hóa. Giúp các sếp tiết kiệm 10+ giờ/ngày trong việc tổng hợp và tra cứu thông tin."
slug: "tieu-dong-xay-dung-tru-lieu-ai-san-sang-outlook-notion-pinecone"
tags: [n8n, automation, ai-agent, pinecone, gpt-4, notion, outlook, vector-database, no-code]
keywords: [n8n workflow tự động hóa, xây dựng trữ liệu AI, pinecone vector database, gpt-4 chatbot, tự động hóa kiến thức doanh nghiệp, lưu trữ email và notion]
---

# 🚀 **Tự Động Xây Dựng Trữ Liệu AI Sẵn Sàng từ Outlook & Notion với Pinecone & GPT-4**

### **Giải pháp cho nỗi đau:**
Các sếp thường phải mất **10-15 giờ/tuần** để:
- **Tổng hợp kiến thức** từ email Outlook (thread, tin nhắn liên quan) và trang Notion (bài viết, tài liệu).
- **Tra cứu thủ công** thông tin trong hàng ngàn email hoặc trang Notion để trả lời khách hàng hoặc hỗ trợ nội bộ.
- **Cập nhật trữ liệu** mỗi khi có thông tin mới, dẫn đến **sai sót** và **trùng lặp dữ liệu**.

**Workflow này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Thu thập** email từ Outlook và nội dung từ Notion.
✅ **Xử lý** và **xóa trùng** dữ liệu.
✅ **Lưu trữ** vào **Pinecone Vector Database** (namespace riêng cho email và Notion).
✅ **Tạo AI Agent** sử dụng **GPT-4** để trả lời câu hỏi dựa trên kiến thức đã tích lũy.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** trong việc tổng hợp và tra cứu thông tin.
- **Trả lời chính xác** nhờ AI Agent sử dụng **GPT-4** và kiến thức từ email/Notion.
- **Cập nhật tự động** khi có thông tin mới (không cần thủ công).
- **Tránh trùng lặp** dữ liệu với chức năng **xóa bỏ trùng lặp** tự động.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào giờ làm việc.
- **Cá nhân hóa** trả lời dựa trên **tone** và **bối cảnh** của email/Notion.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
#### **1. Tài khoản và API Keys**
| Dịch vụ               | Thông tin cần thiết                                                                 | Làm thế nào để lấy?                                                                 |
|-----------------------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **Microsoft Outlook** | - Email và mật khẩu (hoặc OAuth2)                                                  | [Cài đặt OAuth2 cho Outlook](https://docs.microsoft.com/en-us/outlook/desktop-outlook/connect-outlook-to-office-365) |
| **Notion API**        | - API Key (tạo từ [Notion Developer](https://www.notion.so/my-integrations))         | [Hướng dẫn tạo API Key](https://developers.notion.com/docs/getting-started)           |
| **Pinecone API**      | - API Key và Environment (tạo tại [Pinecone](https://www.pinecone.io/))               | [Cài đặt Pinecone](https://docs.pinecone.io/docs/getting-started)                     |
| **Cohere API**        | - API Key (tạo tại [Cohere](https://cohere.com/))                                    | [Hướng dẫn đăng ký](https://docs.cohere.com/docs/getting-started)                    |
| **OpenAI API**        | - API Key (tạo tại [OpenAI](https://platform.openai.com/))                          | [Cài đặt API Key](https://platform.openai.com/account/api-keys)                       |

#### **2. Cấu hình Notion và Outlook**
- **Outlook**: Tạo **1 thư mục riêng** (ví dụ: `KnowledgeBase`) để lưu email cần thu thập.
- **Notion**: Tạo **1 database hoặc trang** để lưu trữ kiến thức (ví dụ: `FAQ`, `Tài liệu nội bộ`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
##### **Cách 1: Import từ file JSON**
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/9614) hoặc copy toàn bộ JSON dưới đây.
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
3. **Không** nhấn **Active** ngay, chỉ **Preview** để kiểm tra cấu hình.

##### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
2. Dán toàn bộ JSON dưới đây vào ô nhập liệu.
3. **Không** nhấn **Active** ngay, chỉ **Preview** để kiểm tra cấu hình.

---
#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **2 phần chính**:
- **Phần 1: Thu thập dữ liệu từ Outlook & Notion → Pinecone**
- **Phần 2: AI Agent trả lời câu hỏi dựa trên kiến thức**

##### **A. Cấu hình phần thu thập dữ liệu**
###### **1. Microsoft Outlook Trigger**
- **Credentials**: Chọn `microsoftOutlookOAuth2Api` (đã cấu hình trước).
- **Folder**: Điền tên thư mục Outlook đã tạo (ví dụ: `KnowledgeBase`).
- **Test**: Nhấn **Execute Node** → Chọn email mẫu để kiểm tra.

###### **2. Notion Trigger**
- **Credentials**: Chọn `notionApi`.
- **Database/Page**: Điền tên **database** hoặc **trang Notion** cần theo dõi.
- **Test**: Nhấn **Execute Node** → Kiểm tra liệu có lấy được dữ liệu từ Notion không.

###### **3. Pinecone Vector Store**
- **Credentials**: Chọn `pineconeApi`.
- **Namespace**:
  - Cho **email**: Điền `emails`.
  - Cho **Notion**: Điền `knowledgebase`.
- **Dimension**: Điền `1024` (do Cohere Embeddings sử dụng).
- **Test**: Nhấn **Execute Node** → Kiểm tra liệu dữ liệu đã lưu vào Pinecone thành công không.

###### **4. Embeddings Cohere**
- **Credentials**: Chọn `cohereApi`.
- **Model**: Sử dụng mặc định (`embed-multilingual-v3.0`).
- **Test**: Nhấn **Execute Node** → Kiểm tra liệu có trả về vector embedding không.

###### **5. Remove Duplicates**
- **Field**: Chọn `text` (để xóa trùng nội dung).
- **Test**: Nhấn **Execute Node** → Kiểm tra số lượng dữ liệu sau khi xóa trùng.

##### **B. Cấu hình AI Agent**
###### **1. OpenAI Chat Model (GPT-4)**
- **Credentials**: Chọn `openAiApi`.
- **Model**: Đảm bảo chọn `gpt-4.1-mini` (hoặc `gpt-4` nếu có).
- **Test**: Nhấn **Execute Node** → Gửi câu hỏi mẫu để kiểm tra AI trả lời có logic không.

###### **2. Simple Memory (Buffer Window)**
- **Size**: Đặt `5` (lưu 5 câu hỏi/trả lời gần nhất).
- **Test**: Nhấn **Execute Node** → Kiểm tra liệu AI có nhớ bối cảnh không.

###### **3. Chat Trigger (When chat message received)**
- **Credentials**: Không cần (sử dụng mặc định).
- **Test**: Gửi **1 câu hỏi mẫu** (ví dụ: *"Trích dẫn nội dung từ email ngày 10/10/2023 về dự án X?"*) → Kiểm tra AI trả lời có sử dụng kiến thức từ Pinecone không.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** với dữ liệu mẫu (email/Notion).
   - Kiểm tra **Pinecone** có lưu dữ liệu không.
   - Gửi **1 câu hỏi** qua **Chat Trigger** → AI trả lời có chính xác không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
#### **1. Kết hợp với Slack/Telegram**
- Thêm **node `slack`** hoặc **`telegram`** sau **Chat Trigger** để thông báo kết quả trả lời cho team.
- **Cách làm**:
  ```json
  {
    "name": "Send to Slack",
    "type": "slack",
    "credentials": ["slackApi"],
    "keyParameters": {
      "channel": "#ai-agent",
      "text": "{{ $node["Chat Trigger"].json["message"] }}"
    }
  }
  ```

#### **2. Lưu log hoạt động**
- Thêm **node `stickyNote`** để ghi lại lịch sử câu hỏi/trả lời.
- **Cách làm**:
  ```json
  {
    "name": "Log Question",
    "type": "stickyNote",
    "keyParameters": {
      "note": "{{ $node["Chat Trigger"].json["question"] }} - {{ $node["OpenAI Chat Model"].json["answer"] }}"
    }
  }
  ```

#### **3. Gửi báo cáo định kỳ**
- Thêm **node `setInterval`** để gửi **báo cáo tổng hợp** về lượng dữ liệu mới được thêm vào Pinecone.
- **Cách làm**:
  ```json
  {
    "name": "Send Daily Report",
    "type": "setInterval",
    "keyParameters": {
      "interval": 86400000, // 1 ngày
      "operation": "execute"
    }
  }
  ```

#### **4. Cập nhật tự động khi có email mới**
- Đặt **Outlook Trigger** ở chế độ **polling** (kiểm tra thư mục định kỳ).
- **Cách làm**:
  ```json
  {
    "name": "Microsoft Outlook Trigger",
    "type": "microsoftOutlookTrigger",
    "keyParameters": {
      "polling": true,
      "interval": 300000 // 5 phút
    }
  }
  ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **tổng hợp, tra cứu và trả lời thủ công**, thay vào đó **AI Agent** sẽ tự động:
✔ **Học hỏi** từ email và Notion.
✔ **Trả lời chính xác** dựa trên kiến thức.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay:**
1. **Chuẩn bị tài khoản** (Outlook, Notion, Pinecone, OpenAI).
2. **Import workflow** và **cấu hình** theo hướng dẫn.
3. **Test Run** trước khi bật **Active**.
4. **Kết nối với team** qua Slack/Telegram để sử dụng AI Agent hiệu quả hơn!

**🚀 Khám phá thêm:**
- [Tutorial Pinecone với n8n](https://docs.pinecone.io/docs/quickstart)
- [Cách sử dụng GPT-4 trong n8n](https://docs.n8n.io/integrations/builtins/nodes/langchain/lmChatOpenAi/)
- [Tự động hóa Notion với n8n](https://docs.n8n.io/integrations/builtins/nodes/notion/)

---
**Chia sẻ workflow này với đồng nghiệp của bạn để cùng tự động hóa công việc!** 💡