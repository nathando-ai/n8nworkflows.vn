---
title: "🚀 Tự động quét Reddit tìm ý tưởng Startup mỗi tuần bằng Groq AI và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét 10 subreddits, lọc tín hiệu phàn nàn, phân tích bằng Groq AI và gửi báo cáo cơ hội startup vào hộp thư Gmail mỗi thứ Hai."
slug: "tu-dong-quet-reddit-tim-y-tuong-startup-groq-ai-n8n"
tags: [n8n, automation, groq-ai, reddit, market-research, ai-summarization]
keywords: [n8n workflow, tự động hóa nghiên cứu thị trường, groq ai, reddit pain mining, ý tưởng startup, tạo báo cáo tự động]
---

# 🚀 Tự động quét Reddit tìm ý tưởng Startup mỗi tuần bằng Groq AI và n8n

Việc nghiên cứu thị trường và tìm kiếm ý tưởng sản phẩm (startup idea) thủ công trên các diễn đàn như Reddit tốn rất nhiều thời gian và dễ bỏ sót các tín hiệu quan trọng từ khách hàng. Thay vì lướt Reddit hàng giờ mỗi ngày, các sếp có thể để hệ thống tự động hóa làm thay toàn bộ công việc từ quét bài viết, lọc nỗi đau (pain points), phân tích bằng AI cho đến gửi báo cáo chi tiết thẳng vào hộp thư Gmail chỉ trong vòng chưa đầy 60 giây mỗi tuần!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Tự động quét ~1.000 bài viết từ 10 subreddits hàng đầu mỗi tuần mà không cần thao tác thủ công.
- **Phát hiện nhu cầu thực tế:** Lọc chính xác các tín hiệu phàn nàn (pain points) thực sự của người dùng dựa trên từ khóa thông minh.
- **Báo cáo chuyên sâu bằng AI:** Sử dụng mô hình AI mạnh mẽ (Groq - Llama 3.3) để gom nhóm nỗi đau, đề xuất giải pháp startup cụ thể, ngách chưa được phục vụ (undeserved niches) và các ý tưởng Quick Wins.
- **Chủ động nhận tin:** Báo cáo HTML định dạng đẹp mắt được gửi thẳng vào Gmail cá nhân vào mỗi sáng thứ Hai lúc 8:00.
:::

### 📦 Các thành phần trong Workflow
- **Trigger:** Schedule Trigger (Chạy lúc 8h sáng thứ Hai hàng tuần) hoặc Manual Trigger (Chạy thủ công khi cần).
- **Xử lý dữ liệu (Code Nodes):** Định nghĩa danh sách subreddits, lọc bài viết theo từ khóa phàn nàn, tổng hợp dữ liệu, tạo prompt AI và định dạng HTML email.
- **API tương tác:** HTTP Request gọi Reddit Public JSON API (không cần tài khoản Reddit) và Groq AI API (`llama-3.3-70b-versatile`).
- **Gửi thông báo:** Gmail Node gửi báo cáo hoàn thiện.

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đang hoạt động (Self-hosted hoặc Cloud).
- **Groq API Key:** Miễn phí tại [console.groq.com](https://console.groq.com) để sử dụng mô hình AI phân tích.
- **Gmail Account:** Tài khoản Google để kết nối qua n8n Gmail OAuth2 credential.
- **Không cần tài khoản Reddit:** Workflow sử dụng API JSON công khai của Reddit kèm User-Agent.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn gốc hoặc copy toàn bộ JSON.
- Trong giao diện n8n Editor, bấm vào menu **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `6. HTTP Request @Groq`:** 
  - Chọn hoặc tạo mới **Credential** loại `Header Auth`.
  - Nhập tên Header là `Authorization` và giá trị là `Bearer <groq_api_key_cua_ban>`.
- **Node `8. Gmail. Send Email Report`:**
  - Chọn hoặc kết nối **Credential** loại `Gmail OAuth2`.
  - Mở node này và thay đổi trường **To Email Address** thành địa chỉ email nhận báo cáo của các sếp.
- **Tùy chỉnh (Tùy chọn):**
  - Node `1. Define Subreddits`: Có thể thay đổi danh sách các subreddit theo ngách kinh doanh của các sếp (ví dụ: `ecommerce`, `shopify`, `AI`,... thay vì các sub mặc định).
  - Node `3. Filter Pain Points`: Thêm hoặc bớt các từ khóa phàn nàn ("I hate", "wish there was a tool",...) để điều chỉnh độ nhạy khi quét bài viết.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thủ công một lần và kiểm tra hộp thư Gmail xem báo cáo đã về chưa.
- Nếu mọi thứ hoạt động trơn tru, hãy chuyển trạng thái workflow sang **Active** để chạy tự động định kỳ.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Thay vì chỉ gửi Gmail, các sếp có thể kết nối thêm node **Slack** hoặc **Telegram** để nhận cảnh báo ngay lập tức trên điện thoại khi có ý tưởng hot.
- **Tăng tần suất:** Đổi Schedule Trigger thành chạy hàng ngày (Daily) nếu ngách thị trường có lượng thảo luận cực lớn.
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Notion** trước bước gửi email để lưu lại toàn bộ lịch sử các ý tưởng startup, tiện cho việc tra cứu và theo dõi dài hạn.
- **Đổi AI Model:** Có thể dễ dàng thay thế Groq bằng OpenAI GPT-4o hoặc Anthropic Claude bằng cách đổi URL và Header trong node HTTP Request tương ứng.

---

### 📌 Kết luận
Workflow "Generate weekly Reddit startup opportunity reports with Groq AI" là một trợ lý nghiên cứu thị trường hoàn hảo, giúp các sếp khai thác mỏ vàng ý tưởng kinh doanh từ cộng đồng quốc tế một cách tự động và hoàn toàn miễn phí (với hạn mức của Groq). Hãy áp dụng ngay vào hệ thống n8n của các sếp để đón đầu các xu hướng sản phẩm tiềm năng trong tuần này!