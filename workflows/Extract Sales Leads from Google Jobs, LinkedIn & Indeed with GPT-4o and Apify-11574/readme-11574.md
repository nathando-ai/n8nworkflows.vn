---
title: "🚀 Tự động quét Lead từ Google Jobs, LinkedIn & Indeed bằng AI và Apify"
description: "Xây dựng hệ thống tự động tìm kiếm khách hàng tiềm năng từ dữ liệu tuyển dụng trên Google Jobs, LinkedIn, Indeed, phân tích qua GPT-4o và gửi cảnh báo qua Slack, Email."
slug: "tu-dong-quet-lead-tu-google-jobs-linkedin-indeed-gpt-4o-apify"
tags: [n8n, automation, lead-generation, apify, openai, gpt-4o, google-sheets]
keywords: [n8n workflow, apify scraping, ai sales leads, gpt-4o lead generation, tu dong tim kiem khach hang, linkedin jobs scraper]
---

# 🚀 Tự động quét Lead từ Google Jobs, LinkedIn & Indeed bằng AI và Apify

Việc thủ công lướt qua hàng trăm tin tuyển dụng trên LinkedIn, Indeed hay Google Jobs mỗi ngày để tìm kiếm cơ hội bán hàng (Sales Leads) thực sự là một cơn ác mộng tốn kém thời gian. Các sếp có thấy mệt mỏi khi đội ngũ Sales cứ phải cào dữ liệu bằng tay, lọc trùng lặp rồi loay hoay viết email chào hàng (cold email) cho từng khách hàng không?

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code) giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động quét tin tuyển dụng từ 3 nền tảng lớn, làm sạch dữ liệu, lọc từ khóa, sử dụng **GPT-4o** để phân tích độ phù hợp, soạn thảo nội dung email cá nhân hóa và gửi cảnh báo ngay lập tức về Slack hoặc Gmail cho đội ngũ Sales!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7**: Quét tin tuyển dụng hàng ngày lúc 9:00 sáng mà không cần con người can thiệp.
- **Tiếp cận đúng khách hàng tiềm năng**: Lọc thông minh dựa trên từ khóa mục tiêu và danh sách công ty cần nhắm tới.
- **AI thông minh hóa bán hàng**: GPT-4o tự động tìm ra điểm đau (pain points), chấm điểm độ khẩn cấp (urgency score) và viết sẵn nội dung email tiếp cận cực kỳ chuyên nghiệp.
- **Báo cáo định kỳ**: Tổng hợp số liệu và phân tích xu hướng tuyển dụng hàng tuần gửi qua Slack & Gmail vào thứ Hai hàng tuần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Apify**: Dùng để chạy các Actor cào dữ liệu việc làm (Google Jobs, LinkedIn, Indeed).
- **OpenAI API Key**: Sử dụng mô hình `gpt-4o` cho việc phân tích Lead và viết Email.
- **Google Sheets**: Lưu trữ danh sách công ty mục tiêu, dữ liệu thô, danh sách lead chất lượng và báo cáo tuần.
- **Slack Workspace**: Nhận cảnh báo lead nóng và báo cáo tuần.
- **Gmail Account**: Gửi báo cáo tổng hợp qua email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này (hoặc tải file từ n8n.io) và import trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình các node cốt lõi sau:
- **Node `Set Configuration`**: Thiết lập các biến quan trọng như `daysToCheck` (số ngày cần quét lại), `maxJobsPerSource` (giới hạn số lượng job mỗi nguồn), và `targetIndustry` (ngành nghề mục tiêu).
- **Node `Apify - Scrape ... Jobs`**: Kết nối tài khoản Apify của các sếp và điền đúng Actor ID chuyên dụng cho Google Jobs, LinkedIn, và Indeed.
- **Node `Google Sheets - Get Target Companies` & Các node Google Sheets khác**: Tạo một file Google Sheets gồm 4 tab đúng chuẩn: `Target Companies`, `Raw Jobs`, `Qualified Leads`, và `Weekly Reports`. Sau đó kết nối Google Sheets Credentials cho tất cả các node liên quan.
- **Node `OpenAI Chat Model (Daily)` & `(Weekly)`**: Nhập OpenAI API Key và đảm bảo model được chọn là `gpt-4o`.
- **Node `Slack - Send Lead Alert` & `Gmail - Send Weekly Report`**: Kết nối thông tin tài khoản Slack (Webhook/Bot Token) và Gmail OAuth2 để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) một vài node cào dữ liệu và phân tích AI để kiểm tra kết nối API.
- Sau khi dữ liệu đổ về đúng Google Sheets và Slack, bật công tắc **Active** để workflow chạy tự động theo lịch trình (`Schedule Trigger - Daily 9AM` và `Schedule Trigger - Weekly Monday 8AM`).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM**: Có thể mở rộng workflow bằng cách đẩy dữ liệu `Qualified Leads` trực tiếp lên HubSpot, Salesforce hoặc Pipedrive thay vì chỉ lưu Google Sheets.
- **Thêm kênh thông báo**: Thay vì chỉ Slack, các sếp có thể cấu hình thêm node Telegram Bot để nhận lead nóng ngay trên điện thoại cá nhân bất cứ lúc nào có cơ hội mới.
- **Tối ưu Prompt AI**: Tùy chỉnh system prompt trong `AI Agent - Analyze and Generate Email` để điều chỉnh giọng văn của email phù hợp với phong cách thương hiệu công ty các sếp.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh giúp tự động hóa khâu prospecting (tìm kiếm khách hàng) dựa trên tín hiệu tuyển dụng (hiring signals). Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian cho đội ngũ sales và bứt phá doanh thu!