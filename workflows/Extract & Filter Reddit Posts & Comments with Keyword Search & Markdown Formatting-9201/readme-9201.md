---
title: "🚀 Tự Động Trích Xuất & Lọc Bài Viết Reddit Kèm Bình Luận Chuẩn Markdown"
description: "Hướng dẫn xây dựng hệ thống tự động hóa n8n giúp tìm kiếm, lọc bài viết và bình luận Reddit theo từ khóa, upvotes với định dạng Markdown chuyên nghiệp."
slug: "tu-dong-trich-xuat-loc-reddit-posts-comments-n8n"
tags: [n8n, automation, reddit, content-creation, ai-automation]
keywords: [n8n workflow, trích xuất reddit, lọc bài viết reddit, tự động hóa n8n, reddit api automation]
---

# 🚀 Tự Động Trích Xuất & Lọc Bài Viết Reddit Kèm Bình Luận Chuẩn Markdown

Các sếp có đang tốn hàng giờ mỗi ngày để lướt Reddit tìm ý tưởng nội dung, nghiên cứu thị trường hay theo dõi các xu hướng mới nhất không? Việc tìm kiếm thủ công, lọc bài viết chất lượng cao và tổng hợp bình luận thực sự ngốn rất nhiều thời gian và công sức.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do **Muhammad Asadullah** phát triển. Hệ thống này sẽ tự động hóa 100% quy trình tìm kiếm bài viết, lọc theo từ khóa, giới hạn thời gian, kiểm tra lượt upvote, bóc tách các bình luận hàng đầu và xuất ra định dạng Markdown cực kỳ gọn gàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động quét Reddit theo từ khóa hoặc subreddit chỉ trong vài giây.
- **Lọc thông minh:** Loại bỏ rác, trùng lặp và chỉ giữ lại những bài viết chất lượng cao dựa trên mốc thời gian (số ngày gần đây) và lượng upvote tối thiểu.
- **Tổng hợp chuyên sâu:** Tự động lấy top các bình luận nổi bật nhất của bài viết.
- **Định dạng sẵn sàng sử dụng:** Kết quả trả về dưới dạng Markdown hoàn chỉnh, sẵn sàng đưa vào LLM, Notion, Google Docs hoặc hệ thống báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản Reddit Developer / API Credentials (Client ID & Client Secret) để kết nối với các node Reddit.
- Webhook client (như Postman, cURL hoặc một ứng dụng frontend) để gửi request kích hoạt workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp (hoặc copy mã JSON) và sử dụng tính năng **Import from File / Clipboard** trực tiếp trong giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công 24 nodes, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:
- **Webhook Nodes (`reddit tool webhook`, `reddit tool webhook subreddit`):** Nơi nhận các tham số đầu vào (từ khóa tìm kiếm, tên subreddit, số lượng cần lấy). Hãy cấu hình phương thức HTTP (POST/GET) phù hợp với hệ thống gọi của các sếp.
- **Reddit Nodes (`Search for posts by keywords`, `Get posts from subreddit`, `Get Comments`):** Cần thiết lập tài khoản Reddit Credential (OAuth2 API) của các sếp để n8n có quyền gọi API lấy dữ liệu bài viết và bình luận.
- **Code Nodes (`Posted in Last x days`, `Remove Duplicates`, `Format Comments`, `Extract Top 20 Comments`, `Combine Posts`):** Các đoạn mã JavaScript xử lý logic lọc thời gian, loại bỏ bài viết trùng lặp (`Remove Duplicates`), định dạng lại nội dung bình luận sang chuẩn Markdown (`Format Comments`) và gom nhóm dữ liệu. Không cần sửa code trừ khi các sếp muốn custom lại số lượng comment (mặc định lấy top 20).
- **If Node (`Upvotes Requirement Filtering`):** Tùy chỉnh điều kiện lọc số lượng Upvotes tối thiểu (`upvotes >= x`) cho phù hợp với tiêu chuẩn chất lượng của doanh nghiệp.
- **Respond to Webhook Node (`Respond to Webhook`):** Đảm bảo node này trả về kết quả cuối cùng (`Set Final Report`) theo định dạng JSON hoặc Markdown để hệ thống gọi tiếp nhận được dữ liệu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request mẫu qua Webhook để kiểm tra luồng chạy (Test run).
- Sau khi kiểm tra dữ liệu trả về chính xác và đúng định dạng Markdown, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI/LLM:** Nối thêm các node OpenAI hoặc Anthropic Claude vào sau node tổng hợp để tự động tóm tắt nội dung bài viết và phân tích cảm xúc (Sentiment Analysis) của cộng đồng Reddit.
- **Tự động lưu trữ:** Kết hợp thêm node Notion, Google Sheets hoặc Airtable để lưu lại toàn bộ báo cáo nghiên cứu thị trường một cách có hệ thống.
- **Gửi thông báo:** Thêm node Telegram hoặc Slack để bắn tin nhắn cảnh báo ngay lập tức khi có bài viết hot xuất hiện trên subreddit mục tiêu.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các nhà sáng tạo nội dung, Marketer và Data Scientist muốn khai thác nguồn dữ liệu khổng lồ từ Reddit một cách tự động và chuyên nghiệp. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa hiệu suất công việc ngày hôm nay!