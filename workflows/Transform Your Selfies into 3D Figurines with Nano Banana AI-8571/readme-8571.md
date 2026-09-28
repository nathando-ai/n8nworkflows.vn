---
title: "🎨 Chuyển đổi ảnh selfie thành nhân vật 3D với Nano Banana AI"
description: "Hướng dẫn tự động hóa chuyển đổi ảnh selfie thành nhân vật 3D với Nano Banana AI thông qua n8n. Tiết kiệm thời gian và tạo ra những tác phẩm nghệ thuật ấn tượng."
slug: "chuyen-doi-anh-selfie-thanh-nhan-vat-3d-voi-nano-banana-ai"
tags: [n8n, automation, no-code, AI, 3D]
keywords: [n8n workflow, tự động hóa, Nano Banana AI, chuyển đổi ảnh, nhân vật 3D]
---

# 🎨 Chuyển đổi ảnh selfie thành nhân vật 3D với Nano Banana AI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải tạo nhân vật 3D từ ảnh selfie thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tạo nhân vật 3D từ 30-60 phút xuống còn vài giây
- Tạo ra những tác phẩm nghệ thuật ấn tượng với chất lượng chuyên nghiệp
- Tự động hóa toàn bộ quy trình từ upload ảnh đến nhận kết quả
- Tích hợp dễ dàng với các hệ thống khác thông qua API
- Tạo ra những nhân vật 3D độc đáo cho các sản phẩm thương mại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản và API key từ [Defapi.org](https://defapi.org/model/google/nano-banana)
- Ảnh selfie chất lượng cao (không nên sử dụng ảnh tối)
- Prompt sáng tạo mô tả nhân vật 3D mong muốn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào menu "Workflows" ở góc trái
3. Chọn "Import from URL" và nhập link: https://n8n.io/workflows/8571
4. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Upload Image" (formTrigger)**:
   - Đảm bảo các trường sau được cấu hình:
     - Image (file upload)
     - API Key (text field)
     - Prompt (text field)

2. **Node "Send Image Generation Request to Defapi.org API" (httpRequest)**:
   - Cấu hình endpoint: `https://api.defapi.org/api/image/gen`
   - Phương thức: POST
   - Headers:
     ```
     Content-Type: application/json
     Authorization: Bearer {{API_KEY}}
     ```

3. **Node "Obtain the generated status" (httpRequest)**:
   - Cấu hình endpoint: `https://api.defapi.org/api/task/query`
   - Phương thức: GET
   - Headers:
     ```
     Authorization: Bearer {{API_KEY}}
     ```

4. **Node "Wait for Image Processing Completion" (wait)**:
   - Thời gian chờ: 10 giây

5. **Node "Check if Image Generation is Complete" (if)**:
   - Điều kiện: `{{$node["Obtain the generated status"].json["status"]}} === "success"`

#### 3. Kích hoạt ⚡️
1. Nhấn "Execute Workflow" để kiểm tra hoạt động
2. Truy cập URL form được tạo ra
3. Upload ảnh selfie của bạn
4. Nhập API key và prompt sáng tạo
5. Nhấn "Submit" và chờ kết quả

### ✍️ Mẹo & gợi ý nâng cao
- Sử dụng các prompt chi tiết hơn để đạt kết quả tốt hơn (ví dụ: mô tả kích thước, phong cách, môi trường...)
- Kết hợp với các node khác để tự động gửi kết quả qua email hoặc lưu vào Google Drive
- Tạo nhiều phiên bản khác nhau từ cùng một ảnh với các prompt khác nhau
- Sử dụng workflow này trong các chiến dịch marketing để tạo ra những sản phẩm quảng cáo ấn tượng
- Tích hợp với các nền tảng thương mại điện tử để tạo ra những sản phẩm ảo hóa

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc tạo ra những nhân vật 3D ấn tượng từ ảnh selfie. Với chỉ vài bước đơn giản, bạn có thể tạo ra những tác phẩm nghệ thuật chất lượng chuyên nghiệp mà không cần kiến thức lập trình. Hãy thử ngay và biến những khoảnh khắc tự nhiên thành những tác phẩm nghệ thuật 3D độc đáo!