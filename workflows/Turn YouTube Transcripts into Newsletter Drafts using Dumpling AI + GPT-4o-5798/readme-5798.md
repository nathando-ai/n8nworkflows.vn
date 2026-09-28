---
title: "🚀 Tự động hóa YouTube → Bản nháp Newsletter với Dumpling AI + GPT-4o"
description: "Hướng dẫn tự động hóa chuyển đổi nội dung video YouTube thành bản nháp newsletter chuyên nghiệp bằng Dumpling AI và GPT-4o, tiết kiệm thời gian và nâng cao hiệu quả nội dung"
slug: "tu-dong-hoa-youtube-sang-newsletter-dumpling-ai-gpt-4o"
tags: [n8n, automation, no-code, content creation, ai]
keywords: [n8n workflow, tự động hóa nội dung, Dumpling AI, GPT-4o, newsletter]
---

# 🚀 Tự động hóa YouTube → Bản nháp Newsletter với Dumpling AI + GPT-4o

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải chuyển đổi nội dung video YouTube thành bản nháp newsletter thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian chuyển đổi nội dung từ 60% đến 80%
- Tự động hóa quy trình tạo nội dung chuyên nghiệp
- Dễ dàng quản lý và theo dõi quá trình tạo nội dung
- Tăng hiệu quả nội dung nhờ tích hợp AI tiên tiến
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail)
- API Key từ Dumpling AI và OpenAI
- Google Sheets với 2 cột: `link` (YouTube video URL) và `blog post` (Newsletter output field)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5798](https://n8n.io/workflows/5798)
2. Click "Import" và chọn "Import from URL"
3. Dán link workflow vào và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Read YouTube Links from Google Sheets"**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Điền ID của Google Sheet chứa danh sách video YouTube
   - Đảm bảo Sheet có cột "link" chứa URL video

2. **Node "Dumpling AI: Get YouTube Transcript"**:
   - Chọn credentials "httpHeaderAuth"
   - Thêm API Key của Dumpling AI vào header Authorization
   - Đảm bảo API Key có quyền truy cập vào dịch vụ transcript

3. **Node "GPT-4o: Write Newsletter Draft from Transcript"**:
   - Chọn credentials "openAiApi"
   - Đảm bảo tài khoản OpenAI có đủ credit
   - Tùy chỉnh prompt nếu cần thay đổi phong cách viết

4. **Node "Log Newsletter Draft to Google Sheets"**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Đảm bảo Sheet có cột "blog post" để lưu kết quả

5. **Node "Send Email Notification When Draft is Ready"**:
   - Chọn credentials "gmailOAuth2"
   - Điền địa chỉ email nhận thông báo
   - Tùy chỉnh nội dung email nếu cần

#### 3. Kích hoạt ⚡️
1. Test run workflow với 1-2 video mẫu
2. Kiểm tra kết quả trong Google Sheets
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Tích hợp với Google Calendar để lập lịch tự động chạy workflow
- Thêm node để lưu log quá trình tạo nội dung
- Tùy chỉnh prompt GPT-4o để phù hợp với phong cách viết riêng của các sếp

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình chuyển đổi nội dung video YouTube thành bản nháp newsletter chuyên nghiệp, tiết kiệm thời gian và nâng cao hiệu quả nội dung. Hãy thử ngay để trải nghiệm sự khác biệt!