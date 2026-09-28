---
title: "🚀 **Tự Động Hóa Cố Vấn Radar Công Nghệ AI-Powered Với SQL, RAG & Routing Agent (N8n + LangChain)**"
description: "Workflow này tự động hóa việc chuyển đổi dữ liệu Tech Radar từ Google Sheets sang cơ sở dữ liệu MySQL và vector database Pinecone, sau đó kết hợp với AI Agent để phân tích, trả lời câu hỏi và đưa ra hướng dẫn chiến lược cho doanh nghiệp. Giúp các sếp tiết kiệm thời gian lên đến 80% trong việc cập nhật và phân tích dữ liệu công nghệ."
slug: "tự-dộng-hoa-ai-powered-tech-radar-advisor"
tags: [n8n, automation, ai, langchain, mysql, pinecone, google-sheets, google-drive, no-code]
keywords: [n8n workflow ai, tự động hóa radar công nghệ, RAG với n8n, AI Agent SQL, Pinecone vector database, tự động hóa doanh nghiệp]
---

# 🚀 **Tự Động Hóa Cố Vấn Radar Công Nghệ AI-Powered: Từ Dữ Liệu → AI → Chiến Lược**

## **Giới Thiệu**
Các sếp đã từng phải mất **từ 10-20 giờ/tuần** để cập nhật, phân tích và trả lời các câu hỏi liên quan đến **công nghệ mới, xu hướng thị trường, hoặc so sánh công nghệ giữa các doanh nghiệp**? Hoặc phải **đọc hàng trăm trang Google Sheets** để tìm thông tin về một công nghệ cụ thể?

Workflow này là **giải pháp tự động hóa hoàn chỉnh** giúp:
✅ **Chuyển đổi dữ liệu Tech Radar** từ Google Sheets sang **cơ sở dữ liệu MySQL** và **vector database Pinecone** (sẵn sàng cho RAG).
✅ **Tích hợp AI Agent** để phân tích, so sánh và trả lời câu hỏi về công nghệ một cách **chính xác và nhanh chóng**.
✅ **Routing Agent** tự động chọn **SQL Agent** (trả lời từ cơ sở dữ liệu) hoặc **RAG Agent** (trả lời từ vector database) dựa trên yêu cầu.
✅ **Cập nhật tự động** khi có thay đổi trong Google Sheets hoặc tài liệu Google Drive.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công.
- **Trả lời câu hỏi công nghệ trong giây lát** (ví dụ: "Công nghệ nào đang được Company X sử dụng?").
- **Cập nhật tự động** khi có thay đổi trong dữ liệu Tech Radar.
- **Chiến lược hóa dữ liệu** với AI Agent đưa ra gợi ý chiến lược.
- **Hoạt động 24/7** mà không cần can thiệp người dùng.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
#### **1. Dịch Vụ & API Keys**
| Dịch vụ/API | Mô Tả | Hướng Dẫn Lấy API Key |
|-------------|--------|----------------------|
| **Google Sheets** | Dữ liệu Tech Radar (các công nghệ, công ty, trạng thái sử dụng) | [Tạo OAuth 2.0 API Key](https://developers.google.com/sheets/api/quickstart/python) |
| **Google Drive** | Lưu trữ tài liệu Google Docs đã chuyển đổi từ Sheets | [Cấu hình OAuth 2.0](https://developers.google.com/drive/api/v3/quickstart/python) |
| **Google Cloud (Vertex AI)** | API cho **Google Gemini (PaLM)** | [Tạo API Key](https://ai.google.dev/tutorials/quickstart) |
| **Pinecone** | Vector database cho RAG | [Đăng ký miễn phí](https://www.pinecone.io/) + [Tạo Index `seanrag`](https://app.pinecone.io/) |
| **Groq API** | API cho các mô hình LLM (Qwen, DeepSeek, Llama) | [Đăng ký API Key](https://console.groq.com/) |
| **Anthropic API** | API cho **Claude 3.5 Sonnet** | [Đăng ký API Key](https://www.anthropic.com/api) |
| **MySQL** | Cơ sở dữ liệu để lưu trữ dữ liệu Tech Radar | [Cài đặt MySQL](https://dev.mysql.com/doc/mysql-installation-excerpt/8.0/en/) |

#### **2. Tài Khoản & Thư Mục**
- **Google Drive**: Tạo **1 thư mục riêng** để lưu tài liệu Google Docs.
- **Google Sheets**: **1 bảng Tech Radar** (cấu trúc mẫu [đây](https://docs.google.com/spreadsheets/d/1R8nj0SXWWmkMaLg0iHt6K0RuTsbUZ5TvMmZwkQkDAyk/edit)).
- **MySQL Database**: Tạo **1 cơ sở dữ liệu mới** để lưu dữ liệu từ Sheets.

#### **3. Hệ Thống N8n**
- **N8n Self-Hosted** (không dùng phiên bản cloud) để **hoạt động 24/7**.
- **N8n Node LangChain** (đã tích hợp sẵn trong workflow).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
1. **Tải workflow JSON** từ [n8n.io/workflows/3151](https://n8n.io/workflows/3151).
2. **Import vào n8n Editor**:
   - Mở **n8n Workflow Editor**.
   - Nhấn **Import** → Chọn file JSON → **Import**.
   - **Hoặc** copy toàn bộ JSON vào **Import Workflow** (Ctrl+V).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** và có **3 phần chính**:
- **Phần 1: Chuyển đổi dữ liệu** (Sheets → Docs → Vector DB + MySQL).
- **Phần 2: AI Agent Routing** (SQL Agent vs RAG Agent).
- **Phần 3: Webhook API** (cho frontend gọi API).

##### **A. Cấu Hình Credentials (BẮT BUỘC)**
| Node | Credential Cần Điền | Hướng Dẫn |
|------|----------------------|------------|
| **Google Sheets** | `googleSheetsOAuth2Api` | [Cấu hình OAuth 2.0](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.googleSheets.html) |
| **Google Drive** | `googleDriveOAuth2Api` | [Cấu hình OAuth 2.0](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.googleDrive.html) |
| **Google Gemini (PaLM)** | `googlePalmApi` | Điền **API Key** từ Google Cloud. |
| **Pinecone** | `pineconeApi` | Điền **API Key** + **Index Name** (`seanrag`). |
| **Groq API** | `groqApi` | Điền **API Key**. |
| **Anthropic API** | `anthropicApi` | Điền **API Key**. |
| **MySQL** | `mySql` | Điền **Host, Port, Username, Password, Database Name**. |

##### **B. Cấu Hình Node Quan Trọng**
1. **`Google Drive - Doc File Updated`**
   - **Watch folder**: Chọn **thư mục Google Drive** đã tạo.
   - **File types**: Chọn **Google Docs** (`.gdoc`).

2. **`MySQL -delete all data`**
   - **SQL Query**: `DELETE FROM tech_radar` (hoặc tên bảng của bạn).

3. **`MySQL - insert all from sheets`**
   - **SQL Query**: `INSERT INTO tech_radar (...) VALUES (...)`
   - **Lưu ý**: Cần **chuyển đổi dữ liệu từ Sheets thành dạng SQL** (node `Code - Transform table into rows`).

4. **`Pinecone Vector Store`**
   - **Index Name**: `seanrag` (hoặc tên index của bạn).
   - **Environment**: Chọn **environment Pinecone** đã tạo.

5. **`API Request - Webhook`**
   - **Path**: `radar-rag` (không đổi).
   - **HTTP Method**: `POST`.
   - **Lưu ý**: Nếu **self-hosted**, thay đổi `https://n8n.jom.lol` thành **domain của bạn**.

6. **`Execute Workflow - Sql Agent` & `Execute Workflow - RAG Agent`**
   - **Copy 2 workflow con** (Subworkflow 1 & 2) vào **n8n của bạn**, sau đó **link lại**.

##### **C. Cấu Hình Cron (Nếu Cần Cập Nhật Định Kỳ)**
- Node **`Cron`** được sử dụng để **xóa và cập nhật dữ liệu MySQL** định kỳ.
- **Cấu hình**:
  - **Schedule**: `0 0 * * *` (lúc 00:00 hàng ngày).
  - **Active**: Bật nếu muốn **cập nhật tự động**.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** với **dữ liệu mẫu** (ví dụ: `{"chatInput": "Công nghệ nào đang được Company X sử dụng?"}`).
   - Kiểm tra **MySQL** và **Pinecone** có dữ liệu không.

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN THÊM]
1. **Gửi Báo Cáo Định Kỳ**
   - Sử dụng **node `executeWorkflow`** kết hợp với **Google Sheets** để **tạo báo cáo tuần/month** về xu hướng công nghệ.

2. **Kết Nối Slack/Telegram**
   - Thêm **node `slack`** hoặc **`telegram`** vào cuối workflow để **báo lỗi** hoặc **cập nhật kết quả** tự động.

3. **Lưu Lịch Sử Chat**
   - Sử dụng **node `memoryBufferWindow`** để **lưu lịch sử câu hỏi** của người dùng vào **NocoDB** (mô tả trong ghi chú).

4. **Tối Ưu Hóa AI Agent**
   - Thay đổi **mô hình LLM** (ví dụ: từ **Claude 3.5** sang **Qwen 32B** nếu có API key).
   - **Cải thiện prompt** trong node `chainLlm` để trả lời **chính xác hơn**.

5. **Tạo Dashboard**
   - Sử dụng **n8n Dashboard** hoặc **Grafana** để **hiển thị thống kê** về:
     - Số lượng câu hỏi được trả lời.
     - Thời gian phản hồi trung bình.
     - Xu hướng công nghệ phổ biến.

---
### 📌 **Kết Luận**
Workflow này **không chỉ tự động hóa việc cập nhật dữ liệu Tech Radar**, mà còn **tích hợp AI để phân tích và đưa ra chiến lược** cho doanh nghiệp. **Các sếp không cần viết code**, chỉ cần **cấu hình các API key và kết nối dịch vụ** là có thể sử dụng ngay.

**Bắt đầu ngay hôm nay!**
1. **Cài đặt n8n Self-Hosted** (để hoạt động 24/7).
2. **Import workflow** và **cấu hình credentials**.
3. **Test và bật Active**.
4. **Kết nối với frontend** (ví dụ: React, Flutter) để **trả lời câu hỏi công nghệ một cách tự động**.

---
:::note[🔹 **Lưu Ý Cuối Cùng**]
- **N8n Self-Hosted** là **yêu cầu bắt buộc** vì workflow này **phức tạp** và cần **hoạt động liên tục**.
- **Nếu không muốn tự cài**, các sếp có thể **đăng ký VPS** từ:
  - 👉 [TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388) (Giảm tới 39%)
  - 👉 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)

**Chúc các sếp thành công với AI Tech Radar Advisor!** 🚀