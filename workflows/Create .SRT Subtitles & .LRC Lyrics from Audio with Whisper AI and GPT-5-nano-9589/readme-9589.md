---
title: "🎵 Tự Động Hóa Chuyển Audio → Chú Thích .SRT & Lời Bài Hát .LRC Với Whisper AI + GPT-5-nano (N8N)"
description: "Workflow tự động hóa chuyển đổi file âm thanh (MP3) thành file chú thích chuyên nghiệp (.SRT cho YouTube) và file lời bài hát (.LRC cho Musixmatch) với độ chính xác cao, không cần code. Phù hợp cho nhạc sĩ, nhà sản xuất âm nhạc và content creator."
slug: "tieu-dong-hoa-chuyen-doi-audio-srt-lrc-voi-whisper-ai-gpt-5-nano"
tags: [n8n, automation, no-code, ai, audio-processing, subtitle-generation, lyrics-generation, whisper-ai, gpt-5-nano]
keywords: [n8n workflow tự động hóa, chuyển đổi audio thành srt lrc, tự động hóa nhạc sĩ, subtitle từ âm thanh, lyrics từ audio, whisper ai n8n, gpt-5-nano n8n]
---

# 🚀 **Tự Động Hóa Chuyển Audio → Chú Thích .SRT & Lời Bài Hát .LRC Với AI (Whisper + GPT-5-nano)**

### **🔍 Nỗi Đau Của Các Sếp**
Hiện nay, việc tạo **chú thích (.SRT)** cho video YouTube hoặc **lời bài hát (.LRC)** cho streaming (Musixmatch, Spotify) thường là công việc thủ công, tốn thời gian và dễ sai sót. Các nhạc sĩ, nhà sản xuất âm nhạc và content creator phải:
- **Nghe và ghi lại từng dòng lời** một cách cẩn thận.
- **Đánh dấu thời gian** bằng tay, dẫn đến sai lệch so với âm thanh thực tế.
- **Chỉnh sửa nhiều lần** để đảm bảo trùng khớp hoàn hảo với âm thanh.
- **Tốn nhiều giờ** cho một bài hát hoặc đoạn video dài.

**Workflow này giải quyết tất cả vấn đề đó bằng AI!** Chỉ cần **upload file âm thanh (MP3)**, hệ thống sẽ tự động:
✅ **Phân tích và chuyển âm thanh thành văn bản** với thời gian chính xác (Whisper AI).
✅ **Định dạng lời bài hát thành các dòng tự nhiên** (2-8 từ/dòng) bằng GPT-5-nano.
✅ **Tạo file .SRT** (chú thích YouTube) và **.LRC** (lời bài hát) sẵn sàng xuất bản.
✅ **Cải thiện chất lượng** qua kiểm tra tự động hoặc thủ công (nếu cần).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **giờ** xuống còn **phút** cho mỗi bài hát/video.
- **Chính xác cao**: Thời gian chú thích tự động trùng khớp với âm thanh (sai lệch < 0.3s).
- **Dạng file chuyên nghiệp**: Sẵn sàng upload lên YouTube, Musixmatch, Spotify.
- **Hỗ trợ nhiều ngôn ngữ**: Tự động nhận diện và chuyển đổi âm thanh sang văn bản theo mã ISO (Vietnamese, English, Spanish...).
- **Tùy chỉnh linh hoạt**: Chọn **chế độ tự động** (skip kiểm tra) hoặc **chế độ thủ công** (sửa lỗi trước khi xuất file).
- **Không cần lưu trữ**: Tải file .SRT/.LRC trực tiếp mà không cần server.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản OpenAI** (để sử dụng Whisper AI và GPT-5-nano):
   - [Đăng ký tài khoản OpenAI](https://platform.openai.com/signup) (miễn phí với giới hạn API).
   - **API Key**: Cài đặt trong n8n dưới **Credentials** → **Add New** → **OpenAI API**.
   - **Ngân sách**: GPT-5-nano và Whisper AI có chi phí thấp (~$0.000005/1000 token). Xem [OpenAI Pricing](https://openai.com/pricing) để kiểm tra.

2. **File âm thanh sạch**:
   - **Định dạng**: MP3 (không hỗ trợ WAV, OGG).
   - **Yêu cầu**: Âm thanh phải rõ ràng (không có tiếng ồn, echo). Nếu chất lượng kém, kết quả chuyển đổi sẽ sai lệch.

3. **n8n Self-hosted** (không dùng phiên bản miễn phí):
   - **Lý do**: Workflow này cần **API Key OpenAI** và **tính năng upload file** (không hỗ trợ trên n8n.cloud).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9589](https://n8n.io/workflows/9589) (ấn **Export**).
- **Cách 1**: Trên n8n Editor, nhấn **Import** → Chọn file JSON.
- **Cách 2**: Copy toàn bộ JSON từ file → Paste vào **Import Workflow** (nút ở góc trên bên phải).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **12 node**, nhưng **3 node quan trọng nhất** cần cấu hình kỹ:

##### **A. Cấu Hình OpenAI API (Node "OpenAI Chat Model" & "PostProcessing")**
- **Bước 1**: Vào **Credentials** → **Add New** → **OpenAI API**.
  - **API Key**: Dán từ tài khoản OpenAI.
  - **Model**: Chọn **gpt-5-nano** (đã được cài đặt sẵn trong workflow).
- **Bước 2**: Kiểm tra **node "WhisperTranscribe"** (HTTP Request):
  - **URL**: `https://api.openai.com/v1/audio/transcriptions` (sẵn trong workflow).
  - **Headers**:
    - `Authorization: Bearer {API_KEY}` (điền từ Credentials).
    - `Content-Type: multipart/form-data`.
  - **Body**: Chọn **Form Data** → Thêm field `file` (type: `File`).

##### **B. Node "AudioInput" (Form Trigger)**
- **Cấu hình**:
  - **File Upload**: Bật **Enable File Upload**.
  - **File Types**: Chỉ cho phép `.mp3` (điền `mp3` vào trường **File Types**).
  - **Max File Size**: Đặt **10MB** (đủ cho hầu hết bài hát).

##### **C. Node "RoutingQualityCheck" (If)**
- **Lựa chọn chế độ**:
  - **Auto**: Bỏ qua kiểm tra chất lượng (nhanh hơn).
  - **Manual**: Chọn nếu muốn **tải file TXT** để sửa lỗi trước khi xuất .SRT/.LRC.
  - **Lưu ý**: Chế độ **Manual** yêu cầu các sếp **tải file TXT** từ node "TranscribedLyrics" → Sửa lỗi → Upload lại.

##### **D. Node "DiffMatch + SrcPrep" (Code)**
- **Không cần chỉnh sửa** (đã có mã tự động align timestamp).
- **Nếu muốn tối ưu**: Các sếp có thể mở node này để xem **công thức Levenshtein distance** (độ tương đồng giữa văn bản gốc và sửa đổi).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Upload **một file âm thanh mẫu** (ví dụ: bài hát ngắn).
  - Kiểm tra **node "SRT"** và **"LRC"** để xem kết quả.
- **Bật Active**:
  - Nhấn **Active** ở góc trên bên phải.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu chi phí OpenAI**:
   - Sử dụng **Whisper Small** (rẻ hơn) thay vì Whisper Large (đã có trong workflow).
   - **Lưu ý**: Whisper Small có độ chính xác thấp hơn với âm thanh ồn ào.

2. **Xử lý âm thanh trước khi upload**:
   - **Sử dụng Audacity** để cắt bỏ tiếng ồn, echo.
   - **Định dạng MP3 320kbps** để chất lượng tốt nhất.

3. **Tích hợp với Slack/Telegram**:
   - Thêm **node "Slack Webhook"** sau node "SRT" để thông báo khi hoàn thành.
   - **Cách làm**:
     ```json
     {
       "node": "slack",
       "operation": "sendMessage",
       "text": "🎵 File .SRT & .LRC đã tạo xong! Link tải: {{$node["SRT"].fileUrl}}",
       "attachments": [
         {
           "title": "Kết quả",
           "text": "Tải file tại: {{$node["SRT"].fileUrl}}",
           "color": "#36a64f"
         }
       ]
     }
     ```

4. **Lưu log tự động**:
   - Thêm **node "Google Sheets"** để ghi lại lịch sử chuyển đổi (file, thời gian, người upload).
   - **Cấu hình**:
     - **Credentials**: Thêm **Google Sheets API Key**.
     - **Sheet Name**: Đặt tên như `Subtitle_Lyrics_Log`.
     - **Data**: Ghi các cột: `File Name`, `Upload Time`, `Status`, `Download Link`.

5. **Báo cáo định kỳ**:
   - Sử dụng **node "Set"** + **node "Google Calendar"** để gửi email báo cáo hàng tuần về số lượng file đã xử lý.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các nhạc sĩ, nhà sản xuất âm nhạc và content creator muốn **tự động hóa việc tạo chú thích và lời bài hát** mà không cần kỹ năng code. Với **AI Whisper + GPT-5-nano**, chất lượng file .SRT/.LRC sẽ **cao hơn thủ công gấp 10 lần**, tiết kiệm **thời gian và công sức**.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để tránh giới hạn của n8n.cloud).
2. **Import workflow** và cấu hình OpenAI API.
3. **Upload file âm thanh** và tải file .SRT/.LRC ngay!

👉 [Tải workflow nguyên bản](https://n8n.io/workflows/9589) và bắt đầu tự động hóa ngay! 🚀

---
**Chia sẻ ý kiến của các sếp về workflow này ở phần comment dưới đây!** 👇