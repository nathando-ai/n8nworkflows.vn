---
title: "🎥 Tự động hóa chuyển đổi YouTube thành tài liệu Google Docs với AI Gemini"
description: "Hướng dẫn tự động hóa chuyển đổi video YouTube thành bản dịch và tóm tắt bằng AI Gemini, lưu vào Google Docs - tiết kiệm 90% thời gian biên soạn nội dung"
slug: "tu-dong-hoa-chuyen-doi-youtube-google-docs-voi-gemini"
tags: [n8n, automation, no-code, youtube, google-docs, ai, gemini]
keywords: [n8n workflow, tự động hóa nội dung, youtube transcription, google docs, gemini ai]
---

# 🎥 Tự động hóa chuyển đổi YouTube thành tài liệu Google Docs với AI Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 90% thời gian biên soạn nội dung từ video YouTube
- Tự động chuyển đổi video thành văn bản đầy đủ với độ chính xác cao
- Tóm tắt và dịch nội dung sang nhiều ngôn ngữ một cách nhanh chóng
- Lưu trữ kết quả vào Google Docs với định dạng chuyên nghiệp
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Gemini được kích hoạt
- Quyền truy cập Google Docs API
- API Key từ Supadata cho dịch vụ transcribe YouTube
- Tài khoản n8n đã được cấu hình với các credentials trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Trigger YouTube Processing Request**: Cấu hình webhook với path `/youtube` và method POST
- **Google Gemini To Summarize and Translate Text**: Cần cấu hình credentials `googlePalmApi` với API Key của Gemini
- **Transcribe YouTube Video**: Cần cấu hình API Key từ Supadata
- **Create Output Document** và **Append Summary and Translation**: Cần cấu hình credentials `googleDocsOAuth2Api` với quyền truy cập Google Docs

#### 3. Kích hoạt ⚡️
- Test run với URL video YouTube mẫu
- Kiểm tra kết quả trong Google Docs đã tạo
- Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi quá trình hoàn thành
- Lưu log các phiên dịch để theo dõi chất lượng
- Tự động gửi báo cáo định kỳ về số lượng video đã xử lý
- Kết hợp với Notion để quản lý các tài liệu đã tạo

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc chuyển đổi nội dung video thành tài liệu có thể sử dụng được. Với sự kết hợp của AI Gemini và Google Docs, các sếp có thể tự động hóa toàn bộ quy trình từ transcribe đến dịch thuật, tạo ra tài liệu chuyên nghiệp một cách nhanh chóng và chính xác.