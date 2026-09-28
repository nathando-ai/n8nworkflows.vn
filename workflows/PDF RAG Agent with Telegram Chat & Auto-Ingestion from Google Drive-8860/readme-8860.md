---
title: "🤖 **PDF RAG Agent Tự Động Hỗ Trợ Chat Telegram + Nhập Dữ liệu Tự Động từ Google Drive**"
description: "Workflow tự động hóa AI sử dụng RAG (Retrieval-Augmented Generation) để phân tích PDF, lưu trữ vector trong Postgres, và hỗ trợ chat 24/7 qua Telegram. Giúp các sếp tiết kiệm thời gian tìm kiếm thông tin và tự động hóa quy trình content research."
slug: "pdf-rag-agent-telegram-auto-ingestion"
tags: [n8n, automation, no-code, ai-multimodal, google-drive, telegram-bot, langchain, openai, postgres]
keywords: [n8n workflow pdf rag, tự động hóa chatbot telegram, tự động nhập dữ liệu google drive, ai hỗ trợ content creation, vector database postgres]
---

# 🚀 **PDF RAG Agent: Chat AI Tự Động Hỗ Trợ từ Telegram + Nhập Dữ liệu Tự Động từ Google Drive**

### **Giải pháp cho các sếp:**
- **Thời gian tìm kiếm thông tin trong PDF dài và tẻ nhạt?** → AI RAG sẽ tự động phân tích và trả lời câu hỏi trong giây lát.
- **Cần tự động hóa việc cập nhật tài liệu mới từ Google Drive?** → Workflow này sẽ tự động nhúng và lưu trữ dữ liệu mới vào vector database.
- **Muốn chatbot AI hỗ trợ 24/7 mà không cần code?** → Telegram Bot sẽ là "người trợ lý" ảo của bạn, trả lời mọi câu hỏi liên quan đến tài liệu PDF.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên **self-host** n8n trên VPS với cấu hình tối thiểu:
- **CPU:** 2 nhân (x86_64)
- **RAM:** 4GB+
- **Disk:** 20GB SSD
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** AI tự động phân tích PDF và trả lời câu hỏi trong Telegram **không cần manual search**.
- **Tự động hóa nhập liệu:** Tài liệu mới từ Google Drive được **nhúng và lưu trữ tự động** vào vector database.
- **Chat AI cá nhân hóa:** Hỗ trợ **hỏi đáp liên tục** về nội dung PDF, với khả năng nhớ lịch sử chat (thanks đến `memoryBufferWindow`).
- **Hoạt động liên tục:** Workflow chạy **24/7** mà không cần can thiệp của con người.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lấy file PDF tự động).
2. **Tài khoản Telegram Bot** (để kết nối với Telegram).
3. **API Key Azure OpenAI** (để sử dụng model chat AI).
4. **Database Postgres + PGVector** (để lưu trữ vector embeddings).
5. **Tài khoản Mistral Cloud** (để tạo embeddings cho PDF).
6. **Credentials cho n8n** (để kết nối với các dịch vụ trên).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/8860](https://n8n.io/workflows/8860) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và paste vào **Create Workflow** → **Import Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **2 phần chính**:
- **Phần 1: Auto-Ingestion từ Google Drive** (nhúng PDF vào vector DB).
- **Phần 2: Chat AI qua Telegram** (hỏi đáp về nội dung PDF).

#### **A. Cấu hình Auto-Ingestion (Google Drive → Vector DB)**
| Node | Tham số cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **List All File Names** (`googleDrive`) | `Folder ID`, `Credentials` | Chọn folder chứa PDF cần nhúng. |
| **Download Corresponding File** (`googleDrive`) | `File ID`, `Credentials` | Đảm bảo file PDF được tải xuống thành công. |
| **Token Splitter** (`textSplitterTokenSplitter`) | `Chunk Size` (ví dụ: 1000 tokens) | Điều chỉnh kích thước chunk để phù hợp với PDF. |
| **Embeddings Mistral Cloud** | `API Key`, `Model` (ví dụ: `mistral-embed`) | Điền API Key và chọn model embeddings. |
| **Postgres PGVector Store** | `Connection String`, `Table Name` | Thiết lập kết nối với Postgres + PGVector. |

#### **B. Cấu hình Chat AI qua Telegram**
| Node | Tham số cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **Telegram Trigger** | `Bot Token`, `Chat ID` | Lấy từ `@BotFather` trên Telegram. |
| **Azure OpenAI Chat Model** | `API Key`, `Model` (ví dụ: `gpt-4`) | Điền API Key và chọn model chat. |
| **AI Agent** | `Tools` (gồm `Postgres PGVector Store`, `Embeddings`) | Đảm bảo agent có quyền truy cập vector DB. |
| **Send a Text Message** (`telegram`) | `Bot Token`, `Chat ID` | Giống như Telegram Trigger. |

#### **C. Cấu hình Manual Trigger (Run Ingestion)**
- Node **`Run Ingestion`** (`manualTrigger`) cho phép các sếp **bắt đầu quá trình nhúng PDF** một cách thủ công.
- Sau khi nhấn **Run**, workflow sẽ:
  1. Lấy danh sách file từ Google Drive.
  2. Tải và nhúng từng file vào Postgres.
  3. Cập nhật vector DB.

#### **D. Cấu hình Chat Trigger (Hỏi đáp AI)**
- Khi người dùng gửi tin nhắn qua Telegram, workflow sẽ:
  1. Kiểm tra nếu tin nhắn là **PDF** (được gửi qua `Download PDF File`).
  2. Nếu là **text**, AI sẽ trả lời dựa trên vector DB.
  3. Nếu là **PDF**, hệ thống sẽ **nhúng và trả lời** trong cùng một chat.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một file PDF qua Telegram (đã cấu hình trong `Download PDF File`).
   - Gửi một câu hỏi về nội dung PDF (ví dụ: *"Tóm tắt nội dung trang 5?"*).
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động nhúng PDF mới mỗi khi có thay đổi:**
   - Sử dụng **Google Drive Webhook** để kích hoạt `Run Ingestion` khi có file mới.
2. **Lưu log hoạt động:**
   - Thêm node **`stickyNote`** để ghi lại lịch sử nhúng và chat.
3. **Gửi báo cáo định kỳ:**
   - Kết hợp với **n8n + Email/Slack** để báo cáo số lượng file đã nhúng.
4. **Cải thiện model chat:**
   - Thay đổi `Azure OpenAI Chat Model` sang `gpt-4o` (nếu có budget) để trả lời chính xác hơn.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần:
✅ **Tự động hóa việc phân tích PDF** mà không cần code.
✅ **Chat AI hỗ trợ 24/7** qua Telegram.
✅ **Lưu trữ và truy xuất thông tin nhanh chóng** bằng vector database.

**Hành động ngay!**
1. Import workflow và cấu hình theo hướng dẫn.
2. Thêm file PDF vào Google Drive và **bắt đầu tự động hóa**!
3. **Chat với AI** và trải nghiệm sự tiện lợi của RAG + Telegram Bot.

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/8860) và **cài đặt ngay!** 🚀