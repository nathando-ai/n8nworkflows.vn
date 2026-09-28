---
title: "📤 Tự động hóa Upload Tài liệu với Kiểm tra, Loại bỏ Trùng và Lưu vào Postgres"
description: "Hướng dẫn tự động hóa quy trình upload tài liệu với kiểm tra kích thước, loại file, loại bỏ trùng lặp và lưu vào cơ sở dữ liệu Postgres bằng n8n"
slug: "tu-dong-hoa-upload-tai-lieu-voi-kiem-tra-loai-bo-trung-lap-va-luu-vao-postgres"
tags: [n8n, automation, no-code, document-management, postgres]
keywords: [n8n workflow, tự động hóa upload tài liệu, kiểm tra trùng lặp, lưu trữ Postgres]
---

# 📤 Tự động hóa Upload Tài liệu với Kiểm tra, Loại bỏ Trùng và Lưu vào Postgres

[Các sếp] có bao giờ phải xử lý hàng loạt tài liệu từ nhiều nguồn khác nhau? Từ việc kiểm tra kích thước file, loại file, đến việc loại bỏ những tài liệu trùng lặp và lưu vào cơ sở dữ liệu? Quy trình này không chỉ tốn thời gian mà còn dễ gây lỗi nếu làm thủ công. Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình upload và kiểm tra tài liệu.
- **Chính xác cao**: Kiểm tra kích thước, loại file và loại bỏ trùng lặp một cách chính xác.
- **Tích hợp liền mạch**: Lưu trữ tài liệu vào cơ sở dữ liệu Postgres một cách tự động.
- **Dễ dàng mở rộng**: Có thể kết nối với các hệ thống khác như Slack, Telegram để thông báo kết quả.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã cài đặt và cấu hình.
- Cơ sở dữ liệu Postgres đã sẵn sàng.
- Bảng `documents` đã được tạo trong Postgres với cấu trúc phù hợp.
- Các thông tin kết nối Postgres (host, port, username, password, database name).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập link: [https://n8n.io/workflows/14274](https://n8n.io/workflows/14274).
3. Hoặc tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Document Upload Form"**:
   - Cấu hình form để nhận file upload từ người dùng.
   - Đảm bảo form có trường để upload file và các trường thông tin bổ sung nếu cần.

2. **Node "Webhook Upload"**:
   - Cấu hình webhook với path: `/document-upload` và phương thức HTTP: `POST`.
   - Đảm bảo webhook được kích hoạt và có thể nhận yêu cầu từ các ứng dụng khác.

3. **Node "Workflow Configuration"**:
   - Cấu hình các tham số như kích thước file tối đa, các loại file được phép.
   - Ví dụ:
     ```json
     {
       "maxFileSize": 10485760, // 10MB
       "allowedMimeTypes": ["application/pdf", "image/jpeg", "image/png"]
     }
     ```

4. **Node "Check File Size"**:
   - Kiểm tra kích thước file upload có vượt quá giới hạn đã cấu hình không.

5. **Node "Check MIME Type"**:
   - Kiểm tra loại file upload có nằm trong danh sách các loại file được phép không.

6. **Node "Generate Document Metadata"**:
   - Sử dụng JavaScript để tạo metadata cho tài liệu, bao gồm:
     - Document ID (có thể sử dụng UUID).
     - File hash (sử dụng thuật toán SHA-256 để tạo hash từ nội dung file).
     - Các thông tin khác như tên file, kích thước, loại file, ngày upload.

7. **Node "Check for Duplicate"**:
   - Cấu hình truy vấn SQL để kiểm tra xem file đã tồn tại trong cơ sở dữ liệu chưa.
   - Ví dụ truy vấn:
     ```sql
     SELECT * FROM documents WHERE file_hash = '{{$node["Generate Document Metadata"].json["fileHash"]}}'
     ```

8. **Node "Is Duplicate?"**:
   - Kiểm tra kết quả từ truy vấn SQL để xác định xem file có phải là trùng lặp không.

9. **Node "Insert Document Record"**:
   - Cấu hình truy vấn SQL để chèn bản ghi mới vào bảng `documents`.
   - Ví dụ truy vấn:
     ```sql
     INSERT INTO documents (document_id, file_name, file_size, file_type, file_hash, upload_date, status)
     VALUES ('{{$node["Generate Document Metadata"].json["documentId"]}}',
             '{{$node["Generate Document Metadata"].json["fileName"]}}',
             {{$node["Generate Document Metadata"].json["fileSize"]}},
             '{{$node["Generate Document Metadata"].json["fileType"]}}',
             '{{$node["Generate Document Metadata"].json["fileHash"]}}',
             NOW(),
             'received')
     ```

10. **Node "Return Success Response"**:
    - Cấu hình phản hồi thành công khi tài liệu được upload và lưu thành công.
    - Ví dụ:
      ```json
      {
        "status": "success",
        "message": "Document uploaded successfully",
        "documentId": "{{$node["Generate Document Metadata"].json["documentId"]}}"
      }
      ```

11. **Node "Return Duplicate Response"**:
    - Cấu hình phản hồi khi phát hiện tài liệu trùng lặp.
    - Ví dụ:
      ```json
      {
        "status": "duplicate",
        "message": "Document already exists",
        "documentId": "{{$node["Check for Duplicate"].json[0].document_id}}"
      }
      ```

12. **Node "Return Validation Error"**:
    - Cấu hình phản hồi lỗi khi kiểm tra kích thước hoặc loại file thất bại.
    - Ví dụ:
      ```json
      {
        "status": "error",
        "message": "File validation failed"
      }
      ```

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Upload một file mẫu để kiểm tra quy trình từ đầu đến cuối.
   - Kiểm tra các node để đảm bảo dữ liệu được xử lý đúng cách.

2. **Bật Active workflow**:
   - Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, bật chế độ Active để workflow có thể nhận và xử lý các yêu cầu upload tài liệu.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối với Slack/Telegram**: Thêm các node để gửi thông báo kết quả upload tài liệu đến các kênh Slack hoặc Telegram.
- **Lưu log**: Thêm các node để lưu log các hoạt động của workflow để theo dõi và giám sát.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp các tài liệu đã upload trong một khoảng thời gian nhất định.
- **Xử lý lỗi nâng cao**: Thêm các node để xử lý các lỗi không mong muốn và gửi thông báo lỗi đến các kênh giám sát.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình upload tài liệu một cách hiệu quả, đảm bảo tính chính xác và tránh trùng lặp. Với các bước cấu hình đơn giản và các lưu ý chi tiết, các sếp có thể triển khai workflow này một cách nhanh chóng và dễ dàng. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả làm việc!