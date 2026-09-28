---
title: "🚀 Tự động Upload Video & Image Ads từ Google Sheets & Google Drive lên Meta Ads Manager"
description: "Hướng dẫn tự động hóa upload video và hình ảnh quảng cáo từ Google Sheets và Google Drive lên Meta Ads Manager bằng n8n, tiết kiệm thời gian và đảm bảo quảng cáo chạy ổn định."
slug: "tu-dong-upload-video-image-ads-tu-google-sheets-google-drive-len-meta-ads-manager"
tags: [n8n, automation, no-code, social media, marketing]
keywords: [n8n workflow, tự động hóa quảng cáo, meta ads manager, google sheets, google drive]
---

# 🚀 Tự động Upload Video & Image Ads từ Google Sheets & Google Drive lên Meta Ads Manager

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi quản lý nhiều chiến dịch quảng cáo trên Meta Ads Manager, các sếp thường phải thực hiện nhiều bước thủ công như tải lên tài nguyên, tạo creative và quản lý dữ liệu. Quá trình này tốn thời gian, dễ xảy ra lỗi và không đảm bảo tính nhất quán. Workflow này giúp tự động hóa toàn bộ quy trình từ Google Sheets và Google Drive lên Meta Ads Manager, đảm bảo quảng cáo chạy ổn định và hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ tải lên tài nguyên đến tạo quảng cáo.
- Chính xác: Giảm thiểu lỗi do thủ công và đảm bảo dữ liệu đồng bộ.
- Cá nhân hóa: Tùy chỉnh các creative và quảng cáo theo nhu cầu cụ thể.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không phụ thuộc vào lịch trình thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive và Google Sheets với dữ liệu quảng cáo.
- Tài khoản Meta Ads Manager với quyền truy cập API.
- API keys và credentials cho Google Drive, Google Sheets và Meta Ads Manager.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Google Drive Folder Updated**: Cấu hình để theo dõi thư mục chứa tài nguyên quảng cáo.
- **Get Ads to Process**: Cấu hình để lấy dữ liệu từ Google Sheets chứa thông tin quảng cáo.
- **Create Video Ad Creative** và **Create Image Creative**: Cấu hình để tạo creative cho video và hình ảnh.
- **Upload Ad Video** và **Upload Ad Image**: Cấu hình để tải lên tài nguyên quảng cáo lên Meta Ads Manager.
- **Save Video Ad Details** và **Save Image Ad Details**: Cấu hình để lưu thông tin quảng cáo vào Google Sheets.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log hoạt động của workflow để theo dõi và phân tích hiệu suất.
- Gửi báo cáo định kỳ về hiệu suất quảng cáo và số liệu từ Meta Ads Manager.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình quản lý quảng cáo trên Meta Ads Manager, tiết kiệm thời gian và đảm bảo quảng cáo chạy ổn định. Hãy áp dụng ngay để tối ưu hóa hiệu suất quảng cáo!