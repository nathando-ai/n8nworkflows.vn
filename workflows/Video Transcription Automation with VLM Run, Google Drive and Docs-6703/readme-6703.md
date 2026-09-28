---
title: "🎥 Tự động hóa chuyển đổi Video thành Văn bản với VLM Run, Google Drive và Docs"
description: "Hướng dẫn tự động hóa chuyển đổi video thành văn bản với VLM Run, Google Drive và Google Docs - Giải pháp hoàn hảo cho các sếp quản lý nội dung, ghi chú cuộc họp và tạo tài liệu từ video."
slug: "tu-dong-hoa-chuyen-doi-video-thanh-van-ban-voi-vlm-run-google-drive-docs"
tags: [n8n, automation, no-code, video-transcription, ai, google-drive, google-docs]
keywords: [n8n workflow, tự động hóa video, chuyển đổi video thành văn bản, VLM Run, Google Drive, Google Docs]
---

# 🎥 Tự động hóa chuyển đổi Video thành Văn bản với VLM Run, Google Drive và Docs

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi phải chuyển đổi video thành văn bản thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian chuyển đổi video thành văn bản thủ công
- Tạo ra bản ghi chú cuộc họp chính xác và chi tiết
- Lưu trữ và chia sẻ nội dung video dưới dạng văn bản dễ dàng
- Tự động hóa quy trình xử lý video lớn mà không gặp lỗi timeout
- Tạo tài liệu từ video một cách hiệu quả và chuyên nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản VLM Run API
- Quyền truy cập Google Drive OAuth2
- Quyền truy cập Google Docs
- Webhook endpoint (có thể sử dụng n8n's built-in webhook)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6703](https://n8n.io/workflows/6703)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, chọn "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Monitor Video Uploads (Google Drive Trigger)**
   - Chọn credentials: `googleDriveOAuth2Api`
   - Cấu hình folder cần theo dõi trong Google Drive

2. **Download Video (Google Drive)**
   - Chọn credentials: `googleDriveOAuth2Api`
   - Không cần cấu hình thêm, node này sẽ tự động tải video mới được upload

3. **VLM Run Video Transcriber**
   - Chọn credentials: `vlmRunApi`
   - Đảm bảo API key của VLM Run có quyền truy cập
   - Cấu hình webhook endpoint để nhận kết quả (sử dụng webhook node tiếp theo)

4. **Receive Transcription Results (Webhook)**
   - Đặt path: `video-transcription-vlm-run`
   - Phương thức: POST
   - Lưu ý: Cần cấu hình webhook endpoint này trong VLM Run API settings

5. **Save Transcription to Docs (Google Docs)**
   - Chọn credentials: `googleDocsOAuth2Api`
   - Chỉ định document ID để lưu kết quả (hoặc tạo mới)
   - Cấu hình định dạng văn bản mong muốn

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu với một video ngắn trước khi kích hoạt workflow chính thức
- Kiểm tra kết quả trong Google Docs sau khi workflow chạy thành công
- Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để thông báo khi có video mới được xử lý
- Lưu log các video đã xử lý để tránh xử lý trùng lặp
- Tự động gửi báo cáo hàng tuần về các video đã được chuyển đổi
- Thêm node để xử lý các video có chất lượng thấp hoặc nhiễu
- Tích hợp với các công cụ phân tích nội dung để trích xuất thông tin quan trọng từ transcriptions

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa chuyển đổi video thành văn bản, giúp các sếp tiết kiệm thời gian và công sức trong việc quản lý nội dung video. Với khả năng xử lý bất đồng bộ và tích hợp với các dịch vụ Google phổ biến, workflow này là công cụ hoàn hảo cho các doanh nghiệp và cá nhân cần quản lý nội dung video hiệu quả.