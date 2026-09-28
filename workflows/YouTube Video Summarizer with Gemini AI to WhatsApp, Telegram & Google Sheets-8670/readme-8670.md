---
title: "🎬 Tự động hóa tóm tắt video YouTube bằng AI Gemini và gửi kết quả qua WhatsApp, Telegram, Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tóm tắt video YouTube bằng AI Gemini và gửi kết quả qua WhatsApp, Telegram, Google Sheets. Tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-hoa-tom-tat-video-youtube-bang-ai-gemini"
tags: [n8n, automation, no-code, ai, content-creation]
keywords: [n8n workflow, tự động hóa, tóm tắt video, ai summarization, google gemini]
---

# 🎬 Tự động hóa tóm tắt video YouTube bằng AI Gemini và gửi kết quả qua WhatsApp, Telegram, Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ phải tốn thời gian dài để xem và tóm tắt video YouTube dài? Hoặc phải gửi kết quả tóm tắt qua nhiều kênh khác nhau? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình từ nhận link video đến gửi kết quả tóm tắt qua WhatsApp, Telegram và lưu vào Google Sheets - chỉ trong vài phút cấu hình!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian lên đến 80% so với làm thủ công
- Tự động hóa hoàn toàn quá trình tóm tắt video
- Nhận kết quả qua nhiều kênh truyền thông (WhatsApp, Telegram)
- Lưu trữ dữ liệu tóm tắt trong Google Sheets cho quản lý lâu dài
- Hỗ trợ xử lý video YouTube lên đến 30 phút
- Tóm tắt và phiên dịch tự động sang tiếng Anh
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Google Gemini đã kích hoạt
- Tài khoản Google Sheets với quyền truy cập đầy đủ
- Tài khoản WhatsApp Business API (nếu sử dụng tính năng này)
- Tài khoản Telegram Bot (nếu sử dụng tính năng này)
- Link video YouTube cần tóm tắt
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/8670)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "On form submission" (formTrigger)**:
   - Không cần cấu hình đặc biệt, chỉ cần đảm bảo form hoạt động

2. **Node "Message a model" (googleGemini)**:
   - Chọn credentials "googlePalmApi"
   - Đảm bảo đã kích hoạt Google Gemini API trong Google Cloud Console
   - Model ID mặc định: `models/gemini-2.0-flash`
   - Prompt mặc định đã được cấu hình sẵn:
     ```
     You are a YouTube Summarizer AI. Your task is to process the YouTube video provided by the user and generate two outputs:

     1. Video Summary: Summarize the key points/steps of the video in English, neutral and structured (using bullets or sections).
     2. Full Transcript: Provide a translated English transcript, with meaning and tone preserved, not just literal translation.

     Rules:
     - Only process videos up to 30 minutes
     - Output always in English
     - Be concise and neutral
     ```

3. **Node "Update transcript into Sheet" (googleSheets)**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Cấu hình Spreadsheet ID và Sheet Name tương ứng
   - Đảm bảo tài khoản Google có quyền chỉnh sửa sheet này

4. **Node "Send message" (whatsApp)**:
   - Chọn credentials "whatsAppApi"
   - Cấu hình số điện thoại nhận tin nhắn
   - Đảm bảo đã kích hoạt WhatsApp Business API

5. **Node "WhatsApp Trigger" (whatsAppTrigger)**:
   - Để kích hoạt, chọn node và nhấn phím "D" trên bàn phím
   - Cấu hình số điện thoại nhận tin nhắn kích hoạt workflow

6. **Node "Telegram Trigger" (telegramTrigger)**:
   - Chọn credentials "telegramApi"
   - Để kích hoạt, chọn node và nhấn phím "D" trên bàn phím
   - Cấu hình bot Telegram và chat ID nhận tin nhắn kích hoạt

7. **Node "Send a text message" (telegram)**:
   - Chọn credentials "telegramApi"
   - Cấu hình bot Telegram và chat ID nhận kết quả tóm tắt

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, chọn từng node và nhấn phím "D" để kích hoạt
2. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
3. Bật Active workflow để chạy 24/7

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh prompt**: Các sếp có thể chỉnh sửa prompt trong node "Message a model" để phù hợp với nhu cầu cụ thể (ví dụ: tóm tắt theo định dạng khác, thêm thông tin chi tiết...)
2. **Kết hợp với Slack**: Thêm node Slack để nhận thông báo khi workflow hoàn thành
3. **Lưu log hoạt động**: Thêm node lưu log hoạt động vào Google Sheets để theo dõi lịch sử xử lý
4. **Gửi báo cáo định kỳ**: Cấu hình workflow chạy định kỳ để gửi báo cáo tóm tắt qua email

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình tóm tắt video YouTube và gửi kết quả qua nhiều kênh truyền thông. Với việc tích hợp AI Gemini, các sếp có thể nhận được tóm tắt chất lượng cao và phiên dịch tự động sang tiếng Anh. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả làm việc!