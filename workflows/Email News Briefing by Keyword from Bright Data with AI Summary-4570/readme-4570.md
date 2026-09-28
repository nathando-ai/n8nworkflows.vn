---
title: "🚀 Tự động tổng hợp bản tin theo từ khóa với Bright Data và Google Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu tin tức qua Bright Data dựa trên từ khóa, sử dụng Google Gemini AI để tóm tắt và gửi báo cáo qua email chuyên nghiệp."
slug: "tu-dong-tong-hop-ban-tin-theo-tu-khoa-bright-data-google-gemini"
tags: [n8n, automation, ai, marketing, bright-data, google-gemini, web-scraping]
keywords: [n8n workflow, tóm tắt tin tức tự động, bright data api, google gemini ai, gửi email báo cáo n8n, web scraping tự động]
---

# 🚀 Tự động tổng hợp bản tin theo từ khóa với Bright Data và Google Gemini AI

Các sếp có bao giờ cảm thấy ngợp trước hàng ngàn bài báo, tin tức xuất hiện mỗi ngày liên quan đến ngành nghề, đối thủ hay sản phẩm của mình? Việc phải ngồi tìm kiếm, đọc lướt và tổng hợp thủ công ngốn rất nhiều thời gian, khiến các sếp bỏ lỡ những thông tin quan trọng nhất. 

Đừng lo nữa! Workflow n8n siêu việt này sẽ giải quyết triệt để vấn đề đó. Chỉ với một từ khóa đầu vào do các sếp chỉ định, hệ thống sẽ tự động cào dữ liệu tin tức thông qua **Bright Data**, sử dụng sức mạnh trí tuệ nhân tạo **Google Gemini** để phân tích, tóm tắt và tự động gửi một bản tin (News Briefing) cực kỳ chỉn chu, sắc sảo thẳng vào hộp thư email của các sếp. Hoàn toàn tự động 100% và không tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tự tay tra cứu từng trang tin tức hay đọc hàng tá bài viết dài dòng.
- **Cập nhật thông tin trọng tâm:** Google Gemini AI giúp lọc bỏ thông tin rác và cô đọng những ý chính đắt giá nhất.
- **Chủ động theo nhu cầu:** Nhập từ khóa bất kỳ qua Form giao diện là hệ thống tự động chạy ngay lập tức.
- **Trình bày chuyên nghiệp:** Báo cáo được đóng gói thành định dạng HTML sạch sẽ, gửi thẳng qua Email cá nhân hoặc doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã thiết lập sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Bright Data:** Cần có API Key và cấu hình Web Scraper/Dataset phù hợp để cào dữ liệu tin tức.
- **Google Gemini API Key:** Để kết nối với mô hình ngôn ngữ lớn (LLM) phục vụ việc phân tích và tóm tắt.
- **Tài khoản Email/SMTP:** Cấu hình trong node `Email Report` để gửi thư đi (Gmail SMTP, SendGrid, Resend...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow từ nguồn (`https://n8n.io/workflows/4570`) và dán trực tiếp vào n8n Editor của mình, hoặc tải file JSON về và chọn **Import from File**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **When User Completes Form:** Đây là điểm khởi đầu. Các sếp có thể tùy chỉnh giao diện form để người dùng (hoặc chính các sếp) nhập vào từ khóa muốn quét tin tức.
- **HTTP Request - Post API call to Bright Data:** Điền API Key và endpoint của Bright Data để kích hoạt tiến trình cào dữ liệu (Snapshot). 
*Lưu ý từ tác giả:* Nên giữ bộ lọc sắp xếp là *"relevance"* (độ liên quan), vì các bước sau sẽ tự động phân loại theo ngày tháng mới nhất.
- **Wait - Polling Bright Data & Snapshot Progress & If - Checking status...:** Bộ ba node này làm nhiệm vụ "chờ đợi thông minh". Nó sẽ kiểm tra xem Bright Data đã cào xong dữ liệu chưa trước khi cho phép workflow chạy tiếp.
- **HTTP Request - Getting data from Bright Data:** Kéo toàn bộ dữ liệu tin tức thô về sau khi Bright Data đã hoàn tất snapshot.
- **Google Gemini Chat Model & Google Gemini - Summary Analisys:** Kết nối tài khoản Google Gemini bằng API Key, cấu hình Prompt để AI tiến hành đọc hiểu, chắt lọc và tóm tắt các bài viết theo từ khóa.
- **Code - Build HTML & Email Report:** Node Code sẽ biến dữ liệu tóm tắt thành một bản tin HTML đẹp mắt. Sau đó, node `Email Report` sẽ gửi nó đến địa chỉ email nhận định sẵn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và điền thử một từ khóa vào Form để test xem dữ liệu có chạy qua tất cả các bước hay không.
- Nếu email gửi về thành công và nội dung tóm tắt chính xác, hãy gạt công tắc sang **Active** để chính thức đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Thay vì chỉ gửi qua Email, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để nhận bản tin tóm tắt ngay trên điện thoại cho nhanh gọn.
- **Lưu trữ lịch sử:** Thêm node **Google Sheets** hoặc **Airtable** vào trước bước gửi email để lưu lại toàn bộ lịch sử các bản tin đã tạo phục vụ cho việc tra cứu sau này.
- **Chạy tự động định kỳ:** Thay thế node `When User Completes Form` bằng node **Schedule Trigger** (Ví dụ: Chạy lúc 7:00 sáng mỗi ngày) để tự động hóa hoàn toàn mà không cần nhập tay từ khóa.

### 📌 Kết luận
Workflow "Email News Briefing by Keyword from Bright Data with AI Summary" là một vũ khí cực kỳ lợi hại cho các nhà làm marketing, nghiên cứu thị trường hoặc bất kỳ ai muốn nắm bắt tin tức nóng hổi một cách thông minh. Hãy thiết lập ngay hôm nay để AI làm thay những công việc tẻ nhạt cho các sếp!