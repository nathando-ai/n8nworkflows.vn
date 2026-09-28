---
title: "🚀 Tự động lưu trữ file từ form n8n lên Digital Ocean Spaces"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình upload file từ form n8n lên Digital Ocean Spaces, tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "tu-dong-luu-tru-file-tu-form-n8n-len-digital-ocean-spaces"
tags: [n8n, automation, no-code, Digital Ocean, cloud storage]
keywords: [n8n workflow, tự động hóa, Digital Ocean Spaces, lưu trữ file, form n8n]
---

# 🚀 Tự động lưu trữ file từ form n8n lên Digital Ocean Spaces

[Các sếp đang gặp khó khăn khi phải upload file thủ công lên Digital Ocean Spaces mỗi khi có dữ liệu mới từ form. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải upload file thủ công mỗi khi có dữ liệu mới
- Tự động hóa hoàn toàn: Quá trình upload được thực hiện tự động khi form được submit
- Tăng cường bảo mật: File được lưu trữ trên Digital Ocean Spaces với các tính năng bảo mật cao
- Giảm thiểu lỗi: Giảm thiểu các lỗi do upload thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Digital Ocean với quyền truy cập vào Digital Ocean Spaces
- API Key của Digital Ocean Spaces
- Form n8n đã được thiết lập và có trường upload file
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/2660
3. Hoặc copy JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Đảm bảo form n8n đã được thiết lập với trường upload file
   - Kiểm tra xem form đã được kích hoạt và có thể nhận dữ liệu

2. **Node "S3"**:
   - Chọn credentials là "s3" (hoặc tạo mới nếu chưa có)
   - Điền các thông tin cần thiết:
     - Bucket Name: Tên bucket trên Digital Ocean Spaces
     - Operation: Chọn "upload"
     - File Name: Bạn có thể sử dụng biểu thức để đặt tên file động (ví dụ: `{{$node["On form submission"].json["fileName"]}}`)
     - File Content: Chọn "Binary" và chọn trường chứa file từ node "On form submission"

3. **Node "Form"**:
   - Đảm bảo form đã được thiết lập với trường upload file
   - Kiểm tra xem form đã được kích hoạt và có thể nhận dữ liệu

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra xem file đã được upload thành công lên Digital Ocean Spaces
3. Bật Active workflow để chạy tự động khi có dữ liệu mới từ form

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo khi upload thành công
- Thiết lập lịch gửi báo cáo định kỳ về các file đã được upload
- Kết hợp với Slack để nhận thông báo tức thời khi có file mới được upload
- Thêm node xử lý file trước khi upload (ví dụ: chuyển đổi định dạng, nén file)

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình upload file từ form n8n lên Digital Ocean Spaces, tiết kiệm thời gian và giảm thiểu lỗi. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!