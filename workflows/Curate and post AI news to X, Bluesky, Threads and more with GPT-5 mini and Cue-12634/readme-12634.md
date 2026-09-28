---
title: "🚀 Tự động tổng hợp và đăng tin tức AI lên X, Bluesky, Threads với GPT-4o mini và Cue"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc tin tức RSS, sử dụng AI để tóm tắt và lên lịch đăng bài đa nền tảng mạng xã hội qua Cue một cách chuyên nghiệp."
slug: "tu-dong-tong-hop-va-dang-tin-tuc-ai-len-mang-xa-hoi-n8n"
tags: [n8n, automation, no-code, social-media, ai, openai, cue]
keywords: [n8n workflow, tự động hóa mạng xã hội, đăng bài tự động, AI news, GPT-4o mini, Cue social media]
---

# 🚀 Tự động tổng hợp và đăng tin tức AI lên X, Bluesky, Threads với GPT-4o mini và Cue

Các sếp có đang chật vật mỗi ngày vì phải vào từng trang tin công nghệ, chọn lọc nội dung, viết lại caption rồi thủ công đăng lên X (Twitter), Bluesky, Threads hay LinkedIn không? Công việc lặp đi lặp lại này ngốn rất nhiều thời gian quý báu mà lẽ ra các sếp nên dùng để phát triển kinh doanh.

Đừng lo, giải pháp ở đây rồi! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh, tự động hóa từ A-Z quy trình: đọc tin tức RSS, dùng AI (OpenAI GPT-4o mini) để biên tập lại thành các bài đăng hấp dẫn, và tự động đẩy lên các nền tảng mạng xã hội thông qua công cụ **Cue**. 100% tự động, không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tự tay copy-paste hay viết nội dung mạng xã hội mỗi ngày.
- **AI thông minh cá nhân hóa:** GPT-4o mini giúp tóm tắt, tạo tiêu đề bắt tai và định dạng nội dung phù hợp với văn phong từng nền tảng.
- **Đa kênh đồng thời:** Đăng tải liền mạch lên X, Bluesky, Threads chỉ với một lần kích hoạt workflow.
- **Hoạt động 24/7 không mệt mỏi:** Chạy tự động theo lịch trình định sẵn (Schedule Trigger), đảm bảo kênh của các sếp luôn có nội dung mới đều đặn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Hệ thống n8n:** Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI:** Lấy OpenAI API Key để AI xử lý và viết nội dung.
- **Nguồn tin RSS:** Các đường link RSS Feed về công nghệ hoặc AI mà các sếp muốn theo dõi.
- **Tài khoản Cue:** Công cụ quản lý và lên lịch mạng xã hội (Cuehq) cùng API/Credentials kết nối.
- **Google Sheets (Tùy chọn):** Dùng để lưu lịch sử các bài đã đăng nếu muốn kiểm tra lại.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã JSON của workflow từ trang chủ n8n (Link gốc: [n8n Workflow #12634](https://n8n.io/workflows/12634)), sau đó thực hiện import trực tiếp vào n8n Editor của mình bằng cách chọn **Add workflow** -> **Import from File/Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đã import thành công, các sếp cần cấu hình lại các node cốt lõi sau để workflow chạy mượt mà:

- **Schedule Trigger:** Cài đặt khung giờ chạy tự động mong muốn (ví dụ: mỗi sáng lúc 8:00 AM hoặc chạy vài lần một ngày).
- **RSS Feed Read (`n8n-nodes-base.rssFeedRead`):** Dán các đường link RSS Feed tin tức công nghệ/AI mà các sếp muốn thu thập.
- **OpenAI Chat Model & AI Agent (`@n8n/n8n-nodes-langchain`):** Kết nối OpenAI Credentials, thiết lập prompt cho AI Agent để đóng vai trò biên tập viên chuyên nghiệp, tóm tắt tin tức ngắn gọn, sắc sảo và kèm hashtag phù hợp. Sử dụng thêm **Output Parser Structured** để ép kiểu dữ liệu trả về theo đúng định dạng JSON mà các bước sau cần.
- **Cue Node (`@cuehq/n8n-nodes-cue.cue`):** Kết nối tài khoản Cue của các sếp để đẩy nội dung đã được AI viết xong lên các mạng xã hội như X, Bluesky, Threads. Chọn đúng tài khoản và cấu hình lịch đăng.
- **Google Sheets (`n8n-nodes-base.googleSheets`):** Cấu hình file Google Sheet để lưu lại log các bài viết đã được xử lý và lên lịch thành công (tránh việc đăng trùng lặp tin cũ).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với một vài bản ghi dữ liệu mẫu từ RSS Feed xem AI viết nội dung có chuẩn chỉnh và đẩy sang Cue thành công không.
- Sau khi test ngon lành, gạt công tắc sang chế độ **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow xịn sò hơn nữa, các sếp có thể tham khảo các ý tưởng mở rộng sau:
- **Thêm bước duyệt bài (Human-in-the-loop):** Trước khi gửi sang Cue để đăng, cấu hình gửi thông báo kèm nút bấm duyệt qua Telegram hoặc Slack để các sếp kiểm tra lại nội dung AI viết.
- **Lưu trữ đa nền tảng:** Kết nối thêm Notion hoặc Airtable thay vì chỉ dùng Google Sheets để lưu trữ kho tàng content tự động.
- **Đa dạng hóa nguồn tin:** Gom nhóm nhiều RSS Feed khác nhau từ các lĩnh vực: AI, Startup, Tech News để AI tổng hợp thành một bản tin tổng hợp hàng ngày (Daily Digest).

### 📌 Kết luận
Tự động hóa việc sáng tạo nội dung mạng xã hội với n8n và AI không chỉ giúp các sếp giải phóng thời gian mà còn giữ cho các kênh truyền thông luôn sôi động, bắt kịp xu hướng công nghệ từng phút. Hãy "lên đồ" ngay cho hệ thống của mình và tối ưu hóa hiệu suất làm việc ngay hôm nay thôi nào các sếp!