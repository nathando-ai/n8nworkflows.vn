---
title: "🚀 Tự động Upload & Phân loại File lên Supabase Storage với URL Bảo mật"
description: "Hướng dẫn chi tiết cách tự động upload file lên Supabase Storage và tạo URL bảo mật để chia sẻ an toàn, tiết kiệm thời gian và nâng cao bảo mật dữ liệu"
slug: "tu-dong-upload-phan-loai-file-supabase-storage-url-bao-mat"
tags: [n8n, automation, no-code, supabase, storage]
keywords: [n8n workflow, tự động hóa, supabase storage, upload file, url bảo mật]
---

# 🚀 Tự động Upload & Phân loại File lên Supabase Storage với URL Bảo mật

[Các sếp] có thể đang gặp khó khăn khi phải upload và quản lý hàng loạt file lên Supabase Storage một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản, giúp tiết kiệm thời gian và nâng cao bảo mật dữ liệu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động upload file lên Supabase Storage với chỉ 1 lần cấu hình
- Phân loại file tự động dựa trên mime-type
- Tạo URL bảo mật có thời hạn sử dụng
- Tiết kiệm thời gian xử lý thủ công hàng loạt file
- Nâng cao bảo mật dữ liệu bằng cách không chia sẻ toàn bộ bucket
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Supabase với Storage đã kích hoạt
- API Key của Supabase (anon key hoặc service key)
- Bucket đã tạo sẵn trong Supabase Storage
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/4920)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Upload to Supabase Storage" và "Generate Signed Url"**:
   - Chọn credentials là "supabaseApi"
   - Thay đổi URL trong các node này thành URL của Supabase Storage của các sếp (ví dụ: `https://your-project-ref.supabase.co/storage/v1/object/your-bucket-name/`)
   - Đảm bảo bucket name trong URL khớp với bucket đã tạo trong Supabase

2. **Node "Prepare Upload Data"**:
   - Cấu hình mapping từ mime-type đến bucket name theo cấu trúc lưu trữ của các sếp
   - Ví dụ cấu hình:
     ```json
     {
       "image/jpeg": "images",
       "image/png": "images",
       "application/pdf": "documents"
     }
     ```

3. **Node "temp form to test workflow"**:
   - Đây là node tạm thời dùng để test workflow, các sếp nên xóa node này trước khi đưa workflow vào sản xuất
   - Để test, các sếp có thể sử dụng lệnh `base64 -i /path/to/file | pbcopy` để tạo chuỗi base64 từ file test

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả ở các node "Success Response" và "Sign Error Response"
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi upload thành công hoặc thất bại
2. **Lưu log hoạt động**: Thêm node ghi log các hoạt động upload vào Google Sheets hoặc database
3. **Tự động xóa file cũ**: Kết hợp với node "Delete Object" để tự động xóa file cũ sau một khoảng thời gian
4. **Báo cáo định kỳ**: Tạo workflow con để gửi báo cáo tổng hợp các file đã upload trong ngày

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động upload và quản lý file trên Supabase Storage. Với việc tạo URL bảo mật có thời hạn, các sếp có thể chia sẻ file một cách an toàn mà không cần chia sẻ toàn bộ bucket. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả quản lý dữ liệu!