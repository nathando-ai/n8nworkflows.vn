---
title: "🚀 Tự động hóa quản lý file với Supabase Storage qua n8n - Hướng dẫn đầy đủ"
description: "Học cách tự động upload, lấy, tạo link tạm thời và liệt kê file trong Supabase Storage chỉ với n8n. Giải pháp hoàn hảo cho quản lý file không cần code."
slug: "tu-dong-hoa-quan-ly-file-supabase-storage-n8n"
tags: [n8n, automation, no-code, supabase, file-management]
keywords: [n8n workflow, tự động hóa, supabase storage, quản lý file, no-code]
---

# 🚀 Tự động hóa quản lý file với Supabase Storage qua n8n - Hướng dẫn đầy đủ

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình quản lý file trong Supabase Storage
- Giảm thiểu thời gian thủ công lên tới 90%
- Tạo link chia sẻ tạm thời với thời gian hết hạn tùy chỉnh
- Liệt kê và quản lý tất cả file trong kho lưu trữ một cách dễ dàng
- Tích hợp liền mạch với các hệ thống khác thông qua n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Supabase đã kích hoạt với dịch vụ Storage
- Project URL và API Key (Anon Key) từ Supabase
- Bucket đã tạo trong Supabase (ví dụ: test-n8n)
- Credentials Supabase API đã cấu hình trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/8228)
2. Click vào nút "Copy Workflow Code"
3. Trong n8n Editor, click vào "Import from Clipboard" và dán mã JSON đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "On form submission" (formTrigger)**:
   - Cấu hình form để nhận file upload từ người dùng
   - Đảm bảo trường input có tên "file" để nhận file

2. **Node "upload_to_supabase_storage" (httpRequest)**:
   - Chọn credentials "supabaseApi" đã cấu hình
   - Cấu hình request:
     - Method: POST
     - URL: `https://{{$credentials.supabaseApi.projectUrl}}/storage/v1/object/{{$node["On form submission"].json["bucket"]}}/{{$node["On form submission"].json["filename"]}}`
     - Headers:
       ```
       apikey: {{$credentials.supabaseApi.apiKey}}
       Authorization: Bearer {{$credentials.supabaseApi.apiKey}}
       Content-Type: multipart/form-data
       ```
     - Body: Chọn "Binary" và chọn file từ node trước đó

3. **Node "fetch_file_to_review1" (httpRequest)**:
   - Chọn credentials "supabaseApi" đã cấu hình
   - Cấu hình request:
     - Method: GET
     - URL: `https://{{$credentials.supabaseApi.projectUrl}}/storage/v1/object/{{$node["On form submission1"].json["bucket"]}}/{{$node["On form submission1"].json["filename"]}}`
     - Headers:
       ```
       apikey: {{$credentials.supabaseApi.apiKey}}
       Authorization: Bearer {{$credentials.supabaseApi.apiKey}}
       ```

4. **Node "get_sign_file_for_temp_access" (httpRequest)**:
   - Chọn credentials "supabaseApi" đã cấu hình
   - Cấu hình request:
     - Method: POST
     - URL: `https://{{$credentials.supabaseApi.projectUrl}}/storage/v1/object/sign/{{$node["On form submission2"].json["bucket"]}}/{{$node["On form submission2"].json["filename"]}}`
     - Headers:
       ```
       apikey: {{$credentials.supabaseApi.apiKey}}
       Authorization: Bearer {{$credentials.supabaseApi.apiKey}}
       Content-Type: application/json
       ```
     - Body:
       ```json
       {
         "expiresIn": {{$node["On form submission2"].json["expiresIn"]}}
       }
       ```

5. **Node "list_all_the_object" (httpRequest)**:
   - Chọn credentials "supabaseApi" đã cấu hình
   - Cấu hình request:
     - Method: POST
     - URL: `https://{{$credentials.supabaseApi.projectUrl}}/storage/v1/object/list/{{$node["When clicking ‘Execute workflow’"].json["bucket"]}}`
     - Headers:
       ```
       apikey: {{$credentials.supabaseApi.apiKey}}
       Authorization: Bearer {{$credentials.supabaseApi.apiKey}}
       Content-Type: application/json
       ```

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Đối với các node formTrigger, điền thông tin mẫu và submit
   - Đối với node manualTrigger, click "Execute Workflow" để chạy thử
2. Kiểm tra kết quả ở các node cuối cùng để đảm bảo dữ liệu được xử lý đúng
3. Bật Active workflow khi đã kiểm tra và xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp thông báo**: Thêm node gửi email hoặc Slack thông báo khi file được upload thành công
2. **Quản lý phiên bản**: Thêm tiền tố ngày tháng vào tên file để quản lý phiên bản
3. **Bảo mật nâng cao**: Thiết lập các chính sách truy cập phức tạp hơn trong Supabase
4. **Tự động hóa nâng cao**: Kết hợp với các dịch vụ khác như Google Drive, Dropbox để đồng bộ dữ liệu

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện cho việc quản lý file trong Supabase Storage thông qua n8n. Với các tính năng tự động hóa mạnh mẽ, các sếp có thể tiết kiệm thời gian đáng kể trong việc quản lý file và tạo ra các liên kết chia sẻ tạm thời một cách dễ dàng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!