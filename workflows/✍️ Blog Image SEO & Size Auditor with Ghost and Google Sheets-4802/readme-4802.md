---
title: "🚀 Tự động kiểm tra SEO hình ảnh cho Blog với Ghost và Google Sheets"
description: "Workflow n8n giúp tự động kiểm tra kích thước và tối ưu hóa hình ảnh trong bài viết blog, lưu kết quả vào Google Sheets để theo dõi và cải thiện SEO."
slug: "tu-dong-kiem-tra-seo-hinh-anh-blog-voi-ghost-va-google-sheets"
tags: [n8n, automation, no-code, ghost, google-sheets]
keywords: [n8n workflow, tự động hóa, kiểm tra hình ảnh, SEO hình ảnh, Ghost, Google Sheets]
---

# 🚀 Tự động kiểm tra SEO hình ảnh cho Blog với Ghost và Google Sheets

[Các sếp] có biết rằng hình ảnh trong bài viết blog chiếm tới 65% lưu lượng truy cập trang web? Nhưng bạn có biết rằng hình ảnh không tối ưu có thể làm giảm tốc độ tải trang, ảnh hưởng đến trải nghiệm người dùng và thậm chí làm giảm thứ hạng SEO? Với workflow này, các sếp có thể tự động kiểm tra kích thước và tối ưu hóa hình ảnh trong bài viết blog, lưu kết quả vào Google Sheets để theo dõi và cải thiện SEO.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động kiểm tra kích thước và tối ưu hóa hình ảnh trong bài viết blog
- Lưu kết quả vào Google Sheets để theo dõi và cải thiện SEO
- Giảm thời gian kiểm tra thủ công từ hàng giờ xuống còn vài phút
- Tăng tốc độ tải trang và cải thiện trải nghiệm người dùng
- Tăng thứ hạng SEO bằng cách đảm bảo hình ảnh được tối ưu hóa
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Ghost Blog với quyền truy cập API
- Tài khoản Google với quyền truy cập Google Sheets API
- Google Sheet để lưu kết quả kiểm tra
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4802](https://n8n.io/workflows/4802)
2. Nhấn nút "Import" để tải workflow về máy
3. Mở n8n Editor và nhấn nút "Import from File" để import workflow

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Extract Blog Posts"**:
   - Thêm tài khoản Ghost Blog Credentials
   - Chọn số lượng bài viết bạn muốn kiểm tra

2. **Node "Add Records" và "Results Images"**:
   - Thêm tài khoản Google Sheets API Credentials
   - Chọn file Google Sheet để lưu kết quả
   - Chọn sheet trong file Google Sheet để lưu kết quả
   - Mapping các trường: **article_id**, **article_Title**, **article_url**, **image_url**, **alt_text**, **file_size_kb**, **format**, **filename_seo**

#### 3. Kích hoạt ⚡️
- Nhấn nút "Test workflow" để kiểm tra workflow
- Nhấn nút "Activate workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có hình ảnh không tối ưu
- Lưu log kiểm tra để theo dõi lịch sử kiểm tra
- Gửi báo cáo định kỳ về kết quả kiểm tra qua email

### 📌 Kết luận
Workflow này giúp các sếp tự động kiểm tra kích thước và tối ưu hóa hình ảnh trong bài viết blog, lưu kết quả vào Google Sheets để theo dõi và cải thiện SEO. Với workflow này, các sếp có thể tiết kiệm thời gian, tăng tốc độ tải trang và cải thiện trải nghiệm người dùng.