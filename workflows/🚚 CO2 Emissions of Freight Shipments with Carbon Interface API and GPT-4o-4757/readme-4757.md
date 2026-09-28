---
title: "🚀 Tự động tính CO2 phát thải hàng hóa với Carbon Interface API và GPT-4o"
description: "Hướng dẫn tự động hóa quy trình tính CO2 phát thải hàng hóa từ email đến Google Sheets chỉ trong 5 phút với n8n và GPT-4o"
slug: "tu-dong-tinh-co2-phat-thai-hang-hoa"
tags: [n8n, automation, no-code, carbon-interface, google-sheets]
keywords: [n8n workflow, tự động hóa, carbon interface, google sheets, gpt-4o]
---

# 🚀 Tự động tính CO2 phát thải hàng hóa với Carbon Interface API và GPT-4o

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 90% thời gian xử lý thủ công
- Tự động trích xuất dữ liệu từ email hàng hóa
- Tính toán CO2 phát thải chính xác với Carbon Interface API
- Lưu trữ dữ liệu vào Google Sheets một cách tự động
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để nhận email hàng hóa
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key từ Carbon Interface (miễn phí)
- API Key từ OpenAI (cho GPT-4o)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4757](https://n8n.io/workflows/4757)
2. Nhấn nút "Import" để tải workflow về máy
3. Trong n8n Editor, nhấn "Import from File" và chọn file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node Gmail Trigger**:
- Cấu hình credentials Gmail OAuth2
- Chọn hộp thư email nhận thông tin hàng hóa
- Đặt tiêu đề email để lọc (ví dụ: "Hàng hóa mới")

**Node OpenAI Chat Model2**:
- Cấu hình credentials OpenAI API
- Chọn model "gpt-4o-mini"
- Điều chỉnh prompt để phù hợp với định dạng email hàng hóa của bạn

**Node Collect CO2 Emissions**:
- Thêm API Key Carbon Interface vào header:
  ```
  Authorization: Bearer YOUR_API_KEY
  ```

**Node Record Shipment Information và Load Results**:
- Cấu hình credentials Google Sheets OAuth2
- Chọn file Google Sheets để lưu dữ liệu
- Đảm bảo sheet có các cột:
  - shipment_number
  - pickup_location
  - pickup_address
  - expected_pickup_time
  - temperature_control
  - destination_store_name
  - destination_address
  - expected_delivery_time
  - driving_distance_km
  - estimated_transit_min
  - cargo_quantity
  - cargo_weight_tons
  - weight_value_g
  - co2_kg
  - co2_estimation_time

#### 3. Kích hoạt ⚡️
1. Chạy test với email mẫu để kiểm tra toàn bộ quy trình
2. Kích hoạt workflow bằng cách nhấn "Active"

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi có hàng hóa mới
- Tạo báo cáo định kỳ về CO2 phát thải hàng tháng
- Kết hợp với Google Maps API để tự động tính khoảng cách vận chuyển
- Thiết lập cảnh báo khi CO2 phát thải vượt ngưỡng cho phép

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý hàng hóa và tính toán CO2 phát thải. Với sự tự động hóa hoàn toàn, bạn có thể tập trung vào những nhiệm vụ quan trọng hơn trong quá trình vận hành doanh nghiệp. Hãy thử ngay và trải nghiệm sự khác biệt!