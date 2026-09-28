---
title: "🚀 Tự động tìm kiếm khách hàng tiềm năng trên Reddit và tạo phản hồi cá nhân hóa bằng Llama3 AI"
description: "Hướng dẫn xây dựng workflow n8n tự động quét bài đăng Reddit, phân tích mức độ liên quan bằng Llama3 AI, ghi log Google Sheets và tự động phản hồi khách hàng."
slug: "tu-dong-tim-khach-hang-reddit-voi-llama3-ai-va-google-sheets"
tags: [n8n, automation, reddit, ai, llama3, google-sheets, marketing]
keywords: [n8n workflow, tự động hóa reddit, tìm kiếm khách hàng reddit, llama3 ai, google sheets automation]
---

# 🚀 Tự động tìm kiếm khách hàng tiềm năng trên Reddit và tạo phản hồi cá nhân hóa bằng Llama3 AI

Các sếp có đang tốn hàng giờ mỗi ngày để lướt Reddit tìm kiếm khách hàng tiềm năng, đọc từng bài đăng và suy nghĩ cách bình luận sao cho tự nhiên nhất để không bị coi là spam? Công việc thủ công này cực kỳ tốn thời gian và dễ bỏ lỡ cơ hội vàng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh, tự động hóa toàn bộ quy trình: quét bài đăng trên Reddit, sử dụng **Llama3 AI** để phân tích xem bài viết đó có phù hợp với sản phẩm/dịch vụ hay không, lưu trữ dữ liệu vào **Google Sheets** và tự động tạo ra những câu trả lời cực kỳ cá nhân hóa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần phải cày cuốc lướt Reddit thủ công nữa, AI sẽ làm thay việc quét và lọc bài viết.
- **Phân tích thông minh:** Llama3 AI giúp đánh giá chính xác bài đăng nào thực sự có tiềm năng kinh doanh thay vì những bài rác hoặc không liên quan.
- **Cá nhân hóa đỉnh cao:** Tạo nội dung phản hồi tự nhiên, khéo léo lồng ghép giải pháp của các sếp vào đúng "nỗi đau" của khách hàng.
- **Quản lý tập trung:** Mọi bài đăng và kết quả phân tích đều được tự động đồng bộ và ghi log rõ ràng trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
- **Tài khoản Reddit API:** Đã tạo ứng dụng (Reddit App) để lấy Client ID và Client Secret.
- **Google Sheets:** Chuẩn bị sẵn một Google Sheet để lưu trữ log bài đăng (cả bài phù hợp và bài không phù hợp).
- **Ollama:** Cài đặt Ollama đang chạy mô hình **Llama3** (hoặc kết nối qua API tương đương) để AI xử lý ngữ nghĩa.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc (`https://n8n.io/workflows/4068`) hoặc tạo mới trên n8n Editor và thêm các node tương ứng vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Get Reddit Posts (Node `reddit`):** Kết nối tài khoản Reddit của các sếp, cấu hình Subreddit mục tiêu và từ khóa cần quét bài viết.
- **Filter New Posts & Parse AI Response (Node `code`):** Kiểm tra logic lọc bài viết mới để tránh xử lý trùng lặp các bài đã quét trước đó.
- **AI Relevance Analysis & Ollama Chat Model (Node `agent` & `lmChatOllama`):** Kết nối tới mô hình Llama3 qua Ollama. Viết System Prompt rõ ràng để AI biết cách đánh giá mức độ liên quan và viết nội dung phản hồi phù hợp.
- **Get Existing Posts1, Log Irrelevant Post, Log Relevant Post (Node `googleSheets`):** Kết nối tài khoản Google Drive/Sheets, chọn đúng file Google Sheet và mapping các trường dữ liệu như Tiêu đề bài viết, Link, Nội dung phân tích của AI, Trạng thái phù hợp/không phù hợp.
- **Post Reddit Comment (Node `reddit`):** Cấu hình quyền đăng bài/bình luận tự động lên Reddit (Lưu ý: Cần cân nhắc kỹ việc tự động đăng comment để tránh bị Reddit ban tài khoản do spam, có thể đổi thành tạo bản nháp trong Google Sheets để duyệt thủ công).

#### 3. Kích hoạt ⚡️
- Nhấn nút **When clicking ‘Test workflow’** để chạy thử nghiệm với một vài bài đăng mẫu.
- Kiểm tra kết quả trên Google Sheets và các node AI xem phản hồi đã chuẩn chỉnh chưa.
- Sau khi test ngon lành, gạt công tắc **Active** để workflow chạy tự động theo lịch trình (Cron node nếu có thêm vào hệ thống).

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước duyệt thủ công (Human-in-the-loop):** Thay vì để node Reddit tự động đăng comment ngay lập tức, các sếp có thể cho dừng lại ở Google Sheets, sau đó gửi thông báo qua Telegram/Slack để sếp bấm nút duyệt trước khi đăng.
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack để nhận thông báo ngay lập tức mỗi khi có một khách hàng tiềm năng "cực chất" xuất hiện trên Reddit.
- **Lưu lịch sử chạy:** Thiết lập thêm Google Sheets để lưu trữ toàn bộ các câu trả lời mà Llama3 đã tạo ra để dễ dàng tối ưu prompt theo thời gian.

### 📌 Kết luận
Việc tự động hóa tìm kiếm khách hàng trên Reddit bằng Llama3 AI và n8n không chỉ giúp tiết kiệm hàng đống thời gian mà còn giúp các sếp tiếp cận đúng đối tượng khách hàng mục tiêu với thông điệp cá nhân hóa nhất. Hãy triển khai ngay hôm nay để tối ưu hóa phễu marketing không đồng của doanh nghiệp nhé!