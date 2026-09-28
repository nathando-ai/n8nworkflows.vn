---
title: "🚀 Tự động giám sát và phân loại thương hiệu từ Instagram và Google với Gemini"
description: "Hướng dẫn xây dựng hệ thống Social Listening tự động 100% bằng n8n, Apify và Google Gemini để quét mentions, phân tích cảm xúc và gửi cảnh báo Slack."
slug: "giam-sat-va-phan-loai-thuong-hieu-instagram-google-gemini"
tags: [n8n, automation, ai-summarization, market-research, apify, google-gemini, slack]
keywords: [n8n workflow, social listening tự động, giám sát thương hiệu, apify instagram scraper, google gemini n8n]
---

# 🚀 Tự động giám sát và phân loại thương hiệu từ Instagram & Google với Gemini

Mỗi ngày, hàng trăm khách hàng có thể đang bàn tán về thương hiệu của các sếp trên Instagram, các diễn đàn, Reddit hay các trang tin tức. Việc kiểm tra thủ công vừa tốn thời gian, vừa dễ bỏ lỡ các cuộc thảo luận quan trọng hay các khủng hoảng truyền thông tiềm ẩn. 

Giải pháp gì đây? Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, tự động quét thông tin từ mạng xã hội và web mở, phân tích ý kiến bằng AI (Google Gemini) và bắn thông báo ngay lập tức lên Slack. Không cần code, hoạt động 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn Social Listening:** Không còn tốn hàng giờ lướt tìm kiếm thủ công trên Instagram hay Google.
- **Phân tích thông minh bằng AI:** Google Gemini tự động đánh giá mức độ liên quan, phân loại sắc thái cảm xúc (sentiment) và mức độ khẩn cấp (urgency) của từng bài viết.
- **Chống trùng lặp thông minh:** Hệ thống tự lưu log vào n8n Data Table, đảm bảo không quét lại các mention cũ đã xử lý.
- **Cảnh báo tức thì:** Bắn tin nhắn trực tiếp vào kênh Slack ngay khi phát hiện mention có độ khẩn cấp cao.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ AI/LangChain).
- **Tài khoản Apify:** Để sử dụng các Actor quét dữ liệu Instagram và Google Search (Cần có Apify API/OAuth2 API).
- **Google Gemini API Key:** Sử dụng mô hình Google Gemini làm "bộ não" phân tích văn bản.
- **Slack Workspace:** Kênh Slack để nhận các thông báo cảnh báo khẩn cấp.
- **n8n Data Table:** Tạo sẵn một bảng dữ liệu trong n8n với cột `mention_id` (kiểu string).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép mã JSON của workflow từ [n8n Workflow Marketplace](https://n8n.io/workflows/16120) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các thành phần sau:

- **Node `Daily at 9am UTC` (Schedule Trigger):** 
  - Mặc định workflow chạy lúc 9:00 sáng UTC mỗi ngày. Các sếp có thể chỉnh lại múi giờ hoặc thời gian chạy tùy theo nhu cầu thực tế của doanh nghiệp.
- **Node `Brand Config` (Set):** 
  - Khai báo từ khóa thương hiệu cần theo dõi:
    - `instagramHashtags`: Mảng hashtag cần quét, ví dụ: `["thuonghieu", "mybrand"]`.
    - `googleQueries`: Các câu lệnh tìm kiếm trên Google, ví dụ: `thuonghieu`, `thuonghieu site:reddit.com`.
- **Node `Scrape Instagram` & `Scrape Google` (Apify):** 
  - Kết nối tài khoản Apify thông qua **Apify OAuth2 API**. Các Actor này sẽ chịu trách nhiệm bóc tách dữ liệu sạch sẽ từ các nền tảng chống bot mạnh mẽ như Instagram.
- **Node `Filter to New Mentions` & `Insert row` (Data Table):** 
  - Chọn đến bảng dữ liệu **"Brand monitoring DB"** đã tạo ở phần chuẩn bị để hệ thống lọc các mention chưa từng xuất hiện.
- **Node `Google Gemini Chat Model` & `Classify Mention` (AI Agent):** 
  - Cấu hình thông tin xác thực cho **Google Palm/Gemini API**. AI sẽ nhận dữ liệu thô và trả về cấu trúc chuẩn (`Mention Schema`) gồm: cảm xúc, điểm liên quan (1-10), độ khẩn cấp, và tóm tắt ngắn gọn.
- **Node `Slack high-urgency alert` (Slack):** 
  - Kết nối tài khoản **Slack OAuth2 API**, chọn channel nhận thông báo để nhận cảnh báo ngay lập tức khi độ khẩn cấp đạt mức cao.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) từng nhánh để kiểm tra dữ liệu trả về từ Apify và Gemini.
- Bật công tắc **Active** để workflow tự động chạy ngầm hàng ngày.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hệ thống Social Listening này, các sếp có thể mở rộng thêm:
1. **Đa dạng hóa kênh thông báo:** Thay vì chỉ dùng Slack, kết hợp thêm node Telegram hoặc gửi Email qua Gmail/SendGrid khi gặp khủng hoảng truyền thông.
2. **Lưu trữ mở rộng:** Ngoài n8n Data Table, có thể đẩy toàn bộ dữ liệu mention đã phân tích vào Google Sheets hoặc Notion để đội ngũ Marketing dễ dàng làm báo cáo hàng tuần.
3. **Tinh chỉnh bộ lọc AI:** Điều chỉnh prompt trong Agent hoặc thay đổi điều kiện ở node `Relevance >= 6?` và `High Urgency?` để nhận được lượng thông báo cô đọng và chính xác nhất, tránh bị "ngợp" thông tin.

### 📌 Kết luận
Với sự kết hợp hoàn hảo giữa **Apify** (bóc tách dữ liệu web/mạng xã hội mạnh mẽ), **n8n** (tự động hóa linh hoạt) và **Google Gemini** (trí tuệ nhân tạo phân tích thông minh), các sếp giờ đây đã sở hữu một hệ thống Social Listening 24/7 chuyên nghiệp với chi phí tối ưu. Triển khai ngay hôm nay để không bỏ lỡ bất kỳ tiếng nói nào từ khách hàng!