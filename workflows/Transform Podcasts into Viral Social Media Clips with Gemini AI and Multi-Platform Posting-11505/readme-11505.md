---
title: "🚀 Tự động hóa Podcast thành Clip TikTok Viral với AI Gemini và Đa nền tảng"
description: "Hướng dẫn tự động hóa chuyển đổi podcast thành clip TikTok viral sử dụng AI Gemini và tự động đăng lên nhiều nền tảng với n8n"
slug: "tu-dong-hoa-podcast-thanh-clip-tiktok-viral-voi-ai-gemini"
tags: [n8n, automation, no-code, content creation, multimodal AI]
keywords: [n8n workflow, tự động hóa podcast, AI Gemini, clip TikTok, tự động đăng bài]
---

# 🚀 Tự động hóa Podcast thành Clip TikTok Viral với AI Gemini và Đa nền tảng

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi podcast dài thành clip TikTok ngắn gọn, hấp dẫn
- Tiết kiệm thời gian xử lý từ 80% đến 90%
- Tăng tương tác trên các nền tảng xã hội
- Tự động đăng lên nhiều nền tảng (TikTok, YouTube, Facebook...)
- Cá nhân hóa nội dung cho từng nền tảng
- Hoạt động liên tục 24/7 không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản AssemblyAI (miễn phí)
- Tài khoản Google AI Studio (miễn phí)
- Tài khoản Andynocode (miễn phí)
- Tài khoản Upload-Post (miễn phí)
- API Key từ các dịch vụ trên
- Membership của tác giả (giá $29/tháng)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/11505)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

**Phần Xử lý Audio Podcast:**
- **Transcribe Podcast Audio**: Cấu hình AssemblyAI credentials
  - Name: Authorization
  - Value: [API Key của AssemblyAI]

- **Audio Transcription**: Cấu hình OpenAI credentials
  - API Key: [API Key của OpenAI]
  - Base URL: https://api.openai.com/v1

**Phần AI Gemini:**
- **Google Gemini Chat Model**: Cấu hình Google AI Studio credentials
  - Host: https://generativelanguage.googleapis.com
  - API Key: [API Key của Google AI Studio]

**Phần Andynocode:**
- **Editing Clips** và **Clip Ready?**: Cấu hình Andynocode credentials
  - Name: api_key
  - API Key: [API Key của Andynocode]

**Phần Upload-Post:**
- **Post To TikTok**: Cấu hình Upload-Post credentials
  - Name: Authorization
  - Value: Apikey [API Key của Upload-Post]
  - Thêm tham số Form Data:
    - Name: user
    - Value: [Tên người dùng của bạn]

**Phần Membership:**
- Sau khi kích hoạt membership, cần cấu hình node **Download Audio Stage 1**:
  - Name: auth-token
  - Value: [Membership Key của bạn]

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu với URL podcast và video nền mẫu
2. Kiểm tra từng bước xử lý từ transcribe đến đăng bài
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
- Thử nghiệm với các video nền khác nhau để tìm ra clip hấp dẫn nhất
- Tùy chỉnh prompt cho AI Gemini để tạo nội dung phù hợp với thương hiệu
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log xử lý vào Google Sheets để theo dõi hiệu suất
- Tự động gửi báo cáo hàng tuần về hiệu suất của các clip đã đăng

### 📌 Kết luận
Workflow này là giải pháp toàn diện cho các sếp muốn chuyển đổi podcast thành nội dung TikTok viral một cách tự động, tiết kiệm thời gian và tăng tương tác. Với cấu hình đơn giản và kết quả hấp dẫn, đây là công cụ không thể thiếu cho bất kỳ ai làm content creator nào. Hãy thử ngay và biến podcast của bạn thành những clip viral!