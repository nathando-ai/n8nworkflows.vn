---
title: "🚀 Tự động hóa tạo giọng đọc AI (Voiceover) từ kịch bản với Google Gemini TTS & Google Drive"
description: "Biến kho kịch bản video trên Google Sheets thành file âm thanh chuyên nghiệp tự động 100% bằng Gemini TTS, xử lý qua FFmpeg và lưu trữ trực tiếp lên Google Drive."
slug: "tao-giong-doc-ai-gemini-tts-google-drive"
tags: [n8n, automation, ai-voiceover, google-gemini, google-drive, ffmpeg]
keywords: [n8n workflow, gemini tts, text to speech, tu dong hoa giong doc, tao voiceover ai, google sheets to audio]
---

# 🚀 Tự động hóa tạo giọng đọc AI (Voiceover) từ kịch bản với Google Gemini TTS & Google Drive

Các sếp có đang đau đầu vì tốn quá nhiều thời gian thuê voice-talent hoặc tự ngồi thu âm hàng chục kịch bản video quảng cáo mỗi ngày? Việc sản xuất nội dung video hàng loạt đòi hỏi lượng tài nguyên âm thanh khổng lồ, và làm thủ công thì cực kỳ tốn thời gian.

Workflow n8n này chính là mảnh ghép cuối cùng trong chuỗi "AI Content Factory" của các sếp. Nó tự động hóa toàn bộ quy trình: đọc kịch bản từ Google Sheets, gọi API Gemini Text-to-Speech (TTS) để tạo giọng đọc, sử dụng FFmpeg xử lý định dạng âm thanh, lưu trữ vào Google Drive và cập nhật ngược lại link file vào bảng quản lý. Hoàn toàn tự động, không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và hỗ trợ xử lý file cục bộ (FFmpeg, Read/Write Disk), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến danh sách kịch bản dạng chữ thành một thư mục chứa file âm thanh sẵn sàng dựng video.
- **Chất lượng AI cao cấp:** Tận dụng sức mạnh từ Google Gemini TTS với khả năng tùy chỉnh giọng đọc, ngữ điệu và sắc thái linh hoạt.
- **Quy trình khép kín:** Tự động lọc các kịch bản chưa xử lý, tạo file chuẩn `.wav`, lưu Drive và đồng bộ trạng thái tránh trùng lặp.
- **Tiết kiệm chi phí nhân sự:** Cắt giảm hoàn toàn thời gian thu âm và quản lý file thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Self-hosted n8n Instance:** Workflow này sử dụng các node thao tác ổ cứng (`Read/Write Files`) và chạy lệnh (`Execute Command`), do đó **không hoạt động trên n8n Cloud**.
- **Cài đặt FFmpeg:** Máy chủ chạy n8n phải được cài sẵn [FFmpeg](https://ffmpeg.org/download.html) để convert file âm thanh sang định dạng tiêu chuẩn.
- **Google Gemini API Key:** Dùng để gọi dịch vụ Text-to-Speech.
- **Tài khoản Google:** Kết nối Google Sheets (chứa kịch bản) và Google Drive (lưu file audio).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình kỹ các node sau:

- **Node "Getting Video Scripts" (Google Sheets):** 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Dán URL của Google Sheet chứa kịch bản video (được tạo từ workflow tiền nhiệm). Node **Filter** sẽ tự động lọc ra các dòng chưa có file voiceover.
- **Node "HTTP Request To Generate Voice" (HTTP Request):**
  - Vào phần **Query Parameters**, thay thế đoạn `INSERT YOUR API KEY HERE` bằng Google Gemini API Key chính thức của các sếp.
  - Trong **JSON Body**, các sếp có thể tùy chỉnh prompt, đổi ngữ điệu hoặc giọng đọc theo ý muốn.
- **Node "Read/Write Files from Disk" (Đọc/Ghi file cục bộ):**
  - **Lưu ý quan trọng:** Chỉ áp dụng cho n8n Self-hosted.
  - Cập nhật trường **File Name** thành một đường dẫn thư mục thực tế trên máy chủ n8n có quyền ghi file (Ví dụ: `/home/n8n/audio/` hoặc `C:\n8n\audio\`).
- **Node "Uploading Wav File" (Google Drive):**
  - Kết nối tài khoản Google Drive và chọn thư mục cụ thể để lưu trữ các file `.wav` xuất ra nhằm dễ quản lý.
- **Node "Uploading Google Drive Link of File To Google Sheet" (Google Sheets):**
  - Đảm bảo trỏ đúng vào file Google Sheet ban đầu. Node này sẽ tự động cập nhật link Google Drive vào bảng và đánh dấu trạng thái hoàn thành để tránh xử lý lặp lại.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử với một vài bản ghi mẫu, kiểm tra thư mục ổ cứng và Google Drive xem file `.wav` đã xuất chuẩn chưa.
- Sau khi test thành công, bật công tắc **Active** để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào cuối chuỗi để nhận thông báo ngay khi toàn bộ kịch bản được chuyển đổi thành công sang âm thanh.
- **Kết nối dựng video tự động:** Lấy link file audio từ Google Drive để đẩy tiếp vào các workflow dựng video tự động (như Shotcut, Premiere API hoặc các công cụ AI Video generation khác).
- **Quản lý lỗi thông qua Log:** Lưu các bản ghi lỗi vào một Sheet riêng nếu Google Gemini API gặp sự cố hoặc kịch bản quá dài.

### 📌 Kết luận
Workflow tạo giọng đọc AI với Gemini TTS và Google Drive là mảnh ghép hoàn hảo giúp tự động hóa toàn bộ dây chuyền sản xuất content video của doanh nghiệp. Hãy thiết lập ngay hôm nay để giải phóng thời gian và tăng tốc độ phủ sóng nội dung của các sếp!