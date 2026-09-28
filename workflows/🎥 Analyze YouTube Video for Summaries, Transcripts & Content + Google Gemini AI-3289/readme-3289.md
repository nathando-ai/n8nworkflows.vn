---
title: "🎥 Tự động hóa phân tích video YouTube với Google Gemini AI"
description: "Workflow n8n giúp tự động hóa việc tổng hợp, chuyển ngữ và phân tích nội dung video YouTube bằng trí tuệ nhân tạo, tiết kiệm thời gian và nâng cao hiệu quả nội dung"
slug: "tu-dong-hoa-phan-tich-video-youtube-voi-google-gemini-ai"
tags: [n8n, automation, no-code, youtube, google-gemini]
keywords: [n8n workflow, tự động hóa, phân tích video, google gemini, youtube]
---

# 🎥 Tự động hóa phân tích video YouTube với Google Gemini AI

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải xem hàng loạt video YouTube để tìm kiếm thông tin quan trọng? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình phân tích video YouTube bằng trí tuệ nhân tạo của Google Gemini, từ tổng hợp nội dung đến chuyển ngữ và phân tích chi tiết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình phân tích video từ 30 phút xuống còn vài giây
- **Nội dung chính xác**: Phân tích sâu sắc nội dung video với các tùy chọn chuyên biệt
- **Tích hợp liền mạch**: Lưu kết quả vào Google Drive và gửi email tự động
- **Tùy chỉnh linh hoạt**: Hỗ trợ nhiều loại phân tích khác nhau (tóm tắt, chuyển ngữ, mô tả cảnh...)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Google Generative Language (Gemini) đã kích hoạt
- Tài khoản Google Drive để lưu kết quả
- Tài khoản Gmail để gửi email kết quả
- API Key của YouTube Data API
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3289](https://n8n.io/workflows/3289)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào menu "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Start Workflow"**:
   - Cấu hình form để nhận input từ người dùng (ID video YouTube và loại phân tích)

2. **Node "Get YouTube Video Details"**:
   - Thêm credentials cho YouTube Data API
   - Đảm bảo API Key đã được kích hoạt và có quyền truy cập vào YouTube Data API

3. **Node "Get YouTube Information by Prompt Type"**:
   - Thêm credentials cho Google Generative Language API
   - Đảm bảo API đã được kích hoạt và có quyền truy cập

4. **Node "Save to Google Drive as Text File"**:
   - Thêm credentials cho Google Drive OAuth2
   - Cấu hình thư mục lưu trữ trong Google Drive

5. **Node "Send to Gmail as HTML"**:
   - Thêm credentials cho Gmail OAuth2
   - Cấu hình địa chỉ email nhận kết quả

#### 3. Kích hoạt ⚡️
1. Test run với video mẫu (ví dụ: ID video "wBuULAoJxok")
2. Kiểm tra kết quả trong Google Drive và email
3. Bật Active workflow để sử dụng thực tế

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để thông báo khi phân tích hoàn thành
- Lưu log các video đã phân tích để theo dõi lịch sử
- Tạo báo cáo định kỳ về nội dung video quan trọng
- Tích hợp với các công cụ quản lý nội dung khác như WordPress

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình phân tích video YouTube, từ tiết kiệm thời gian đến nâng cao hiệu quả nội dung. Hãy thử ngay và trải nghiệm sức mạnh của trí tuệ nhân tạo trong quản lý nội dung!