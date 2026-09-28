---
title: "🚀 Tự động hóa sáng tạo nội dung SEO chuẩn chỉnh với Claude AI, Phân tích đối thủ & Supabase RAG trong n8n"
description: "Hướng dẫn chi tiết workflow n8n tự động hóa nghiên cứu từ khóa, cào dữ liệu đối thủ, kết hợp Claude AI và Supabase RAG để viết content SEO đỉnh cao."
slug: "tu-dong-hoa-tao-content-seo-claude-ai-supabase-rag"
tags: [n8n, automation, ai, seo, claude-ai, supabase, firecrawl]
keywords: [n8n workflow, tạo content seo tự động, claude ai seo, supabase rag, cào dữ liệu đối thủ, firecrawl n8n]
---

# 🚀 Tự động hóa sáng tạo nội dung SEO chuẩn chỉnh với Claude AI, Phân tích đối thủ & Supabase RAG

Viết content SEO chất lượng cao là một công việc cực kỳ tốn thời gian: từ nghiên cứu từ khóa, mổ xẻ top 10 đối thủ, lên outline, tối ưu thẻ meta cho đến đảm bảo giọng điệu thương hiệu. Làm thủ công thì chậm, mà thuê nhân sự thì chi phí lớn. 

Workflow n8n đỉnh cao từ **Growth AI** này chính là giải pháp tự động hóa 100% quy trình trên, giúp các sếp tạo ra các chiến lược content SEO và brief bài viết chuyên sâu chỉ trong vài nốt nhạc nhờ sức mạnh của **Claude AI**, **Apify**, **Firecrawl** và **Supabase RAG**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Từ cào top Google, phân tích đối thủ đến xuất nội dung hoàn chỉnh vào Google Sheets.
- **Cá nhân hóa chuẩn xác**: Tích hợp dữ liệu từ Supabase RAG giúp AI hiểu sâu về sản phẩm/dịch vụ của doanh nghiệp, không bịa đặt thông tin.
- **Tối ưu SEO chuẩn chỉnh**: Tự động sinh Meta Title (max 65 ký tự), Meta Description (max 165 ký tự), H1 (max 70 ký tự) và Content Brief MECE chi tiết.
- **Xử lý hàng loạt mượt mà**: Vận hành theo dạng batch (lô) giúp xử lý hàng chục từ khóa mà không sợ tràn giới hạn API.
:::

### 📦 Chuẩn bị trước khi "lên đồ"
:::info[YÊU CẦU CẦN THIẾT]
Trước khi import workflow, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Khuyên dùng bản self-hosted mới nhất).
- **Google Sheets**: Copy template mẫu tại [đường dẫn này](https://docs.google.com/spreadsheets/d/1cRlqsueCTgfMjO7AzwBsAOzTCPBrGpHSzRg05fLDnWc) để cấu hình `Client Information` và `SEO information`.
- **Anthropic API Key**: Để sử dụng model `Claude Sonnet 4` cho việc viết lách và phân tích.
- **OpenAI API Key**: Dùng cho `Embeddings OpenAI` kết nối Vector Store.
- **Supabase Account**: Nơi lưu trữ vector database chứa thông tin doanh nghiệp (RAG).
- **Firecrawl API Key**: Dùng để scrape dữ liệu các trang đối thủ hàng đầu.
- **Apify API Key**: Dùng để lấy top kết quả tìm kiếm Google (SERP).
:::

---

## 🛠️ Chi tiết các giai đoạn hoạt động trong Workflow

### Phase 0 & 1: Thiết lập & Đọc dữ liệu đầu vào
- **Node `When chat message received` / `Client Information` / `SEO information`**: Nhận yêu cầu khởi chạy qua chat hoặc đọc trực tiếp từ Google Sheets.
- **Node `If1` & `Filter1`**: Kiểm tra tính hợp lệ của dữ liệu, lọc ra các từ khóa cần xử lý (có từ khóa nhưng chưa có H1) để đưa vào hàng đợi.
- **Node `Loop Over Items`**: Chia nhỏ danh sách thành từng batch để xử lý tuần tự qua các bước tiếp theo.

### Phase 2: Nghiên cứu & Phân tích đối thủ (Competitor Research)
- **Node `Apify`**: Gửi yêu cầu tìm kiếm Google để lấy top 10 kết quả hữu cơ cho từ khóa mục tiêu.
- **Node `Scrape 1` đến `Scrape 5` (Firecrawl)**: Cào nội dung chi tiết từ 5 đối thủ đứng đầu.
- **Node `Titre 1` đến `Titre 5` (Code)**: Trích xuất cấu trúc thẻ heading (H1-H6) của đối thủ bằng Javascript để phân tích cách họ cấu trúc bài viết.

### Phase 3 & 4: Tạo thẻ Meta, H1 & Nội dung Brief (Claude AI & Supabase RAG)
- **Node `Supabase Vector Store` & `Embeddings OpenAI`**: Truy vấn cơ sở dữ liệu vector của doanh nghiệp để lấy thông tin ngữ cảnh chính xác, tránh việc AI tự bịa đặt thông tin (hallucination).
- **Node `Meta tag + h1` & `Content brief` (LangChain Agents)**: Sử dụng **Claude Sonnet 4** kết hợp với `Structured Output Parser2` để tạo ra:
  - Meta Title, Meta Description, H1 chuẩn SEO.
  - Phân tích ý định tìm kiếm (Search Intent: informational, transactional...).
  - Cấu trúc bài viết chuẩn MECE với các thẻ H2, H3, gợi ý rich media (hình ảnh, video, bảng biểu) và điểm số chi tiết.

### Phase 5: Lưu trữ kết quả
- **Node `Update row in sheet` (Google Sheets)**: Tự động cập nhật các kết quả đã sinh (Title, Meta-desc, H1, Brief) ngược lại vào file Google Sheets của các sếp mà không làm mất dữ liệu cũ.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ n8n template (ID: `8945`).
- Vào n8n Editor -> Chọn **Add workflow** -> **Import from File** (hoặc paste trực tiếp mã JSON vào).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Google Sheets Nodes (`Client Information`, `SEO information`, `Update row in sheet`)**: 
  - Kết nối tài khoản Google thông qua **OAuth2**.
  - Thay thế Document ID bằng file Google Sheets bản sao của các sếp.
- **Anthropic Nodes (`Anthropic Chat Model`, `Anthropic Chat Model2`)**: 
  - Thêm Credentials cho tài khoản Anthropic (Claude API Key).
- **Firecrawl & Apify Nodes**: 
  - Điền API Key tương ứng vào mục Credentials của từng node.
- **Supabase & OpenAI Nodes**: 
  - Thiết lập kết nối Supabase và OpenAI API Key để hệ thống RAG hoạt động trơn tru.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với 1 dòng dữ liệu mẫu trong Google Sheets để kiểm tra xem dữ liệu có trả về đúng chuẩn hay không.
- Nếu mọi thứ xanh mướt (success), hãy bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng phục vụ 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram**: Thêm node thông báo qua Telegram hoặc Slack ngay sau node `Update row in sheet` để nhận thông báo mỗi khi AI viết xong một bài SEO brief.
- **Mở rộng xuất file**: Thay vì chỉ ghi vào Google Sheets, các sếp có thể kết nối thêm node để tự động tạo Draft bài viết trực tiếp lên **WordPress** hoặc **Webflow**.
- **Quản lý Token**: Vì sử dụng Claude Sonnet 4 với lượng data lớn từ Firecrawl, hãy theo dõi hạn mức API của Anthropic để tránh bị gián đoạn khi xử lý hàng loạt từ khóa.

---

### 📌 Kết luận
Workflow **Generate SEO Content with Claude AI, Competitor Analysis & Supabase RAG** là một "vũ khí tối thượng" cho các đội ngũ Content và SEO muốn tối ưu hóa hiệu suất làm việc gấp 10 lần. Áp dụng ngay hôm nay để tiết kiệm hàng chục giờ nghiên cứu thủ công mỗi tuần!

---
*Cần giải pháp tự động hóa chuyên sâu hơn cho doanh nghiệp? Hãy liên hệ ngay với nhóm tác giả **Growth AI** qua LinkedIn để được tư vấn custom workflow riêng biệt!*
- [Allan Vaccarizi](https://www.linkedin.com/in/allanvaccarizi/)
- [Hugo Marinier](https://www.linkedin.com/in/hugo-marinier-%F0%9F%A7%B2-6537b633/)