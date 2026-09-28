---
title: "🚀 Tự động hóa Lời khẳng định tích cực mỗi ngày & Tổng kết lòng biết ơn hàng tuần với Notion, Email và Telegram qua n8n"
description: "Xây dựng thói quen chánh niệm và biết ơn tự động 100% bằng n8n. Workflow kết hợp Notion để lưu trữ, gửi khẳng định hàng ngày và tổng kết hàng tuần qua Email/Telegram/Slack."
slug: "tu-dong-hoa-loi-khang-dinh-tich-cuc-va-biet-on-notion-n8n"
tags: [n8n, automation, notion, telegram, email, productivity]
keywords: [n8n workflow, tự động hóa notion, daily affirmations, weekly gratitude digest, n8n telegram bot, productivity automation]
---

# 🚀 Tự động hóa Lời khẳng định tích cực & Tổng kết lòng biết ơn với Notion, Email & Telegram

Trong cuộc sống bận rộn hiện đại, việc duy trì thói quen thực hành chánh niệm, đọc lời khẳng định tích cực (daily affirmations) hay viết nhật ký biết ơn thường dễ bị lãng quên. Việc làm thủ công các việc này mỗi ngày không chỉ tốn thời gian mà còn thiếu tính đều đặn. 

Được thiết kế bởi **Shelly-Ann Davy** (The Workflow Muse), workflow n8n tuyệt đẹp này sinh ra để giải quyết triệt để vấn đề đó. Nó hoạt động như một "trợ lý tinh thần" tự động 100%, tự động gửi lời khẳng định mỗi ngày, tổng kết lòng biết ơn hàng tuần từ **Notion**, và gửi thẳng đến **Email, Telegram, Slack hoặc Discord** của các sếp mà không cần đụng tay vào code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo động lực mỗi ngày:** Tự động nhận các câu khẳng định tích cực vào khung giờ cố định qua Telegram hoặc Email.
- **Nuôi dưỡng lòng biết ơn:** Tự động tổng hợp (Digest) các nội dung biết ơn từ Notion trong suốt 7 ngày qua vào mỗi cuối tuần.
- **Lưu trữ thông minh:** Tự động ghi lại lịch sử các lời khẳng định và nhật ký vào Notion Database để dễ dàng tra cứu.
- **Cảnh báo lỗi tự động:** Tích hợp Error Trigger gửi thông báo qua Slack/Discord ngay lập tức nếu workflow gặp sự cố.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance:** (Self-hosted hoặc n8n Cloud).
- **Notion Account:** Có sẵn Database lưu trữ Affirmations và Gratitude.
- **Telegram Bot Token:** Để gửi tin nhắn qua Telegram.
- **SMTP Email / Email Node:** Để gửi thông báo qua email.
- **Slack App / Discord Webhook:** (Tùy chọn) Dùng để nhận cảnh báo lỗi hệ thống.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ [n8n.io/workflows/7555](https://n8n.io/workflows/7555), sau đó paste trực tiếp vào n8n Editor của mình hoặc import file JSON tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 24 nodes được chia thành các luồng chính, các sếp cần chú ý cấu hình kỹ các node sau:

- **Cron Triggers (`Cron: Daily Affirmation`, `Cron: Weekly Digest`):** 
  - Cấu hình lại múi giờ (Timezone) cho đúng với giờ Việt Nam (`Asia/Ho_Chi_Minh`) để tin nhắn được gửi đúng giờ mong muốn.
- **Config Nodes (`Set: User Config`, `Set: Digest Config`, `Set: Alert Config`):** 
  - Điền các thông tin cấu hình cá nhân như tên người dùng, cấu trúc tin nhắn hoặc ID cấu hình cơ bản.
- **Notion Nodes (`Notion: Log Affirmation`, `Notion: Query Gratitude (7d)`):** 
  - Kết nối tài khoản Notion bằng **Notion API Key (Integration)**.
  - Chọn đúng **Database ID** lưu trữ các lời khẳng định và nhật ký biết ơn của các sếp.
- **Notification Nodes (`Email: Send Affirmation`, `Telegram: Send Affirmation`, `Slack: Post Alert`,...):** 
  - Thiết lập credentials cho SMTP email, Telegram Bot, và kênh Slack/Discord để hệ thống có chỗ "gửi quà" cho các sếp.
- **Error Handler (`On Error: Any Node`):** 
  - Đảm bảo nhánh bắt lỗi được kết nối đúng cách tới các nền tảng thông báo (Slack/Discord) để các sếp không bị bỏ lỡ khi workflow gặp trục trặc kỹ thuật.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử từng nhánh (Daily Affirmation và Weekly Digest) để kiểm tra xem tin nhắn đã đổ về Telegram/Email hay chưa.
- Sau khi test mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Các sếp có thể kết hợp thêm node **Zalo ZNS** hoặc **Messenger** nếu muốn nhận lời khẳng định qua các nền tảng chat phổ biến tại Việt Nam.
- **Tích hợp AI (OpenAI / Claude):** Thay vì dùng nội dung cố định, các sếp có thể thêm một node AI trước bước build message để tạo ra các lời khẳng định độc bản, mang tính cá nhân hóa cực cao dựa trên cảm xúc của sếp ngày hôm đó.
- **Lưu lịch sử chạy:** Sử dụng thêm Google Sheets hoặc một bảng Notion riêng để log lại lịch sử gửi tin nhằm đánh giá mức độ duy trì thói quen.

### 📌 Kết luận
Một workflow tuyệt vời giúp nâng cao năng suất cá nhân, chăm sóc sức khỏe tinh thần (mental wellness) mà không tốn một đồng chi phí phần mềm đắt đỏ nào. Hãy cài đặt ngay trên hệ thống n8n của các sếp để bắt đầu ngày mới với năng lượng tích cực nhất nhé!