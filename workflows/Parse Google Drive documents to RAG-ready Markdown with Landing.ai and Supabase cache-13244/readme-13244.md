---
title: "🚀 Tự Động Hóa Xuất Trích Lập Trình RAG từ Tài Liệu Google Drive với Landing.ai & Supabase (Không Code)"
description: "Workflow này tự động theo dõi và chuyển đổi tất cả tài liệu mới (PDF, DOCX...) trong Google Drive thành Markdown sẵn sàng cho RAG (Retrieval-Augmented Generation), tránh tái xử lý bằng cách lưu cache vào Supabase. Giúp tiết kiệm API call Landing.ai lên đến 80% và tối ưu hóa pipeline AI của doanh nghiệp."
slug: "tieu-dong-hoa-xuat-trich-rag-google-drive-landingai-supabase"
tags: [n8n, automation, document-processing, ai-rag, landingai, supabase, google-drive, no-code]
keywords: [tự động hóa xuất trích tài liệu, RAG pipeline, Landing.ai API, cache Supabase, Google Drive automation, tự động hóa AI không code]
---

# 🚀 **Tự Động Hóa Xuất Trích Tài Liệu Google Drive thành Markdown RAG Sẵn Sàng với Landing.ai & Supabase**

## **🔍 Nỗi Đau Của Doanh Nghiệp**
Các sếp đang phải mất **thời gian và chi phí** để:
- **Xuất trích thủ công** hàng trăm trang tài liệu (PDF, DOCX, PPT) để chuẩn bị cho hệ thống AI.
- **Tái xử lý** cùng một tài liệu nhiều lần khi hệ thống không lưu trữ kết quả trước đó.
- **Quản lý API call** Landing.ai một cách thủ công, dẫn đến chi phí không cần thiết.
- **Không tối ưu hóa** pipeline RAG, khiến hệ thống AI không hiệu quả.

**Workflow này giải quyết tất cả bằng cách:**
✅ **Tự động theo dõi** tất cả tài liệu mới trong Google Drive.
✅ **Xuất trích thành Markdown RAG sẵn sàng** (dùng cho LangChain, LlamaIndex, hay các framework khác).
✅ **Lưu cache vào Supabase** để tránh tái xử lý, tiết kiệm **API call Landing.ai lên đến 80%**.
✅ **Báo cáo lỗi & thời gian chờ** để quản lý hiệu quả.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% API call Landing.ai** nhờ cache Supabase.
- **Xuất trích tự động** tất cả tài liệu mới trong Google Drive (PDF, DOCX, PPT...).
- **Markdown RAG sẵn sàng** cho LangChain, LlamaIndex, hay các hệ thống AI khác.
- **Báo cáo lỗi & thời gian chờ** để quản lý hiệu quả.
- **Hoạt động liên tục 24/7** trên VPS riêng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để chọn folder theo dõi).
2. **Tài khoản Landing.ai** (để xuất trích tài liệu).
3. **Tài khoản Supabase** (để lưu cache và quản lý trạng thái).
4. **API Keys & Credentials**:
   - **Google Drive OAuth2** (để truy cập folder).
   - **Landing.ai API Key** (để gọi API xuất trích).
   - **Supabase API Key** (để lưu cache và quản lý trạng thái).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13244](https://n8n.io/workflows/13244).
- **Import vào n8n Editor** bằng cách:
  - Nhấn **Import** → Chọn file JSON → **Import**.
  - **Hoặc** copy toàn bộ JSON vào **Import Workflow** (tab bên trái).

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **20 node**, các sếp cần **cấu hình chính xác** các node sau:

#### **🔹 Node 1: Google Drive Trigger**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Folder ID**: Điền **ID folder** bạn muốn theo dõi (lấy từ liên kết Google Drive: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
  - **File Types**: Chọn `pdf`, `docx`, `pptx` (hoặc tùy chỉnh).

#### **🔹 Node 2: Download File**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api` (giống node trước).
  - **File ID**: Auto lấy từ trigger.

#### **🔹 Node 3: Check Cache (Supabase)**
- **Cấu hình**:
  - **Credentials**: Chọn `supabaseApi`.
  - **Query**: Kiểm tra xem file đã được xuất trích chưa bằng `SELECT * FROM landing_parse_cache WHERE file_id = $file_id`.
  - **Nếu có kết quả**: Bỏ qua xử lý (node `STOP — Cached`).

#### **🔹 Node 4: Submit to Landing.ai**
- **Cấu hình**:
  - **Credentials**: Chọn `httpBearerAuth` (điền **API Key Landing.ai**).
  - **Headers**:
    - `Content-Type: application/json`
    - `organization-id: [Tên tổ chức của bạn]` (nếu có).
  - **Body**:
    ```json
    {
      "file": "base64_encoded_file",
      "format": "markdown"
    }
    ```
  - **Lưu ý**: File phải được encode base64 trước khi gửi.

#### **🔹 Node 5: Poll Job Status (Landing.ai)**
- **Cấu hình**:
  - **Credentials**: Chọn `httpBearerAuth`.
  - **Headers**: `organization-id: [Tên tổ chức]`.
  - **Body**:
    ```json
    {
      "job_id": "$job_id"
    }
    ```
  - **Thời gian chờ**: Cấu hình `wait till interval set time` (ví dụ: 10 giây).

#### **🔹 Node 6: Save Parse Result (Supabase)**
- **Cấu hình**:
  - **Credentials**: Chọn `supabaseApi`.
  - **Query**: Lưu kết quả vào bảng `landing_parse_cache`:
    ```sql
    INSERT INTO landing_parse_cache
    (file_id, document_name, mime_type, file_size_bytes, job_id, job_status, markdown, uploaded_at, workflow_run_id)
    VALUES ($file_id, $document_name, $mime_type, $file_size_bytes, $job_id, $job_status, $markdown, NOW(), $workflow_run_id)
    ```

#### **🔹 Node 7: Log Timeout (Supabase)**
- **Cấu hình**:
  - **Credentials**: Chọn `supabaseApi`.
  - **Query**: Cập nhật trạng thái `job_status = "timeout"` nếu quá thời gian chờ.

---

### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Upload một file mẫu (PDF/DOCX) vào folder Google Drive đã cấu hình.
  - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
- **Bật Active**:
  - Chuyển trạng thái workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo định kỳ** (ví dụ: hàng tuần) về tài liệu đã xuất trích thành công qua **Slack/Email**.
2. **Lưu log chi tiết** vào Supabase để theo dõi lỗi và hiệu suất.
3. **Kết hợp với LLM** để tự động phân loại tài liệu (ví dụ: hợp đồng, báo cáo, email).
4. **Tối ưu cache** bằng cách thêm trường `last_updated_at` để xóa cache cũ.
5. **Báo động lỗi** khi Landing.ai API bị lỗi (ví dụ: gửi thông báo Slack).
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc xuất trích tài liệu thủ công, đồng thời **tối ưu hóa chi phí API** bằng cách tránh tái xử lý. **Đã đến lúc tự động hóa pipeline RAG của bạn!**

👉 **Bắt đầu ngay** bằng cách import workflow và cấu hình theo hướng dẫn trên.
👉 **Cần hỗ trợ?** Đăng ký **VPS n8n** để chạy ổn định 24/7: [TinoHost](https://tino.vn/vps-n8n?affid=388).

**Hãy thử và cảm nhận sự khác biệt!** 🚀