---
title: "🚀 Tự động tạo Shorts từ Video dài với AI và lên lịch đăng lên MXH"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi video dài thành các đoạn ngắn viral, phân tích nội dung với AI và lên lịch đăng lên TikTok, Instagram và YouTube hoàn toàn không cần code."
slug: "tu-dong-tao-shorts-tu-video-dai-voi-ai-va-len-lich-dang-len-mxh"
tags: [n8n, automation, no-code, content-creation, ai]
keywords: [n8n workflow, tự động hóa nội dung, AI tạo shorts, lên lịch đăng MXH, video dài]
---

# 🚀 Tự động tạo Shorts từ Video dài với AI và lên lịch đăng lên MXH

[Các sếp] có biết rằng mỗi giây của video dài có thể trở thành một đoạn ngắn viral trên MXH? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ việc phân tích nội dung, chọn lọc các đoạn hấp dẫn nhất đến việc tạo và lên lịch đăng lên các nền tảng MXH hàng đầu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình từ 30 phút xuống còn vài giây.
- **Nội dung cá nhân hóa**: AI phân tích và chọn lọc các đoạn hấp dẫn nhất từ video dài.
- **Hoạt động liên tục**: Tự động tạo và lên lịch đăng các shorts hàng ngày.
- **Tối ưu hóa MXH**: Các shorts được tối ưu hóa cho từng nền tảng (TikTok, Instagram, YouTube).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API key (để sử dụng Whisper).
- Tài khoản Google AI Studio API key (để sử dụng Google Gemini).
- Tài khoản trên [app.upload-post.com](https://app.upload-post.com) và API token.
- Video dài cần chuyển đổi (MP4, MOV, AVI...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9867](https://n8n.io/workflows/9867).
2. Nhấn nút "Import" và chọn "Import from URL".
3. Dán URL của workflow vào ô nhập liệu và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Form: Upload Video**
   - Node này tạo form để upload video. Các sếp có thể thay đổi đường dẫn (path) trong tham số "path" nếu cần.

2. **Whisper: Transcribe with Timestamps**
   - Node này sử dụng OpenAI Whisper để chuyển đổi âm thanh thành văn bản.
   - Các sếp cần thêm OpenAI API key vào credentials của node này.

3. **Google Gemini Chat Model**
   - Node này sử dụng Google Gemini để phân tích nội dung và chọn lọc các đoạn hấp dẫn nhất.
   - Các sếp cần thêm Google AI Studio API key vào credentials của node này.

4. **Schedule to TikTok, Instagram, and YouTube**
   - Node này sử dụng Upload-Post API để lên lịch đăng các shorts.
   - Các sếp cần tạo credentials cho node này với API token từ [app.upload-post.com](https://app.upload-post.com).

5. **HTTP Request Nodes (FFmpeg)**
   - Các node này sử dụng FFmpeg để xử lý video. Các sếp cần thêm credentials với API token từ [app.upload-post.com](https://app.upload-post.com).

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình các node, các sếp cần test run workflow với một video mẫu.
2. Nếu mọi thứ hoạt động tốt, các sếp có thể kích hoạt workflow bằng cách nhấn nút "Active" trên giao diện n8n.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh thời gian đăng**: Các sếp có thể thay đổi thời gian đăng trong node "Schedule to TikTok, Instagram, and YouTube".
- **Thêm các nền tảng MXH**: Các sếp có thể thêm các nền tảng MXH khác bằng cách cấu hình thêm trong node "Schedule to TikTok, Instagram, and YouTube".
- **Tối ưu hóa nội dung**: Các sếp có thể điều chỉnh prompt trong node "Google Gemini Chat Model" để phù hợp với phong cách nội dung của mình.
- **Lưu log hoạt động**: Các sếp có thể thêm node để lưu log các hoạt động của workflow.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình từ việc phân tích nội dung, chọn lọc các đoạn hấp dẫn nhất đến việc tạo và lên lịch đăng các shorts lên các nền tảng MXH hàng đầu. Với workflow này, các sếp có thể tiết kiệm thời gian, tạo ra nội dung chất lượng cao và tối ưu hóa hiệu suất đăng bài trên MXH.