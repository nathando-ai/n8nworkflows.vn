---
title: "🎥 Tự động đồng bộ video YouTube lên Google Sheets cho cơ sở dữ liệu nội dung"
description: "Hướng dẫn chi tiết cách tự động hóa việc lấy thông tin video (tiêu đề, tags, phụ đề, ngày đăng...) từ kênh YouTube và lưu vào Google Sheets - giải pháp hoàn hảo cho content creator và marketer"
slug: "tu-dong-dong-bo-video-youtube-len-google-sheets"
tags: [n8n, automation, no-code, youtube, google-sheets]
keywords: [n8n workflow, tự động hóa, youtube api, google sheets, content database]
---

# 🎥 Tự động đồng bộ video YouTube lên Google Sheets cho cơ sở dữ liệu nội dung

[Đoạn mở đầu: Phân tích nỗi đau thực tế của content creator và marketer khi phải thủ công cập nhật thông tin video lên bảng tính. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian thủ công cập nhật thông tin video
- Tự động cập nhật thông tin mới nhất từ YouTube
- Dễ dàng quản lý và phân tích nội dung trên Google Sheets
- Hoạt động liên tục 24/7 không cần can thiệp
- Có thể kết hợp với các công cụ phân tích khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập YouTube Data API
- Google Sheet mẫu đã được chia sẻ (hoặc tạo mới từ template)
- API Key từ Google Cloud Console (với YouTube Data API và Google Sheets API đã được kích hoạt)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9824](https://n8n.io/workflows/9824)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get My Channel"**:
   - Kết nối với Google OAuth2 API
   - Đảm bảo tài khoản Google có quyền truy cập YouTube Data API

2. **Node "List Uploads"**:
   - Kết nối với Google OAuth2 API
   - Đảm bảo tài khoản Google có quyền truy cập YouTube Data API

3. **Node "Update Posts" và "Update Posts1"**:
   - Kết nối với Google Sheets OAuth2 API
   - Thay đổi Sheet ID trong URL Google Sheets thành Sheet ID của bạn
   - Đảm bảo tài khoản Google có quyền chỉnh sửa Google Sheet

4. **Node "Get Video Details"**:
   - Kết nối với Google OAuth2 API
   - Đảm bảo tài khoản Google có quyền truy cập YouTube Data API

5. **Node "Get captions text" và "Get captions ID"**:
   - Kết nối với Google OAuth2 API
   - Đảm bảo tài khoản Google có quyền truy cập YouTube Data API
   - Nếu không cần lấy phụ đề, có thể ngắt kết nối branch này

6. **Node "Get row(s) in sheet"**:
   - Kết nối với Google Sheets OAuth2 API
   - Thay đổi Sheet ID trong URL Google Sheets thành Sheet ID của bạn
   - Đảm bảo tài khoản Google có quyền đọc Google Sheet

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Execute workflow" để test
2. Kiểm tra kết quả trên Google Sheet của bạn
3. Nếu mọi thứ hoạt động tốt, click vào nút "Active workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi có video mới được thêm vào cơ sở dữ liệu
2. **Lưu log hoạt động**: Thêm node ghi log các hoạt động quan trọng vào Google Sheet khác
3. **Gửi báo cáo định kỳ**: Thiết lập workflow chạy hàng tuần để gửi báo cáo tổng hợp nội dung mới
4. **Tự động phân loại nội dung**: Sử dụng node Code để thêm logic phân loại nội dung dựa trên tiêu đề hoặc tags

### 📌 Kết luận
Workflow này giúp các content creator và marketer tiết kiệm thời gian đáng kể trong việc quản lý nội dung. Bằng cách tự động hóa việc đồng bộ thông tin video từ YouTube lên Google Sheets, các sếp có thể tập trung vào việc tạo nội dung chất lượng hơn thay vì phải thủ công cập nhật thông tin. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!