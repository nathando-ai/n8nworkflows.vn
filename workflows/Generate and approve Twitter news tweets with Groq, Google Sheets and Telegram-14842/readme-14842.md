---
title: "🚀 Tự động tạo và kiểm duyệt Tweet tin tức bằng Groq AI, Google Sheets và Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy tin tức, dùng Groq AI viết tweet, gửi qua Telegram duyệt bài và lưu log vào Google Sheets hoàn toàn tự động."
slug: "tu-dong-tao-va-kiem-duyet-tweet-groq-ai-google-sheets-telegram"
tags: [n8n, automation, groq, telegram, google-sheets, ai-agent, social-media]
keywords: [n8n workflow, tạo tweet tự động, Groq AI n8n, duyệt bài qua Telegram, Google Sheets automation]
---

# 🚀 Tự động tạo và kiểm duyệt Tweet tin tức bằng Groq AI, Google Sheets và Telegram

Các sếp có đang cảm thấy mệt mỏi mỗi ngày khi phải lướt tin tức, chọn lọc bài viết, vắt óc suy nghĩ nội dung tweet, rồi lại ngồi loay hoay lên lịch đăng bài thủ công không? Việc này vừa tốn thời gian, vừa ngốn năng lượng sáng tạo vốn có hạn.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ xịn sò giúp tự động hóa từ A-Z quy trình: **Lấy tin tức RSS -> AI (Groq) viết tweet -> Gửi thông báo & Duyệt bài qua Telegram -> Lưu log vào Google Sheets**. Các sếp chỉ việc bấm "Approve" (Phê duyệt) hoặc "Reject" (Từ chối) ngay trên chiếc điện thoại của mình!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công tìm kiếm tin tức hay nghĩ nội dung đăng Twitter/X mỗi ngày.
- **AI thông minh:** Sử dụng sức mạnh của Groq AI (`qwen/qwen3-32b`) để tạo ra các bài tweet cuốn hút, chuẩn văn phong mạng xã hội.
- **Kiểm soát linh hoạt:** Tích hợp Telegram Bot với nút bấm tương tác trực quan (Approve/Reject) giúp các sếp duyệt nội dung mọi lúc mọi nơi.
- **Quản lý dữ liệu chuyên nghiệp:** Tự động lưu trữ lịch sử tweet và đánh dấu các bài báo đã sử dụng lên Google Sheets, tránh trùng lặp nội dung.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Groq Cloud:** Lấy API Key để AI viết tweet.
- **Google Sheets:** Chuẩn bị sẵn một Google Sheet để lưu log và quản lý bài báo.
- **Telegram Bot:** Tạo một Bot thông qua `@BotFather` để gửi tin nhắn và nhận phản hồi tương tác (Callback).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 18 nodes được chia thành các cụm chức năng rõ ràng. Các sếp cần cấu hình các điểm cốt lõi sau:

- **Fetch Google News RSS (`Fetch Google News RSS`):** Node dạng HTTP Request, các sếp có thể thay đổi đường dẫn URL RSS sang chủ đề tin tức yêu thích của mình (Công nghệ, AI, Crypto, Kinh doanh...).
- **Đọc & Ghi dữ liệu Google Sheets (`Read Used Articles`, `Log Tweets in Sheets`, `Log Article as Used`, `Update Approval in Sheets`, `Update Rejection in Sheets`):** Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`. Trỏ tới file Google Sheet chuẩn bị sẵn và ánh xạ đúng tên các cột (Columns).
- **AI Tweet Generation (`AI Tweet Generation Agent` & `AI Groq Interaction`):** Cấu hình credentials cho Groq. Node `AI Groq Interaction` đang sử dụng model `qwen/qwen3-32b`, các sếp có thể tinh chỉnh Prompt trong Agent để AI viết tweet theo đúng phong cách cá nhân hoặc thương hiệu.
- **Tương tác Telegram (`Send Telegram Message`, `When Telegram Callback Triggered`, v.v.):** Kết nối `telegramApi` cho các node gửi tin nhắn và nhận sự kiện bấm nút. Đảm bảo Bot đã được thêm vào nhóm chat hoặc chat cá nhân của các sếp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử thủ công với cụm trigger lịch trình `When Scheduled at 8 AM` hoặc test nhanh qua `Fetch Google News RSS` để kiểm tra luồng dữ liệu.
- Sau khi mọi thứ chạy mượt mà, gạt nút **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh mạng xã hội:** Thay vì chỉ đăng Twitter, các sếp có thể nối thêm node LinkedIn hoặc Facebook Page sau bước duyệt bài trên Telegram.
- **Tích hợp thêm thông báo:** Bắn thêm một thông báo phụ qua Slack hoặc Discord mỗi khi có một tweet được phê duyệt thành công.
- **Tùy chỉnh lịch trình:** Thay đổi thời gian chạy ở node `When Scheduled at 8 AM` thành nhiều khung giờ khác trong ngày nếu muốn tăng tần suất đăng bài.

### 📌 Kết luận
Một hệ thống tự động hóa hoàn hảo kết hợp giữa Tin tức RSS, Sức mạnh AI từ Groq và tính tiện lợi của Telegram Bot. Hãy áp dụng ngay vào dự án của các sếp để tối ưu hóa hiệu suất làm việc với mạng xã hội ngay hôm nay!