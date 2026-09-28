---
title: "🚀 Chuyển Văn Bản Thành Giọng Nói Với Kokoro TTS Cục Bộ"
description: "Tự động chuyển đổi bất kỳ đoạn văn bản nào thành file âm thanh MP3 bằng Kokoro TTS chạy trên máy chủ của bạn – không cần dịch vụ cloud, không mất phí."
slug: "chuyen-van-ban-thanh-giong-noi-kokoro-tts"
tags: [n8n, automation, no-code, AI, text-to-speech, python]
keywords: [n8n workflow, tự động hóa, chuyển văn bản thành giọng nói, Kokoro TTS, python script]
---

# 🚀 Chuyển Văn Bản Thành Giọng Nói Với Kokoro TTS Cục Bộ

Trong môi trường doanh nghiệp, việc tạo file âm thanh từ nội dung văn bản thường phải dựa vào các dịch vụ cloud trả phí, chậm trễ và phụ thuộc vào kết nối internet. Khi phải thực hiện hàng chục, hàng trăm lần mỗi ngày, công việc này trở nên **tiêu tốn thời gian, tốn kém và không ổn định**.

**Workflow “Convert Text to Speech with Local KOKORO TTS”** chính là giải pháp **tự động 100%**, chạy hoàn toàn trên server nội bộ của bạn, không cần code, không cần API bên ngoài. Chỉ cần đưa đoạn text vào, workflow sẽ:
1. Định dạng và truyền biến cho script Python.
2. Gọi Kokoro TTS để sinh file âm thanh MP3.
3. Đọc file âm thanh và phát ngay trong n8n (hoặc gửi tới các kênh khác).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chỉ cần một click, văn bản thành âm thanh trong vài giây.  
- **Chi phí gần bằng 0**: Không phải trả phí dịch vụ TTS cloud.  
- **Độ chính xác & giọng nói tùy chỉnh**: Kokoro TTS cho phép chọn ngôn ngữ, tốc độ, giọng nam/nữ.  
- **Hoạt động liên tục**: Không phụ thuộc internet, chạy trên server nội bộ 24/7.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Python 3.8+** được cài trên máy chủ chạy n8n.  
- **Kokoro TTS** (binary hoặc pip package) đã được cài và có thể gọi từ dòng lệnh.  
- Thư mục lưu trữ tạm thời cho file âm thanh (ví dụ: `/tmp/tts-output`).  
- Quyền thực thi cho script Python (`chmod +x`).  
- (Tùy chọn) Node **Read Binary Files** cần quyền đọc thư mục trên.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file `Convert_Text_to_Speech_with_Local_KOKORO_TTS.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import** → Workflow sẽ xuất hiện với 4 node: **Start**, **Passing variables**, **Run python script**, **Play sound**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Start** (`manualTrigger`) | Nút khởi động thủ công. | Không cần thay đổi, chỉ dùng để test hoặc kích hoạt bằng webhook nếu muốn. |
| **Passing variables** (`set`) | Đặt các biến truyền cho script Python. | - **text**: nội dung muốn chuyển (ví dụ: `"Xin chào các sếp, đây là báo cáo ngày hôm nay."`) <br> - **language**: mã ngôn ngữ Kokoro TTS (ví dụ: `vi`) <br> - **outputPath**: đường dẫn lưu file MP3 (ví dụ: `"/tmp/tts-output/output.mp3"`). |
| **Run python script** (`executeCommand`) | Gọi script Python thực hiện TTS. | - **Command**: `python3 /path/to/kokoro_tts.py "{{ $json["text"] }}" "{{ $json["language"] }}" "{{ $json["outputPath"] }}"` <br> - **Working Directory**: thư mục chứa script (nếu cần). <br> - **Shell**: `/bin/bash`. <br> - **Output**: Đánh dấu **Binary Data** để n8n nhận file MP3 dưới dạng binary. |
| **Play sound** (`readBinaryFiles`) | Đọc file MP3 vừa tạo và trả về dưới dạng binary để phát hoặc gửi. | - **File Path**: `{{ $json["outputPath"] }}` <br> - **Binary Property**: `data`. <br> - **MIME Type**: `audio/mpeg`. |

> **Lưu ý:** Đảm bảo đường dẫn `outputPath` trong node **Set** và **Read Binary Files** trùng khớp. Nếu server có quyền hạn chế, hãy tạo thư mục `/tmp/tts-output` và cấp quyền `chmod 777`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** trên node **Start**, nhập một đoạn text mẫu. Kiểm tra log của node **Run python script** để chắc script chạy không lỗi.  
2. Nếu file MP3 được tạo, node **Play sound** sẽ trả về binary – bạn có thể mở **Output** để nghe thử.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển sang màu xanh) để workflow sẵn sàng nhận trigger.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau **Play sound** để gửi file MP3 tới kênh thông báo.  
- **Lưu trữ lâu dài**: Thêm node **Google Drive**, **AWS S3** hoặc **Dropbox** để lưu bản ghi âm vào đám mây.  
- **Lập lịch tự động**: Dùng node **Cron** để chạy workflow định kỳ (ví dụ: mỗi sáng 8h tạo bản tin audio từ báo cáo ngày).  
- **Tùy chỉnh giọng**: Mở rộng script Python để nhận thêm tham số `speed`, `pitch`, hoặc chọn giọng nam/nữ từ Kokoro TTS.  

### 📌 Kết luận
Với chỉ **4 node** đơn giản, workflow này cho phép các sếp **tự động hoá hoàn toàn** quy trình chuyển văn bản thành âm thanh, giảm chi phí, tăng tốc độ phản hồi và mở ra nhiều cơ hội tích hợp với các kênh truyền thông nội bộ. Hãy **import ngay**, cấu hình một vài biến, và để n8n làm việc cho bạn! 🚀