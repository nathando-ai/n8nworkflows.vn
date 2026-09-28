---
title: "🚀 Tự động hóa sản xuất bài viết chuẩn SEO với Perplexity, OpenAI & GitHub"
description: "Xây dựng hệ thống tự động tìm kiếm xu hướng, nghiên cứu chuyên sâu và xuất bản bài viết blog 2000+ từ lên GitHub mỗi 8 giờ hoàn toàn tự động bằng n8n."
slug: "tu-dong-hoa-viet-blog-seo-perplexity-openai-github"
tags: [n8n, automation, content-creation, ai, openai, perplexity, github]
keywords: [n8n workflow, tự động hóa viết blog, AI content generation, Perplexity AI, OpenAI GPT, GitHub automation]
keywords: [n8n workflow, tự động hóa viết blog, AI content generation, Perplexity AI, OpenAI GPT, GitHub automation]
---

# 🚀 Tự động hóa sản xuất bài viết chuẩn SEO với Perplexity, OpenAI & GitHub

Việc duy trì một lượng content đều đặn, chất lượng cao và chuẩn SEO cho website là "cực hình" đối với mọi team Marketing. Các sếp thường phải tốn hàng giờ để nghiên cứu từ khóa, tổng hợp tài liệu, viết bài dài hơn 2000 từ và đẩy lên CMS. 

Chưa kể, nếu thuê nhân sự viết bài thủ công thì chi phí lớn mà tốc độ lại chậm. Workflow n8n này sinh ra để giải quyết triệt để bài toán đó: **Tự động tìm xu hướng, nghiên cứu chuyên sâu, viết bài dài chuẩn SEO và đẩy thẳng code lên GitHub** mà không cần con người nhúng tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Hệ thống tự quét trend, viết bài và publish định kỳ 8 tiếng/lần nhờ `Schedule Trigger`.
- **Hàm lượng thông tin cực cao:** Kết hợp sức mạnh tìm kiếm thời gian thực của **Perplexity AI** giúp bài viết không bị lỗi thời, cập nhật sát xu hướng thị trường.
- **Bài viết chuẩn SEO chuyên sâu:** **OpenAI GPT** đảm nhận việc nhào nặn cấu trúc, viết bài dài hơn 2000 từ mạch lạc, chuẩn SEO.
- **Lưu trữ an toàn:** Tự động đẩy file markdown trực tiếp vào kho lưu trữ **GitHub**, sẵn sàng tích hợp với các nền tảng Static Site Generator (như Astro, Hugo, Next.js).
:::

### 📦 Các Nodes trong Workflow
Workflow này gọn nhẹ nhưng cực kỳ mạnh mẽ với 7 nodes:
1. **Every 8 hours (`scheduleTrigger`)**: Bộ định giờ kích hoạt quy trình tự động chạy mỗi 8 tiếng.
2. **Find Trending Topics (`perplexity`)**: Sử dụng Perplexity để tìm các chủ đề đang hot trong ngành.
3. **Set Topic Data (`set`)**: Lưu trữ và chuẩn hóa dữ liệu chủ đề vừa tìm được.
4. **Deep Research (`perplexity`)**: Khai thác thông tin chi tiết, số liệu, tài liệu tham khảo chuyên sâu về chủ đề.
5. **Generate 2000+ Word Article (`openAi`)**: Sử dụng mô hình OpenAI để viết bài blog hoàn chỉnh dài hơn 2000 từ dựa trên nghiên cứu.
6. **Format Blog JSON (`code`)**: Dùng đoạn mã JavaScript để định dạng lại kết quả thành cấu trúc JSON chuẩn trước khi đẩy đi.
7. **Create File in GitHub (`github`)**: Tự động tạo và commit file bài viết mới vào repository trên GitHub.

---

### 🔧 Yêu cầu cần thiết
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (phiên bản Cloud hoặc Self-hosted).
- **Perplexity API Key:** Tài khoản và API key để gọi mô hình nghiên cứu.
- **OpenAI API Key:** Tài khoản OpenAI có quyền gọi các mô hình GPT mới nhất.
- **GitHub Account & Repository:** Một kho lưu trữ (repo) trên GitHub đã cấp quyền truy cập (Personal Access Token) cho n8n để có thể tạo file.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow (hoặc copy mã nguồn JSON).
- Mở n8n Dashboard -> Chọn **Workflows** -> Nhấp vào **Import from JSON** (hoặc dùng tổ hợp phím `Ctrl + V` trực tiếp vào màn hình trống).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thông số sau tại các node tương ứng:
- **Find Trending Topics & Deep Research (`perplexity`)**: 
  - Chọn Credentials: Tạo mới **Perplexity API** credential và dán API Key vào.
  - Tùy chỉnh câu lệnh Prompt (System/User Prompt) để định hướng chủ đề tìm kiếm phù hợp với ngách (niche) website của các sếp.
- **Generate 2000+ Word Article (`openAi`)**:
  - Chọn Credentials: Kết nối tài khoản **OpenAI API**.
  - Kiểm tra lại Model (ví dụ: `gpt-4o` hoặc các dòng model mới nhất) và tinh chỉnh tham số độ dài, cấu trúc bài viết trong phần Prompt để đảm bảo bài viết đạt chuẩn 2000+ từ.
- **Format Blog JSON (`code`)**:
  - Node này dùng JavaScript để xử lý chuỗi văn bản trả về từ AI thành dạng JSON sạch sẽ. Các sếp có thể xem và điều chỉnh lại định dạng tên file (`slug`), tiêu đề (`title`) cho khớp với cấu trúc Frontmatter của website mình.
- **Create File in GitHub (`github`)**:
  - Chọn Credentials: Cấu hình **GitHub OAuth2** hoặc **GitHub API (Personal Access Token)**.
  - Điền chính xác: `Owner` (Tên tài khoản/Tổ chức), `Repository` (Tên kho chứa), `Branch` (Nhánh chính như `main` hoặc `master`), và đường dẫn lưu file (`FilePath`, ví dụ: `content/blog/{{ $json.slug }}.md`).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** ở một nhánh nhỏ hoặc chạy thử node `Find Trending Topics` để test dữ liệu đầu vào.
- Kiểm tra kết quả trả về ở từng node xem có lỗi API hay sai sót cấu trúc không.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm theo lịch trình.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau node GitHub để nhận thông báo tức thì mỗi khi hệ thống viết xong và publish một bài viết mới.
- **Kiểm duyệt con người (Human-in-the-loop):** Thay vì publish thẳng lên GitHub, các sếp có thể cấu hình gửi bản nháp vào Google Sheets hoặc Notion, kèm theo nút bấm phê duyệt trước khi chuyển sang bước đẩy code lên GitHub.
- **Đa ngôn ngữ:** Tinh chỉnh prompt của OpenAI để tự động dịch và xuất bản song song bản tiếng Anh và tiếng Việt.

---

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một "phòng biên tập robot" hoạt động không mệt mỏi 24/7. Tiết kiệm hàng chục triệu đồng chi phí nhân sự mỗi tháng mà vẫn đảm bảo lượng traffic organic đều đặn đổ về website. Áp dụng ngay thôi các sếp ơi!