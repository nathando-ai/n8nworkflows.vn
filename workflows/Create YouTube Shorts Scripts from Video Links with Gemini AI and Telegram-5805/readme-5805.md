---
title: "🚀 Tự động tạo kịch bản YouTube Shorts từ link video với Gemini AI và Telegram"
description: "Biến mọi video YouTube dài thành kịch bản Shorts ngắn gọn, thu hút tự động thông qua Telegram bot tích hợp Gemini AI và Supadata."
slug: "tao-kich-ban-youtube-shorts-tu-link-video-voi-gemini-ai-va-telegram"
tags: [n8n, automation, no-code, youtube, ai, telegram, gemini]
keywords: [n8n workflow, tạo kịch bản youtube shorts, gemini ai, supadata, telegram bot tự động hóa]
keywords: [n8n workflow, tự động hóa, tạo kịch bản youtube shorts, gemini ai, supadata, telegram bot]
---

# 🚀 Tự động tạo kịch bản YouTube Shorts từ link video với Gemini AI và Telegram

Các sếp làm nội dung trên YouTube chắc chắn hiểu rõ cảm giác "cạn kiệt" ý tưởng hoặc tốn hàng giờ đồng hồ chỉ để xem lại một video dài và cô đọng lại thành kịch bản YouTube Shorts / TikTok hấp dẫn. Việc này không chỉ tốn thời gian mà còn làm chậm quá trình sản xuất video hàng loạt.

Đừng lo, workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Bằng cách kết hợp sức mạnh của **Telegram Bot**, dịch vụ trích xuất transcript **Supadata**, và trí thông minh nhân tạo **Google Gemini AI**, hệ thống sẽ tự động nhận link video YouTube, bóc tách nội dung, phân tích và trả về một kịch bản Shorts chuẩn chỉnh ngay trên Telegram của các sếp chỉ trong vài giây. Hoàn toàn tự động, 100% không cần code thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần ngồi xem video dài và tự viết kịch bản tóm tắt nữa.
- **Sản xuất content tốc độ cao:** Dễ dàng tạo hàng loạt ý tưởng video Shorts/Reels từ các nguồn video tham khảo.
- **Tự động hóa qua Chat:** Chỉ cần gửi link vào Telegram cá nhân hoặc nhóm, bot sẽ tự động làm phần việc còn lại.
- **Cấu trúc kịch bản chuyên nghiệp:** Ứng dụng Gemini AI kết hợp Structured Output Parser giúp kịch bản có mở đầu thu hút, thân bài súc tích và kêu gọi hành động (CTA) rõ ràng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram để làm cổng giao tiếp nhận link và gửi kịch bản.
2. **Supadata API Key:** Đăng ký tài khoản tại [Supadata](https://supadata.com/) để lấy API key phục vụ việc bóc tách transcript video YouTube.
3. **Google Gemini API Key:** Key truy cập Google AI Studio để sử dụng mô hình Gemini xử lý ngôn ngữ tự nhiên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ kho lưu trữ n8n, sau đó vào giao diện n8n của mình, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình làm việc n8n Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Input URL (`telegramTrigger`):** Kết nối với tài khoản Telegram của các sếp bằng cách điền **Telegram API Credentials**. Node này sẽ lắng nghe link video YouTube được gửi vào khung chat của bot.
- **Make Transcribe (`n8n-nodes-supadata.supadata`):** Cấu hình Supadata API Key. Node này có nhiệm vụ gọi API để lấy toàn bộ transcript (phụ đề/lời thoại) từ đường dẫn video YouTube mà các sếp vừa gửi.
- **Google Gemini Chat Model (`lmChatGoogleGemini`) & Create Script (`chainLlm`):** Thêm Google Gemini API Key. Đây là "bộ não" phân tích nội dung transcript, lọc các ý chính và viết lại thành kịch bản video ngắn theo định dạng chuẩn.
- **Parsing (`outputParserStructured`) & Script mapping (`set`):** Đảm bảo cấu trúc dữ liệu đầu ra từ AI được định dạng sạch sẽ, dễ đọc trước khi chuyển đến bước tiếp theo.
- **Send Summary (`telegram`):** Sử dụng cùng Telegram Credentials để bot tự động gửi kịch bản hoàn chỉnh ngược lại đoạn chat trên Telegram cho các sếp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một link video YouTube bất kỳ vào Telegram Bot của các sếp để kiểm tra kết quả.
- Nếu mọi thứ hiển thị chính xác, hãy gạt công tắc sang trạng thái **Active** để bot hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Kết nối thêm node **Google Sheets** hoặc **Notion** sau bước `Script mapping` để tự động lưu mọi kịch bản đã tạo vào một bảng quản lý content dài hạn.
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể cấu hình gửi bản tóm tắt đồng thời lên kênh **Slack** hoặc **Discord** của team sản xuất nội dung.
- **Tùy chỉnh Prompt AI:** Tại node `Create Script`, các sếp có thể tùy chỉnh lại câu lệnh (prompt) hướng dẫn AI để kịch bản phù hợp hơn với văn phong cá nhân (hài hước, trang trọng, chuyên gia...).

### 📌 Kết luận
Workflow này là trợ thủ đắc lực cho bất kỳ nhà sáng tạo nội dung hay Marketer nào muốn tối ưu hóa quy trình làm video ngắn. Hãy cài đặt ngay hôm nay để biến mọi video dài thành kho tàng ý tưởng Shorts phong phú chỉ với vài cú click trên Telegram!