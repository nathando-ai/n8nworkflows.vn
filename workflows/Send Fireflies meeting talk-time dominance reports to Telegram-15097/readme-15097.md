---
title: "🚀 Tự động gửi báo cáo thời gian nói chuyện trong cuộc họp từ Fireflies lên Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích dữ liệu cuộc họp từ Fireflies.ai, vẽ biểu đồ thời gian nói chuyện và gửi báo cáo chi tiết qua Telegram."
slug: "tu-dong-gui-bao-cao-thoi-gian-noi-chuyen-fireflies-telegram"
tags: [n8n, automation, fireflies, telegram, meeting-analytics, productivity]
keywords: [n8n workflow, fireflies ai, telegram automation, quan ly cuop hop, phan tich thoi gian noi chuyen]
---

# 🚀 Tự động gửi báo cáo thời gian nói chuyện Fireflies lên Telegram

Các sếp có bao giờ cảm thấy có những cuộc họp mà một vài cá nhân chiếm trọn sóng, trong khi những người khác hoàn toàn im lặng? Việc theo dõi "ai nói bao nhiêu" trong các cuộc họp thủ công là bất khả thi, và việc dò xét qua lại tốn rất nhiều thời gian. 

Workflow n8n này sẽ tự động hóa hoàn toàn quy trình: ngay khi Fireflies.ai hoàn thành việc ghi âm và biên bản cuộc họp, hệ thống sẽ phân tích thời gian nói chuyện của từng người, vẽ biểu đồ cột trực quan, phát hiện xem ai đang "độc chiếm" cuộc họp và gửi thẳng báo cáo chi tiết đến Telegram của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và nhận webhook mượt mà từ Fireflies, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Minh bạch thời gian:** Biết chính xác tỷ lệ thời gian nói của từng thành viên trong cuộc họp mà không cần xem lại video hay bản ghi dài dòng.
- **Cảnh báo độc chiếm:** Tự động phát hiện nếu có cá nhân vượt ngưỡng thời gian quy định (ví dụ: >70%) để các sếp kịp thời điều phối.
- **Biểu đồ trực quan:** Báo cáo đi kèm biểu đồ cột ASCII trực quan, tổng số câu hỏi, tốc độ nói và số từ rác (filler words) ngay trên Telegram.
- **Tiết kiệm thời gian:** Hoạt động hoàn toàn tự động 24/7 ngay khi Fireflies xử lý xong transcript.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Fireflies.ai:** Đã cấu hình và có API Key để gọi GraphQL API.
- **Telegram Bot:** Đã tạo Bot thông qua `@BotFather` và lấy Token.
- **n8n Instance:** Đã chạy và có thể nhận Webhook công khai (Public URL).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ hệ thống n8n hoặc copy trực tiếp và paste vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính, các sếp cần cấu hình cẩn thận các điểm sau:

- **1. Webhook — Fireflies Transcript Done**: Node này đóng vai trò nhận tín hiệu POST từ Fireflies khi bản ghi hoàn tất. Sau khi kích hoạt workflow, hãy copy Production Webhook URL và dán vào phần cài đặt Webhook của Fireflies (`Settings` -> `Developer Settings` -> `Webhooks`).
- **2. Set — Config Values**: Đây là nơi các sếp lưu các thông số cấu hình quan trọng:
  - Thay thế `YOUR_FIREFLIES_API_KEY` bằng API Key thật của tài khoản Fireflies.
  - Thay thế `YOUR_TELEGRAM_CHAT_ID` bằng Chat ID Telegram của các sếp hoặc nhóm quản lý.
  - Tùy chỉnh `dominanceThreshold` (mặc định là `70`%) - ngưỡng cảnh báo nếu ai đó nói quá tỷ lệ này.
- **3. HTTP — Fetch Speaker Analytics**: Node này sẽ gọi GraphQL API của Fireflies để lấy toàn bộ dữ liệu chi tiết từng diễn giả (tỷ lệ % thời gian nói, số từ, tốc độ, số câu hỏi, độc thoại dài nhất...). Đảm bảo node Set phía trước truyền đúng `meetingId`.
- **4. Code — Analyze Speaker Data**: Node JavaScript xử lý dữ liệu thô, sắp xếp diễn giả theo thời gian nói, vẽ biểu đồ cột dạng ASCII và lắp ráp nội dung thông điệp gửi đi.
- **5. Telegram — Send Talk-Time Report**: Kết nối credential **Telegram Bot API** của các sếp. *Lưu ý quan trọng:* Các sếp phải bấm `/start` với bot của mình trước khi test để bot có quyền gửi tin nhắn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** ở bước Webhook hoặc dùng tính năng Test để kiểm tra dữ liệu mẫu.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Kết nối thêm node Slack hoặc Microsoft Teams để gửi báo cáo song song vào kênh chung của team.
- **Lưu trữ dữ liệu lịch sử:** Thêm node Google Sheets hoặc Supabase để lưu lại lịch sử thời gian nói chuyện của từng thành viên qua các tuần, giúp đánh giá mức độ đóng góp trong các cuộc họp định kỳ.
- **Tích hợp AI tóm tắt:** Kết hợp thêm OpenAI/Claude node để phân tích thêm ngữ cảnh cuộc họp ngoài dữ liệu thống kê thời gian.

### 📌 Kết luận
Với workflow này, việc quản lý và cân bằng thời gian trong các cuộc họp của team chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay để tối ưu hóa hiệu suất làm việc nhóm và nâng cao chất lượng các buổi meeting nhé các sếp!