---
title: "🤖 **Tự Động Hóa Trí Tuệ Nhân Tạo (RAG) Cho Hệ Thống GLPI: Tạo Câu Trả Lời Tự Động Từ Wiki Nội Bộ Bằng Google Gemini & PostgreSQL**"
description: "Workflow này tự động hóa việc tạo cơ sở tri thức (Knowledge Base) cho GLPI bằng AI RAG, giúp các sếp trả lời nhanh chóng các câu hỏi kỹ thuật từ nội bộ bằng Google Gemini và lưu trữ vector trong PostgreSQL. Giảm thời gian hỗ trợ IT từ 30 phút xuống 5 giây!"
slug: "tieu-dong-hoa-rag-glpi-google-gemini-postgresql"
tags: [n8n, automation, no-code, ai-rag, google-gemini, postgresql, glpi, knowledge-base, langchain]
keywords: [n8n workflow glpi, tự động hóa hỗ trợ kỹ thuật, ai chatbot glpi, google gemini postgresql, vector database n8n, tri thức nội bộ tự động]
---

# 🚀 **Tự Động Hóa Trí Tuệ Nhân Tạo (RAG) Cho GLPI: Hỗ Trợ Kỹ Thuật 24/7 Bằng Google Gemini**

### **Nỗi Đau Của Các Sếp IT**
Các sếp quản lý hệ thống **GLPI** (Helpdesk & IT Asset Management) thường phải:
- **Tra cứu thủ công** thông tin kỹ thuật trong wiki nội bộ (Confluence, Notion, hoặc cơ sở dữ liệu GLPI) khi nhân viên gọi hỗ trợ.
- **Phản hồi chậm** vì phải chuyển đổi giữa nhiều tab (Slack, email, ticket GLPI) để tìm câu trả lời.
- **Mất thời gian** để cập nhật tri thức mới khi có sự kiện mới (patch security, hướng dẫn mới).

**Workflow này giải quyết tất cả!** Bằng cách kết hợp **Google Gemini (AI multimodal)**, **PostgreSQL (vector database)**, và **n8n**, các sếp có thể:
✅ **Tạo một bot hỗ trợ tự động** trả lời câu hỏi kỹ thuật từ GLPI trong **5 giây** (thay vì 30 phút).
✅ **Tích hợp tri thức từ nhiều nguồn** (Confluence, GLPI, hoặc cơ sở dữ liệu nội bộ) vào một hệ thống duy nhất.
✅ **Cập nhật tự động** khi có thông tin mới (ví dụ: khi ticket GLPI được đóng với tag "knowledge").
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy ổn định 24/7, các sếp nên cài **n8n Self-hosted** trên VPS để đảm bảo:
- **Tính riêng tư** (không phụ thuộc vào n8n.cloud).
- **Tốc độ cao** (Google Gemini và PostgreSQL yêu cầu băng thông ổn định).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** cho đội hỗ trợ kỹ thuật.
- **Chính xác 95%** (so với tra cứu thủ công) nhờ AI RAG (Retrieval-Augmented Generation).
- **Cập nhật tự động** khi có sự kiện mới trong GLPI (ví dụ: ticket được đóng với tag "knowledge").
- **Hoạt động liên tục** 24/7, không cần can thiệp của con người.
- **Tích hợp đa nguồn** (Confluence, GLPI, hoặc cơ sở dữ liệu PostgreSQL).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** với API **Google Gemini** (Chat & Embeddings) được kích hoạt.
   - [Hướng dẫn kích hoạt API Gemini](https://ai.google.dev/gemini-api/docs/get-started)
   - **API Key** cho `lmChatGoogleGemini` và `embeddingsGoogleGemini`.
2. **Cơ sở dữ liệu PostgreSQL** với plugin **pgvector** (để lưu trữ embeddings).
   - [Cài đặt pgvector cho PostgreSQL](https://github.com/pgvector/pgvector)
   - **Thông tin kết nối**:
     - Hostname/IP
     - Port (thường là `5432`)
     - Database name
     - Username & Password
3. **Dữ liệu tri thức** (knowledge base) đã được **embedding** và lưu trong PostgreSQL.
   - Workflow này giả định đã có 2 bảng trong PostgreSQL:
     - `CONHECIMENTO_TI_GLPI` (tri thức kỹ thuật GLPI)
     - `CONFLUENCE_TI_CONFLUENCE_SGU_GPL` (tri thức từ Confluence)
   - Nếu chưa có, các sếp cần **pre-process** dữ liệu trước bằng Python hoặc LangChain.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7171) hoặc copy JSON từ editor n8n.
- **Import vào n8n Editor**:
  - Mở n8n Workflow Editor → Nhấn `Import` → Dán JSON hoặc tải file `.json`.
  - **Kích hoạt mode "Edit"** để cấu hình.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **8 node** quan trọng, các sếp cần cấu hình cẩn thận:

##### **A. Cấu Hình API Google Gemini**
1. **Node `Google Gemini Chat Model`** (type: `lmChatGoogleGemini`):
   - **Credentials**:
     - Chọn `Google Cloud` trong danh sách credentials.
     - Điền **API Key** từ Google Cloud Console.
   - **Tham số**:
     - `Model`: Chọn `gemini-1.5-pro` (hoặc phiên bản mới nhất).
     - `Temperature`: Giá trị mặc định (0.7) hoặc điều chỉnh theo nhu cầu.

2. **Node `Embeddings Google Gemini1` & `Embeddings Google Gemini3`** (type: `embeddingsGoogleGemini`):
   - **Credentials**: Sử dụng cùng **API Key** như trên.
   - **Tham số**:
     - `Model`: Chọn `embedding-001` (hoặc phiên bản mới nhất).
     - **Lưu ý**: Hai node này được sử dụng để **embedding** dữ liệu trước khi lưu vào PostgreSQL.

##### **B. Cấu Hình PostgreSQL Vector Store**
1. **Node `CONHECIMENTO_TI_GLPI`** và `CONFLUENCE_TI_CONFLUENCE_SGU_GPL` (type: `vectorStorePGVector`):
   - **Credentials**:
     - Thêm **credentials mới** cho PostgreSQL.
     - Điền:
       - Hostname/IP
       - Port
       - Database name
       - Username & Password
   - **Tham số**:
     - `Table Name`: Đối với `CONHECIMENTO_TI_GLPI` → `conhecimento_ti_glpi` (không dấu).
     - `Embedding Model`: Chọn `embeddingsGoogleGemini1` (hoặc `embeddingsGoogleGemini3`).
     - `Vector Column`: Tên cột lưu embeddings (ví dụ: `embedding`).
     - `Text Column`: Tên cột lưu nội dung (ví dụ: `content`).
     - **Lưu ý**: Các bảng này **phải đã tồn tại** trong PostgreSQL với schema phù hợp.

##### **C. Cấu Hình AI Agent**
1. **Node `AI Agent`** (type: `agent`):
   - **Credentials**: Sử dụng `Google Gemini Chat Model` (đã cấu hình ở trên).
   - **Tham số**:
     - `Agent Name`: `GLPI Knowledge Agent`.
     - `Memory Buffer`: Chọn `Simple Memory` (node sau).
     - **Lưu ý**: Agent này sẽ **trả lời câu hỏi** dựa trên dữ liệu từ PostgreSQL.

2. **Node `Simple Memory`** (type: `memoryBufferWindow`):
   - **Tham số**:
     - `Window Size`: 5 (lưu 5 câu hỏi gần nhất).
     - **Lưu ý**: Dùng để **bảo lưu lịch sử** của cuộc hội thoại.

##### **D. Trigger: Khi Nhận Tin Nhắn**
1. **Node `When chat message received`** (type: `chatTrigger`):
   - **Lưu ý**: Node này **không cần cấu hình** nếu sử dụng **n8n Webhook** hoặc **Slack/Telegram trigger** khác.
   - **Gợi ý**: Các sếp có thể kết nối với **Slack** hoặc **Discord** để nhận tin nhắn tự động.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn `Run Workflow` và gửi **dữ liệu mẫu** (ví dụ: `"Tôi cần hướng dẫn cách reset mật khẩu GLPI"`).
   - Kiểm tra kết quả trả lời của AI.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** và lưu workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Sử dụng **node `Slack`** hoặc `Telegram Bot` để nhận tin nhắn tự động.
   - **Cách làm**:
     - Thêm node `Slack Incoming Webhook` trước `When chat message received`.
     - Cấu hình URL webhook từ Slack.

2. **Lưu Log & Báo Cáo**:
   - Thêm node `Google Sheets` hoặc `Notion` để **lưu lịch sử câu hỏi** và **báo cáo hiệu suất**.
   - **Cách làm**:
     - Sau node `AI Agent`, thêm node `Google Sheets` với action `Create Row`.
     - Điền các trường: `Question`, `Answer`, `Timestamp`.

3. **Cập Nhật Tri thức Tự Động**:
   - Khi có **ticket mới trong GLPI** với tag `"knowledge"`, tự động **embedding** và lưu vào PostgreSQL.
   - **Cách làm**:
     - Sử dụng **node `GLPI API`** (n8n có node `glpi`) để lấy ticket mới.
     - Sau đó, chạy **node `Embeddings Google Gemini`** và lưu vào PostgreSQL.

4. **Optimize Performance**:
   - **Chia nhỏ dữ liệu** vào nhiều bảng PostgreSQL nếu dữ liệu quá lớn.
   - **Sử dụng caching** với node `Set` để tránh gọi API Gemini nhiều lần.

---

### 📌 **Kết Luận**
Workflow này **giải phóng đội hỗ trợ kỹ thuật** khỏi công việc tra cứu thủ công, đồng thời **cải thiện chất lượng hỗ trợ** nhờ AI RAG của Google Gemini. Các sếp chỉ cần:
1. **Chuẩn bị dữ liệu** (tri thức GLPI & Confluence).
2. **Cấu hình PostgreSQL** với pgvector.
3. **Import & test** workflow.

**Hành động ngay!** Tự động hóa hỗ trợ kỹ thuật của công ty với **n8n + Google Gemini** và giảm thời gian phản hồi xuống **5 giây**!

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/7171) | 📢 [Hỏi đáp trên LinkedIn](http://linkedin.com/in/thiago-vazzoler-loureiro-24056227)**