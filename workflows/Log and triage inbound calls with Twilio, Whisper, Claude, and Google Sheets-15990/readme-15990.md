---
title: "🚀 Tự động hóa ghi âm cuộc gọi đến với Twilio, Whisper, Claude và Google Sheets trên n8n"
description: "Hướng dẫn xây dựng hệ thống tự động nhận cuộc gọi, chuyển đổi giọng nói thành văn bản, phân tích ý định bằng AI và ghi log vào Google Sheets với n8n."
slug: "tu-dong-hoa-ghi-am-cuoc-goi-twilio-whisper-claude-google-sheets"
tags: [n8n, automation, ai-agents, twilio, openai-whisper, claude, google-sheets]
keywords: [n8n workflow, tự động hóa cuộc gọi, twilio webhook, whisper transcribe, claude ai, google sheets automation]
---

# 🚀 Tự động hóa ghi âm cuộc gọi đến với Twilio, Whisper, Claude và Google Sheets

Việc quản lý và xử lý các cuộc gọi đến từ khách hàng thường ngốn rất nhiều thời gian của doanh nghiệp. Nhân sự phải nghe lại file ghi âm, tóm tắt thủ công, phân loại mức độ khẩn cấp rồi mới nhập liệu vào Google Sheets hay chuyển tiếp cho cấp trên. Nếu bỏ lỡ cuộc gọi khẩn cấp, doanh nghiệp có thể mất đi những khách hàng tiềm năng giá trị.

Giải pháp? Workflow n8n này sẽ tự động hóa **100% quy trình từ A-Z**: Nhận file ghi âm cuộc gọi từ Twilio $\rightarrow$ Chuyển giọng nói thành văn bản bằng Whisper $\rightarrow$ Phân tích ý định & độ khẩn cấp bằng Claude AI $\rightarrow$ Lưu trữ vào Google Sheets $\rightarrow$ Gửi email cảnh báo khẩn cấp ngay lập tức nếu cần. Không cần code phức tạp, các sếp chỉ cần "lên đồ" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần nghe lại file ghi âm hay thủ công nhập liệu.
- **Phân loại thông minh:** AI tự động hiểu ý định khách hàng và xác định độ khẩn cấp của cuộc gọi.
- **Phản ứng tức thì:** Tự động gửi email cảnh báo ngay lập tức đối với các cuộc gọi quan trọng/khẩn cấp.
- **Lưu trữ minh bạch:** Mọi thông tin cuộc gọi, bản ghi (transcript) và kết quả phân tích được đồng bộ hóa hoàn hảo vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- Tài khoản **Twilio** (đã cấu hình số điện thoại và tính năng ghi âm cuộc gọi).
- Tài khoản **OpenAI API Key** (để sử dụng Whisper Transcribe).
- Tài khoản **Anthropic API Key** (để sử dụng Claude AI phân tích).
- Tài khoản **Google Sheets** (tạo sẵn file Google Sheet để lưu log cuộc gọi).
- Tài khoản **Gmail** (để gửi email cảnh báo cuộc gọi khẩn cấp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 10 nodes chính, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Receive Call Recording (`webhook`):** Cấu hình path là `twilio-recording`, phương thức `POST`. Lấy URL của Webhook này dán vào phần cấu hình Webhook khi có cuộc gọi hoàn tất trên **Twilio**.
- **Download Call Recording & Transcribe Audio with Whisper (`httpRequest`):** Điền OpenAI API Key vào phần credentials để cấp quyền tải file và gọi API Whisper chuyển giọng nói thành văn bản.
- **Analyze Intent with AI (`httpRequest`):** Cấu hình Anthropic API Key và tinh chỉnh prompt trong Claude để hệ thống phân tích đúng ý định và đánh giá mức độ khẩn cấp (Urgent/Normal) theo nhu cầu doanh nghiệp.
- **Append Call Data to Sheets (`googleSheets`):** Kết nối tài khoản Google Sheets, chọn đúng File Google Sheet và Sheet Name đã chuẩn bị sẵn để map các cột dữ liệu (Số điện thoại, Thời gian, Transcript, Ý định, Độ khẩn cấp...).
- **Dispatch Urgent Email Alert (`gmail`):** Kết nối tài khoản Gmail và thiết lập địa chỉ người nhận, tiêu đề, nội dung cảnh báo khi node điều kiện phát hiện cuộc gọi khẩn cấp.
- **Respond with TwiML Message (`respondToWebhook`):** Đảm bảo trả về phản hồi TwiML hoặc mã xác nhận hợp lệ để Twilio đóng kết nối mượt mà.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test run** bằng một cuộc gọi mẫu từ Twilio để kiểm tra dữ liệu chảy qua từng node.
- Kiểm tra kết quả trên Google Sheets và Gmail xem đã hoạt động chính xác chưa.
- Bật công tắc **Active** để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot/Messaging:** Kết hợp thêm node Telegram hoặc Slack để bắn thông báo cuộc gọi khẩn cấp trực tiếp lên nhóm chat nội bộ thay vì chỉ dùng Gmail.
- **Lưu trữ Audio:** Tải file ghi âm MP3 từ Twilio lưu trữ trực tiếp lên Google Drive hoặc AWS S3 để dễ dàng nghe lại khi cần thiết.
- **Phân loại nâng cao:** Tùy chỉnh prompt của Claude AI để tự động gán nhãn (tag) khách hàng (ví dụ: Khiếu nại, Tư vấn mua hàng, Hỗ trợ kỹ thuật...).

### 📌 Kết luận
Hệ thống tự động hóa xử lý cuộc gọi đến với sự hỗ trợ của Twilio, Whisper và Claude AI sẽ giúp doanh nghiệp của các sếp chuyên nghiệp hóa quy trình chăm sóc khách hàng, không bỏ lỡ bất kỳ cơ hội kinh doanh hay vấn đề khẩn cấp nào. Hãy áp dụng ngay hôm nay để tối ưu hóa năng suất đội ngũ!