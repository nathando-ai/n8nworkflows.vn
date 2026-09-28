---
title: "🚀 Tự động hóa Crawl Sitemap và Lưu trữ Vector cho hệ thống RAG với n8n"
description: "Hướng dẫn xây dựng workflow n8n toàn diện giúp cào dữ liệu từ sitemap website, xử lý, tạo embeddings và lưu vào Supabase Vector Store phục vụ cho RAG một cách tự động."
slug: "tu-dong-hoa-crawl-sitemap-vector-storage-rag-n8n"
tags: [n8n, automation, rag, supabase, openai, sitemap, crawling, vector-store]
keywords: [n8n workflow, crawl sitemap, vector store supabase, RAG automation, embeddings openai, crawl4ai]
---

# 🚀 Tự động hóa Crawl Sitemap và Lưu trữ Vector cho hệ thống RAG

Các sếp đang xây dựng chatbot AI hoặc hệ thống RAG (Retrieval-Augmented Generation) nhưng gặp khó khăn trong việc cập nhật dữ liệu từ website doanh nghiệp? Việc cào dữ liệu thủ công, làm sạch HTML và tạo vector embedding tốn hàng giờ đồng hồ mỗi khi website có bài viết mới?

Đừng lo, workflow n8n được thiết kế bởi chuyên gia **Mariela Slavenova** này sẽ giải quyết triệt để vấn đề trên. Đây là giải pháp tự động hóa từ A-Z: từ việc đọc Sitemap của website, kiểm tra trùng lặp qua Supabase, cào nội dung bằng Crawl4AI, phân tách văn bản (Text Splitting), tạo OpenAI Embeddings và lưu trữ trực tiếp vào Supabase Vector Store.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các trang web lớn mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quét toàn bộ sitemap, tự động phát hiện URL mới và đưa vào hàng đợi xử lý mà không cần can thiệp thủ công.
- **Tối ưu hóa chi phí & tài nguyên:** Kiểm tra thông minh qua cơ sở dữ liệu Supabase để đảm bảo không cào trùng lặp các URL đã tồn tại.
- **Dữ liệu RAG chất lượng cao:** Tự động làm sạch mã HTML, trích xuất metadata tốt hơn và chia nhỏ văn bản (Text Splitter) trước khi tạo Embeddings bằng OpenAI.
- **Vận hành bền bỉ:** Sử dụng cơ chế vòng lặp (Batch/Loop), chờ (Wait) và quản lý trạng thái task giúp hệ thống không bị quá tải hay vượt quá giới hạn API (Rate Limit).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted trên VPS).
- **Supabase Account:** Tạo sẵn một Project trên Supabase (cần chuẩn bị thông tin kết nối Database PostgreSQL và API Keys).
- **OpenAI API Key:** Dùng để tạo Vector Embeddings (`text-embedding-ada-002` hoặc các model tương đương).
- **Crawl4AI Service / API Header Auth:** Dịch vụ cào web được cấu hình thông qua HTTP Request node trong workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn gốc.
- Mở giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc dán trực tiếp JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **HTTP Request (Crawl Sitemap):** Trỏ URL đến file `sitemap.xml` của trang web mà các sếp muốn crawl dữ liệu (ví dụ: `https://websitecua-ban.com/sitemap.xml`).
- **Supabase Nodes (`Check if the URL is in the Supabase Table`, `URL in a new row`, v.v.):** Cấu hình `SupabaseApi` Credentials, kết nối đến project Supabase và đảm bảo tên bảng (`scrape_queue`) khớp với cấu trúc cơ sở dữ liệu.
- **CREATE TABLE scrape_queue in Supabase & CREATE TABLE scrape_queue in Supabase1:** Sử dụng node `Postgres` với credentials database Postgres của Supabase để tự động khởi tạo bảng hàng đợi (`scrape_queue`) nếu bảng chưa tồn tại.
- **Embeddings OpenAI:** Nhập `OpenAI API Key` và cấu hình model nhúng (Embeddings Model) phù hợp (mặc định là `text-embedding-ada-002`).
- **Supabase Vector Store_documents:** Cấu hình kết nối Supabase để lưu trữ các chunks văn bản và vector embeddings sau khi qua các node `Default Data Loader` và `Character Text Splitter`.
- **Crawl4ai Web Page Scrape & Crawl4AI_Task Status:** Thiết lập `HTTP Header Auth` để xác thực với dịch vụ Crawl4AI khi thực hiện tác vụ cào nội dung chi tiết từng trang web.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** trên node `When clicking ‘Test workflow’` để kiểm tra luồng chạy với một vài URL mẫu.
- Kiểm tra kết quả trả về trong Supabase xem dữ liệu đã được phân tách và lưu trữ vào Vector Store thành công chưa.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow tự động hoạt động theo lịch trình hoặc sự kiện kích hoạt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối workflow để nhận thông báo mỗi khi hệ thống quét xong sitemap hoặc gặp lỗi ở một URL cụ thể.
- **Thiết lập Cron Trigger:** Thay thế `Manual Trigger` bằng `Schedule Trigger` để n8n tự động cập nhật kiến thức cho hệ thống RAG hàng tuần hoặc hàng tháng.
- **Kết hợp LLM kiểm định chất lượng nội dung:** Sử dụng thêm các node AI Agent hoặc OpenAI Chat Model trước bước lưu vector để lọc bỏ các trang rác, trang lỗi 404 hoặc nội dung không liên quan.

### 📌 Kết luận
Workflow "From Sitemap Crawling to Vector Storage" là một cỗ máy tự động hóa cực kỳ mạnh mẽ giúp các doanh nghiệp xây dựng và duy trì cơ sở tri thức (Knowledge Base) cho AI một cách bài bản, tiết kiệm tối đa thời gian và chi phí. Hãy setup ngay trên hệ thống n8n của các sếp để nâng tầm các ứng dụng RAG của mình nhé!