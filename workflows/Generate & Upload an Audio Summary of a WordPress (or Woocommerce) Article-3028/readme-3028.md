---
title: "🚀 Tự động hóa tạo và tải lên tóm tắt âm thanh cho bài viết WordPress"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy bài viết WordPress, tóm tắt bằng AI, chuyển đổi thành giọng nói MP3 và cập nhật lại bài viết."
slug: "tao-va-tai-len-tom-tat-am-thanh-wordpress"
tags: [n8n, automation, wordpress, ai, text-to-speech, openai, elevenlabs]
keywords: [n8n workflow, tóm tắt bài viết wordpress, text to speech n8n, elevenlabs api, tự động hóa wordpress]
---

# 🚀 Tự động hóa tạo và tải lên tóm tắt âm thanh cho bài viết WordPress

Các sếp có đang gặp tình trạng người dùng ngày nay rất lười đọc các bài viết dài trên blog hay trang thương mại điện tử (WooCommerce) không? Việc sản xuất nội dung âm thanh (audio summary) cho từng bài viết là một xu hướng tuyệt vời để giữ chân độc giả, nhưng nếu làm thủ công (copy bài viết -> tóm tắt -> thu âm/TTS -> tải lên -> chèn vào bài) sẽ ngốn rất nhiều thời gian và công sức. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để bài toán trên!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn từ khâu đọc bài viết gốc, tóm tắt, chuyển thành giọng nói đến cập nhật lên web.
- **Nâng cao trải nghiệm người dùng:** Khách hàng có thể nghe tóm tắt bài viết trực tiếp khi đang di chuyển hoặc bận rộn.
- **Tối ưu SEO & Tương tác:** Tăng thời gian on-site cho trang web WordPress/WooCommerce của các sếp.
- **Chất lượng AI thông minh:** Sử dụng OpenAI để làm sạch HTML, tóm tắt cô đọng hoặc chuyển đổi nội dung linh hoạt theo ý muốn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **WordPress Site:** Đã kích hoạt REST API và có tài khoản Application Passwords.
- **OpenAI API Key:** Để xử lý việc tóm tắt/làm sạch nội dung bài viết.
- **ElevenLabs Account:** Tài khoản và API Key để sử dụng dịch vụ Text-to-Speech chất lượng cao.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **When clicking ‘Test workflow’ (`manualTrigger`):** Node kích hoạt thủ công để test (có thể thay thế bằng Webhook hoặc Schedule Trigger nếu muốn chạy tự động hàng ngày).
- **Retrieve WordPress Article (`wordpress`):** 
  - Chọn Credentials WordPress API của các sếp.
  - Cấu hình ID bài viết cần lấy nội dung (`operation: get`).
- **settings (`set`):** Nơi cấu hình các tham số phụ như ID giọng đọc của ElevenLabs (`voice_id`) và các thiết lập khác.
- **OpenAI Chat Model & Generate Summary or Transcription (`chainLlm`):** 
  - Chọn credentials `OpenAiApi` và model `gpt-4o-mini`.
  - Tùy chỉnh prompt trong node LLM để yêu cầu AI tóm tắt ngắn gọn, làm sạch các thẻ HTML từ bài viết gốc hoặc trích dẫn các điểm nổi bật (rất hữu ích cho trang thương mại điện tử).
- **Generate Speech (`httpRequest`):** 
  - Sử dụng HTTP Request để gọi API của ElevenLabs.
  - Cấu hình Custom Auth header: `{"xi-api-key": "your-elevenlabs-api-key"}`.
  - Thiết lập body request với `model_id` (khuyên dùng `"eleven_multilingual_v2"` cho đa ngôn ngữ) và `output_format` (`"mp3_44100_128"`).
- **Upload MP3 (`httpRequest`):** Gửi file MP3 vừa tạo lên thư viện Media của WordPress.
- **Update WordPress Post (`wordpress`):** Cập nhật lại bài viết gốc (`operation: update`), tự động chèn đường dẫn file audio vào bài viết (ví dụ: gắn vào custom field hoặc cuối bài).

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với một bài viết mẫu trên WordPress.
- Kiểm tra kết quả trên thư viện Media và bài viết trên website của các sếp.
- Sau khi mọi thứ chạy mượt mà, hãy bật **Active** workflow để hệ thống tự động làm việc.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng Trigger:** Thay vì dùng manual trigger, các sếp có thể kết hợp **WordPress Trigger** để tự động tạo audio summary ngay khi có bài viết mới được **Publish**.
- **Lưu trữ backup:** Lưu trữ file MP3 vừa tạo lên Google Drive hoặc AWS S3 để làm tài nguyên riêng cho Podcast.
- **Gửi thông báo:** Thêm node Telegram hoặc Slack để nhận thông báo mỗi khi một bài viết có audio mới được cập nhật thành công.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các nhà sáng tạo nội dung, blogger và các chủ doanh nghiệp E-commerce muốn tối ưu hóa nội dung đa phương tiện mà không mất nhiều nguồn lực. Hãy cài đặt ngay hôm nay để nâng cấp website WordPress của các sếp lên một tầm cao mới!