---
title: "🚀 Hệ thống dự báo giá vàng tự động với Perplexity Sonar-Pro, FRED & WordPress"
description: "Tự động hóa hoàn toàn quy trình phân tích và dự báo thị trường vàng 6 tiếng/lần sử dụng AI Perplexity Sonar-Pro, dữ liệu kinh tế vĩ mô FRED, xuất bản bài viết lên WordPress và gửi cảnh báo qua Slack/Email."
slug: "he-thong-du-bao-gia-vang-tu-dong-n8n"
tags: [n8n, automation, ai-agent, wordpress, financial-analysis, openrouter]
keywords: [n8n workflow, dự báo giá vàng, tự động hóa tài chính, Perplexity Sonar-Pro, OpenRouter, WordPress automation]
keywords: [n8n workflow, du bao gia vang, tu dong hoa tai chinh, Perplexity Sonar-Pro, OpenRouter, WordPress automation]
---

# 🚀 Hệ thống dự báo giá vàng tự động với Perplexity Sonar-Pro, FRED & WordPress

Các nhà đầu tư, phân tích tài chính hay các trang tin tức thường tốn rất nhiều thời gian để tổng hợp dữ liệu giá vàng trực tiếp, cập nhật tin tức tài chính, các chỉ số kinh tế vĩ mô (lạm phát, lãi suất, việc làm từ FRED) rồi viết bài phân tích. Việc làm thủ công này không chỉ chậm trễ mà còn dễ bỏ lỡ các biến động thị trường quan trọng diễn ra từng giờ.

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: Thu thập dữ liệu đa nguồn -> Phân tích xu hướng bằng AI đỉnh cao (Perplexity Sonar-Pro qua OpenRouter) -> Xuất bản bài viết lên WordPress -> Gửi thông báo tức thì qua Slack và Email.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng giờ tổng hợp số liệu vĩ mô và viết báo cáo, hệ thống tự động hoàn thành chỉ trong vài phút.
- **Phân tích chuyên sâu với AI:** Sử dụng mô hình Perplexity Sonar-Pro có khả năng truy xuất web thực tế, kết hợp dữ liệu FRED giúp dự báo giá vàng cực kỳ chuẩn xác.
- **Đa kênh phân phối:** Tự động đăng bài báo cáo lên website WordPress, đồng thời gửi bản tóm tắt nhanh qua Slack và Email cho đội ngũ quản trị.
- **Hoạt động 24/7:** Chạy ngầm định kỳ mỗi 6 tiếng, đảm bảo các sếp không bao giờ bỏ lỡ bất kỳ biến động nào của thị trường vàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n instance** (v1.0 trở lên).
- **OpenRouter API Key** (để sử dụng mô hình `perplexity/sonar-pro`).
- **API Keys cho dữ liệu thị trường:** MetalPrice API, NewsAPI, và FRED (Federal Reserve Economic Data).
- **Tài khoản WordPress** (đã cấp quyền REST API hoặc Application Passwords).
- **Tài khoản Slack** (Webhook hoặc Bot Token để gửi thông báo).
- **SMTP / Email Credential** (để gửi email báo cáo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:
- **Every 6 Hours (`scheduleTrigger`):** Mặc định chạy 6 tiếng/lần. Các sếp có thể chỉnh lại tần suất nếu muốn.
- **Get Current Gold Price, Fetch Financial News, Get Inflation/Interest/Employment Data (`httpRequest`):** Điền các API Endpoint tương ứng và cấu hình Header/API Key của MetalPrice, NewsAPI, FRED.
- **OpenRouter Chat Model (`lmChatOpenRouter`):** Chọn credentials OpenRouter và đảm bảo model được cấu hình chính xác là `perplexity/sonar-pro`.
- **AI Agent - Gold Market Analysis (`agent`):** Node cốt lõi xử lý dữ liệu. Các sếp có thể tinh chỉnh Prompt trong này để AI viết báo cáo theo văn phong mong muốn (Tiếng Việt hoặc Tiếng Anh).
- **Publish to WordPress (`wordpress`):** Kết nối tài khoản WordPress của các sếp để tự động tạo Post mới dưới dạng Draft hoặc Publish.
- **Send Slack Summary (`slack`) & Send Email Summary (`emailSend`):** Điền kênh Slack nhận tin và địa chỉ Email nhận báo cáo tổng hợp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử một lần xem dữ liệu chảy qua các node có mượt mà hay không.
- Nếu mọi thứ xanh ngắt (thành công), hãy bật công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng tài sản theo dõi:** Các sếp có thể nhân bản các node `httpRequest` để theo dõi thêm Giá bạc (Silver), Dầu mỏ (Oil) hoặc Bitcoin kết hợp vào mô hình AI.
- **Đa dạng hóa kênh thông báo:** Thay vì chỉ Slack và Email, các sếp có thể gắn thêm node Telegram Bot để bắn tin nhắn thẳng vào nhóm chat Telegram của team đầu tư.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Notion ở cuối workflow để lưu lịch sử các bản dự báo giá vàng phục vụ việc backtest sau này.

### 📌 Kết luận
Hệ thống dự báo giá vàng tự động này là một trợ thủ đắc lực giúp các nhà đầu tư và nhà sáng tạo nội dung tài chính tiết kiệm thời gian tối đa, đồng thời cung cấp các góc nhìn phân tích sắc bén dựa trên dữ liệu vĩ mô thực tế. Hãy triển khai ngay trên VPS của các sếp để tối ưu hóa quy trình đầu tư và làm nội dung ngay hôm nay!