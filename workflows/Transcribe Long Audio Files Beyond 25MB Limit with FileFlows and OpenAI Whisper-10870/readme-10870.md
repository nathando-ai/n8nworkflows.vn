---
title: "🎧 [Hướng dẫn tự động hóa] Chuyển đổi âm thanh dài hơn 25MB sang văn bản với FileFlows và OpenAI Whisper"
description: "Hướng dẫn chi tiết cách tự động chuyển đổi âm thanh dài (hơn 20 phút) sang văn bản bằng n8n, vượt qua giới hạn 25MB của OpenAI Whisper"
slug: "chuyen-doi-am-thanh-dai-sang-van-ban-fileflows-openai-whisper"
tags: [n8n, automation, no-code, audio, transcription, ai]
keywords: [n8n workflow, tự động hóa âm thanh, chuyển đổi âm thanh, OpenAI Whisper, FileFlows]
---

# 🎧 [Hướng dẫn tự động hóa] Chuyển đổi âm thanh dài hơn 25MB sang văn bản với FileFlows và OpenAI Whisper

[Các sếp đang gặp khó khăn khi phải chuyển đổi các file âm thanh dài (hơn 20 phút) sang văn bản thủ công. OpenAI Whisper có giới hạn 25MB, tương đương khoảng 20 phút âm thanh. Workflow này giúp các sếp vượt qua giới hạn này bằng cách chia nhỏ file âm thanh, chuyển đổi từng phần và hợp nhất kết quả.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi âm thanh dài thành văn bản hoàn chỉnh
- Vượt qua giới hạn 25MB của OpenAI Whisper
- Tiết kiệm thời gian xử lý thủ công
- Nhận kết quả đầy đủ qua email
- Hỗ trợ nhiều định dạng âm thanh
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key
- Tài khoản Gmail với quyền truy cập OAuth2
- FileFlows đã cài đặt và cấu hình
- FFmpeg đã cài đặt trên hệ thống
- Thư mục lưu trữ tạm thời (/media/segments/)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10870](https://n8n.io/workflows/10870)
2. Nhấn nút "Import" để tải workflow về máy
3. Trong n8n Editor, nhấn "Import from File" và chọn file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Configuration**:
   - **FileFlows Connection**:
     - Cập nhật URL của FileFlows trong node "Configuration"
     - Đặt đúng Flow UID từ FileFlows
     - Đảm bảo FileFlows có thể truy cập từ n8n

   - **OpenAI Credentials**:
     - Thêm OpenAI API key vào credentials
     - Gán credentials này cho node "OpenAI"

   - **Gmail Credentials**:
     - Cấu hình Gmail OAuth2 credentials
     - Gán credentials này cho tất cả các node email

   - **Ngôn ngữ (Tùy chọn)**:
     - Mặc định: Tiếng Pháp (fr)
     - Thay đổi trong tham số của node OpenAI
     - Hoặc bỏ trống để tự động phát hiện ngôn ngữ

2. **FileFlows Setup**:
   - Import workflow FileFlows từ [đây](https://github.com/JulienDelRio/My-Interesting-n8n-Workflows/blob/main/Full%20audio%20transcription%20with%20FileFlows%20and%20OpenAI/FileFlows%20-%20Split%20audio%20for%20n8n.json)
   - Cài đặt FFmpeg
   - Cấu hình thư mục lưu trữ tạm thời (/media/segments/)

#### 3. Kích hoạt ⚡️
1. Test run với file âm thanh mẫu
2. Kiểm tra kết quả chuyển đổi
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo khi quá trình hoàn thành
- Lưu log các quá trình chuyển đổi vào Google Sheets
- Tự động xóa các file tạm thời sau khi hoàn thành
- Tích hợp với Google Drive để lưu trữ file âm thanh và kết quả

### 📌 Kết luận
Workflow này giúp các sếp tự động chuyển đổi âm thanh dài thành văn bản một cách hiệu quả, vượt qua giới hạn của OpenAI Whisper. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao năng suất làm việc!