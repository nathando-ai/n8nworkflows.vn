---
title: "🚀 Tự động lọc tin tức địa chính trị nóng với AI Scoring & Telegram Alerts bằng n8n"
description: "Xây dựng hệ thống tự động cào tin tức từ 6 nguồn uy tín, lọc thông minh bằng từ khóa và chấm điểm mức độ khẩn cấp bằng OpenAI GPT-4o-mini trước khi gửi cảnh báo qua Telegram."
slug: "loc-tin-tuc-dia-chinh-tri-ai-telegram-n8n"
tags: [n8n, automation, ai, openai, telegram, rss]
keywords: [n8n workflow, lọc tin tức AI, telegram alerts, OpenAI gpt-4o-mini, tự động hóa tin tức địa chính trị]
---

# 🚀 Tự động lọc tin tức địa chính trị nóng với AI Scoring & Telegram Alerts

Các nhà nghiên cứu thị trường, nhà đầu tư hay chuyên gia phân tích thường xuyên đối mặt với một "núi" thông tin: hàng trăm bài báo mỗi ngày từ các hãng thông tấn lớn như BBC, Al Jazeera, NYT... Việc đọc thủ công không chỉ tốn thời gian mà còn dễ bỏ lỡ các tin tức địa chính trị cực kỳ quan trọng (breaking news). 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp gom nhóm, lọc sơ bộ bằng từ khóa thông minh để tiết kiệm 80-90% chi phí gọi AI, sau đó dùng AI chấm điểm mức độ khẩn cấp (1-10) và gửi cảnh báo trực tiếp về Telegram cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80-90% chi phí OpenAI:** Nhờ lớp lọc từ khóa động (Dynamic Filter) sơ bộ, chỉ những bài viết thực sự liên quan mới được đưa vào AI phân tích.
- **Cảnh báo thời gian thực:** Nhận tin "nóng" qua Telegram ngay sau mỗi 30 phút mà không cần canh gác màn hình.
- **Chấm điểm thông minh:** AI Agent sử dụng `gpt-4o-mini` để đánh giá thang điểm khẩn cấp (1-10), loại bỏ các tin tức rác hoặc thông tin lặp lại.
- **Quản lý lịch sử thông minh:** Tự động kiểm tra trùng lặp (Duplicate Check) và dọn dẹp các bản ghi cũ hơn 7 ngày trong n8n Data Table.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã bật tính năng n8n Data Table.
- **OpenAI API Key:** Cho node `OpenAI Chat Model` (sử dụng model `gpt-4o-mini`).
- **Telegram Bot Token & Chat ID:** Tạo bot thông qua BotFather để cấu hình cho node `Send Breaking News Alert`.
- **Google Drive / File Config:** File cấu hình JSON chứa danh sách từ khóa và ngưỡng điểm cảnh báo (`alert_threshold`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Load Config from Google Drive (HTTP Request):** Trỏ tới file cấu hình từ khóa và ngưỡng điểm của các sếp (có thể tham khảo cấu trúc file từ [Github Repo chính thức](https://github.com/devdutta/n8n-geopolitics-breaking-news-alert)).
- **RSS Feed Nodes (NYT, TOI, Al Jazeera, BBC, SCMP, NDTV):** Các node `rssFeedRead` này sẽ cào khoảng 200+ bài báo mỗi chu kỳ chạy.
- **Dynamic Filter & RSS_Cleanup_Node:** Chạy logic code tùy chỉnh để lọc sơ bộ dựa trên cấu hình từ khóa chính và phụ.
- **Check for Duplicates & Cleanup Old Records (Data Table):** Đảm bảo n8n Data Table được cấu hình đúng tên bảng để lưu `analyzed_articles`, tránh việc gửi lặp lại các tin đã thông báo.
- **Breaking News Analyzer (Agent & OpenAI Chat Model):** Chọn credentials OpenAI và giữ nguyên model `gpt-4o-mini` với Temperature đặt ở mức `0.3` để đảm bảo kết quả phân tích ổn định, nhất quán.
- **If Node:** Kiểm tra điều kiện bài báo có điểm số vượt ngưỡng (ví dụ: `> 6`) mới chuyển sang nhánh True.
- **Send Breaking News Alert (Telegram):** Kết nối Telegram Credentials và đảm bảo Chat ID nhận tin đã được thiết lập chính xác.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm (Test Run) với dữ liệu mẫu từ các RSS Feed.
- Kiểm tra kết quả trên Telegram xem thông báo đã bắn về chuẩn xác chưa.
- Gạt công tắc sang **Active** để workflow tự động chạy mỗi 30 phút (thời gian có thể điều chỉnh tại node `Every 30 Minutes`).

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Kết hợp thêm node Slack hoặc Discord song song với Telegram để đội ngũ cùng nắm bắt thông tin.
- **Lưu trữ Log mở rộng:** Đồng thời ghi lại các bản báo cáo tin tức quan trọng vào Google Sheets hoặc Notion để phục vụ làm báo cáo tuần/tháng.
- **Tùy chỉnh từ khóa theo ngành:** Thay vì địa chính trị, các sếp có thể đổi file config trên Google Drive thành các từ khóa về Crypto, AI Trends, hoặc Competitor Tracking để áp dụng cho lĩnh vực kinh doanh của mình.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc kết hợp giữa quy luật lọc truyền thống (Keyword Filtering) và trí tuệ nhân tạo (AI Scoring) nhằm tối ưu chi phí vận hành. Hãy cài đặt ngay để biến n8n thành một "trợ lý tình báo" tin tức 24/7 cho doanh nghiệp của các sếp!