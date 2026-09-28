---
title: "🚛🗺️ Tự động hóa Geocoding cho Logistics với Open Route API và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình lấy tọa độ GPS từ địa chỉ bằng Open Route API và lưu kết quả vào Google Sheets - giải pháp hoàn hảo cho quản lý logistics và vận chuyển."
slug: "tu-dong-hoa-geocoding-logistics-open-route-api-google-sheets"
tags: [n8n, automation, logistics, google-sheets, open-route-api]
keywords: [geocoding, logistics, open route api, google sheets, tự động hóa]
---

# 🚛🗺️ Tự động hóa Geocoding cho Logistics với Open Route API và Google Sheets

[Các sếp] có bao giờ phải đối mặt với tình trạng phải nhập tay tọa độ GPS cho hàng trăm địa chỉ vận chuyển? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản, tiết kiệm hàng giờ công sức mỗi ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình lấy tọa độ GPS từ địa chỉ
- Tiết kiệm hàng giờ công sức mỗi ngày
- Dữ liệu chính xác và cập nhật liên tục
- Tích hợp liền mạch với Google Sheets - công cụ quản lý dữ liệu quen thuộc
- Hỗ trợ tối đa 5000 địa chỉ mỗi lần chạy (giới hạn của Open Route API)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt
- API Key từ Open Route Service (miễn phí)
- Google Sheet chứa danh sách địa chỉ cần lấy tọa độ (cột "country" và "address")
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4593](https://n8n.io/workflows/4593)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Collect Addresses"**:
   - Thêm Google Sheet API credentials
   - Chọn file Google Sheet chứa danh sách địa chỉ
   - Chọn sheet chứa dữ liệu
   - Map các trường: **country**, **address**, **longitude**, **latitude**, **borough**, **neighbourhood**, **localadmin**

2. **Node "Query Open Route API"**:
   - Nhập API Key từ Open Route Service
   - Đảm bảo API Key còn hạn sử dụng

3. **Node "Save Results"**:
   - Thêm Google Sheet API credentials (cùng với node "Collect Addresses")
   - Chọn cùng file và sheet với node "Collect Addresses"
   - Map các trường cần cập nhật: **longitude**, **latitude**, **borough**, **neighbourhood**, **localadmin**

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Test workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheet
3. Nếu mọi thứ ổn, nhấn nút "Active workflow" để kích hoạt

### ✍️ Mẹo & gợi ý nâng cao
1. **Xử lý lỗi**: Thêm node "Error Handling" để ghi log khi có địa chỉ không thể geocoding
2. **Tự động hóa định kỳ**: Thêm node "Schedule Trigger" để chạy workflow tự động mỗi ngày
3. **Báo cáo**: Kết nối với node "Email" để gửi báo cáo kết quả mỗi khi workflow chạy
4. **Visualization**: Tích hợp với Google Maps API để tạo bản đồ trực quan từ dữ liệu geocoding

### 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các doanh nghiệp logistics muốn tự động hóa quá trình lấy tọa độ GPS từ địa chỉ. Với việc tích hợp liền mạch với Google Sheets và Open Route API, các sếp có thể tiết kiệm hàng giờ công sức mỗi ngày và tập trung vào những công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự khác biệt!