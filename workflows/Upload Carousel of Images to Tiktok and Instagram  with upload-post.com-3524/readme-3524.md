---
title: "🚀 Tự động đăng Carousel ảnh lên TikTok & Instagram bằng n8n"
description: "Hướng dẫn chi tiết cách tự động đăng carousel ảnh lên TikTok và Instagram bằng n8n, tiết kiệm thời gian và nâng cao hiệu quả marketing"
slug: "tu-dong-dang-carousel-anh-len-tiktok-instagram-n8n"
tags: [n8n, automation, no-code, marketing, social-media]
keywords: [n8n workflow, tự động hóa, đăng ảnh, carousel, TikTok, Instagram]
---

# 🚀 Tự động đăng Carousel ảnh lên TikTok & Instagram bằng n8n

[Các sếp marketing đang gặp khó khăn khi phải đăng nhiều ảnh carousel lên TikTok và Instagram mỗi ngày. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi tự động đăng carousel ảnh lên nhiều nền tảng
- Đảm bảo nội dung được đồng bộ nhất quán giữa TikTok và Instagram
- Tăng hiệu quả marketing nhờ có thể lập lịch và quản lý nội dung dễ dàng
- Giảm thiểu lỗi do thủ công trong quá trình đăng ảnh
- Có thể mở rộng để tự động hóa các tác vụ marketing khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản TikTok và Instagram đã kết nối với upload-post.com
- API Key từ upload-post.com
- Các ảnh cần đăng sẵn có (có thể từ Google Drive, Dropbox, hoặc URL trực tiếp)
- Nền tảng n8n đã được cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [https://n8n.io/workflows/3524](https://n8n.io/workflows/3524)
2. Click vào nút "Download" để tải file JSON về máy
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When clicking ‘Test workflow’" (manualTrigger)**:
   - Cấu hình các tham số đầu vào:
     - `image1_url`: URL của ảnh đầu tiên
     - `image2_url`: URL của ảnh thứ hai
     - `caption`: Nội dung chú thích cho carousel

2. **Node "Get Image 1" và "Get Image 2" (httpRequest)**:
   - Đảm bảo các URL ảnh được nhập chính xác
   - Kiểm tra kết nối internet ổn định

3. **Node "POST TO TIKTOK" và "POST TO INSTAGRAM1" (httpRequest)**:
   - Cấu hình credentials với API Key từ upload-post.com
   - Điền đúng các tham số:
     - `api_key`: API Key của upload-post.com
     - `post_type`: Đặt là "carousel" cho cả hai nền tảng

4. **Các node xử lý tên file (Change name to photo1, Change name to photo2, Send as 1 merged file)**:
   - Kiểm tra các đoạn code JavaScript để đảm bảo tên file được xử lý đúng
   - Đảm bảo các biến được truyền đúng giữa các node

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả trên cả TikTok và Instagram
3. Nếu mọi thứ ổn, bật chế độ "Active" cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Lập lịch tự động**: Kết hợp với node "Schedule Trigger" để tự động đăng carousel vào giờ cao điểm
2. **Quản lý nội dung**: Kết nối với Google Sheets để quản lý danh sách ảnh và nội dung chú thích
3. **Báo cáo hiệu suất**: Thêm node gửi email báo cáo sau khi đăng thành công
4. **Xử lý lỗi**: Thêm node xử lý lỗi để thông báo khi có vấn đề xảy ra trong quá trình đăng

### 📌 Kết luận
Với workflow này, các sếp marketing có thể tự động hóa hoàn toàn quá trình đăng carousel ảnh lên TikTok và Instagram, tiết kiệm thời gian quý giá và nâng cao hiệu quả marketing. Hãy thử ngay và trải nghiệm sự tiện lợi mà n8n mang lại!