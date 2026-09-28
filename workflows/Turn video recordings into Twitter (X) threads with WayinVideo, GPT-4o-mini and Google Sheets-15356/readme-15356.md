---
title: "🚀 Tự động chuyển video thành luồng bài đăng Twitter/X với WayinVideo, GPT-4o-mini và Google Sheets"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi video thành luồng bài đăng Twitter/X bằng công nghệ AI, tiết kiệm thời gian và nâng cao hiệu quả nội dung"
slug: "tu-dong-chuyen-video-thanh-luong-bai-dang-twitter-x"
tags: [n8n, automation, no-code, content-creation, ai, social-media]
keywords: [n8n workflow, tự động hóa nội dung, AI tạo nội dung, Twitter/X, Google Sheets]
---

# 🚀 Tự động chuyển video thành luồng bài đăng Twitter/X với WayinVideo, GPT-4o-mini và Google Sheets

[Các sếp nội dung, marketer và người sáng tạo nội dung thường gặp khó khăn khi phải chuyển đổi nội dung video dài thành các luồng bài đăng Twitter/X. Quy trình thủ công này tốn thời gian, dễ bị lỗi và không nhất quán. Workflow này giúp tự động hóa toàn bộ quy trình từ việc nhập URL video đến việc đăng bài lên Twitter/X, giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả nội dung.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ 15 phút xuống còn vài giây
- Nâng cao hiệu quả nội dung: Tạo ra các bài đăng Twitter/X chất lượng, phù hợp với đối tượng mục tiêu
- Tăng tính nhất quán: Đảm bảo các bài đăng đều tuân thủ các quy tắc của Twitter/X
- Tích hợp dễ dàng: Kết nối liền mạch với các công cụ khác như Google Sheets và Twitter/X
- Giảm thiểu lỗi: Hệ thống tự động kiểm tra và xử lý các trường hợp lỗi
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Twitter/X với quyền đăng bài (tweet.write scope)
- API Key từ WayinVideo (wayin.ai)
- Tài khoản OpenAI với quyền truy cập GPT-4o-mini
- Google Sheets với tab "Twitter Threads" có cấu trúc cột như sau:
  - Video Title
  - Video URL
  - Thread ID
  - Tweet Number
  - Tweet Text
  - Character Count
  - Generated On
  - Status
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15356](https://n8n.io/workflows/15356)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 2. WayinVideo — Submit Transcription** và **Node 4. WayinVideo — Get Transcript Results**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thực tế từ wayin.ai

2. **Node 9. OpenAI — GPT-4o-mini Model**:
   - Kết nối credential OpenAI của bạn
   - Đảm bảo tài khoản OpenAI có quyền truy cập GPT-4o-mini

3. **Node 11. Google Sheets — Save Thread Draft** và **Node 14. Google Sheets — Update Status to Posted**:
   - Kết nối credential Google Sheets OAuth2 của bạn
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet thực tế
   - Đảm bảo Google Sheet có tab "Twitter Threads" với cấu trúc cột như đã mô tả

4. **Node 13. Twitter/X — Post Tweet**:
   - Kết nối credential Twitter OAuth2 của bạn với quyền tweet.write
   - Đảm bảo tài khoản Twitter/X có quyền đăng bài

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để kiểm tra hoạt động của workflow
2. Nhập dữ liệu mẫu vào form để kiểm tra toàn bộ quy trình
3. Sau khi kiểm tra thành công, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node để nhận thông báo khi quy trình hoàn thành
2. **Lưu log hoạt động**: Thêm node để lưu log các hoạt động quan trọng vào Google Sheets
3. **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp hàng tuần
4. **Tối ưu hóa nội dung**: Thêm node để phân tích nội dung trước khi đăng lên Twitter/X

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình chuyển đổi video thành luồng bài đăng Twitter/X, tiết kiệm thời gian và nâng cao hiệu quả nội dung. Với các bước cấu hình đơn giản và kết quả đáng tin cậy, đây là công cụ lý tưởng cho các nhà sáng tạo nội dung và marketer. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của mình!