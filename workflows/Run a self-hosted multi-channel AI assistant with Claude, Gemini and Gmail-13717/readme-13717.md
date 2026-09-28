---
title: "🤖 Tự Động Hóa Trợ Lý AI Multi-Channel Tự Hosted: Claude + Gemini + Gmail (Không Cần Code)"
description: "Tạo một trợ lý AI thông minh tự động hóa cuộc trò chuyện qua Telegram, WhatsApp, Gmail và Google Drive bằng Claude, Gemini, và các công cụ AI tiên tiến. Lưu trữ trí nhớ dài hạn trên Postgres và Supabase, tự động xử lý email, quản lý tài liệu và nghiên cứu web."
slug: "tro-ly-ai-multi-channel-claude-gemini-gmail"
tags: [n8n, automation, ai-chatbot, self-hosted, no-code, claude, gemini, gmail, telegram, whatsapp, google-drive]
keywords: [n8n workflow ai, tự động hóa trợ lý ai, claude sonnet gemini, gmail automation, telegram bot ai, self-hosted ai assistant, no-code automation]
---

# 🚀 **Trợ Lý AI Multi-Channel Tự Hosted: Claude + Gemini + Gmail (Không Cần Code)**

## **🔥 Giới Thiệu: Giải Pháp Tự Động Hóa Trợ Lý AI Tối Đa Cho Doanh Nghiệp & Cá Nhân**
Bạn đã bao giờ mệt mỏi với việc phải quản lý nhiều kênh thông tin khác nhau như **Telegram, WhatsApp, Gmail, và Google Drive**? Hay phải nhớ lại lịch sử trò chuyện cũ để tiếp tục cuộc đối thoại? Hoặc muốn một trợ lý AI **tự động hóa** việc **nghiên cứu web, quản lý email, phân tích tài liệu** mà không cần viết một dòng code?

**Workflow này là giải pháp hoàn hảo!** Nó kết hợp **Claude (Sonnet, Haiku, Opus), Gemini, và các công cụ AI tiên tiến** để tạo ra một **trợ lý AI tự động hóa** hoạt động trên **4 kênh chính**:
- **Telegram** (text, voice, image, document)
- **WhatsApp** (via Evolution API)
- **Gmail** (quản lý email tự động)
- **Google Drive & Docs** (tự động hóa tài liệu)

Với **trí nhớ dài hạn** được lưu trên **Postgres và Supabase**, trợ lý này **hiểu lịch sử trò chuyện** của bạn và **tự động hóa** các tác vụ phức tạp như:
✅ **Trả lời email tự động** (đọc, trả lời, xóa, chuyển email)
✅ **Nghiên cứu web** (tìm kiếm Google, Wikipedia, Tavily)
✅ **Phân tích tài liệu** (PDF, Word, Excel)
✅ **Quản lý nhiệm vụ** (tạo, cập nhật, phân công subtask)
✅ **Tự động hóa Google Drive** (tạo folder, di chuyển file, xóa file)

---

## :::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy **ổn định 24/7**, các sếp nên **tự host n8n** trên **VPS riêng** để đảm bảo **tính riêng tư và hiệu suất cao**.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Trợ lý AI tự động hóa **những tác vụ lặp lại** như trả lời email, quản lý tài liệu, nghiên cứu web.
- **Tính chính xác cao**: Sử dụng **Claude Sonnet, Gemini, và OpenAI Embeddings** để trả lời chính xác và logic.
- **Trí nhớ dài hạn**: Lưu trữ **lịch sử trò chuyện** trên **Postgres và Supabase**, giúp AI **hiểu bối cảnh** và trả lời thông minh.
- **Hoạt động liên tục 24/7**: Với **scheduled trigger**, trợ lý **tự động cập nhật** và xử lý nhiệm vụ định kỳ.
- **Tích hợp đa kênh**: **Telegram, WhatsApp, Gmail, Google Drive** đều được tự động hóa trong một hệ thống duy nhất.
- **Không cần code**: **100% no-code**, chỉ cần cấu hình các node trong n8n.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| **Dịch vụ**               | **Tham số cần thiết**                          | **Liên kết cài đặt** |
|---------------------------|-----------------------------------------------|----------------------|
| **OpenRouter**            | API Key (để kết nối với Claude, Gemini)       | [Tạo API Key](https://openrouter.ai/) |
| **PostgreSQL**            | Connection String (để lưu trí nhớ dài hạn)     | [Cài đặt PostgreSQL](https://www.postgresql.org/download/) |
| **Supabase**              | URL, API Key, Database Name (vector store)     | [Tạo Supabase](https://supabase.com/) |
| **Google Cloud**          | API Key (để sử dụng Gemini)                   | [Cài đặt Google Cloud](https://cloud.google.com/) |
| **Tavily**                | API Key (để tìm kiếm web)                     | [Tạo Tavily API](https://tavily.com/) |
| **Telegram Bot**          | Token Bot (để gửi nhận tin nhắn)              | [Tạo Bot Telegram](https://core.telegram.org/bots) |
| **Evolution API**         | API Key (để kết nối WhatsApp)                 | [Tạo Evolution API](https://evolution-api.com/) |
| **Gmail**                 | OAuth 2.0 Credentials (để quản lý email)      | [Cài đặt Gmail API](https://developers.google.com/gmail/api/quickstart/python) |
| **Google Drive & Docs**   | OAuth 2.0 Credentials (quản lý file)           | [Cài đặt Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python) |

### **2. Cấu trúc cơ sở dữ liệu**
Workflow sử dụng **n8n Data Tables** để lưu trữ:
- **User profiles** (thông tin người dùng)
- **Chat history** (lịch sử trò chuyện)
- **Tasks & Subtasks** (quản lý nhiệm vụ)
- **Heartbeat** (để theo dõi trạng thái hoạt động)

**Lưu ý**: Các sếp cần **tạo các bảng dữ liệu** tương ứng trong n8n trước khi import workflow.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13717](https://n8n.io/workflows/13717).
2. **Nhấn "Import"** trong n8n Editor và chọn file JSON.
3. **Chọn "Create New Workflow"** và đặt tên (ví dụ: **"AI Multi-Channel Assistant"**).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → **Nhấn "Import"** → **Chọn "Paste JSON"** → **Dán nội dung**.
3. **Chọn "Create New Workflow"** và tiếp tục cấu hình.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** với **79 node**, nhưng chỉ cần chú ý đến **các phần quan trọng sau**:

#### **🔹 1. Cấu hình Triggers (Đầu vào)**
Workflow hỗ trợ **4 kênh đầu vào**:
- **Telegram Trigger** (nhận tin nhắn từ Telegram)
- **WhatsApp Webhook** (nhận tin nhắn từ WhatsApp via Evolution API)
- **Gmail Trigger** (nhận email mới)
- **Hourly Heartbeat** (tự động chạy định kỳ)

**Cách cấu hình:**
- **Telegram Trigger**:
  - Điền **Token Bot** từ Telegram.
  - Chọn **chat ID** của bot (có thể lấy từ `/start` trong Telegram).
- **Evolution API (WhatsApp)**:
  - Điền **API Key** từ Evolution API.
  - Cấu hình **Webhook URL** (được tạo tự động khi import).
- **Gmail Trigger**:
  - Cấu hình **OAuth 2.0 Credentials** trong n8n.
  - Chọn **label** hoặc **folder** muốn theo dõi (ví dụ: "Inbox").
- **Hourly Heartbeat**:
  - Đặt **schedule** là `0 0 * * *` (làm việc hàng giờ).

#### **🔹 2. Cấu hình AI Models (Claude & Gemini)**
Workflow sử dụng **OpenRouter** để kết nối với **Claude và Gemini**:
- **OpenRouter Chat Model** (7 node):
  - **Claude Sonnet 4.5** (mô hình chính)
  - **Claude Haiku 4.5** (mô hình phụ trợ)
  - **Claude Opus 4.6** (mô hình cho công việc phức tạp)
  - **Gemini 3 Flash** (nghiên cứu web)
- **Cách cấu hình**:
  - Điền **API Key OpenRouter** vào tất cả các node `lmChatOpenRouter`.
  - Đảm bảo **model** được chọn đúng (ví dụ: `anthropic/claude-sonnet-4.5`).

#### **🔹 3. Cấu hình Trí Nhớ (Postgres & Supabase)**
Workflow sử dụng:
- **Postgres Chat Memory** (lưu lịch sử trò chuyện gần đây).
- **Supabase Vector Store** (lưu trữ embeddings để RAG - Retrieval-Augmented Generation).

**Cách cấu hình:**
- **Postgres**:
  - Điền **Connection String** (thông tin từ PostgreSQL).
  - Chọn **database name** và **table name** (cần tạo trước).
- **Supabase**:
  - Điền **URL, API Key, Database Name**.
  - Chọn **table name** để lưu embeddings.

#### **🔹 4. Cấu hình Data Tables**
Workflow sử dụng **n8n Data Tables** để quản lý:
- **User profiles** (thông tin người dùng).
- **Tasks & Subtasks** (quản lý công việc).
- **Heartbeat** (theo dõi trạng thái).

**Cách cấu hình:**
- **Tạo các bảng** trong n8n Data Tables trước khi import:
  - **Init Data Table** (lưu thông tin người dùng).
  - **Tasks Table** (lưu nhiệm vụ).
  - **Subtasks Table** (lưu subtask).
  - **Chat History Table** (lưu lịch sử trò chuyện).

#### **🔹 5. Cấu hình Sub-Agents**
Workflow có **5 sub-agent** để phân công công việc:
1. **Research Agent** (Gemini 3 Flash) → Nghiên cứu web.
2. **Email Manager** (Claude Haiku) → Quản lý email.
3. **Document Manager** (Claude Haiku) → Quản lý Google Docs/Drive.
4. **Worker 1, 2, 3** → Xử lý công việc đơn giản, trung bình, phức tạp.

**Cách cấu hình:**
- Đảm bảo **API Key OpenRouter** được điền vào tất cả các node `agentTool`.

#### **🔹 6. Cấu hình Output Routing**
Workflow sử dụng **Switch node** để gửi phản hồi về **kênh gốc**:
- **Telegram** → Gửi tin nhắn qua Telegram Bot.
- **WhatsApp** → Gửi tin nhắn qua Evolution API.
- **Gmail** → Trả lời email tự động.

**Cách cấu hình:**
- Điền **Token Bot Telegram** và **API Key Evolution** vào các node `telegram` và `evolutionApi`.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn từ **Telegram** hoặc **Gmail** để kiểm tra.
   - Kiểm tra **Postgres & Supabase** để đảm bảo dữ liệu được lưu trữ.
2. **Bật Active Workflow**:
   - Nhấn **"Active"** trên n8n Editor.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH NÂNG CAO HỆ THỐNG]
- **Thêm kênh mới**: Sử dụng **Webhook** để kết nối với **Discord, Slack, hoặc Telegram Group**.
- **Tự động hóa báo cáo**: Sử dụng **Schedule Trigger** để gửi **báo cáo hàng ngày** về tiến độ công việc.
- **Lưu log hoạt động**: Sử dụng **Sticky Note** để ghi lại các lỗi hoặc sự kiện quan trọng.
- **Cập nhật mô hình AI**: Khi có mô hình mới (ví dụ: **Claude 3.5**), chỉ cần thay đổi **model name** trong node `lmChatOpenRouter`.
- **Tối ưu hóa trí nhớ**: Sử dụng **Postgres Chat Memory** kết hợp với **Supabase Vector Store** để AI trả lời **nhanh chóng và chính xác**.
- **Quản lý tài nguyên**: Nếu workflow quá tải, **tăng RAM** cho VPS hoặc **optimize các node AI** bằng cách giảm **context window**.
:::

---

## 📌 **Kết luận: Áp dụng ngay để tự động hóa công việc!**
Workflow này là **giải pháp hoàn hảo** cho những ai muốn:
✔ **Tự động hóa cuộc trò chuyện** qua nhiều kênh (Telegram, WhatsApp, Gmail).
✔ **Quản lý email, tài liệu, và nhiệm vụ** một cách thông minh.
✔ **Sử dụng AI tiên tiến** (Claude, Gemini) **không cần viết code**.
✔ **Lưu trữ trí nhớ dài hạn** để AI **hiểu bối cảnh** và trả lời thông minh.

**Hành động ngay!**
1. **Chuẩn bị tài khoản & API Keys**.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và bật Active** để trải nghiệm **trợ lý AI tự động hóa** của mình!

**🚀 CÓ THỂ TĂNG CƯỜNG HỆ THỐNG NÀY THÊM NHIỀU CHỨC NĂNG KHÁC NHƯ:**
- **Kết nối với Zapier/Make** để tự động hóa thêm dịch vụ.
- **Thêm mô hình AI mới** (ví dụ: **Mistral, Llama 3**).
- **Tạo dashboard theo dõi** với **n8n Dashboard** để theo dõi hoạt động.

**Chúc các sếp thành công với workflow tự động hóa AI này!** 🤖💡