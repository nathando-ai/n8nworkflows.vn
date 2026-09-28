---
title: "🎥 Tự động hóa chuyển đổi video AI và đăng lên TikTok với n8n & Blotato"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình chuyển đổi video bằng AI (thay đổi gương mặt, giọng nói) và đăng lên TikTok chỉ với 1 tin nhắn Telegram"
slug: "tu-dong-hoa-chuyen-doi-video-ai-va-dang-len-tiktok"
tags: [n8n, automation, no-code, ai, content-creation, multimodal-ai]
keywords: [n8n workflow, tự động hóa video, ai avatar, thay đổi giọng nói, đăng video tiktok]
---

# 🎥 Tự động hóa chuyển đổi video AI và đăng lên TikTok với n8n & Blotato

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian xử lý video thủ công
- Tạo nội dung cá nhân hóa với avatar và giọng nói AI
- Tự động đăng lên TikTok chỉ với 1 tin nhắn Telegram
- Theo dõi quá trình xử lý và lưu trữ kết quả trên Google Sheets
- Tăng tốc độ sản xuất nội dung lên 10 lần
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot đã cấu hình
- API keys cho các dịch vụ: FAL AI, Replicate, OpenAI, Google Sheets, Blotato
- File video nguồn và hình ảnh avatar
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/11043)
2. Click "Download" để tải file JSON
3. Trong n8n Editor, chọn "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

**1. Telegram Trigger**
- Cấu hình credentials cho Telegram API
- Đảm bảo bot đã được thêm vào nhóm chat

**2. Workflow Configuration**
- Điền API keys cho các dịch vụ:
  - `falApiKey`: API key từ FAL AI
  - `replicateApiKey`: API key từ Replicate
  - `targetVoiceAudioUrl`: URL của file âm thanh mẫu cho giọng nói mục tiêu

**3. OUTPUT (Google Sheet Write)**
- Cấu hình Google Sheets OAuth2 credentials
- Chọn spreadsheet và sheet đích (phải có cột: url original và url output)

**4. Blotato Nodes**
- Cài đặt community node `@blotato/n8n-nodes-blotato`
- Cấu hình Blotato API credentials
- Đảm bảo tài khoản Blotato đã được kết nối với các tài khoản mạng xã hội

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi tin nhắn Telegram với:
     - Hình ảnh avatar
     - URL video nguồn trong caption
2. Kiểm tra kết quả trên Google Sheets
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa nội dung**:
   - Kết hợp với node OpenAI để tự động tạo caption từ nội dung video
   - Sử dụng node Telegram để nhận thông báo khi xử lý hoàn tất

2. **Nâng cao chất lượng**:
   - Thêm bước chỉnh sửa video sau khi merge (cắt, ghép, thêm hiệu ứng)
   - Sử dụng node FAL AI khác để cải thiện chất lượng video

3. **Theo dõi hiệu suất**:
   - Thêm node để ghi log thời gian xử lý cho từng bước
   - Tạo báo cáo định kỳ về số lượng video đã xử lý

4. **Tích hợp đa nền tảng**:
   - Thêm node để đăng lên YouTube, Facebook, LinkedIn cùng lúc
   - Sử dụng node Slack để nhận thông báo khi đăng thành công

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc tạo và phân phối nội dung video. Bằng cách tự động hóa quy trình chuyển đổi video bằng AI và đăng lên TikTok, các sếp có thể tập trung vào việc sáng tạo nội dung hơn là xử lý kỹ thuật. Hãy thử ngay và nâng cao hiệu suất nội dung của bạn!