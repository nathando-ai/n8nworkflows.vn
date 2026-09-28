---
title: "📚 Tự động chuyển đổi bài báo thành sách audio và truyện tranh cho trẻ em qua Telegram"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình chuyển đổi nội dung bài báo thành sách audio và truyện tranh cho trẻ em bằng n8n, Telegram, BrowserAct, Gemini và ElevenLabs"
slug: "tu-dong-chuyen-doi-bai-bao-thanh-sach-audio-truyen-tranh-cho-tre-em"
tags: [n8n, automation, no-code, telegram, ai, browseract, elevenlabs, google-gemini]
keywords: [n8n workflow, tự động hóa, sách audio, truyện tranh, telegram bot, ai, browseract, elevenlabs, google gemini]
---

# 📚 Tự động chuyển đổi bài báo thành sách audio và truyện tranh cho trẻ em qua Telegram

[Các sếp đang gặp khó khăn khi phải chuyển đổi nội dung bài báo thành sách audio và truyện tranh cho trẻ em một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc chuyển đổi nội dung
- Tạo ra sách audio và truyện tranh chất lượng cao cho trẻ em
- Tự động hóa toàn bộ quy trình từ lấy nội dung đến phân phối
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tăng cường tương tác với trẻ em thông qua nội dung giáo dục
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và API key
- Tài khoản BrowserAct với template "Children’s Book Storytelling & Illustration"
- Tài khoản OpenRouter và Google Gemini (PaLM)
- Tài khoản ElevenLabs cho dịch vụ chuyển đổi văn bản thành giọng nói
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12365](https://n8n.io/workflows/12365)
2. Nhấn nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Nhấn "OK" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **User Sends Message to Bot** (telegramTrigger):
  - Cần cấu hình credentials cho Telegram API
  - Đảm bảo bot Telegram đã được tạo và API key đã được lưu trong n8n

- **Get Story via BrowserAct** (browserAct):
  - Cần cấu hình credentials cho BrowserAct API
  - Đảm bảo đã lưu template "Children’s Book Storytelling & Illustration" trong tài khoản BrowserAct
  - Thiết lập tham số "templateId" với ID của template đã lưu

- **OpenRouter** (lmChatOpenRouter) và **Google Gemini** (lmChatGoogleGemini):
  - Cần cấu hình credentials cho OpenRouter và Google Gemini API
  - Đảm bảo các API key đã được lưu trong n8n
  - Thiết lập model phù hợp (ví dụ: "google/gemini-3-pro-preview" cho OpenRouter)

- **Generate Story Audio** (elevenLabs):
  - Cần cấu hình credentials cho ElevenLabs API
  - Thiết lập tham số "voiceId" với ID giọng nói phù hợp cho trẻ em

- **Generate Strory image** (googleGemini):
  - Cần cấu hình credentials cho Google Gemini API
  - Thiết lập tham số "prompt" với giá trị: `={{ $json["output.comic_book_prompts"] }}`

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, nhấn nút "Execute Workflow" để kiểm tra hoạt động
2. Gửi một URL bài báo đến bot Telegram để kiểm tra quy trình chuyển đổi
3. Kiểm tra kết quả trong Telegram để đảm bảo nội dung đã được chuyển đổi đúng cách
4. Nếu mọi thứ hoạt động tốt, nhấn nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log hoạt động của workflow để theo dõi hiệu suất
- Kết hợp với Slack hoặc Discord để nhận thông báo khi workflow hoàn thành
- Tạo bản sao lưu định kỳ của workflow để đảm bảo an toàn dữ liệu
- Thiết lập lịch gửi báo cáo hàng tuần về số lượng nội dung đã chuyển đổi
- Tích hợp với các dịch vụ lưu trữ đám mây để lưu trữ các tệp audio và hình ảnh đã tạo

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động chuyển đổi nội dung bài báo thành sách audio và truyện tranh cho trẻ em. Với quy trình tự động hóa hoàn chỉnh, các sếp có thể tiết kiệm thời gian đáng kể và cung cấp nội dung giáo dục chất lượng cao cho trẻ em một cách dễ dàng. Hãy thử ngay và trải nghiệm cách thức tự động hóa thay đổi cách tiếp cận của các sếp với việc tạo nội dung giáo dục!