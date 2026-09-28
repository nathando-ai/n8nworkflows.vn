---
title: "🚀 Tự động học bất cứ thứ gì từ Hacker News với AI và n8n"
description: "Xây dựng hệ thống tự động tìm kiếm, tổng hợp tài nguyên tốt nhất từ Hacker News về một chủ đề bất kỳ và gửi báo cáo qua email bằng Google Gemini AI."
slug: "hoc-bat-cu-thu-gi-tu-hacker-news-voi-ai-va-n8n"
tags: [n8n, automation, ai, hacker-news, google-gemini, lang-chain]
keywords: [n8n workflow, tự động hóa hacker news, google gemini ai, học lập trình tự động, ai content curation]
---

# 🚀 Tự động học bất cứ thứ gì từ Hacker News với AI và n8n

Các sếp có bao giờ muốn học một công nghệ mới, một kỹ năng hay ho nhưng lại ngợp trước biển thông tin trên Internet? Hacker News (HN) là một mỏ vàng chứa đựng những thảo luận sâu sắc, tài nguyên chất lượng cao từ các chuyên gia hàng đầu thế giới, nhưng việc tìm kiếm và chắt lọc thủ công vô cùng tốn thời gian.

Với workflow n8n này, các sếp chỉ cần nhập chủ đề muốn học vào một biểu mẫu (Form), hệ thống sẽ tự động lùng sục dữ liệu từ Hacker News, nhờ **Google Gemini AI** phân tích các bình luận sâu sắc và tổng hợp thành danh sách tài nguyên đỉnh cao, sau đó gửi thẳng vào email cho các sếp. Hoàn toàn tự động, không tốn một giọt mồ hôi thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu:** Không cần phải lướt hàng trăm thread hay đọc từng comment dài dòng trên Hacker News.
- **Tài liệu chắt lọc đỉnh cao:** Nhận được các đề xuất sách, khóa học, bài viết, công cụ thực tế từ trải nghiệm xương máu của cộng đồng dev thế giới.
- **Tự động hóa toàn diện:** Từ khâu nhập yêu cầu (Form) đến phân tích AI (Gemini) và trả kết quả qua Email đều chạy tự động mượt mà.
- **Cá nhân hóa theo ý muốn:** Muốn học về Go, Rust, AI hay quản trị kinh doanh? Cứ nhập vào form là có ngay báo cáo chuyên sâu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Dành cho node AI phân tích dữ liệu.
- **SMTP Credentials:** Tài khoản email (Gmail, SendGrid, Resend...) để hệ thống gửi email báo cáo kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n -> Nhấp vào menu **Workflows** -> **Import from JSON** và dán vào để hệ thống tự vẽ sơ đồ các node.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 10 nodes phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **GetTopicFromToLearn (`formTrigger`):** Đây là điểm khởi đầu. Sếp sẽ nhận được một đường link form. Hãy mở form này lên và nhập chủ đề mình muốn học mỗi khi cần tìm tài liệu.
- **SearchAskHN (`hackerNews`):** Node này thực hiện truy vấn tìm kiếm các bài viết / "Ask HN" liên quan đến chủ đề mà sếp vừa nhập vào form.
- **FindHNComments (`httpRequest`):** Lấy chi tiết các bình luận (comments) giá trị từ các thread Hacker News tìm được.
- **Google Gemini Chat Model & Basic LLM Chain (`lmChatGoogleGemini` & `chainLlm`):** 
  - Kết nối `Google Gemini Chat Model` bằng **Google Palm/Gemini API Key**.
  - Tại `Basic LLM Chain`, cấu hình Prompt yêu cầu AI đóng vai trò là một chuyên gia nghiên cứu, đọc các bình luận từ HN và lọc ra danh sách tài nguyên, khóa học, sách kèm đánh giá chi tiết.
- **Convert2HTML (`markdown`):** Chuyển đổi định dạng văn bản markdown trả về từ AI thành HTML đẹp mắt để hiển thị trực quan trong email.
- **SendEmailWithTopResources (`emailSend`):** Điền thông tin SMTP của sếp (Host, Port, User, Password) và cấu hình địa chỉ email nhận kết quả báo cáo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và test thử bằng cách điền form nhập một chủ đề bất kỳ (ví dụ: *"Learn System Design"*).
- Kiểm tra kết quả trả về ở các node xem dữ liệu có chạy thông suốt không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để chính thức vận hành hệ thống 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn xò hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Tích hợp Slack/Telegram:** Thay vì chỉ gửi email, hãy thêm node Slack hoặc Telegram để bắn thông báo tóm tắt tài nguyên thẳng vào nhóm chat học tập của team.
- **Lưu lịch sử vào Google Sheets:** Thêm node Google Sheets để lưu lại các chủ đề đã học và danh sách tài nguyên tương ứng, tạo thành một thư viện tri thức riêng cho bản thân hoặc doanh nghiệp.
- **Lên lịch định kỳ:** Thay vì dùng Form Trigger, có thể đổi thành Schedule Trigger để mỗi tuần AI tự động quét chủ đề "hot" nhất trên Hacker News và gửi báo cáo xu hướng công nghệ mới nhất cho sếp.

### 📌 Kết luận
Việc tự học công nghệ mới chưa bao giờ dễ dàng và thông minh đến thế khi kết hợp sức mạnh của n8n, Hacker News và Google Gemini AI. Hãy cài đặt ngay workflow này để tối ưu hóa năng lực tự học và cập nhật kiến thức công nghệ mỗi ngày cho bản thân các sếp nhé! Chúc các sếp thao tác thành công!