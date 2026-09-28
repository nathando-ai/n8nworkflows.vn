---
title: "🚀 Tạo Giọng Đọc AI Tự Nhiên với Google Text-to-Speech, Google Drive & Airtable trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa chuyển đổi văn bản thành giọng nói AI siêu thực với Google TTS Chirp 3 HD, lưu trữ Google Drive và quản lý dữ liệu trên Airtable."
slug: "tao-giong-doc-ai-tu-nhien-google-tts-drive-airtable"
tags: [n8n, automation, google-tts, airtable, google-drive, ai-voiceover]
keywords: [n8n workflow, google text to speech, tạo giọng đọc ai, chuyển văn bản thành giọng nói, ai voiceover n8n]
---

# 🚀 Tạo Giọng Đọc AI Tự Nhiên với Google Text-to-Speech, Google Drive & Airtable

Các sếp đang làm nội dung số, video ngắn, podcast hay bài viết blog chắc chắn đều hiểu cảm giác "đau đầu" khi phải tốn hàng giờ thu âm giọng đọc hoặc chi tiền cho các dịch vụ lồng tiếng đắt đỏ. Việc làm thủ công này vừa tốn thời gian, khó cá nhân hóa hàng loạt, lại cực kỳ bất tiện khi cần thay đổi kịch bản phút chót.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), giúp các sếp biến mọi văn bản thành giọng đọc AI siêu thực (sử dụng công nghệ Chirp 3 HD của Google), tự động lưu file vào Google Drive, đo độ dài file và lưu trữ toàn bộ thông tin vào Airtable một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thu âm thủ công, chỉ cần nhập kịch bản qua Form và nhận lại file âm thanh hoàn chỉnh.
- **Giọng đọc AI chất lượng cao:** Khai thác sức mạnh của Google Text-to-Speech (Chirp 3 HD) với ngữ điệu tự nhiên, hỗ trợ ngắt nghỉ linh hoạt bằng thẻ lệnh.
- **Tự động hóa toàn diện:** File audio tự động lưu vào Google Drive, tự động tính toán thời lượng file qua `fal.ai` và đồng bộ mọi thông tin vào Airtable để dễ dàng quản lý.
- **Hoạt động liên tục 24/7:** Chạy ngầm ổn định trên hệ thống tự động hóa của n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Cloud Account** với OAuth2 Client và đã bật **Text-to-Speech API**.
- **Google Drive Account** để lưu trữ các file audio được tạo ra.
- **Tài khoản `fal.ai`** để sử dụng dịch vụ FFmpeg API tính thời lượng file audio.
- **Airtable Account** tạo sẵn một Table chứa các trường tương ứng (Script, Audio Link, Duration,...) để ghi nhận dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó vào giao diện n8n Editor, chọn **Add workflow** -> Dán (Paste) trực tiếp vào bảng làm việc hoặc Import file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình kỹ các node sau:
- **On form submission2 (`formTrigger`):** Node khởi chạy bằng giao diện Form. Các sếp có thể tùy chỉnh các trường nhập kịch bản (Script), chọn ngôn ngữ và giọng đọc (Chirp 3 HD voices). *Lưu ý: Có thể thay thế node này bằng Webhook, Google Sheets trigger tùy nhu cầu.*
- **Request TTS (`httpRequest`):** Node gửi yêu cầu đến Google Text-to-Speech API. Cần cấu hình **Google OAuth2 API credentials** và đảm bảo Google Cloud Project đã bật dịch vụ TTS.
- **Convert to File (`convertToFile`):** Chuyển đổi chuỗi dữ liệu Base64 nhận từ Google API thành file nhị phân (Binary audio file) chuẩn xác trước khi đẩy lên Drive.
- **Upload file (`googleDrive`):** Kết nối tài khoản Google Drive qua **Google Drive OAuth2 API** để chọn thư mục đích lưu trữ file audio.
- **Request Duration / Get Status / Get Duration (`httpRequest`):** Nhóm node gọi API của `fal.ai` để phân tích thời lượng file audio (sử dụng hệ thống hàng đợi - queue system, kết hợp node **If** và **Wait** để kiểm tra trạng thái hoàn thành).
- **Create a record (`airtable`):** Kết nối **Airtable Token API**, trỏ tới Base và Table tương ứng để lưu log gồm kịch bản, link file Google Drive và độ dài audio.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form mẫu để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công và không báo lỗi, hãy bật nút **Active** ở góc trên bên phải để workflow chính thức hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bot gửi thông báo ngay lập tức về máy khi file audio đã được tạo và lưu thành công.
- **Mẹo tối ưu giọng đọc:** Tận dụng tính năng Pause Control của Google TTS Chirp 3 HD bằng các thẻ lệnh trong kịch bản như `[pause short]`, `[pause long]`, hoặc `[pause]` để giọng đọc có nhịp điệu tự nhiên như người thật.
- **Mở rộng nguồn dữ liệu:** Thay vì dùng Form Trigger thủ công, các sếp có thể đổi thành Google Sheets Trigger để tự động tạo hàng loạt file audio từ một danh sách bài viết có sẵn.

### 📌 Kết luận
Workflow tạo giọng đọc AI kết hợp Google TTS, Google Drive và Airtable này là một "vũ khí" cực kỳ lợi hại cho các nhà sáng tạo nội dung và doanh nghiệp muốn tối ưu hóa quy trình sản xuất media. Hãy cài đặt ngay hôm nay để tiết kiệm hàng đống thời gian và nâng tầm chất lượng sản phẩm số của các sếp!