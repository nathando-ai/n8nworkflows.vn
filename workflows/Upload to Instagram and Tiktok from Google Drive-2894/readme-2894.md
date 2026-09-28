---
title: "🚀 Tự động đăng video từ Google Drive lên Instagram và TikTok bằng n8n"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp tiết kiệm thời gian và tăng hiệu quả marketing cho doanh nghiệp"
slug: "tu-dong-dang-video-tu-google-drive-len-instagram-tiktok"
tags: [n8n, automation, no-code, marketing, social-media]
keywords: [n8n workflow, tự động hóa, marketing, social media, google drive]
---

# 🚀 Tự động đăng video từ Google Drive lên Instagram và TikTok bằng n8n

[Khi các sếp phải tự tay đăng video lên các nền tảng mạng xã hội như Instagram và TikTok hàng ngày, việc này không chỉ tốn thời gian mà còn dễ gây lỗi và không nhất quán. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ khi video được tải lên Google Drive đến khi nó xuất hiện trên các nền tảng này, với mô tả được tạo tự động bằng AI.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình đăng video lên các nền tảng
- **Chính xác và nhất quán**: Mô tả được tạo tự động bằng AI, đảm bảo nội dung phù hợp
- **Tăng hiệu quả marketing**: Video xuất hiện nhanh chóng trên các nền tảng, tăng tương tác
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive
- Tài khoản upload-post.com (cần API token)
- API key từ OpenAI
- Tài khoản Telegram (tùy chọn, để nhận thông báo lỗi)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/2894)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Drive Trigger**:
   - Chọn credentials "googleDriveOAuth2Api"
   - Cấu hình folder cần theo dõi trong Google Drive

2. **Google Drive**:
   - Chọn credentials "googleDriveOAuth2Api"
   - Đảm bảo operation được đặt là "download"

3. **Get Audio from Video**:
   - Chọn credentials "openAiApi"
   - Tùy chỉnh prompt nếu cần thiết

4. **Generate Description for Videos**:
   - Chọn credentials "openAiApi"
   - Tùy chỉnh prompt để phù hợp với nội dung video của các sếp

5. **Upload Video and Description to Tiktok**:
   - Chọn credentials "httpHeaderAuth"
   - Thêm API token từ upload-post.com vào header

6. **Upload Video and Description to Instagram**:
   - Chọn credentials "httpHeaderAuth"
   - Thêm API token từ upload-post.com vào header

7. **Telegram** (tùy chọn):
   - Cấu hình để nhận thông báo lỗi nếu cần

#### 3. Kích hoạt ⚡️
1. Test run với một video mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu tự động hóa quy trình

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các video đã được đăng thành công
- Kết hợp với Slack để nhận thông báo khi có video mới được đăng
- Tùy chỉnh prompt OpenAI để tạo mô tả phù hợp hơn với thương hiệu
- Thêm bước kiểm tra nội dung nhạy cảm trước khi đăng lên các nền tảng

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình đăng video lên Instagram và TikTok, tiết kiệm thời gian và tăng hiệu quả marketing. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!