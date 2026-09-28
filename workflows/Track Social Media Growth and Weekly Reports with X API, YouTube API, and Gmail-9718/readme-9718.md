---
title: "📈 Tự động theo dõi tăng trưởng mạng xã hội và gửi báo cáo hàng tuần với X API, YouTube API và Gmail"
description: "Hướng dẫn tự động hóa theo dõi số lượng người theo dõi trên X (Twitter) và YouTube, lưu trữ dữ liệu và gửi báo cáo hàng tuần qua email bằng n8n"
slug: "tu-dong-theo-doi-tang-truong-mang-xa-hoi-voi-n8n"
tags: [n8n, automation, no-code, social media, marketing]
keywords: [n8n workflow, tự động hóa, theo dõi mạng xã hội, báo cáo hàng tuần]
---

# 📈 Tự động theo dõi tăng trưởng mạng xã hội và gửi báo cáo hàng tuần với X API, YouTube API và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động thu thập dữ liệu hàng ngày mà không cần can thiệp thủ công
- Dễ theo dõi: Lưu trữ dữ liệu lịch sử để phân tích xu hướng tăng trưởng
- Tự động báo cáo: Nhận báo cáo hàng tuần về sự tăng trưởng của tài khoản mạng xã hội
- Tăng cường hiệu quả: Dựa trên dữ liệu chính xác để tối ưu hóa chiến lược truyền thông
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản X (Twitter) và YouTube với quyền truy cập API
- API Key từ Google Cloud Console
- Tài khoản Gmail với quyền gửi email
- Bảng dữ liệu (Data Table) trong n8n với cấu trúc sau:
  | Field Name          | Type     |
  | ------------------- | -------- |
  | `date`              | DateTime |
  | `xFollowersCount`   | Number   |
  | `ytSubscriberCount` | Number   |
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/9718)
2. Click vào nút "Import" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Set X Username" và "Set YT Channel Username"**:
   - Chỉnh sửa các giá trị `xUsername` và `ytChannelId` để theo dõi tài khoản mạng xã hội của bạn
   - Đảm bảo các giá trị này chính xác để lấy dữ liệu đúng

2. **Node "Fetch X Profile Metrics"**:
   - Cấu hình xác thực "Bearer YOUR_TOKEN_HERE" với token từ X Developer Portal
   - Đảm bảo token có quyền truy cập vào tài khoản bạn muốn theo dõi

3. **Node "Fetch YT Channel Stats"**:
   - Cấu hình xác thực "Query Auth" với API Key từ Google Cloud Console
   - Đảm bảo API Key đã được kích hoạt YouTube Data API

4. **Node "Send a message" (Gmail)**:
   - Cấu hình xác thực "Google OAuth2" với Client ID và Secret từ Google Cloud Console
   - Đảm bảo đã thêm redirect URI `https://<your-n8n-domain>/rest/oauth2-credential/callback`
   - Thiết lập địa chỉ email nhận báo cáo trong trường "To Email"

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách kích hoạt workflow và kiểm tra dữ liệu được lưu trong bảng
2. Đợi đến Chủ Nhật để kiểm tra báo cáo hàng tuần được gửi qua email
3. Bật Active workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo tức thời khi có thay đổi đáng kể
- Tích hợp với Google Sheets để lưu trữ dữ liệu và tạo biểu đồ trực quan
- Thiết lập cảnh báo khi số lượng người theo dõi giảm đột ngột
- Kết hợp với các công cụ phân tích khác để tạo báo cáo chi tiết hơn
- Thêm tính năng so sánh với tài khoản đối thủ để đánh giá hiệu suất tương đối

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình theo dõi tăng trưởng mạng xã hội hàng ngày và nhận báo cáo hàng tuần một cách dễ dàng. Với việc tích hợp các API lớn như X, YouTube và Gmail, workflow này cung cấp giải pháp toàn diện cho việc quản lý và tối ưu hóa chiến lược truyền thông mạng xã hội. Hãy áp dụng ngay để tiết kiệm thời gian và tăng cường hiệu quả truyền thông của bạn!