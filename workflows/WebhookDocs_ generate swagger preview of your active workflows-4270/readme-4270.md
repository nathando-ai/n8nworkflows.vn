---
title: "🚀 Tự động tạo preview Swagger cho workflow n8n của bạn"
description: "Hướng dẫn chi tiết cách tự động tạo preview Swagger cho các workflow đang hoạt động trong n8n, giúp quản lý và chia sẻ API một cách hiệu quả."
slug: "tu-dong-tao-preview-swagger-workflow-n8n"
tags: [n8n, automation, no-code, swagger, api]
keywords: [n8n workflow, tự động hóa, swagger preview, api documentation]
---

# 🚀 Tự động tạo preview Swagger cho workflow n8n của bạn

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý và chia sẻ tài liệu API từ workflow n8n. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để tạo preview Swagger.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tạo preview Swagger tự động cho các workflow đang hoạt động
- Quản lý và chia sẻ tài liệu API một cách hiệu quả
- Tiết kiệm thời gian và công sức trong việc tạo tài liệu API thủ công
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n với quyền truy cập API
- API key của n8n để kết nối với workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn file JSON của workflow này
4. Hoặc copy/paste JSON vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node n8n**:
   - Chọn credentials "n8nApi" đã được cấu hình
   - Đảm bảo API key của bạn có quyền truy cập đầy đủ

2. **Node Get Swagger**:
   - Đảm bảo path "swagger" được cấu hình đúng
   - Mở phần ghi chú của webhook và thêm các dòng sau để hỗ trợ parameter labels:
     ```
     //@body field_name string description
     //@query field_name string description
     ```

3. **Node Code**:
   - Kiểm tra và điều chỉnh mã JavaScript nếu cần thiết
   - Đảm bảo mã xử lý dữ liệu đầu vào và đầu ra đúng cách

4. **Node Respond to Webhook**:
   - Kiểm tra cấu hình response để đảm bảo dữ liệu trả về đúng định dạng

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để kiểm tra hoạt động của workflow
2. Bật Active workflow sau khi đã kiểm tra và cấu hình đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có thay đổi trong workflow
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Tạo báo cáo định kỳ về hoạt động của các workflow

### 📌 Kết luận
Workflow này giúp các sếp tự động tạo preview Swagger cho các workflow đang hoạt động trong n8n, tiết kiệm thời gian và công sức trong việc quản lý và chia sẻ tài liệu API. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của bạn!