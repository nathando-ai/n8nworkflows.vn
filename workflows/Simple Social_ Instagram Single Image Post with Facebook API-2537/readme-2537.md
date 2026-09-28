---
title: "📸 Tự động đăng ảnh đơn trên Instagram bằng Facebook API - Workflow n8n đơn giản"
description: "Hướng dẫn chi tiết cách tự động đăng ảnh đơn lên Instagram bằng workflow n8n, tiết kiệm thời gian và đảm bảo hiệu quả quảng cáo"
slug: "tu-dong-dang-anh-instagram-facebook-api"
tags: [n8n, automation, no-code, instagram, marketing]
keywords: [n8n workflow, tự động hóa, instagram, facebook api, quảng cáo]
---

# 📸 Tự động đăng ảnh đơn trên Instagram bằng Facebook API - Workflow n8n đơn giản

[Các sếp marketing] đang gặp khó khăn khi phải đăng ảnh đơn trên Instagram thủ công mỗi ngày? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình đăng ảnh đơn lên Instagram chỉ trong vài bước đơn giản, tiết kiệm thời gian quý giá và đảm bảo hiệu quả quảng cáo.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình đăng ảnh đơn lên Instagram
- Chính xác: Đảm bảo ảnh và caption được đăng chính xác theo kế hoạch
- Cá nhân hóa: Có thể tùy chỉnh nội dung và thời gian đăng
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần can thiệp
- Theo dõi hiệu quả: Nhận thông báo email khi đăng thành công hoặc thất bại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Facebook Developer với quyền truy cập Facebook API
- Trang Instagram Business đã kết nối với Facebook Page
- Thư viện ảnh chứa các ảnh cần đăng
- Địa chỉ email để nhận thông báo kết quả
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/2537)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When clicking ‘Test workflow’"**:
   - Chọn "Manual Trigger" để kích hoạt workflow thủ công khi cần

2. **Node "Instagram params"**:
   - Cấu hình các tham số cần thiết:
     - `imageUrl`: URL của ảnh cần đăng
     - `caption`: Nội dung caption cho ảnh
     - `instagramBusinessProfileId`: ID của trang Instagram Business

3. **Node "Node just for retrive id of instagram page"**:
   - Đảm bảo đã thêm credentials Facebook API
   - Cấu hình đúng endpoint để lấy ID của trang Instagram

4. **Node "Instagram prepare media"**:
   - Đảm bảo đã thêm credentials Facebook API
   - Cấu hình đúng endpoint để chuẩn bị media

5. **Node "Instagram publish media"**:
   - Đảm bảo đã thêm credentials Facebook API
   - Cấu hình đúng endpoint để đăng media

6. **Node "Instagram check status of media uploaded before"**:
   - Đảm bảo đã thêm credentials Facebook API
   - Cấu hình đúng endpoint để kiểm tra trạng thái media đã tải lên

7. **Node "If media status is finished"**:
   - Cấu hình điều kiện để kiểm tra trạng thái media đã hoàn thành

8. **Node "Instagram check status of media published before"**:
   - Đảm bảo đã thêm credentials Facebook API
   - Cấu hình đúng endpoint để kiểm tra trạng thái media đã đăng

9. **Node "If media status is finished1"**:
   - Cấu hình điều kiện để kiểm tra trạng thái media đã đăng hoàn thành

10. **Node "Send Email"**:
    - Cấu hình thông tin email để nhận thông báo khi đăng thành công
    - Thêm nội dung email tùy chỉnh

11. **Node "Send Email1"**:
    - Cấu hình thông tin email để nhận thông báo khi đăng thất bại
    - Thêm nội dung email tùy chỉnh

12. **Node "Send Email2"**:
    - Cấu hình thông tin email để nhận thông báo khi tải lên thất bại
    - Thêm nội dung email tùy chỉnh

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Test Workflow" để kiểm tra hoạt động
2. Kiểm tra email để đảm bảo nhận được thông báo kết quả
3. Nếu mọi thứ hoạt động tốt, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo tức thì thay vì qua email
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Tự động hóa quá trình chọn ảnh từ thư viện và tạo caption dựa trên nội dung
- Lên lịch đăng ảnh theo thời gian cụ thể để tối ưu hóa tương tác

### 📌 Kết luận
Workflow này giúp các sếp marketing tự động hóa toàn bộ quy trình đăng ảnh đơn lên Instagram, tiết kiệm thời gian và đảm bảo hiệu quả quảng cáo. Hãy áp dụng ngay để nâng cao hiệu suất làm việc và tối ưu hóa chiến dịch marketing của các sếp!