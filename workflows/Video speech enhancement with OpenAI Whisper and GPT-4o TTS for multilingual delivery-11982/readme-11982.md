---
title: "🎤 Tự động hóa tạo video đa ngôn ngữ với Whisper và GPT-4o TTS"
description: "Hướng dẫn tự động hóa tạo video đa ngôn ngữ từ file âm thanh sử dụng OpenAI Whisper và GPT-4o TTS, tiết kiệm 80% thời gian xử lý thủ công"
slug: "tu-dong-hoa-tao-video-da-ngon-ngu-voi-whisper-gpt4o-tts"
tags: [n8n, automation, no-code, video-processing, ai-content-creation]
keywords: [n8n workflow, tự động hóa video, OpenAI Whisper, GPT-4o TTS, đa ngôn ngữ]
---

# 🎤 Tự động hóa tạo video đa ngôn ngữ với Whisper và GPT-4o TTS

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian xử lý video đa ngôn ngữ
- Tự động chuyển đổi âm thanh thành văn bản và ngược lại
- Hỗ trợ 100+ ngôn ngữ thông qua OpenAI
- Tích hợp hoàn hảo với hệ thống lưu trữ FTP/SSH
- Thông báo kết quả qua Telegram ngay lập tức
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key (Whisper và GPT-4o TTS)
- Thông tin kết nối FTP/SSH để lưu trữ file
- Tài khoản Google Drive (tùy chọn)
- Bot Telegram và chat ID để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/11982)
2. Click "Copy JSON" và paste vào n8n Editor
3. Hoặc tải file JSON về máy và import trực tiếp

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Attach files2" (formTrigger)**:
   - Cấu hình form để upload file âm thanh (MP3, WAV, FLAC)
   - Đặt tên trường input là "audioFile"

2. **Node "C3" (set)**:
   - Thiết lập các biến môi trường:
     - `OPENAI_API_KEY`: API key của OpenAI
     - `FTP_HOST`, `FTP_USER`, `FTP_PASSWORD`: Thông tin kết nối FTP
     - `SSH_HOST`, `SSH_USER`, `SSH_PASSWORD`: Thông tin kết nối SSH

3. **Node "S", "S1", "S2", "S4", "S5", "S6" (ftp)**:
   - Cấu hình credentials FTP với thông tin từ node "C3"
   - Thiết lập đường dẫn lưu trữ file theo nhu cầu

4. **Node "E", "E1", "T" (ssh)**:
   - Cấu hình credentials SSH với thông tin từ node "C3"
   - Thiết lập các lệnh SSH cần thiết cho quá trình xử lý

5. **Node "W", "O" (httpRequest)**:
   - Đảm bảo các endpoint API hoạt động
   - Kiểm tra headers và authentication

6. **Node "A" (openAi)**:
   - Cấu hình credentials OpenAI với API key
   - Thiết lập các tham số cho Whisper và GPT-4o TTS

7. **Node "S7" (telegram)**:
   - Cấu hình bot Telegram với token và chat ID
   - Thiết lập template thông báo

#### 3. Kích hoạt ⚡️
1. Test run với file âm thanh mẫu
2. Kiểm tra kết quả chuyển đổi và lưu trữ
3. Bật Active workflow khi đã kiểm tra thành công

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "googleDrive" để lưu trữ backup file
- Kết hợp với Slack để nhận thông báo
- Thiết lập lịch chạy định kỳ cho các file mới
- Tích hợp với hệ thống quản lý nội dung (CMS) để tự động cập nhật video
- Sử dụng node "limit" để quản lý số lượng xử lý đồng thời

### 📌 Kết luận
Workflow này giúp tự động hóa hoàn toàn quá trình tạo video đa ngôn ngữ từ file âm thanh, tiết kiệm thời gian đáng kể và đảm bảo chất lượng nội dung. Các sếp có thể tùy chỉnh theo nhu cầu cụ thể của doanh nghiệp để tối ưu hóa quy trình sản xuất nội dung đa phương tiện.