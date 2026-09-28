---
title: "🎬 Tự động Xóa Nền Video & Ghép Hình Ảnh với Google Drive - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động xóa nền video và ghép hình ảnh nền tùy chỉnh, lưu kết quả lên Google Drive trong 3-5 phút mỗi phút video"
slug: "tu-dong-xoa-nen-video-va-ghép-hinh-anh-voi-google-drive"
tags: [n8n, automation, no-code, video-processing, google-drive]
keywords: [n8n workflow, tự động hóa video, xóa nền video, ghép hình ảnh, google drive]
---

# 🎬 Tự động Xóa Nền Video & Ghép Hình Ảnh với Google Drive - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý video từ 3-5 phút xuống còn vài giây
- Tự động hóa hoàn toàn quy trình xóa nền và ghép hình
- Lưu kết quả trực tiếp lên Google Drive với liên kết chia sẻ
- Xử lý hàng loạt video một cách hiệu quả
- Tiết kiệm chi phí so với dịch vụ xóa nền thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản VideoBgRemover API (https://videobgremover.com/api-management)
- Tài khoản Google Drive đã kích hoạt API
- URL công khai của video cần xử lý và hình nền
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9820](https://n8n.io/workflows/9820)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Trigger**:
   - Đảm bảo đường dẫn "compose-video-image" là duy nhất trong hệ thống của bạn
   - Giữ phương thức HTTP là POST

2. **Manual Trigger**:
   - Cập nhật các URL mẫu trong node "Sample URLs (Edit Here)"
   - Thay thế bằng URL thực tế của video và hình nền

3. **HTTP Request Nodes** (1-4):
   - Tất cả các node này đều sử dụng API của VideoBgRemover
   - Đảm bảo biến môi trường `VIDEOBGREMOVER_KEY` đã được thiết lập
   - Kiểm tra các tham số trong phần "Body" của mỗi node

4. **Google Drive Node**:
   - Kết nối tài khoản Google Drive của bạn
   - Chọn thư mục lưu trữ mong muốn (mặc định là Root của "My Drive")

5. **Composition Template**:
   - Chọn template phù hợp trong node "2. Start Image Composition"
   - Các tùy chọn: centered, fullscreen, picture_in_picture, ai_ugc_ad

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Cập nhật các URL trong node "Sample URLs (Edit Here)"
   - Chạy workflow bằng nút "Execute Workflow"
2. Kiểm tra kết quả:
   - Sau khoảng 3-5 phút, kiểm tra Google Drive để xem video đã xử lý
3. Bật Active workflow:
   - Chuyển đổi nút "Active" ở góc trên bên phải sang trạng thái ON

### ✍️ Mẹo & gợi ý nâng cao
1. **Xử lý hàng loạt**:
   - Kết nối workflow với Google Sheets để xử lý nhiều video cùng lúc
   - Sử dụng node "Google Sheets" để lấy danh sách video và hình nền

2. **Thông báo kết quả**:
   - Thêm node "Slack" hoặc "Email" để nhận thông báo khi xử lý hoàn thành
   - Cấu hình trong node "Build Success Response" và "Build Error Response"

3. **Tối ưu hóa chi phí**:
   - Sử dụng chế độ "Manual Trigger" cho các test nhỏ
   - Chỉ kích hoạt webhook khi cần xử lý tự động

4. **Tùy chỉnh nâng cao**:
   - Thay đổi thời gian chờ trong node "Wait 20s" nếu cần
   - Tùy chỉnh các tham số trong node "Start Image Composition" cho kết quả tốt nhất

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quy trình xóa nền video và ghép hình ảnh nền, giúp tiết kiệm thời gian và nâng cao hiệu quả làm việc. Với khả năng tích hợp Google Drive, các sếp có thể dễ dàng quản lý và chia sẻ các video đã xử lý. Hãy thử ngay để trải nghiệm sự tiện lợi và hiệu quả mà tự động hóa mang lại!