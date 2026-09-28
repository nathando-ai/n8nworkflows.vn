---
title: "🤖 Tự Động Hóa Trợ Lý Mua Sắm AI Trên Telegram: Nhận Dịch Vụ 24/7 Với GPT-4.1, Nhận Diện Giọng Nói & Google Sheets"
description: "Workflow này tự động hóa trợ lý mua sắm AI hoàn toàn trên Telegram, hỗ trợ nhận diện giọng nói, trả lời câu hỏi thông minh bằng GPT-4.1, và ghi chép đơn hàng vào Google Sheets. Giúp các sếp tiết kiệm thời gian, cải thiện trải nghiệm khách hàng và quản lý đơn hàng hiệu quả."
slug: "tro-ly-mua-sam-ai-telegram-gpt-4-1-nhan-dien-giong-noi"
tags: [n8n, automation, ai-rag, telegram-bot, google-sheets, openai, pinecone, no-code]
keywords: [n8n workflow telegram, tự động hóa trợ lý AI, nhận diện giọng nói OpenAI, RAG với Pinecone, ghi chép đơn hàng Google Sheets, GPT-4.1 nano]
---

# 🚀 **Trợ Lý Mua Sắm AI Trên Telegram: Hỗ Trợ Khách Hàng 24/7 Với Giọng Nói & Trí Tuệ Nhân Tạo**

## **💡 Bạn đang gặp phải những vấn đề nào?**
- **Khách hàng liên hệ qua Telegram nhưng phải chờ lâu để được tư vấn?**
- **Bạn phải ghi chép thủ công đơn hàng từ nhiều kênh khác nhau?**
- **Không thể tự động hóa quá trình tư vấn sản phẩm và trả lời câu hỏi một cách thông minh?**
- **Muốn một trợ lý AI có thể hiểu giọng nói và trả lời chính xác như nhân viên?**

Workflow này là **giải pháp hoàn hảo** cho các sếp kinh doanh, cửa hàng trực tuyến, hoặc doanh nghiệp dịch vụ muốn tự động hóa **trợ lý mua sắm AI trên Telegram** với khả năng:
✅ **Nhận diện giọng nói** → Chuyển thành văn bản tự động
✅ **Trả lời thông minh** bằng GPT-4.1-nano (cập nhật mới nhất)
✅ **Tìm kiếm sản phẩm** từ cơ sở dữ liệu bằng **RAG (Retrieval-Augmented Generation)**
✅ **Ghi chép đơn hàng** vào Google Sheets tự động
✅ **Giữ nhớ lịch sử hội thoại** (8 tin nhắn trước đó)

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải trả lời khách hàng 24/7, AI làm việc thay bạn.
- **Tăng trải nghiệm khách hàng**: Trả lời nhanh chóng, chính xác và cá nhân hóa.
- **Quản lý đơn hàng hiệu quả**: Tất cả thông tin đơn hàng được ghi chép tự động vào Google Sheets.
- **Tăng doanh số**: Khách hàng có thể đặt hàng ngay trên Telegram mà không cần gọi điện.
- **Hỗ trợ đa ngôn ngữ**: AI có thể hiểu và trả lời bằng tiếng Việt hoặc tiếng Anh (tùy chỉnh).
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào nhóm hoặc chat cá nhân để test.

2. **API Keys**:
   - **OpenAI API Key** (để sử dụng GPT-4.1-nano và transcribe giọng nói).
   - **Pinecone API Key** (để lưu trữ và tìm kiếm dữ liệu sản phẩm).
   - **Google Sheets OAuth2 API** (để ghi chép đơn hàng).

3. **Cơ sở dữ liệu sản phẩm**:
   - **Pinecone Index**: Cần tạo một **index** và **namespace** trong Pinecone, sau đó upload dữ liệu sản phẩm (ví dụ: tên, mô tả, giá, hình ảnh).
   - **Google Sheet**: Tạo một bảng với các cột: **Name, Phone number, Address, Category, Order Details**.

4. **n8n Self-hosted**:
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
---

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11238) hoặc copy toàn bộ JSON từ đây.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **14 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

#### **🔹 Node Telegram Trigger**
- **Cấu hình**:
  - Chọn **credentials**: `telegramApi` (đã tạo từ BotFather).
  - Chọn **chat ID** của bot (có thể lấy từ `@username_bot` hoặc chat cá nhân).

#### **🔹 Node Download Voice File**
- **Cấu hình**:
  - Sử dụng cùng **credentials**: `telegramApi`.
  - Node này sẽ tải file âm thanh từ tin nhắn giọng nói.

#### **🔹 Node Transcribe Audio (OpenAI)**
- **Cấu hình**:
  - Chọn **credentials**: `openAiApi`.
  - **Model**: Chọn `whisper-1` (mặc định cho transcribe giọng nói).
  - **Prompt**: Có thể tùy chỉnh để yêu cầu OpenAI trả về văn bản sạch (ví dụ: *"Transcribe this audio message into Vietnamese text only"*).

#### **🔹 Node Switch (Phân loại tin nhắn)**
- **Cấu hình**:
  - **Condition 1**: Nếu tin nhắn là **text** → Đi đến node **AI Agent1**.
  - **Condition 2**: Nếu tin nhắn là **voice** → Đi đến node **Transcribe Audio** trước.

#### **🔹 Node AI Agent1 (GPT-4.1-nano)**
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **Model**: `gpt-4.1-nano` (đã được cache).
  - **System Message**: Tùy chỉnh để phù hợp với **ngôn ngữ và sản phẩm** của cửa hàng (ví dụ:
    ```json
    "You are a friendly shopping assistant for a Vietnamese electronics store. Answer in Vietnamese and provide product details from the knowledge base."
    ```
  - **Tools**:
    - **Answer questions with a vector store** (sử dụng Pinecone).
    - **Simple Memory** (giữ 8 tin nhắn trước đó).

#### **🔹 Node Pinecone Vector Store**
- **Cấu hình**:
  - **Credentials**: `pineconeApi`.
  - **Index Name**: Tên index Pinecone đã tạo.
  - **Namespace**: Tên namespace trong index.
  - **Query**: Sử dụng kết quả từ **AI Agent** để tìm kiếm sản phẩm trong cơ sở dữ liệu.

#### **🔹 Node Embeddings OpenAI**
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **Model**: `text-embedding-ada-002` (mặc định cho embeddings).
  - Dùng để chuyển đổi câu hỏi thành vector để Pinecone tìm kiếm.

#### **🔹 Node Append Row in Google Sheets**
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Spreadsheet ID**: Lấy từ liên kết Google Sheet (ví dụ: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`).
  - **Sheet Name**: Tên sheet chứa đơn hàng (ví dụ: `Orders`).
  - **Columns**: Đảm bảo các cột trong sheet phù hợp với dữ liệu từ AI (Name, Phone, Address, Order Details...).

#### **🔹 Node Response (Telegram)**
- **Cấu hình**:
  - **Credentials**: `telegramApi`.
  - **Message**: Sử dụng kết quả từ **AI Agent** hoặc **Google Sheets** để trả lời khách hàng.

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi tin nhắn **text** hoặc **voice** đến bot Telegram.
   - Kiểm tra:
     - AI có transcribe giọng nói thành văn bản không?
     - AI có trả lời chính xác không?
     - Đơn hàng có được ghi vào Google Sheets không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy liên tục.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram Group**:
   - Sử dụng node **Telegram** hoặc **Slack** để gửi thông báo đơn hàng mới cho team.

2. **Lưu log hoạt động**:
   - Thêm node **StickyNote** hoặc **Google Drive** để lưu lịch sử giao dịch.

3. **Báo cáo tự động hàng ngày**:
   - Sử dụng **n8n Cron Trigger** để gửi báo cáo tổng hợp đơn hàng qua email.

4. **Tùy chỉnh AI Agent**:
   - Thêm **custom instructions** cho AI để phù hợp với **ngành hàng** (ví dụ: thực phẩm, điện tử, thời trang).

5. **Hỗ trợ nhiều ngôn ngữ**:
   - Tùy chỉnh **system message** của AI để hỗ trợ tiếng Anh, Trung Quốc, hoặc tiếng Nhật.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa **trợ lý mua sắm AI trên Telegram**, giúp các sếp:
✔ **Tiết kiệm thời gian** với tự động hóa từ nhận giọng nói đến ghi chép đơn hàng.
✔ **Cải thiện trải nghiệm khách hàng** với AI trả lời nhanh chóng và chính xác.
✔ **Quản lý đơn hàng hiệu quả** với Google Sheets tự động cập nhật.

**🚀 Hãy áp dụng ngay workflow này và nâng cao hiệu suất kinh doanh của mình!**
Nếu có vấn đề trong quá trình setup, hãy để lại bình luận bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/).

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/11238)** | **📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**