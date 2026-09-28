---
title: "🚀 Tự động hóa viết Blog chuẩn SEO với Gemini, Scrapeless và Pinecone RAG trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động cào dữ liệu web, phân tích SERP, lưu trữ vector Pinecone và sử dụng AI Agent sinh nội dung blog chuẩn SEO."
slug: "tu-dong-hoa-viet-blog-chuan-seo-gemini-scrapeless-pinecone-rag"
tags: [n8n, automation, ai-agent, content-creation, pinecone, gemini, scrapeless]
keywords: [n8n workflow, viết blog tự động, ai seo blog, scrapeless, pinecone rag, gemini chat model]
---

# 🚀 Tự động hóa viết Blog chuẩn SEO với Gemini, Scrapeless và Pinecone RAG

Viết nội dung blog chuẩn SEO đòi hỏi các sếp phải tốn rất nhiều thời gian để nghiên cứu từ khóa trên Google SERP, phân tích website đối thủ, xây dựng cơ sở kiến thức (Knowledge Base) và cuối cùng là chấp bút viết bài. Quá trình thủ công này vừa chậm, vừa khó duy trì chất lượng đồng đều.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code) giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ kết hợp sức mạnh cào dữ liệu thông minh từ **Scrapeless**, lưu trữ và truy vấn ngữ nghĩa qua **Pinecone RAG**, kết hợp cùng mô hình **Google Gemini AI** để tự động phân tích SERP và sinh ra các bài viết blog tối ưu SEO cực kỳ chất lượng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa nghiên cứu đối thủ:** Tự động crawl dữ liệu từ các website mẫu và phân tích từ khóa Google SERP nhờ Scrapeless.
- **Xây dựng Knowledge Base thông minh:** Tự động lưu trữ nội dung vào **Pinecone Vector Store**, giúp AI hiểu sâu sắc về ngữ cảnh và dữ liệu doanh nghiệp.
- **Sản xuất nội dung chuẩn SEO hàng loạt:** Sử dụng **AI Agent** và **Google Gemini** để viết bài blog chuyên sâu, có cấu trúc Markdown và HTML hoàn chỉnh.
- **Hoạt động linh hoạt:** Hỗ trợ cả kích hoạt thủ công (`When clicking ‘Execute workflow’`) lẫn tương tác thời gian thực qua chat (`When chat message received`).
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Scrapeless API Key**: Dành cho các node crawl và phân tích SERP (`Crawl all Blogs`, `Scrape detailed contents`, `Analyze target keywords on Google SERP`).
- **Google Gemini API Key (Google Palm API)**: Cho các node nhúng (Embeddings) và mô hình chat (`Embeddings Google Gemini`, `Google Gemini Chat Model`).
- **Pinecone API Key**: Cho cơ sở dữ liệu vector (`Pinecone Vector Store`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ mã JSON và dán trực tiếp vào màn hình n8n canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 24 nodes được chia thành các phân đoạn rõ ràng theo ghi chú trên canvas:

- **Phân đoạn 1: Scrape and Crawl Website for Knowledge Base**
  - Các node: `Crawl all Blogs`, `Scrape detailed contents`, `Parse content and extract information`, `Split Out the url and text`.
  - *Cấu hình:* Nhập `Scrapeless API Key` vào credentials của các node Scrapeless. Thay đổi URL nguồn website mục tiêu tại node crawl để lấy dữ liệu làm cơ sở kiến thức.

- **Phân đoạn 2: Store data on Pinecone**
  - Các node: `Pinecone Vector Store`, `Default Data Loader`, `Recursive Character Text Splitter`, `Embeddings Google Gemini`.
  - *Cấu hình:* Kết nối `Pinecone API Key` và `Google Gemini API Key`. Cấu hình đúng tên Index trong Pinecone Vector Store để hệ thống đẩy các vector văn bản vừa crawl lên mây.

- **Phân đoạn 3: SERP Analysis using AI**
  - Node chủ lực: `Analyze target keywords on Google SERP` (dùng Scrapeless).
  - *Cấu hình:* Cung cấp API Key và thiết lập từ khóa mục tiêu cần phân tích trên Google SERP để lấy dữ liệu đối thủ.

- **Phân đoạn 4: Use the Knowledge Base to Create Blogs**
  - Các node: `AI Agent1`, `Pinecone Vector Store3`, `Google Gemini Chat Model3`, `Basic LLM Chain1`, `Markdown`, `HTML`, `Convert to File`.
  - *Cấu hình:* Thiết lập prompt cho AI Agent hướng dẫn cách viết bài blog dựa trên dữ liệu truy vấn từ Pinecone RAG. Đảm bảo các node Gemini sử dụng chung một chuẩn Google Gemini API credentials.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu mẫu để kiểm tra toàn bộ chuỗi từ việc cào dữ liệu, đẩy lên Pinecone cho tới khi AI sinh ra nội dung Markdown/HTML thành công.
- Sau khi test không còn lỗi, gạt công tắc sang **Active** để bật chế độ tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh phân phối tự động:** Nối tiếp node `Convert to File` hoặc `Markdown` với các node Telegram, Slack, hoặc WordPress API để tự động đăng bài blog lên website ngay khi AI viết xong.
- **Lưu trữ dữ liệu lịch sử:** Thêm một node Google Sheets hoặc Notion ở cuối luồng để lưu lại tiêu đề, từ khóa và nội dung bài viết phục vụ cho việc quản lý nội dung (Content Calendar).
- **Tối ưu Prompt AI Agent:** Tinh chỉnh system prompt trong `AI Agent1` để ép AI tuân thủ đúng văn phong thương hiệu (Brand Voice) của doanh nghiệp các sếp.

### 📌 Kết luận
Với sự kết hợp đỉnh cao giữa **Scrapeless** (thu thập dữ liệu web & SERP), **Pinecone RAG** (lưu trữ tri thức dài hạn) và **Google Gemini** (bộ não AI thông minh), workflow này giúp các sếp tối ưu hóa toàn bộ quy trình sản xuất nội dung SEO một cách chuyên nghiệp và tiết kiệm thời gian tuyệt đối. Hãy áp dụng ngay vào hệ thống của các sếp để bứt phá traffic organic!