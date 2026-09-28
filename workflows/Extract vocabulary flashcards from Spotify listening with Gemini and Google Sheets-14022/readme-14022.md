---
title: "🚀 Tự động trích xuất từ vựng học ngoại ngữ từ Spotify nghe nhạc bằng Google Gemini & n8n"
description: "Biến thói quen nghe nhạc trên Spotify thành flashcard học ngoại ngữ tự động hàng tuần với Google Gemini và Google Sheets mà không tốn công sức."
slug: "tu-dong-trich-xuat-tu-vung-spotify-gemini-google-sheets"
tags: [n8n, automation, no-code, spotify, google-sheets, ai-extraction]
keywords: [n8n workflow, trích xuất từ vựng spotify, học ngoại ngữ bằng ai, google gemini n8n, tự động hóa no-code]
---

# 🚀 Tự động trích xuất từ vựng học ngoại ngữ từ Spotify với Google Gemini & Google Sheets

Các sếp có bao giờ vừa nghe nhạc ngoại ngữ vừa tự hỏi nghĩa của những từ mới, nhưng lại lười tra từ điển hay ghi chép thủ công không? Việc học ngoại ngữ qua bài hát rất hiệu quả nhưng việc tổng hợp từ vựng lại cực kỳ tốn thời gian. 

Đừng lo, workflow n8n này sẽ tự động "bắt" các bài hát các sếp nghe trên Spotify mỗi tuần, lấy lời bài hát, nhờ AI (Google Gemini) chọn lọc từ vựng cấp độ B1-B2, lọc bỏ các từ đã học, và lưu thẳng vào Google Sheets để ôn tập qua app flashcard. Tất cả hoàn toàn tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt là các trigger theo lịch trình hàng tuần), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Hàng tuần tự động quét lịch sử nghe nhạc Spotify, không cần thao tác tay.
- **Học từ thông minh:** Google Gemini chọn lọc 40-60 từ vựng hữu ích (trình độ B1-B2) kèm bản dịch chuẩn xác.
- **Tránh trùng lặp:** Tự động đối chiếu với danh sách từ đã học trước đó, chỉ lưu từ mới.
- **Sẵn sàng ôn tập:** Chia thành tab hàng tuần trên Google Sheets, tương thích hoàn hảo với các app flashcard (như Flashcard Lab) có phương pháp lặp lại ngắt quãng (spaced repetition).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Spotify Developer Dashboard** (để lấy Client ID và Client Secret kết nối node Spotify).
- **Google Cloud Console Project** (để tạo OAuth2 Credentials cho Google Sheets và Google Drive API).
- **Google AI Studio API Key** (để sử dụng Google Gemini Chat Model).
- **lrclib.net API** (API công cộng, không cần tài khoản, dùng để lấy lời bài hát).
- **Một Google Sheet** chuẩn bị sẵn với tab tên `All Vocabularies` và các cột tiêu đề (headers): `Word` và `Translation`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ hệ thống hoặc copy đoạn JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thành phần sau để workflow không gặp lỗi:
- **Node `Get the recently played Songs` (Spotify):** Kết nối tài khoản Spotify của các sếp thông qua OAuth2, chọn operation `recentlyPlayed`.
- **Node `Google Gemini Chat Model` & `AI Agent`:** Điền Google Gemini API Key để AI có thể đọc lời bài hát và phân tích từ vựng.
- **Các node Google Sheets (`Read all Vocabularies`, `Create sheet`, `Append to Weekly`, `Append to All Vocabularies`):** Kết nối tài khoản Google Sheets của các sếp và trỏ chính xác đến file Google Sheet đã tạo sẵn.
- **Lưu ý quan trọng về Google Cloud:** Hãy chắc chắn app Google Cloud của các sếp được để ở trạng thái **"In Production"**. Nếu để ở chế độ **"Testing"**, token sẽ hết hạn sau 7 ngày và làm hỏng chu kỳ chạy tự động hàng tuần!

#### 3. Kích hoạt ⚡️
- Chạy thử công thủ công bằng cách bấm nút **"Execute Workflow"** để kiểm tra luồng chạy từ Spotify -> LrcLib -> Gemini -> Google Sheets.
- Nếu dữ liệu đổ về Sheet mượt mà, hãy bật nút **"Active"** ở góc trên cùng bên phải để node `Every Sunday at noon` tự động làm việc mỗi tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào cuối workflow để nhận tin nhắn thông báo mỗi khi hệ thống tạo xong bộ flashcard tuần mới.
- **Tùy chỉnh ngôn ngữ học:** Sửa prompt trong phần AI Agent để yêu cầu Gemini trích xuất từ vựng tiếng Tây Ban Nha, tiếng Đức, hoặc tiếng Nhật thay vì mặc định.
- **Lưu trữ Log lỗi:** Thêm một nhánh Error Trigger để gửi email hoặc thông báo khi tài khoản Spotify hoặc Google Sheets gặp sự cố kết nối.

### 📌 Kết luận
Biến chiếc tai nghe thành công cụ học ngoại ngữ đỉnh cao chưa bao giờ dễ dàng đến thế. Hãy import workflow này ngay hôm nay và bắt đầu tích lũy từ vựng một cách thụ động nhưng cực kỳ hiệu quả các sếp nhé!