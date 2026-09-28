---
title: "🎥 Tự động chuyển đổi video dài thành Shorts với RenderIO và OpenAI"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi video dài thành các đoạn ngắn cho TikTok/Reels với n8n, RenderIO và OpenAI Whisper. Tiết kiệm thời gian và tăng hiệu quả nội dung."
slug: "tu-dong-chuyen-doi-video-dai-thanh-shorts"
tags: [n8n, automation, no-code, video-editing, ai-content]
keywords: [n8n workflow, tự động hóa video, RenderIO, OpenAI Whisper, tạo nội dung]
---

# 🎥 Tự động chuyển đổi video dài thành Shorts với RenderIO và OpenAI

[Các sếp] có bao giờ phải ngồi cắt video dài thành các đoạn ngắn cho TikTok/Reels không? Quy trình này tốn thời gian và công sức, đặc biệt khi phải xử lý hàng loạt video. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ tải video lên đến xuất bản các đoạn ngắn hoàn chỉnh - chỉ với vài bước cấu hình đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình từ 30-60 phút xuống còn vài giây
- **Chính xác cao**: Sử dụng AI để chọn các đoạn highlight tự động
- **Đa dạng định dạng**: Xuất ra các định dạng TikTok, Reels và Square
- **Lưu trữ an toàn**: Tất cả file và log đều được lưu trữ trên Google Drive
- **Theo dõi hiệu quả**: Log chi tiết các đoạn video đã xử lý trên Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với folder để lưu video đầu vào và đầu ra
- Tài khoản RenderIO với API key
- Tài khoản OpenAI với API key (cho dịch vụ Whisper)
- Google Sheet để lưu log hoạt động
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15132](https://n8n.io/workflows/15132)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoặc tải file JSON về máy và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Drive Folder Trigger**:
   - Cấu hình credentials Google Drive OAuth2
   - Chỉ định folder cần theo dõi (folder chứa video đầu vào)

2. **Set Configuration Parameters**:
   - Thiết lập các tham số cấu hình:
     - `folderId`: ID của folder đầu ra trên Google Drive
     - `spreadsheetId`: ID của Google Sheet để lưu log
     - `sheetName`: Tên sheet trong Google Sheet
     - `clipCount`: Số lượng đoạn clip cần tạo (mặc định 3)

3. **Upload Video to RenderIO**:
   - Cấu hình credentials RenderIO API

4. **Transcribe Audio with Whisper**:
   - Cấu hình credentials OpenAI API
   - Có thể điều chỉnh model Whisper (mặc định là whisper-1)

5. **Select Clips for Editing**:
   - Có thể điều chỉnh prompt cho OpenAI để phù hợp với nội dung video
   - Ví dụ prompt: "Chọn 3 đoạn highlight từ video này, mỗi đoạn 15-30 giây, tập trung vào các điểm nổi bật về nội dung và cảm xúc"

6. **Append Clip Data to Sheet**:
   - Cấu hình credentials Google Sheets OAuth2
   - Đảm bảo Google Sheet đã có cấu trúc phù hợp (các cột: Video ID, Clip ID, Timestamp, Duration, Format)

#### 3. Kích hoạt ⚡️
1. Test run với một video mẫu nhỏ
2. Kiểm tra tất cả các bước xử lý:
   - Tải video lên RenderIO
   - Trích xuất và chuyển đổi âm thanh
   - Tạo transcript
   - Chọn và render các đoạn clip
   - Tải các đoạn clip về Google Drive
   - Lưu log vào Google Sheet
3. Sau khi test thành công, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành
2. **Xử lý lỗi tự động**: Thêm các node xử lý lỗi và retry khi có vấn đề
3. **Lịch trình chạy**: Thiết lập workflow chạy theo lịch định kỳ thay vì theo dõi folder
4. **Tối ưu hóa clip**: Thêm bước xử lý ảnh để tạo thumbnail đẹp cho các đoạn clip

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình chuyển đổi video dài thành các đoạn ngắn cho các nền tảng mạng xã hội. Với việc tích hợp AI của OpenAI và công cụ xử lý video của RenderIO, các sếp có thể tạo ra nội dung chất lượng cao một cách nhanh chóng và hiệu quả. Hãy thử ngay và tiết kiệm thời gian quý giá của mình!