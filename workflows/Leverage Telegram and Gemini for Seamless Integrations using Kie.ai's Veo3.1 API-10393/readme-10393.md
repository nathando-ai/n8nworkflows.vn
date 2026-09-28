---
title: "🚀 Tự động hóa tạo video UGC từ ảnh Telegram bằng Google Gemini và Kie.ai Veo3.1 API"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Telegram, Google Gemini và Kie.ai Veo3.1 API để biến ảnh sản phẩm và mô tả thành video quảng cáo UGC chuyên nghiệp tự động."
slug: "tu-dong-hoa-tao-video-ugc-telegram-gemini-kie-ai-veo"
tags: [n8n, automation, telegram, google-gemini, ai-video, content-creation]
keywords: [n8n workflow, tạo video ugc tự động, telegram bot ai, kie ai veo3, google gemini n8n]
---

# 🚀 Tự động hóa tạo video UGC từ ảnh Telegram với Google Gemini & Kie.ai Veo3.1

Các sếp làm nội dung, sáng tạo hay kinh doanh online chắc chắn đều hiểu việc sản xuất video quảng cáo UGC (User Generated Content) tốn kém và mất thời gian thế nào. Phải lên kịch bản, quay dựng, chỉnh sửa... Đừng lo, bài toán đó sẽ được giải quyết trọn gói 100% tự động với workflow n8n siêu cấp này!

Chỉ cần gửi một bức ảnh sản phẩm kèm mô tả ngắn qua **Telegram**, AI sẽ tự động viết kịch bản cuốn hút, đẩy qua **Kie.ai Veo3.1 API** để render video, và trả thẳng video HD hoàn chỉnh về lại Telegram cho các sếp. Quá đỉnh đúng không nào?

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ nặng như render video AI mà không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần đụng tay vào khâu viết kịch bản hay dựng video thủ công.
- **Tốc độ thần tốc:** Biến ảnh tĩnh thành video quảng cáo động chỉ sau vài phút chờ đợi vòng lặp (Loop).
- **Cá nhân hóa cao:** Kịch bản được AI (Google Gemini) viết tự nhiên theo phong cách UGC cực kỳ thu hút người xem.
- **Trải nghiệm liền mạch:** Mọi thao tác tương tác diễn ra trực tiếp trên ứng dụng Telegram quen thuộc.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua @BotFather) để nhận tin nhắn và gửi video.
- **Google Gemini API Key** (Dùng cho node AI Agent viết kịch bản).
- **Tài khoản & API Key tại Kie.ai** (Để sử dụng dịch vụ lưu trữ Storage và Veo3.1 Video Generation API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc sao chép toàn bộ mã JSON, sau đó dán trực tiếp vào n8n Editor của các sếp qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số và credentials cho các node sau:

- **Receive Message (`telegramTrigger`):** Kết nối với Telegram Bot Token của các sếp để lắng nghe tin nhắn gửi tới.
- **Download Telegram Image (`telegram`):** Dùng để tải tệp hình ảnh mà người dùng gửi kèm trong tin nhắn Telegram.
- **Google Gemini Chat Model (`lmChatGoogleGemini`) & Generate Script (`agent`):** 
  - Điền thông tin `googlePalmApi` credentials.
  - Tinh chỉnh prompt trong AI Agent nếu muốn đổi giọng văn của kịch bản quảng cáo (UGC-style).
- **Upload image to Kie Storage & Create Video Generation Task (`httpRequest`):** 
  - Cấu hình API Key của Kie.ai để tải ảnh lên cloud storage và gọi API Veo3.1 tạo tác vụ render video bằng kịch bản và URL ảnh.
- **Check Video Status & Is Video Ready? (`httpRequest` & `if`):** Node kiểm tra tiến độ render video từ phía Kie.ai.
- **Wait 30 Seconds (`wait`):** Node chờ đợi giữa các lần kiểm tra trạng thái để tránh bị quá tải request (Video Status Loop).
- **Get HD Video URL, Download Generated Video & Send Video to User (`httpRequest` & `telegram`):** Lấy link video hoàn thiện, tải về n8n và đẩy trực tiếp file video HD về lại chat Telegram cho người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tấm ảnh kèm caption sản phẩm qua Telegram Bot của các sếp để test xem luồng chạy có mượt mà không.
- Nếu mọi thứ xanh đèn (Success), hãy bật nút **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ Log:** Thêm một node Google Sheets hoặc Airtable vào sau bước gửi video thành công để lưu lại lịch sử ai đã yêu cầu tạo video nào.
- **Mở rộng kênh nhận:** Thay vì chỉ Telegram, các sếp có thể nhân bản luồng sang **Slack**, **Discord** hoặc **WhatsApp** tùy thuộc vào khách hàng mục tiêu.
- **Thông báo lỗi:** Thêm nhánh Error Trigger để nếu Kie.ai API gặp sự cố render, bot Telegram sẽ lập tức nhắn tin báo lỗi cho các sếp xử lý.

### 📌 Kết luận
Sự kết hợp giữa Telegram, Google Gemini và Kie.ai Veo3.1 mở ra một cánh cửa cực kỳ mạnh mẽ để tự động hóa hoàn toàn quy trình sản xuất nội dung video ngắn. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất và làm chủ công nghệ AI trong tay các sếp nhé!