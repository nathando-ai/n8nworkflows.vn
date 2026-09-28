---
title: "🚀 Tự động hóa Podcast thành Clip TikTok Viral với AI Gemini & Auto-Posting"
description: "Hướng dẫn tự động hóa chuyển đổi podcast thành clip TikTok viral sử dụng AI Gemini và tự động đăng tải, tiết kiệm thời gian và tăng tương tác"
slug: "tu-dong-hoa-podcast-thanh-clip-tiktok-viral-voi-ai-gemini"
tags: [n8n, automation, no-code, AI, marketing]
keywords: [n8n workflow, tự động hóa, AI, marketing, podcast]
---

# 🚀 Tự động hóa Podcast thành Clip TikTok Viral với AI Gemini & Auto-Posting

[Các sếp đang gặp khó khăn khi phải chuyển đổi podcast dài thành các clip TikTok ngắn gọn, hấp dẫn để tăng tương tác. Workflow này giúp tự động hóa toàn bộ quy trình từ ghi âm đến đăng tải, tiết kiệm thời gian và tăng hiệu quả marketing.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi podcast dài thành các clip ngắn gọn, hấp dẫn
- Tiết kiệm thời gian xử lý từ 80% đến 90%
- Tăng tương tác trên TikTok nhờ nội dung cá nhân hóa
- Hoạt động liên tục 24/7 không cần can thiệp
- Tăng khả năng tiếp cận đối tượng mục tiêu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản AssemblyAI (API Key)
- Tài khoản Google AI Studio (API Key)
- Tài khoản Andynocode (API Key)
- Tài khoản Upload-Post (API Key và username)
- Tài khoản OpenAI (API Key)
- Thành viên gói \$29/month (để sử dụng các tính năng đặc biệt)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/4568)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Audio Transcription** (httpRequest):
   - Cấu hình credentials "openAiApi"
   - Điền API Key từ tài khoản OpenAI

2. **Google Gemini Chat Model** (lmChatGoogleGemini):
   - Cấu hình credentials "googlePalmApi"
   - Điền API Key từ tài khoản Google AI Studio
   - Host: `https://generativelanguage.googleapis.com`

3. **Submit Job** và **Check Status** (httpRequest):
   - Cấu hình credentials "httpHeaderAuth"
   - Thêm header "Authorization" với giá trị là API Key từ AssemblyAI

4. **Editing Clips** và **Clip Ready?** (httpRequest):
   - Cấu hình credentials "httpQueryAuth"
   - Thêm query parameter "api_key" với giá trị là API Key từ Andynocode

5. **Post To TikTok** (httpRequest):
   - Cấu hình credentials "httpHeaderAuth"
   - Thêm header "Authorization" với giá trị "Apikey your_api_key"
   - Thêm parameter "user" với giá trị là username của tài khoản Upload-Post

6. **Download Audio Stage 1** (httpRequest):
   - Thêm parameter "auth-token" với giá trị là key membership từ [lemolex.gumroad.com](https://lemolex.gumroad.com/l/ypjdr)

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu với URL podcast và URL video nền mẫu
- Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log các clip đã tạo vào Google Sheets để quản lý nội dung
- Tự động gửi báo cáo hàng tuần về hiệu suất các clip TikTok
- Thêm chức năng phân tích cảm xúc từ nội dung podcast để tối ưu hóa tiêu đề và nội dung clip

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc chuyển đổi podcast thành nội dung TikTok hấp dẫn. Bằng cách tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào việc tạo nội dung sáng tạo hơn và tăng tương tác với khán giả. Hãy thử ngay và nâng cao hiệu quả marketing của bạn!