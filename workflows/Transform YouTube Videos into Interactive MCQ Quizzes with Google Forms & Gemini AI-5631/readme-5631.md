---
title: "🚀 Tự động tạo Quiz từ Video YouTube bằng Google Forms & Gemini AI"
description: "Hướng dẫn tự động hóa chuyển đổi video YouTube thành quiz tương tác với Google Forms và trí tuệ nhân tạo Gemini"
slug: "tu-dong-tao-quiz-tu-video-youtube-bang-google-forms-gemini-ai"
tags: [n8n, automation, no-code, google-forms, ai]
keywords: [n8n workflow, tự động hóa, quiz, google forms, gemini ai]
---

# 🚀 Tự động tạo Quiz từ Video YouTube bằng Google Forms & Gemini AI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quá trình từ video đến quiz
- Tăng tương tác: Tạo quiz tương tác từ nội dung video
- Cá nhân hóa: Tùy chỉnh số lượng câu hỏi và chủ đề
- Tích hợp hoàn hảo: Kết nối liền mạch với Google Forms và Gemini AI
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Gemini đã kích hoạt
- Quyền truy cập Google Forms API
- API Key cho Google Cloud Services
- URL video YouTube cần chuyển đổi thành quiz
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5631](https://n8n.io/workflows/5631)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Google Gemini Chat Model"**:
   - Chọn credentials "googlePalmApi"
   - Đảm bảo API Key đã được kích hoạt trong Google Cloud Console

2. **Node "Create a Google Form" và "Create MCQ Quizzes"**:
   - Chọn credentials "googleOAuth2Api"
   - Cấu hình OAuth 2.0 với các quyền truy cập cần thiết

3. **Node "Input YouTube URL"**:
   - Cấu hình form với các trường:
     - YouTube URL (text input)
     - Form name (text input)
     - Number of questions (number input)

4. **Node "Set Prompt and Model"**:
   - Chỉnh sửa prompt để phù hợp với nội dung video
   - Đảm bảo model được chọn là "Gemini-2.5-flash"

#### 3. Kích hoạt ⚡️
1. Test run với URL video mẫu
2. Kiểm tra kết quả trong Google Forms
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để thông báo khi quiz được tạo thành công
2. Lưu log các quiz đã tạo vào Google Sheets cho quản lý
3. Tự động gửi báo cáo định kỳ về hiệu suất quiz
4. Tích hợp với LMS để theo dõi kết quả học viên

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc tạo quiz từ video YouTube. Bằng cách kết hợp sức mạnh của Gemini AI và Google Forms, các sếp có thể tạo ra các quiz tương tác, cá nhân hóa hoàn toàn mà không cần kiến thức lập trình. Hãy thử ngay và nâng cao trải nghiệm học tập của học viên!