---
title: "🚀 Tự động hóa phân tích vé máy bay và thời tiết với AI, Google Flights & WordPress"
description: "Xây dựng hệ thống tự động tìm kiếm deal vé máy bay, phân tích thời tiết, đánh giá bằng OpenAI và tự động đăng bài lên WordPress, gửi thông báo Slack chỉ trong 1 nốt nhạc."
slug: "flight-deal-analyzer-weather-openai-wordpress"
tags: [n8n, automation, no-code, openai, wordpress, travel-tech]
keywords: [n8n workflow, tự động hóa vé máy bay, google flights scraper, openai gpt n8n, wordpress automation]
---

# 🚀 Tự động hóa phân tích vé máy bay và thời tiết với AI, Google Flights & WordPress

Các sếp làm trong lĩnh vực travel blog, săn deal du lịch hay dịch vụ lữ hành có ngán ngẩm cảnh phải ngồi mò mẫm từng chặng bay, so sánh giá, tra cứu thời tiết điểm đến rồi tự tay viết bài lên website không? Công việc thủ công này ngốn rất nhiều thời gian và dễ bỏ lỡ các khung giờ vàng giảm giá.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code. Hệ thống sẽ tiếp nhận yêu cầu từ người dùng, tự động cào dữ liệu giá vé từ Google Flights, kết hợp thông tin thời tiết thời gian thực, nhờ AI phân tích độ hời của deal, tự động xuất bản bài viết lên WordPress và bắn thông báo về Slack cực kỳ chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Thay vì mất hàng giờ research giá vé và thời tiết, hệ thống xử lý trọn gói chỉ trong vài giây.
- **Tích hợp đa nguồn thông minh:** Kết hợp hoàn hảo giữa giá vé thời gian thực, dữ liệu thời tiết và khả năng phân tích ngữ cảnh của OpenAI.
- **Tự động hóa xuất bản:** Tự động lên bài viết chuẩn SEO/Review trên WordPress và thông báo tức thì qua Slack cho đội ngũ.
- **Cá nhân hóa trải nghiệm:** Người dùng nhập yêu cầu qua Form và nhận lại kết quả trực quan ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để vận hành node AI Flight Analyzer.
- **Weather API Key:** Tài khoản từ các dịch vụ cung cấp thời tiết (như OpenWeatherMap) để lấy dữ liệu thời tiết điểm đến.
- **WordPress Site:** Trang web WordPress có bật REST API hoặc Application Password.
- **Slack Workspace:** Kênh Slack để nhận thông báo deal mới.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn mã JSON tương ứng, sau đó vào giao diện n8n Editor chọn **Add workflow** -> **Import from File / Clipboard** để dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **User Input Form (`formTrigger`)**: Thiết lập đường dẫn (`path`) phù hợp (mặc định là `japan-flight-analyzer`) để thu thập thông tin điểm đi, điểm đến và sở thích từ người dùng.
- **Scrape Flight Prices (`httpRequest`) & Extract Flight Data (`html`)**: Cấu hình endpoint cào giá từ Google Flights hoặc dịch vụ trung gian tương ứng để lấy dữ liệu HTML chuẩn xác.
- **Fetch Weather Data (`httpRequest`)**: Cấu hình API kết nối tới dịch vụ thời tiết với tham số điểm đến lấy từ form người dùng.
- **OpenAI Chat Model (`lmChatOpenAi`)**: Kết nối tài khoản OpenAI Credentials và chọn model phù hợp (ví dụ: `gpt-4o` hoặc các model chat mới nhất).
- **AI Flight Analyzer (`agent`) & Structured Output Parser (`outputParserStructured`)**: Định nghĩa prompt và cấu trúc dữ liệu đầu ra để AI đánh giá chất lượng deal vé dựa trên cả giá cả lẫn điều kiện thời tiết.
- **Publish to WordPress (`wordpress`)**: Điền thông tin kết nối website WordPress (URL, Username, Application Password) để tự động tạo bài viết nháp hoặc đăng trực tiếp.
- **Send to Slack (`slack`)**: Chọn channel Slack và kết nối Bot Token để bắn thông báo khi có deal ngon.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một request mẫu qua Form để kiểm tra toàn bộ luồng chạy (Test run).
- Nếu dữ liệu trả về chuẩn chỉnh, hãy bật nút **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Email để gửi thẳng deal vé máy bay cho khách hàng đăng ký nhận bản tin (Newsletter).
- **Lưu trữ dữ liệu:** Thêm node Google Sheets để lưu lại lịch sử các deal đã phân tích nhằm phục vụ việc thống kê, nghiên cứu xu hướng giá vé theo mùa.
- **Tự động hóa Social Media:** Nối tiếp workflow bằng việc tự động lấy nội dung bài viết WordPress vừa tạo để đăng lên Facebook Fanpage hoặc Twitter qua các n8n integration có sẵn.

### 📌 Kết luận
Workflow **Flight Deal Analyzer with Weather Data using GPT, Google Flights & WordPress** là một trợ thủ đắc lực giúp tối ưu hóa quy trình làm nội dung du lịch và săn deal. Hãy triển khai ngay hôm nay để tự động hóa công việc kinh doanh và mang lại trải nghiệm tốt nhất cho khách hàng của các sếp!