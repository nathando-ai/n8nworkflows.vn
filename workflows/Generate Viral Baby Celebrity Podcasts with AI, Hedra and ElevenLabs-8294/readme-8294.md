---
title: "🚀 Tự động hóa sản xuất Podcast trẻ em siêu viral với AI, Hedra và ElevenLabs"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn diện quy trình tạo video podcast người nổi tiếng phiên bản nhí (Baby Celebrity) cực kỳ hút khách bằng AI, ElevenLabs và Hedra."
slug: "tu-dong-hoa-podcast-tre-em-viral-ai-hedra-elevenlabs"
tags: [n8n, automation, no-code, ai-video, elevenlabs, hedra, content-creation]
keywords: [n8n workflow, tạo podcast tự động, ai video generator, hedra ai, elevenlabs text to speech, tự động hóa nội dung]
keywords_vi: [n8n workflow, tạo podcast tự động, ai video generator, hedra ai, elevenlabs text to speech, tự động hóa nội dung]
---

# 🚀 Tự động hóa sản xuất Podcast trẻ em siêu viral với AI, Hedra và ElevenLabs

Các sếp có bao giờ trầm trồ khi thấy các video dạng "Baby Celebrity Podcast" (podcast của các ngôi sao phiên bản nhí) thu hút hàng triệu lượt xem trên TikTok, YouTube Shorts hay Reels chưa? Việc ngồi lên ý tưởng, viết kịch bản, tạo giọng đọc, thiết kế hình ảnh hoạt hình nhí và đồng bộ chúng thành video hoàn chỉnh tiêu tốn rất nhiều thời gian và công sức nếu làm thủ công.

Giờ đây, các sếp hoàn toàn có thể tự động hóa 100% quy trình này nhờ vào siêu phẩm n8n workflow tích hợp AI đa phương thức (Multimodal AI), kết hợp OpenAI, ElevenLabs, Hedra và Google Drive!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Sản xuất tự động liên tục:** Lên lịch chạy định kỳ hoặc chạy thủ công để sinh ra hàng loạt video podcast viral mà không cần động tay.
- **AI thông minh toàn diện:** Tự động sáng tạo ý tưởng, viết kịch bản hài hước, tạo giọng đọc cảm xúc (ElevenLabs) và hoạt họa khuôn mặt biểu cảm (Hedra).
- **Lưu trữ gọn gàng:** Tự động lưu toàn bộ video thành phẩm lên Google Drive để sẵn sàng đăng tải lên các nền tảng mạng xã hội.
- **Tiết kiệm 99% thời gian:** Thay vì mất nhiều ngày dựng phim, giờ đây mọi thứ hoàn thành chỉ trong vài phút chạy workflow.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance:** (Self-hosted hoặc n8n Cloud).
- **OpenAI API Key:** Dành cho các node AI Agent sáng tạo ý tưởng và prompt.
- **ElevenLabs API Key:** Dành cho node Text to Speech tạo giọng đọc nhân vật.
- **Hedra API Key:** Dành cho việc tạo hình ảnh, asset và render video hoạt họa.
- **Google Sheets & Google Drive:** Để lưu trữ kho ý tưởng, quản lý tiến trình và lưu video đầu ra.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> bấm dấu `...` ở góc trên bên phải -> chọn **Import from JSON** và dán vào là xong!

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các thông số sau để workflow không bị lỗi:
- **Idea Generator & OpenAI Chat Model:** Kết nối thông tin Credential OpenAI của các sếp, cấu hình prompt để AI hiểu rõ chủ đề podcast mong muốn (ví dụ: các ngôi sao Hollywood phiên bản nhí trò chuyện vui nhộn).
- **Get Existing Ideas (Google Sheets):** Kết nối tài khoản Google Sheets, trỏ tới file quản lý ý tưởng để tránh việc trùng lặp nội dung.
- **Text to Speech (ElevenLabs):** Điền API Key của ElevenLabs, lựa chọn Voice ID phù hợp với giọng trẻ em hoặc giọng đặc trưng của nhân vật.
- **Create Image Asset (Hedra) & Create Video (Hedra):** Cấu hình API Key của Hedra, thiết lập kích thước video chuẩn dọc (Shorts/Reels) để tối ưu lượt xem.
- **Upload Video (Google Drive):** Chọn thư mục đích trên Google Drive để hệ thống tự động lưu video thành phẩm sau khi render xong qua các node `Wait 5 Mins` và `Download BabyPod Video (Hedra)`.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** tại node `When clicking ‘Test workflow’` hoặc `Schedule Trigger1` để kiểm tra chuỗi xử lý dữ liệu.
- Sau khi test thành công, bật công tắc **Active** để hệ thống tự động chạy ngầm theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Auto-posting:** Nối thêm node đăng video tự động lên YouTube Shorts, TikTok hoặc Facebook Reels ngay sau bước lưu Google Drive.
- **Gửi thông báo Telegram/Slack:** Thêm một node thông báo kèm link video khi quá trình render hoàn tất để các sếp tiện theo dõi thành quả.
- **Mở rộng chủ đề:** Thay đổi prompt trong OpenAI Agent để làm podcast về lịch sử, khoa học hoặc truyện cổ tích phiên bản nhí cực kỳ hấp dẫn cho thiếu nhi.

### 📌 Kết luận
Workflow này là một cỗ máy kiếm traffic thực thụ cho những nhà sáng tạo nội dung muốn đón đầu xu hướng AI Video. Hãy "lên đồ" ngay trên n8n và tạo ra những video podcast triệu view của riêng mình các sếp nhé!