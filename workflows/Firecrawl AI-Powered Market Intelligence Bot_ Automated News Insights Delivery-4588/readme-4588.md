---
title: "🚀 Xây dựng Bot tự động tổng hợp tin tức thị trường bằng FireCrawl và OpenAI trên n8n"
description: "Hướng dẫn chi tiết cách tự động crawl tin tức công nghệ, lọc từ khóa thông minh, tóm tắt bằng AI và gửi báo cáo về Slack mỗi ngày."
slug: "bot-tong-hop-tin-tuc-thi-truong-firecrawl-openai-n8n"
tags: [n8n, automation, firecrawl, openai, ai-agent, slack, market-intelligence]
keywords: [n8n workflow, firecrawl api, openai tóm tắt tin tức, bot thị trường slack, tự động hóa marketing]
---

# 🚀 Tự động hóa nghiên cứu thị trường và tổng hợp tin tức với AI & FireCrawl

Các sếp có bao giờ cảm thấy mất quá nhiều thời gian mỗi ngày chỉ để lướt các trang báo công nghệ như TechCrunch, tìm kiếm các bài viết liên quan đến lĩnh vực của mình, đọc và tóm tắt lại cho team? Việc làm thủ công này vừa tẻ nhạt, vừa dễ bỏ lỡ các thông tin đắt giá.

Đừng lo! Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: **Crawl dữ liệu web -> Lọc thông tin thông minh -> Tóm tắt bằng AI (OpenAI) -> Báo cáo trực tiếp lên Slack** định kỳ mỗi ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tự đọc và tóm tắt thủ công hàng chục bài báo mỗi ngày.
- **Chính xác & Đúng trọng tâm:** Chỉ lọc những bài viết chứa từ khóa quan trọng (AI, Startup, Machine Learning...) theo nhu cầu doanh nghiệp.
- **Cập nhật liên tục:** Tin tức được tổng hợp thành 3 gạch đầu dòng ngắn gọn, súc tích, sẵn sàng đọc nhanh trên Slack mỗi sáng.
- **Vận hành tự động 24/7:** Chạy ngầm đều đặn theo lịch trình đã cài đặt sẵn mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance:** (Cloud hoặc Self-hosted).
- **FireCrawl API Key:** Dùng để cào dữ liệu bài viết từ trang web mục tiêu.
- **OpenAI API Key:** Cung cấp mô hình LLM (`gpt-4o-mini`) để xử lý và tóm tắt nội dung.
- **Slack Workspace:** Kênh Slack để bot bắn tin nhắn báo cáo (cần Slack Bot Token / Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor (hoặc import file JSON thông qua giao diện n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, hãy chú ý cấu hình các node cốt lõi sau:

- **🕒 Daily Market Research Trigger (Schedule Trigger):** Cài đặt mốc thời gian chạy (Cron expression), ví dụ chạy lúc 8:00 sáng mỗi ngày.
- **🌐 Crawl TechCrunch (FireCrawl) (HTTP Request):** 
  - Thêm Credential xác thực API của FireCrawl.
  - Kiểm tra URL nguồn mục tiêu trong body request (mặc định là `https://techcrunch.com`), cấu hình `crawl_type: "scrape"` và `extract_article: true`.
- **🧠 Filter Relevant Articles (Code Node):** 
  - Tùy chỉnh danh sách mảng từ khóa (`keywords`) trong đoạn code Javascript cho phù hợp với lĩnh vực kinh doanh của các sếp (ví dụ: `['AI', 'SaaS', 'automation', 'startup']`).
- **🔗 OpenAI Chat & 🧠 Summarizer Agent (AI Agent):** 
  - Chọn Credential OpenAI đã tạo.
  - Đảm bảo model được chọn là `gpt-4o-mini` (hoặc model tương đương).
  - Tinh chỉnh Prompt của Agent để yêu cầu format kết quả tóm tắt theo đúng ý muốn (ví dụ: *"Summarize the following article in 3 bullet points..."*).
- **💬 Send Summary to Slack (Slack Node):** 
  - Kết nối tài khoản Slack và chọn đúng kênh nhận thông tin (ví dụ: `#market-research`).
  - Map biến kết quả từ AI Agent vào nội dung tin nhắn gửi đi.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm với dữ liệu mẫu xem bot chạy có mượt không.
- Sau khi kiểm tra mọi thứ hoàn hảo, bật nút **Active** ở góc trên cùng bên phải để workflow chính thức chạy tự động.

### ✍️ Nâng cấp & Gợi ý mở rộng
Để workflow trở nên "bá đạo" hơn, các sếp có thể cân nhắc mở rộng:
- **Đa dạng nguồn tin:** Thêm nhiều node FireCrawl để cào đồng thời nhiều trang báo khác nhau (TechCrunch, Product Hunt, VnExpress...).
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Notion** để lưu lại lịch sử các bài báo đã tóm tắt làm thư viện nghiên cứu lâu dài.
- **Đa kênh thông báo:** Ngoài Slack, tích hợp thêm node **Telegram** hoặc **Email** để gửi bản tin cho sếp lớn hoặc team qua nhiều kênh khác nhau.

### 📌 Kết luận
Việc ứng dụng AI và các công cụ No-Code như n8n kết hợp FireCrawl không chỉ giúp tối ưu hóa thời gian nghiên cứu thị trường mà còn mang lại nguồn thông tin chiến lược cực kỳ nhanh chóng cho doanh nghiệp. Hãy thiết lập ngay hôm nay để tối ưu hóa năng suất cho team của các sếp nhé!