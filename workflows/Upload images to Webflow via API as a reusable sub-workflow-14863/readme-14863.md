---
title: "🚀 Tự động Upload Hình Ảnh lên Webflow qua API - Workflow n8n Chuyên Nghiệp"
description: "Hướng dẫn chi tiết cách tự động upload hình ảnh lên Webflow thông qua API với workflow n8n, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-upload-hinh-anh-len-webflow-qua-api"
tags: [n8n, automation, no-code, webflow, api]
keywords: [n8n workflow, tự động hóa, webflow api, upload hình ảnh, no-code]
---

# 🚀 Tự động Upload Hình Ảnh lên Webflow qua API - Workflow n8n Chuyên Nghiệp

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải upload thủ công hàng loạt hình ảnh lên Webflow. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi upload hàng loạt hình ảnh lên Webflow
- Tự động hóa quá trình upload hình ảnh, giảm thiểu lỗi thủ công
- Tích hợp liền mạch với các hệ thống khác thông qua API
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tạo ra URL hình ảnh có thể sử dụng ngay lập tức
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Webflow với quyền truy cập API
- API Token của Webflow site (cần thiết cho xác thực)
- Hình ảnh cần upload (dữ liệu nhị phân)
- ID của Webflow site (wfSiteId)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và nhập link: https://n8n.io/workflows/14863
3. Hoặc copy/paste JSON workflow vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Step A – Announce asset in Webflow"**:
   - Thiết lập credentials: Chọn "httpBearerAuth" và nhập API Token của Webflow
   - Cấu hình tham số: Đảm bảo các tham số sau được điền đầy đủ:
     - `wfSiteId`: ID của Webflow site
     - `fileName`: Tên file hình ảnh
     - `imageData`: Dữ liệu nhị phân của hình ảnh

2. **Node "Step B – Upload binary to S3"**:
   - Node này sẽ tự động nhận thông tin từ bước trước và upload hình ảnh lên S3

3. **Node "ARGS" (executeWorkflowTrigger)**:
   - Đây là điểm đầu vào cho workflow
   - Các sếp cần cấu hình các tham số đầu vào:
     - `imageData`: Dữ liệu nhị phân của hình ảnh
     - `fileName`: Tên file hình ảnh
     - `wfSiteId`: ID của Webflow site

4. **Node "Crypto"**:
   - Node này tự động tính toán MD5 hash cho hình ảnh

5. **Node "RETURN" (set)**:
   - Node này trả về các giá trị sau khi upload thành công:
     - `originalFileName`: Tên file gốc
     - `fileId`: ID của file trong Webflow
     - `assetUrl`: URL của hình ảnh trên Webflow

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu trước khi kích hoạt chính thức
2. Sau khi kiểm tra OK, nhấn "Active workflow" để kích hoạt

### ✍️ Mẹo & gợi ý nâng cao
1. **Upload vào thư mục cụ thể**: Nếu muốn upload vào thư mục cụ thể trong Webflow Asset Manager, các sếp cần thêm folder ID vào body của node "Step A – Announce asset in Webflow"

2. **Tích hợp với các hệ thống khác**: Workflow này có thể được gọi từ các hệ thống khác thông qua API của n8n

3. **Xử lý lỗi tự động**: Các sếp có thể thêm node xử lý lỗi để gửi thông báo khi upload thất bại

4. **Lịch sử upload**: Có thể thêm node lưu log để theo dõi các lần upload thành công/thất bại

### 📌 Kết luận
Workflow "Upload images to Webflow via API" là giải pháp hoàn hảo cho các sếp cần tự động hóa quá trình upload hình ảnh lên Webflow. Với việc tích hợp liền mạch và tự động hóa hoàn toàn, các sếp có thể tiết kiệm thời gian đáng kể và giảm thiểu lỗi thủ công. Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của mình!