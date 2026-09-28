---
title: "🤖 Tạo Trợ Lý Trí Tuệ Nhân Tạo (AI) Tự Động Học Tập Từ Tài Liệu - Ollama + PGVector + Telegram (N8N)"
description: "Tự động hóa việc xây dựng một trợ lý AI thông minh từ cơ sở tri thức nội bộ bằng cách sử dụng Ollama (AI local), PostgreSQL PGVector (tìm kiếm vector), và Telegram. Giúp các sếp tiết kiệm thời gian tìm kiếm thông tin trong hàng trăm tài liệu PDF, Excel, JSON... chỉ với một câu hỏi trên Telegram."
slug: "tai-tao-tro-ly-ai-tu-dong-hoc-tu-tai-lieu-ollama-pgvector-telegram"
tags: [n8n, automation, ai-rag, ollama, pgvector, telegram-bot, no-code, enterprise-ai]
keywords: [n8n workflow ai, tự động hóa trợ lý tri thức, ollama n8n, pgvector postgresql, telegram ai assistant, rag system]
---

# 🚀 **Tạo Trợ Lý AI Tự Động Học Tập Từ Tài Liệu - Ollama + PGVector + Telegram (N8N)**

## **🔍 Nỗi Đau Của Các Sếp: Tìm Kiếm Thông Tin Trong Hàng Trăm Tài Liệu Manual**
Các sếp thường phải mất **giờ đồng hồ** để tìm kiếm thông tin trong các tài liệu như:
- **SOP nội bộ** (PDF, Word)
- **Báo cáo tài chính** (Excel, CSV)
- **Hướng dẫn kỹ thuật** (JSON, Markdown)
- **Chính sách doanh nghiệp** (Docx, PPT)

Thay vì **ghi nhớ** hoặc **tìm kiếm keyword** không chính xác, **trợ lý AI tự động hóa** sẽ giúp bạn:
✅ **Học tập từ tất cả tài liệu** một lần duy nhất
✅ **Trả lời câu hỏi** bằng cách **hiểu ngữ nghĩa** chứ không chỉ keyword
✅ **Cung cấp thông tin chính xác** ngay trên Telegram
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** tìm kiếm thông tin so với cách thủ công.
- **Trả lời chính xác** dựa trên ngữ cảnh từ tài liệu (không sai lệch như Google Search).
- **Bảo mật cao** vì toàn bộ dữ liệu được lưu trữ **local** (không gửi lên cloud).
- **Hoạt động liên tục** 24/7, không cần người quản lý.
- **Dễ dàng mở rộng** cho nhiều bộ phận (HR, Finance, Tech, Sales...).
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Ollama** (cài đặt [Ollama](https://ollama.ai/) trên máy chủ hoặc VPS).
2. **PostgreSQL + PGVector** (cài đặt [PGVector](https://github.com/pgvector/pgvector) để lưu trữ embeddings).
3. **Telegram Bot Token** (tạo bot trên [@BotFather](https://t.me/BotFather)).
4. **Dữ liệu đầu vào**:
   - Các tài liệu PDF, Excel, JSON, CSV (để AI học tập).
   - **Không cần API key nào ngoài các dịch vụ trên**.
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/15707](https://n8n.io/workflows/15707) (chọn **Export JSON**).
2. **Mở n8n Editor** → **Import Workflow** → Dán JSON vào.
3. **Hoặc** copy/paste JSON vào **Create Workflow** → **Import from JSON**.

:::note[LƯU Ý]
- **Không cần chỉnh sửa toàn bộ workflow** nếu đã import đúng.
- **Cần cấu hình các node quan trọng** như sau:
:::

---

### **2. Các Bước Cấu Hình BẮT BUỘC**
#### **🔹 Node 1: Telegram Trigger (Bắt đầu từ Telegram)**
- **Cấu hình**:
  - **Credentials**: Chọn bot token Telegram (đã tạo ở bước chuẩn bị).
  - **Trigger**: Chọn **Message** (để bắt đầu từ tin nhắn Telegram).

#### **🔹 Node 2: Form (Chọn Loại Input)**
- **Cấu hình**:
  - **Fields**:
    - `input_type` (File hoặc Text).
    - `file` (nếu chọn File).
    - `text` (nếu chọn Text).

#### **🔹 Node 3: Extract from File (Xử lý Tài Liệu)**
- **Cấu hình**:
  - **Operation**:
    - **PDF** → `extractFromFile` (operation: `pdf`).
    - **Excel (XLS/XLSX)** → `extractFromFile1` (operation: `xlsx`).
    - **JSON** → `extractFromFile4` (operation: `fromJson`).
    - **CSV** → `extractFromFile5` (operation: `csv`).
  - **Lưu ý**: N8N sẽ **tự động phân loại** file dựa trên định dạng.

#### **🔹 Node 4: Ollama Embeddings (Tạo Embeddings)**
- **Cấu hình**:
  - **Credentials**: Chọn `ollamaApi`.
  - **Model**: `llama3.2:3b-text-q4_0` (đã cấu hình sẵn).
  - **Input**: Dữ liệu từ `Extract from File` hoặc `text`.

#### **🔹 Node 5: PostgreSQL PGVector Store (Lưu Trữ Vector)**
- **Cấu hình**:
  - **Credentials**: Chọn `postgres`.
  - **Table Name**: `documents` (hoặc tự tạo).
  - **Collection Name**: `embeddings`.
  - **Lưu ý**: Cần **cài đặt PGVector** trước trên PostgreSQL.

#### **🔹 Node 6: Ollama Chat Model (Trả Lời Câu Hỏi)**
- **Cấu hình**:
  - **Credentials**: Chọn `ollamaApi`.
  - **Model**: `llama3:latest`.
  - **Prompt**: Sử dụng **RAG (Retrieval-Augmented Generation)** để trả lời dựa trên dữ liệu đã lưu.

#### **🔹 Node 7: Send a Text Message (Trả Lời Telegram)**
- **Cấu hình**:
  - **Credentials**: Chọn bot Telegram.
  - **Message**: Dữ liệu từ `Ollama Chat Model`.

---

### **3. Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn Telegram: `Tôi muốn hỏi về SOP bán hàng`.
   - AI sẽ **tìm kiếm trong tài liệu** và trả lời.
2. **Bật Active** workflow.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NGOÀI THƯỜNG]
- **Thêm nhiều bộ tài liệu**: Chỉ cần **upload lại** vào form, AI sẽ tự động học tập.
- **Cập nhật dữ liệu thường xuyên**: AI sẽ **cập nhật tri thức** khi có file mới.
- **Kết hợp với Slack**: Thay vì Telegram, có thể **gửi tin nhắn Slack** bằng node `slack`.
- **Lưu log hoạt động**: Sử dụng node `stickyNote` để ghi lại lịch sử câu hỏi.
- **Tạo báo cáo định kỳ**: Dùng node `googleSheets` để **lưu lịch sử tương tác**.
:::

---

## **📌 Kết Luận**
Workflow này **giải quyết hoàn toàn** vấn đề tìm kiếm thông tin trong tài liệu nội bộ bằng cách:
✔ **Tự động hóa học tập** từ PDF, Excel, JSON...
✔ **Trả lời câu hỏi bằng ngữ nghĩa** (không chỉ keyword).
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.
✔ **Bảo mật cao** vì toàn bộ dữ liệu **local**.

**🚀 Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất công việc!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Bạn có thể tùy chỉnh workflow này cho nhiều mục đích khác như:**
- **Trợ lý HR** (hỏi về chính sách, thủ tục).
- **Trợ lý Finance** (tìm kiếm báo cáo tài chính).
- **Trợ lý Tech** (hỏi về mã nguồn, SOP kỹ thuật).