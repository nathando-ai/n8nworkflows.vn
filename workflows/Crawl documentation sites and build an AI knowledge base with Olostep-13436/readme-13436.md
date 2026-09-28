---
title: "🤖 **Tự Động Hóa Crawl Documentation + Xây Dựng Trình Đọc Tri Thức AI (Olostep) – Giải Pháp Cho Dev & SaaS**"
description: "Workflow này tự động quét, trích xuất và chuyển đổi tài liệu kỹ thuật từ website thành **bản documentation sạch, có cấu trúc**, lưu trữ trên Google Drive/Docs. Giúp dev teams tiết kiệm 80% thời gian soạn thảo thủ công."
slug: "tieu-dong-hoa-crawl-documentation-xay-dung-trinh-doc-tri-thuc-ai"
tags: [n8n, automation, document-extraction, ai-knowledge-base, olostep, google-drive, google-docs, no-code]
keywords: [n8n workflow crawl documentation, tự động hóa trích xuất tài liệu kỹ thuật, xây dựng knowledge base AI, Olostep API, Google Docs tự động hóa, AI documentation generator]
---

# **🚀 Tự Động Hóa Crawl Documentation + Xây Dựng Trình Đọc Tri Thức AI (Olostep) – Giải Pháp Cho Dev & SaaS**

## **💡 Giới Thiệu: Tại Sao Các Sếp Cần Workflow Này?**
Hiện nay, **dev teams và SaaS companies** phải mất **thời gian và công sức khổng lồ** để:
- **Quét thủ công** tài liệu kỹ thuật từ website (API docs, wiki, blog).
- **Chuyển đổi** nội dung thô thành dạng có cấu trúc (Markdown, Google Docs).
- **Cập nhật liên tục** khi tài liệu thay đổi trên website.
- **Tạo knowledge base** dễ tìm kiếm cho team hoặc khách hàng.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động crawl** tất cả trang documentation từ URL gốc.
✅ **Trích xuất nội dung** bằng AI (Olostep) và **tạo cấu trúc logic** (API endpoints, cURL examples, authentication methods).
✅ **Chuyển đổi thành Google Docs** có **cấu trúc folder tự động** theo URL path.
✅ **Cập nhật liên tục** khi kích hoạt (không cần viết code).

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** soạn thảo documentation thủ công.
- **Cập nhật tự động** khi tài liệu trên website thay đổi.
- **Cấu trúc logic** (API references, cURL examples, warning notes) được AI **tách biệt và sắp xếp**.
- **Lưu trữ sạch sẽ** trên Google Drive với **folder mirror** theo URL path.
- **Dễ dàng chia sẻ** với team hoặc khách hàng qua Google Docs.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản n8n** (Self-hosted hoặc Cloud).
✔ **API Key Olostep** (để crawl và trích xuất nội dung).
✔ **Tài khoản Google Drive & Google Docs** (để lưu trữ documentation).
✔ **API Key Google Gemini** (hoặc OpenAI) (để AI chuyển đổi nội dung).
✔ **URL gốc của documentation** (ví dụ: `https://docs.example.com/api`).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13436](https://n8n.io/workflows/13436) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** để thêm workflow vào workspace.

### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflow gồm **26 node** với logic phức tạp. Dưới đây là **các node quan trọng cần chỉnh**:

#### **🔹 Node 1: Manual Trigger (Bắt Đầu Tự Động)**
- **Không cần cấu hình**, chỉ cần **nhấn "Execute workflow"** khi muốn crawl.

#### **🔹 Node 2-3: Olostep Scrape (Crawl & Tạo Sitemap)**
- **Node "Create a map"** (Olostep Scrape):
  - **Điền `resource: map`** và **URL gốc** (ví dụ: `https://docs.example.com`).
  - **Lưu ý**: Olostep API cần **API Key** (đã cấu hình trong `olostepScrapeApi`).
- **Node "Scrape a URL"** (Olostep Scrape):
  - **Không cần chỉnh**, workflow sẽ tự động scrape từng URL từ sitemap.

#### **🔹 Node 4-7: Google Drive (Tạo Cấu Trúc Folder)**
- **Node "Create Parent Folder"** (Google Drive):
  - **Tên folder**: `API_Documentation_[Tên_Dịch_Vụ]` (ví dụ: `API_Documentation_Stripe`).
  - **Credentials**: `googleDriveOAuth2Api` (đã cấu hình trước).
- **Node "Search files and folders"**:
  - **Kiểm tra** nếu folder đã tồn tại để **tránh trùng lặp**.
- **Node "Create folder"**:
  - **Tự động tạo folder con** theo URL path (ví dụ: `v1/endpoints/payment` → `v1/endpoints/payment/`).

#### **🔹 Node 8-10: AI Trích Xuất & Chuyển Đổi Nội Dung**
- **Node "Information Extractor" (LangChain)**:
  - **AI trích xuất** các phần quan trọng:
    - **API summaries** (mô tả endpoint).
    - **cURL examples** (ví dụ request).
    - **Authentication methods** (API key, OAuth).
    - **Common pitfalls** (lỗi thường gặp).
  - **Không cần chỉnh**, workflow tự động phân tích.
- **Node "Google Gemini Chat Model" (AI Writer Agent)**:
  - **Chuyển đổi nội dung thô** thành **bản documentation sạch** (dạng Markdown).
  - **Prompt mặc định** đã được tối ưu, nhưng có thể **cập nhật** trong `set` node trước đó.

#### **🔹 Node 11-13: Tạo & Cập Nhật Google Docs**
- **Node "Create a document"** (Google Docs):
  - **Tên file**: Tự động lấy từ **URL path** (ví dụ: `payment_create.md`).
  - **Nội dung**: Được AI **chuyển đổi** từ `Information Extractor`.
- **Node "Update a document"** (Google Docs):
  - **Cập nhật nội dung** nếu file đã tồn tại.

#### **🔹 Node 14: Wait (Rate Control)**
- **Giảm tải API** khi crawl nhiều trang.
- **Thời gian mặc định**: 2 giây/URL (có thể điều chỉnh).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với **URL mẫu** (ví dụ: `https://docs.example.com/api/v1/payment`).
2. **Kiểm tra Google Drive** để xem folder và file đã tạo.
3. **Bật "Active"** để workflow chạy tự động khi kích hoạt.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM NÂNG CAO]
- **Lọc URL cụ thể**: Sử dụng **node `If`** để chỉ crawl những trang có `api` trong URL.
- **Thêm vector database**: Kết nối với **Pinecone/Supabase** để tạo **trình đọc tri thức AI** (RAG).
- **Gửi báo cáo Slack/Telegram**: Thêm **node `webhook`** để thông báo khi crawl hoàn tất.
- **Cập nhật tự động**: Sử dụng **n8n Cron Trigger** để crawl hàng ngày.
- **Chuyển sang Notion/Confluence**: Thay thế **Google Docs** bằng **Notion API** hoặc **Confluence**.
:::

---
## **📌 Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow này **giải phóng dev teams** khỏi công việc **quét, chuyển đổi và cập nhật documentation thủ công**. Với **AI + Automation**, các sếp có thể:
✔ **Tạo knowledge base** trong **vài phút** thay vì **tuần**.
✔ **Cập nhật liên tục** khi tài liệu thay đổi.
✔ **Chia sẻ dễ dàng** với team hoặc khách hàng.

**👉 Hành động ngay:**
1. **Import workflow** và **cấu hình API keys**.
2. **Nhấn "Execute"** và **xem kết quả trên Google Drive**.
3. **Tối ưu hóa** bằng cách thêm **Slack notifications** hoặc **vector database**.

**💡 Lưu ý**: Để workflow **ổn định 24/7**, các sếp nên **self-host n8n** trên **VPS** (giá rẻ từ **50k/tháng**).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Chúc các sếp thành công với workflow tự động hóa documentation!** 🤖📚