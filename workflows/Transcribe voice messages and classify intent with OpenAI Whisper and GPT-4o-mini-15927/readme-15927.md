---
title: "🎙️ Tự động hóa chuyển đổi giọng nói thành văn bản và phân loại ý định với OpenAI Whisper và GPT-4o-mini"
description: "Hướng dẫn chi tiết cách tự động chuyển đổi giọng nói thành văn bản và phân loại ý định sử dụng công nghệ Whisper và GPT-4o-mini của OpenAI, giúp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-hoa-chuyen-doi-giong-noi-thanh-van-ban-va-phan-loai-y-dinh"
tags: [n8n, automation, no-code, AI, OpenAI, Whisper, GPT-4o-mini]
keywords: [n8n workflow, tự động hóa, chuyển đổi giọng nói, phân loại ý định, OpenAI Whisper, GPT-4o-mini]
---

# 🎙️ Tự động hóa chuyển đổi giọng nói thành văn bản và phân loại ý định với OpenAI Whisper và GPT-4o-mini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý tin nhắn thoại lên đến 90%
- Tự động phân loại ý định khách hàng (chào hỏi, câu hỏi, yêu cầu, khác)
- Tăng độ chính xác trong xử lý tin nhắn thoại
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tích hợp dễ dàng với các nền tảng tin nhắn phổ biến
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key (để sử dụng Whisper và GPT-4o-mini)
- URL của file âm thanh cần xử lý (có thể từ các nền tảng như Evolution API, Twilio, WhatsApp Cloud API...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/15927](https://n8n.io/workflows/15927)
3. Hoặc tải file JSON về và import từ máy tính của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When clicking ‘Execute workflow’" (manualTrigger)**:
   - Thay đổi URL âm thanh mẫu (JFK) thành URL của file âm thanh thực tế bạn muốn xử lý

2. **Node "Whisper Transcription1" (openAi)**:
   - Thêm credentials OpenAI API
   - Đảm bảo bạn đã kích hoạt dịch vụ Whisper trong tài khoản OpenAI

3. **Node "Intent Classifier" (openAi)**:
   - Thêm credentials OpenAI API
   - Đảm bảo bạn đã kích hoạt dịch vụ GPT-4o-mini trong tài khoản OpenAI

4. **Các node Response (Response - Greeting, Response - Question, Response - Request, Response - Others)**:
   - Tùy chỉnh các phản hồi phù hợp với nhu cầu của bạn cho từng loại ý định

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với các dịch vụ bên ngoài (nếu có)
2. Thực hiện test run với dữ liệu mẫu
3. Bật Active workflow để bắt đầu xử lý tin nhắn thoại tự động

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack hoặc Telegram để nhận thông báo khi có tin nhắn thoại mới
2. Lưu log các phiên xử lý vào Google Sheets hoặc cơ sở dữ liệu để theo dõi hiệu suất
3. Tự động gửi báo cáo hàng ngày về các loại tin nhắn thoại được nhận và xử lý
4. Tích hợp với hệ thống CRM để tự động cập nhật thông tin khách hàng từ tin nhắn thoại

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa chuyển đổi giọng nói thành văn bản và phân loại ý định, giúp doanh nghiệp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. Hãy thử ngay và trải nghiệm sức mạnh của tự động hóa với n8n!