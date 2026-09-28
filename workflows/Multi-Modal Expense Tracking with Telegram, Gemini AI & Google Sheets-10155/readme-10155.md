---
title: "🚀 Tự động ghi chép chi tiêu đa phương thức qua Telegram, Gemini AI và Google Sheets"
description: "Hướng dẫn cấu hình workflow n8n tự động phân tích tin nhắn văn bản, ghi âm giọng nói hoặc hình ảnh hóa đơn từ Telegram, sử dụng Gemini AI để bóc tách dữ liệu và lưu trữ gọn gàng vào Google Sheets."
slug: "quan-ly-chi-tieu-da-phuong-thuc-telegram-gemini-google-sheets"
tags: [n8n, automation, no-code, google-sheets, telegram, ai-agent, gemini]
keywords: [n8n workflow, quản lý chi tiêu tự động, telegram bot expense tracker, gemini ai n8n, google sheets automation]
---

# 🚀 Tự động ghi chép chi tiêu đa phương thức qua Telegram, Gemini AI và Google Sheets

Các sếp có bao giờ cảm thấy việc ghi chép lại các khoản chi tiêu hàng ngày quá rườm rà và dễ bỏ sót? Lúc mua xong một ly cà phê hay bữa ăn, mở app nhập tay thì lười, mà để cuối ngày tổng kết thì không nhớ nổi đã tiêu những gì. 

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Các sếp chỉ cần nhắn tin văn bản, gửi một đoạn ghi âm vu vơ ("Hôm nay ăn trưa hết 50k, uống trà sữa 35k"), hoặc chụp lại tấm hình hóa đơn qua **Telegram**, phần việc còn lại hãy để AI lo. Hệ thống sẽ tự động bóc tách số tiền, tên món, ngày tháng và lưu thẳng vào **Google Sheets**, sau đó gửi tin nhắn xác nhận lại ngay lập tức. Giải pháp tự động hóa 100% không cần code giúp tối ưu hóa thời gian cá nhân!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa phương thức (Multi-modal):** Xử lý mượt mà cả tin nhắn văn bản (Text), giọng nói (Voice notes) và hình ảnh (Hóa đơn/Biển báo).
- **Trí tuệ nhân tạo thông minh:** Sử dụng sức mạnh của Google Gemini để tự động chuẩn hóa dữ liệu tự do thành cấu trúc JSON chặt chẽ (`amount`, `item`, `date`).
- **Tự động hóa toàn diện:** Không cần mở Google Sheets thủ công, mọi giao dịch đều được ghi nhận theo từng hàng (row) riêng biệt.
- **Phản hồi tức thì:** Bot Telegram sẽ gửi thông báo xác nhận chi tiết ngay sau khi ghi dữ liệu thành công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Telegram:** Tạo Bot thông qua `@BotFather` để lấy **Bot Token**.
- **Google Sheets:** Tạo sẵn một file Google Sheet dùng để lưu log chi tiêu.
- **Google Gemini API (Google AI):** Lấy API Key để phục vụ cho các node phiên âm giọng nói, đọc hình ảnh và AI Agent trích xuất dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các điểm mấu chốt sau:
- **`Start: On Telegram Message`**: Kết nối với credential Telegram Bot của sếp để lắng nghe tin nhắn đến.
- **`GSheet: Log Expense`**: Chọn credential Google Sheets OAuth2 và trỏ tới file Google Sheet và Sheet Name đã chuẩn bị sẵn.
- **`Telegram: Send Confirmation` & các node Telegram khác**: Đảm bảo `chatId` được thiết lập chính xác để bot biết đường gửi tin nhắn phản hồi về cho sếp.
- **Các node LLM/Gemini (`LLM: Gemini Flash`, `Gemini: Transcribe Voice`, `Gemini: Analyze an image`, `AI: Extract Expenses`)**: Thêm credential Google Palm/Gemini API key để kích hoạt tính năng AI xử lý ngôn ngữ và hình ảnh.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một tin nhắn văn bản, voice hoặc ảnh chụp hóa đơn qua bot Telegram để test.
- Nếu mọi thứ chạy xanh mướt, hãy bật nút **Active** ở góc trên cùng bên phải để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo nhóm:** Ngoài chat cá nhân, sếp có thể mở rộng workflow để gửi thông báo chi tiêu vào một nhóm Telegram hoặc kênh Slack chung của gia đình/team.
- **Bổ sung bước phân loại danh mục (Categories):** Tinh chỉnh Prompt trong AI Agent để tự động phân loại khoản chi vào các mục như *Ăn uống, Giải trí, Hóa đơn, Mua sắm* giúp việc vẽ biểu đồ thống kê sau này dễ dàng hơn.
- **Báo cáo định kỳ:** Kết hợp thêm node Schedule Trigger để cứ cuối tuần/cuối tháng bot tự động tổng hợp tổng chi phí và gửi báo cáo cho sếp.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa cực kỳ hữu ích cho việc quản lý tài chính cá nhân. Chỉ với vài thao tác cấu hình đơn giản ban đầu, các sếp đã sở hữu ngay một trợ lý AI thông minh trên Telegram. Áp dụng ngay thôi nào!