---
title: "🎬 Tự động hóa dịch và lồng tiếng video YouTube bằng n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình dịch và lồng tiếng video YouTube thông qua Telegram, Gemini, ElevenLabs và BrowserAct"
slug: "tu-dong-hoa-dich-lon-tien-video-youtube"
tags: [n8n, automation, no-code, content-creation, multimodal-ai]
keywords: [n8n workflow, tự động hóa, dịch video, lồng tiếng, YouTube]
---

# 🎬 Tự động hóa dịch và lồng tiếng video YouTube bằng n8n

[Các sếp] có biết không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình dịch và lồng tiếng video YouTube chỉ trong vài bước đơn giản. Không cần phải ngồi chờ đợi, không cần phải làm thủ công từng đoạn văn bản - mọi thứ sẽ được tự động hóa hoàn toàn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình dịch và lồng tiếng video YouTube.
- **Chính xác cao**: Sử dụng các công nghệ AI tiên tiến như Google Gemini và ElevenLabs để đảm bảo chất lượng dịch và lồng tiếng.
- **Tùy chỉnh dễ dàng**: Có thể thay đổi ngôn ngữ mục tiêu và các thiết lập khác theo nhu cầu.
- **Hoạt động liên tục**: Workflow có thể chạy 24/7 để xử lý các yêu cầu từ người dùng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và API key.
- Tài khoản BrowserAct và API key.
- Tài khoản OpenRouter (GPT-4) và API key.
- Tài khoản Google Gemini (PaLM) và API key.
- Tài khoản ElevenLabs và API key.
- Template **YouTube Translator & Auto Dubber** trong tài khoản BrowserAct.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể làm theo các bước sau:
1. Truy cập vào trang [n8n.io/workflows/12361](https://n8n.io/workflows/12361).
2. Nhấp vào nút **Import** để tải xuống file JSON của workflow.
3. Trong n8n Editor, nhấp vào nút **+** để tạo một workflow mới.
4. Nhấp vào nút **Import from File** và chọn file JSON vừa tải xuống.
5. Hoàn tất quá trình import và lưu workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý đến các node quan trọng sau đây:

- **User Sends Message to Bot**: Node này sử dụng Telegram để nhận tin nhắn từ người dùng. Các sếp cần cấu hình đúng API key của Telegram.
- **Validate inputs**: Node này sử dụng Google Gemini để xác thực đầu vào. Các sếp cần cấu hình đúng API key của Google Palm.
- **Extract Youtube Transcript**: Node này sử dụng BrowserAct để trích xuất bản dịch từ video YouTube. Các sếp cần cấu hình đúng API key của BrowserAct và đảm bảo template **YouTube Translator & Auto Dubber** đã được lưu trong tài khoản BrowserAct.
- **Analyze user Input**: Node này sử dụng AI agent để phân tích đầu vào từ người dùng. Các sếp cần cấu hình đúng các tham số cần thiết.
- **Define Language**: Node này sử dụng để định nghĩa ngôn ngữ mục tiêu. Mặc định là tiếng Tây Ban Nha, các sếp có thể thay đổi theo nhu cầu.
- **Convert text to speech**: Node này sử dụng ElevenLabs để chuyển đổi văn bản thành giọng nói. Các sếp cần cấu hình đúng API key của ElevenLabs.
- **Send Summary Back to Bot**: Node này sử dụng Telegram để gửi bản tóm tắt về cho người dùng. Các sếp cần cấu hình đúng API key của Telegram.
- **Send Dubbed Audio File**: Node này sử dụng Telegram để gửi file âm thanh đã lồng tiếng về cho người dùng. Các sếp cần cấu hình đúng API key của Telegram.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình xong các node quan trọng, các sếp có thể kích hoạt workflow bằng cách:
1. Nhấp vào nút **Activate** để kích hoạt workflow.
2. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng như mong đợi.
3. Bật Active workflow để bắt đầu xử lý các yêu cầu từ người dùng.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể kết hợp workflow với Slack hoặc Telegram để nhận thông báo khi có yêu cầu mới hoặc khi quá trình xử lý hoàn thành.
- **Lưu log**: Các sếp có thể lưu log các yêu cầu và kết quả xử lý để theo dõi và phân tích hiệu suất của workflow.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo định kỳ về số lượng yêu cầu đã xử lý, thời gian trung bình xử lý, v.v.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình dịch và lồng tiếng video YouTube một cách dễ dàng và hiệu quả. Với các công nghệ AI tiên tiến và các tính năng mạnh mẽ, workflow này sẽ giúp các sếp tiết kiệm thời gian và nâng cao chất lượng dịch và lồng tiếng. Hãy áp dụng ngay workflow này để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!