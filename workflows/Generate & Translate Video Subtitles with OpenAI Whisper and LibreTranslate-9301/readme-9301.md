---
title: "🚀 Tự Động Tạo và Dịch Phụ Đề Video với OpenAI Whisper và LibreTranslate trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo file phụ đề SRT từ URL video bằng OpenAI Whisper (local) và dịch đa ngôn ngữ qua LibreTranslate."
slug: "tu-dong-tao-va-dich-phu-de-video-whisper-libretranslate-n8n"
tags: [n8n, automation, ai, openai-whisper, libretranslate, video-subtitles]
keywords: [n8n workflow, tạo phụ đề tự động, openai whisper local, libretranslate, dịch phụ đề video, ffmpeg n8n]
---

# 🚀 Tự Động Tạo và Dịch Phụ Đề Video với OpenAI Whisper và LibreTranslate

Các sếp làm sáng tạo nội dung (Content Creator), đội ngũ Marketing hay EdTech chắc chắn hiểu rõ nỗi đau: mỗi khi sản xuất một video mới, việc ngồi nghe lại, gõ từng câu làm phụ đề (subtitle) và sau đó dịch sang các ngôn ngữ khác ngốn hàng giờ đồng hồ. Nếu thuê ngoài thì chi phí đội lên đáng kể mà tiến độ lại chậm.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa **100%** quy trình: Nhận URL video, tách âm thanh, dùng **OpenAI Whisper** để trans-script thành file `.srt` cực kỳ chuẩn xác, sau đó dịch sang ngôn ngữ mong muốn bằng **LibreTranslate** và gửi kết quả qua email cho các sếp. Hoàn toàn tự động, không tốn một xu phí API đắt đỏ nhờ chạy cục bộ (local)!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các file video nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nghe - chép - dịch thủ công từng video dài.
- **Độ chính xác cao:** Sử dụng AI Whisper của OpenAI giúp nhận diện giọng nói siêu chuẩn, kể cả tiếng ồn nền.
- **Đa ngôn ngữ linh hoạt:** Dễ dàng dịch file phụ đề sang nhiều ngôn ngữ khác nhau thông qua LibreTranslate.
- **Vận hành tự động 24/7:** Chỉ cần gửi Webhook chứa URL video, hệ thống tự lo phần còn lại và trả kết quả về Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Vì workflow này cần thao tác với hệ thống máy chủ (chạy lệnh CLI), các sếp cần chuẩn bị:
1. **n8n Self-hosted:** Bắt buộc (vì cloud của n8n không cho phép chạy lệnh terminal cục bộ).
2. **FFmpeg:** Đã được cài đặt sẵn trên server n8n để tách âm thanh từ video.
3. **OpenAI Whisper (Python package):** Cài đặt trên server để chuyển giọng nói thành văn bản.
4. **LibreTranslate API / Instance:** Dùng để dịch thuật nội dung phụ đề.
5. **Gmail Credentials:** Để cấu hình node gửi email nhận file `.srt` hoàn chỉnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần chú ý các node quan trọng sau:

- **Webhook Trigger:** Điểm khởi đầu nhận yêu cầu. Sếp cấu hình đường dẫn `path` (ví dụ: `generate-subtitles`) và phương thức `POST`. Khi gọi webhook này, hãy truyền một JSON chứa URL video.
- **Download Video (HTTP Request):** Node này sẽ tải video từ URL mà webhook truyền vào và lưu tạm dưới dạng binary.
- **Extract Audio (FFmpeg) & Run Whisper (Local) (Execute Command):** 
  - Đảm bảo server n8n đã cài đặt `ffmpeg` và lệnh `whisper`. 
  - Kiểm tra đường dẫn thực thi lệnh (PATH) trong node Execute Command để đảm bảo n8n gọi đúng các công cụ này trên hệ điều hành Linux của VPS.
- **Translate Subtitles (LibreTranslate) (HTTP Request):** Cấu hình endpoint của LibreTranslate (sếp có thể dùng bản public API hoặc tự host một instance riêng tư để miễn phí và bảo mật).
- **Send a message (Gmail):** Kết nối tài khoản Gmail cá nhân/doanh nghiệp thông qua `gmailOAuth2` để nhận file phụ đề `.srt` gốc và file đã dịch ngay trong hộp thư đến.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test Step** từng node để kiểm tra luồng truyền dữ liệu từ Video URL $\rightarrow$ File SRT $\rightarrow$ File Dịch $\rightarrow$ Gmail.
- Bật công tắc **Active** góc trên cùng bên phải để đưa workflow vào trạng thái hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận file:** Thay vì dùng Gmail, các sếp có thể đổi node cuối thành **Slack**, **Telegram** hoặc **Google Drive** để tự động lưu file `.srt` vào thư mục dự án chung của team.
- **Xử lý hàng loạt (Batch Processing):** Kết hợp thêm Google Sheets hoặc Airtable để ném vào một danh sách hàng trăm link video, n8n sẽ tự động xếp hàng (queue) và xử lý lần lượt mà không sợ sập server.
- **Tùy biến ngôn ngữ:** Thêm một biến `target_language` vào Webhook Trigger để người gọi có thể chủ động chọn ngôn ngữ muốn dịch (Anh, Hàn, Nhật, Trung...) tùy ý.

### 📌 Kết luận
Tự động hóa quy trình làm phụ đề video chưa bao giờ dễ dàng và tối ưu chi phí đến thế. Thay vì tốn nhân lực cho những công việc lặp đi lặp lại, hãy để AI và n8n làm thay bạn. Lên đồ ngay thôi các sếp ơi!