---
title: "🎙️ Tự Động Hoá RSS → Podcast Hàng Ngày Với AI Gemini, TTS Kokoro & FFmpeg (N8N)"
description: "Workflow này tự động chuyển đổi tin tức từ RSS thành podcast hàng ngày với giọng nói AI, tiết kiệm thời gian và tối ưu hóa nội dung cho người dùng. Kết quả: Podcast cá nhân hóa, phát trực tiếp qua Telegram, hoạt động 24/7."
slug: "tieu-dong-hoa-rss-sang-podcast-hang-ngay-voi-ai-gemini-tts-kokoro"
tags: [n8n, automation, content-creation, multimodal-ai, podcast, rss, google-gemini, kokoro-tts, ffmpeg]
keywords: [n8n workflow podcast, tự động hóa tin tức thành podcast, google gemini chatbot, kokoro tts api, ffmpeg tự động, podcast hàng ngày từ rss, tự động hóa nội dung ai]
---

# 🎙️ **Tự Động Hoá RSS → Podcast Hàng Ngày Với AI Gemini, TTS Kokoro & FFmpeg**

## **Giới Thiệu**
Các sếp đang mệt mỏi vì phải thủ công tổng hợp tin tức từ nhiều nguồn RSS, viết tóm tắt, và chuyển đổi thành podcast hàng ngày? **Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy tin tức** từ các nguồn RSS (ví dụ: Folha de SP, GE) trong vòng 24h.
✅ **Tạo tóm tắt AI** bằng Google Gemini, gửi ngay qua Telegram.
✅ **Viết kịch bản podcast** với hai giọng nói AI khác biệt.
✅ **Chuyển văn bản thành âm thanh** bằng Kokoro TTS.
✅ **Gộp audio** thành một file MP3 duy nhất bằng FFmpeg.
✅ **Gửi podcast hoàn chỉnh** về Telegram với tên file động (ví dụ: `Podcast_Daily_2024-05-20.mp3`).

**Kết quả?** Một podcast cá nhân hóa, phát trực tiếp vào Telegram mỗi ngày, **không cần can thiệp thủ công!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tổng hợp tin tức thủ công hàng ngày.
- **Nội dung cá nhân hóa**: Podcast được tạo từ các nguồn RSS mà các sếp theo dõi.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi ngày, kể cả khi các sếp ngủ.
- **Chất lượng cao**: Âm thanh được sinh tổng hợp bởi AI với giọng nói tự nhiên.
- **Tối ưu hóa SEO**: Podcast có thể được chia sẻ trên các nền tảng như Spotify/YouTube sau khi xử lý.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Kokoro TTS**:
   - [Đăng ký API Key Kokoro](https://kokoro.ai/) (miễn phí cho một số lượng request hạn chế).
   - Thêm `X-API-KEY` vào header của hai node `Generate Audio (Voice 1)` và `Generate Audio (Voice 2)`.

2. **Bot Telegram**:
   - Tạo bot Telegram và lấy `API Token` từ [@BotFather](https://t.me/BotFather).
   - Thêm `telegramApi` vào credentials của node `Send Text Digest` và `Send Podcast to Telegram`.

3. **Google Gemini API**:
   - [Bật Google Vertex AI](https://console.cloud.google.com/) và lấy `API Key`.
   - Thêm `googlePalmApi` vào credentials của hai node `Google Gemini Chat Model`.

4. **RSS Feeds**:
   - Các sếp có thể thay đổi URL RSS trong node `Fetch RSS 1` và `Fetch RSS 2` (ví dụ: `https://feeds.bbci.co.uk/news/rss.xml`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6945](https://n8n.io/workflows/6945) hoặc copy/paste JSON vào **n8n Editor**.
- Nhấn **Import** và chọn **Create New Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Credentials**
- **Google Gemini**:
  - Trong node `Google Gemini Chat Model` và `Google Gemini Chat Model1`, chọn `googlePalmApi` và điền `API Key` từ Google Vertex AI.
  - **Prompt**: Các sếp có thể chỉnh sửa prompt trong node `Generate Text Digest` và `Generate Podcast Script` để thay đổi phong cách (ví dụ: giọng nói chuyên nghiệp, hài hước, hoặc ngắn gọn).

- **Telegram**:
  - Trong node `Send Text Digest` và `Send Podcast to Telegram`, chọn `telegramApi` và điền `API Token` từ BotFather.
  - **Chat ID**: Thêm ID của chat Telegram muốn nhận podcast (có thể tìm bằng cách gửi tin nhắn cho bot và copy link).

- **Kokoro TTS**:
  - Trong node `Generate Audio (Voice 1)` và `Generate Audio (Voice 2)`:
    - Header: Thay thế `X-API-KEY` bằng API Key của Kokoro.
    - Body: Chỉnh `voice` thành tên giọng nói muốn sử dụng (ví dụ: `en-US-Neural2-A` hoặc `en-US-Neural2-B`).

##### **B. Thay đổi RSS Feeds**
- Trong node `Fetch RSS 1` và `Fetch RSS 2`, thay đổi URL thành các nguồn RSS mà các sếp muốn theo dõi (ví dụ: tin tức thể thao, kinh tế, hoặc chính trị).

##### **C. Thay đổi Thời Gian Trigger**
- Trong node `Daily Trigger`, các sếp có thể chỉnh thời gian chạy (ví dụ: 8h sáng mỗi ngày) bằng cách sửa `cron` expression.

##### **D. Thay đổi Directory Tạm**
- Nếu muốn thay đổi thư mục lưu tạm (`/tmp/dailydigest`), các sếp phải cập nhật trong node `Create Temp Directory` và tất cả các node liên quan (`Save Audio Chunk to Disk`, `Generate FFmpeg Concat List`).

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chạy workflow với dữ liệu mẫu để kiểm tra kết quả.
- **Active Workflow**: Sau khi kiểm tra, bật `Active` để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Nguồn RSS**:
   - Các sếp có thể thêm nhiều node `rssFeedRead` và kết nối vào `Merge News Sources` để lấy tin từ nhiều nguồn khác nhau.

2. **Chuyển Podcast sang Spotify/YouTube**:
   - Sau khi tạo file MP3, các sếp có thể tự động upload lên Spotify hoặc YouTube bằng node `spotifyUpload` hoặc `youtubeUpload`.

3. **Lưu Log & Monitoring**:
   - Thêm node `stickyNote` để ghi lại lỗi hoặc thành công của workflow.
   - Sử dụng node `email` để gửi báo cáo hàng ngày về email cá nhân.

4. **Thay đổi Giọng Nói**:
   - Kokoro TTS có nhiều giọng nói khác nhau. Các sếp có thể thử các giọng như `en-US-Neural2-C` (giọng nữ) hoặc `en-GB-Neural2-A` (giọng Anh Quốc).

5. **Tối ưu Audio**:
   - Trong node `Merge Audio & Clean Up`, các sếp có thể chỉnh sửa command FFmpeg để thêm hiệu ứng âm thanh (ví dụ: fade-in/fade-out).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình tạo podcast từ tin tức RSS. **Không cần code, không cần chuyên môn kỹ thuật cao!** Chỉ cần import, cấu hình và chạy – podcast hàng ngày sẽ tự động được tạo và gửi về Telegram.

**Hãy thử ngay và tiết kiệm thời gian cho công việc quan trọng hơn!** 🚀

---
**📌 Lưu ý cuối cùng**:
- Nếu gặp lỗi, hãy kiểm tra log trong node `stickyNote` hoặc liên hệ cộng đồng n8n tại [Discord n8n](https://discord.gg/n8n).
- Workflow này có thể được mở rộng thêm nhiều tính năng như **chỉnh sửa tự động tiêu đề podcast**, **thêm nhạc nền**, hoặc **chia sẻ trên các nền tảng khác**.