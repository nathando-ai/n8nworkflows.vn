---
title: "🎬 Tự động hóa dịch video Google Drive sang phụ đề tiếng Nhật với AssemblyAI và Gemini"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình dịch video từ tiếng Anh sang tiếng Nhật, tạo phụ đề tự nhiên và render video hoàn chỉnh chỉ với n8n"
slug: "tu-dong-hoa-dich-video-google-drive-sang-phu-de-tieng-nhat"
tags: [n8n, automation, no-code, video-processing, google-drive, assemblyai, gemini, creatomate]
keywords: [n8n workflow, tự động hóa video, dịch phụ đề, google drive, assemblyai, gemini, creatomate]
---

# 🎬 Tự động hóa dịch video Google Drive sang phụ đề tiếng Nhật với AssemblyAI và Gemini

[Các sếp đang gặp khó khăn khi phải thủ công xử lý video: tải xuống, transcribe, dịch, tạo phụ đề và render. Quy trình này tốn thời gian, dễ sai sót và không thể mở rộng. Workflow này giúp tự động hóa hoàn toàn quy trình từ A đến Z chỉ với n8n.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian xử lý video thủ công
- Tạo phụ đề tiếng Nhật tự nhiên với Gemini AI
- Tự động render video hoàn chỉnh với Creatomate
- Nhận thông báo Slack ngay khi video đã sẵn sàng
- Xử lý hàng loạt video mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với video cần xử lý
- Google Sheet chứa danh sách video URL
- Tài khoản AssemblyAI (API Key)
- Tài khoản Google Gemini (API Key)
- Tài khoản Creatomate (API Key)
- Tài khoản Slack (Webhook)
- Kiến thức cơ bản về n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/16139](https://n8n.io/workflows/16139)
2. Chọn "Import" và dán JSON vào n8n Editor
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger: Watch New Video Rows** (googleSheetsTrigger)
   - Cấu hình Google Sheets OAuth2
   - Chỉ định sheet và phạm vi dữ liệu cần theo dõi

2. **Prepare: Convert Drive Share URL to Download URL** (set)
   - Đảm bảo URL video trong Google Drive được chia sẻ công khai

3. **Transcribe: Submit to AssemblyAI** (httpRequest)
   - Cấu hình AssemblyAI HTTP Header Auth
   - Điền API endpoint của AssemblyAI

4. **Model: Gemini Translation** (lmChatGoogleGemini)
   - Cấu hình Google Palm API
   - Tùy chỉnh prompt cho kết quả dịch phù hợp

5. **Render: Combine Video and Subtitle Timeline** (httpRequest)
   - Cấu hình Creatomate HTTP Header Auth
   - Điền template ID và các tham số render

6. **Notify: Send Video Link to Slack** (slack)
   - Cấu hình Slack OAuth2
   - Chỉ định channel nhận thông báo

#### 3. Kích hoạt ⚡️
1. Test run với video mẫu
2. Kiểm tra từng bước xử lý
3. Bật Active workflow sau khi đã cấu hình xong

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm bước xử lý video portrait/landscape tự động
2. Kết hợp với Notion để lưu trữ thông tin video
3. Tạo báo cáo định kỳ về tiến độ xử lý
4. Thêm bước kiểm tra nội dung nhạy cảm trước khi render

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình dịch video từ tiếng Anh sang tiếng Nhật, tạo phụ đề tự nhiên và render video hoàn chỉnh chỉ với n8n. Với kết quả chính xác và hiệu quả, các sếp có thể tập trung vào nội dung sáng tạo thay vì công việc lặp lại. Hãy thử ngay và tiết kiệm thời gian quý giá!