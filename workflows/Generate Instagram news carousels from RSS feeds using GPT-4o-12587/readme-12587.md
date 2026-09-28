---
title: "🚀 Tự động tạo chuỗi ảnh tin tức (Instagram News Carousels) từ RSS với GPT-4o"
description: "Hướng dẫn xây dựng đại lý tin tức tự động hoàn toàn bằng n8n: quét tin tức RSS, dùng GPT-4o viết kịch bản viral, thiết kế slide ảnh và tự động đăng lên Instagram."
slug: "tu-dong-tao-instagram-news-carousels-tu-rss-voi-gpt-4o"
tags: [n8n, automation, no-code, instagram, openai, rss]
keywords: [n8n workflow, tu dong hoa instagram, gpt-4o rss carousel, tao post instagram tu dong, automation marketing]
keywords: [n8n workflow, tự động hóa, instagram automation, gpt-4o, rss feed, content marketing]
---

# 🚀 Tự động tạo chuỗi ảnh tin tức (Instagram News Carousels) từ RSS với GPT-4o

Các sếp có đang mệt mỏi vì phải liên tục cập nhật tin tức nóng hổi, viết kịch bản, thiết kế từng slide ảnh carousel và đăng bài lên Instagram mỗi ngày không? Công việc thủ công này ngốn rất nhiều thời gian mà đôi khi độ tương tác lại không cao.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n đóng vai trò như một **"Hãng Thông Tấn Tự Động"**. Workflow này sẽ thay các sếp làm tất cả từ A-Z: quét tin tức từ RSS, dùng AI phân tích và viết kịch bản viral, thiết kế hình ảnh tự động và xuất bản trực tiếp lên Instagram Business. Tất cả diễn ra tự động 100% không cần tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh cặm cụi copy-paste tin tức hay thiết kế từng slide trên Canva.
- **Bắt trend cực nhanh:** Tự động quét nguồn RSS liên tục để đón đầu các tin tức nóng hổi trong ngành.
- **Kịch bản chuẩn SEO/Viral:** GPT-4o lo phần giật tít, tạo hook thu hút người xem vuốt hết các slide ảnh.
- **Vận hành 24/7:** Lên lịch chạy định kỳ hoặc kích hoạt qua Form tùy ý, bài viết tự động lên sóng Instagram mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản self-hosted để xử lý các tác vụ nặng).
- **Tài khoản OpenAI:** Lấy API Key có tích hợp GPT-4o để viết kịch bản nội dung.
- **Tài khoản Google Drive:** Dùng để lưu trữ tạm thời các hình ảnh slide được tạo ra trước khi đẩy lên Instagram.
- **Facebook / Instagram Business Account:** Đã kết nối Fanpage với tài khoản Instagram Creator/Business và lấy **Instagram Business Account ID** cùng Access Token.
- **Image Engine (Tùy chọn):** Gotenberg (Miễn phí qua Docker) hoặc APITemplate (Có phí) để render hình ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste toàn bộ mã nguồn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **SETUP FORM (`formTrigger`):** Điểm xuất phát của quy trình, nơi các sếp có thể thiết lập form để nhập chủ đề hoặc tùy chỉnh nguồn tin muốn quét.
- **News Source (`rssFeedRead`):** Nơi cấu hình đường dẫn RSS (ví dụ: TechCrunch, VNExpress, các trang tin chuyên ngành...) để lấy danh sách bài viết mới.
- **AI Analyst (`openAi`):** Kết nối với `openAiApi` credentials, cài đặt prompt cho GPT-4o để phân tích nội dung, trích xuất tiêu đề giật gân và chia nhỏ thành 10 slide kịch bản.
- **Upload file & Share file (`googleDrive`):** Kết nối tài khoản Google Drive để lưu hình ảnh được render ra và chia sẻ quyền truy cập công khai giúp Instagram có thể đọc được file ảnh.
- **Create Container, Carousel Bundle, Publish Carousel (`facebookGraphApi`):** 
  - Kết nối `facebookGraphApi` credentials.
  - **CỰC KỲ QUAN TRỌNG:** Mở 3 node này lên và thay thế ID mặc định bằng **Instagram Business Account ID** của các sếp.
- **Route by Engine (`switch`) & Generate Image (`httpRequest`):** Chọn công cụ render ảnh phù hợp (Gotenberg miễn phí chạy qua Docker hoặc APITemplate). Nếu dùng bản trả phí, nhớ điền API Key vào node tạo ảnh.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với dữ liệu mẫu (Test run) để kiểm tra từng bước từ đọc RSS -> AI viết kịch bản -> Render ảnh -> Đăng bài.
- Sau khi kiểm tra mọi thứ chạy xanh mướt, hãy bật **Active** để workflow tự động hoạt động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối chuỗi để nhận thông báo ngay khi bài viết đã được publish thành công lên Instagram kèm link xem trực tiếp.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets để lưu lại danh sách tin tức đã quét và nội dung kịch bản AI đã viết nhằm phục vụ việc kiểm tra nội dung sau này.
- **Đa kênh mạng xã hội:** Từ chuỗi ảnh Carousel Instagram, các sếp có thể mở rộng nhánh để tự động đăng chéo sang LinkedIn hoặc Facebook Page.

### 📌 Kết luận
Workflow "Generate Instagram news carousels from RSS feeds using GPT-4o" là một cỗ máy tự động hóa hoàn hảo giúp biến website tin tức của các sếp hoặc các nguồn RSS yêu thích thành một kênh Instagram chuyên nghiệp, thu hút hàng ngàn lượt tương tác. Hãy thiết lập ngay hôm nay để tối ưu hóa chiến lược nội dung của mình các sếp nhé!