---
title: "🚀 Tự động cào và chuẩn hóa tin tuyển dụng từ Hacker News Who Is Hiring với n8n & OpenAI"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động lấy danh sách việc làm hàng tháng trên Hacker News, dùng AI bóc tách dữ liệu và lưu thẳng vào Airtable."
slug: "hacker-news-job-listing-scraper-parser-n8n"
tags: [n8n, automation, ai, openai, airtable, scraping]
keywords: [n8n workflow, hacker news who is hiring, ai scraper, n8n openai gpt-4o-mini, airtable automation]
---

# 🚀 Tự động cào và chuẩn hóa tin tuyển dụng từ Hacker News Who Is Hiring với n8n & OpenAI

Các sếp làm trong lĩnh vực HR, Sourcing hoặc săn việc làm công nghệ chắc hẳn đều biết đến chuỗi bài đăng hàng tháng **"Ask HN: Who is hiring?"** trên Hacker News. Đây là mỏ vàng chứa hàng trăm cơ hội việc làm chất lượng cao từ các startup và công ty công nghệ lớn trên thế giới. 

Tuy nhiên, việc ngồi đọc, copy thủ công từng bình luận tuyển dụng, sau đó tổng hợp vào Excel hay Notion là một cực hình tốn rất nhiều thời gian. 

Workflow n8n này do chuyên gia **Julian Kaiser** xây dựng sẽ giải quyết triệt để nỗi đau đó: Tự động kết nối tới Hacker News, lấy bài viết tuyển dụng mới nhất, lọc ra hàng loạt bình luận việc làm, sử dụng **OpenAI (GPT-4o-mini)** kết hợp **Structured Output Parser** để bóc tách thông tin thành các trường chuẩn chỉnh, và cuối cùng tự động đẩy dữ liệu gọn gàng vào **Airtable**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần thao tác thủ công, cập nhật ngay khi có bài đăng "Who is hiring?" mới hàng tháng.
- **Dữ liệu thông minh bằng AI:** Dùng sức mạnh của GPT-4o-mini để chuẩn hóa dữ liệu thô từ các bình luận lộn xộn thành JSON có cấu trúc (Công ty, Vị trí, Mức lương, Hình thức làm việc, Link ứng tuyển...).
- **Lưu trữ khoa học:** Đổ thẳng dữ liệu vào bảng Airtable giúp dễ dàng filter, tìm kiếm và quản lý.
- **Tiết kiệm hàng chục giờ:** Thay vì mất 2-3 ngày đọc thủ công, hệ thống xử lý chỉ trong vài phút.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để sử dụng model `gpt-4o-mini` bóc tách dữ liệu văn bản.
- **Airtable Account:** Tài khoản Airtable để lưu trữ kết quả (Có thể dùng mẫu Airtable Base của tác giả: [Link Airtable Base](https://airtable.com/appM2JWvA5AstsGdn/shrAuo78cJt5C2laR)).
- **Algolia API (Hoặc cURL từ Hacker News Algolia):** Để tìm kiếm bài viết "Who is hiring?".
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON của template này và paste trực tiếp vào giao diện làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes, các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Node `Search for Who is hiring posts` (HTTP Request):** 
  - Tác giả sử dụng Algolia Search (`https://hn.algolia.com/`) để tìm bài "Ask HN: Who is hiring?". 
  - *Mẹo:* Các sếp có thể truy cập `hn.algolia.com`, tìm kiếm chính xác cụm từ `"Ask HN: Who is hiring?"`, sort theo date, mở tab Network của trình duyệt để lấy request cURL và import trực tiếp vào node HTTP Request này (vì cần Header Auth riêng).
- **Node `HN API: Get Main Post` & `HI API: Get the individual job post` (HTTP Request):** 
  - Kết nối tới [Hacker News Firebase API](https://github.com/HackerNews/API) để lấy chi tiết bài viết gốc và danh sách các bình luận (children/jobs).
- **Node `Clean text` (Code):** 
  - Sử dụng JavaScript tùy chỉnh để làm sạch dữ liệu JSON thô lấy từ Algolia/HN API trước khi đưa qua AI.
- **Node `OpenAI Chat Model` & `Structured Output Parser`:** 
  - Kết nối tài khoản OpenAI của các sếp.
  - Chọn model: `gpt-4o-mini` (tiết kiệm chi phí và cực kỳ hiệu quả cho tác vụ parse text).
  - Đảm bảo JSON Schema được cấu hình đúng chuẩn các trường: `company`, `title`, `location`, `type`, `salary`, `description`, `apply_url`, `company_url`.
- **Node `Write results to airtable` (Airtable):** 
  - Kết nối `airtableTokenApi`.
  - Chọn Base và Table tương ứng (khuyên dùng base mẫu của tác giả để khớp sẵn các cột dữ liệu).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** tại node `When clicking ‘Test workflow’` để chạy thử nghiệm xem dữ liệu có chảy mượt mà qua các node OpenAI và đổ vào Airtable hay không.
- Sau khi test thành công, bật nút **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để mỗi khi có batch việc làm mới được lưu vào Airtable, hệ thống sẽ bắn một thông báo tóm tắt số lượng công việc vừa quét được lên nhóm chat.
- **Lọc thông minh hơn:** Tinh chỉnh node `Filter` hoặc viết thêm prompt trong node AI để chỉ lấy các công việc Remote hoặc thuộc lĩnh vực cụ thể (như AI Engineer, Fullstack, DevOps).
- **Lên lịch chạy tự động (Schedule Trigger):** Thay thế node `Manual Trigger` bằng `Schedule Trigger` chạy định kỳ vào ngày 2 hàng tháng (thời điểm bài "Who is hiring?" thường được đăng tải).

### 📌 Kết luận
Workflow **Hacker News Job Listing Scraper and Parser** là một ví dụ tuyệt vời cho việc kết hợp giữa Web Scraping, AI (LLM Structured Output) và No-Code Automation để giải quyết bài toán thực tế. Hãy triển khai ngay hôm nay để xây dựng cơ sở dữ liệu việc làm công nghệ tự động cho riêng mình các sếp nhé!