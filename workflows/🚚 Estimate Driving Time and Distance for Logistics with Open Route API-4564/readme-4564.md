---
title: "🚚 Tự động tính thời gian và khoảng cách lái xe cho logistics với Open Route API"
description: "Hướng dẫn tự động hóa tính toán thời gian và khoảng cách lái xe cho logistics bằng n8n và Open Route API, tiết kiệm thời gian và tối ưu hóa chuỗi cung ứng"
slug: "tu-dong-tinh-thoi-gian-khoang-cach-lai-xe-logistics-open-route-api"
tags: [n8n, automation, logistics, google-sheets, open-route-api]
keywords: [n8n workflow, tự động hóa logistics, tính khoảng cách lái xe, open route api, google sheets]
---

# 🚚 Tự động tính thời gian và khoảng cách lái xe cho logistics với Open Route API

[Các sếp logistics] đang gặp khó khăn khi phải tính toán thủ công thời gian và khoảng cách lái xe cho hàng trăm tuyến đường hàng ngày. Việc này tốn thời gian, dễ sai sót và không thể tự động hóa. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này bằng cách kết hợp n8n với Open Route API.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc tính toán thủ công
- Dữ liệu chính xác và cập nhật liên tục
- Tối ưu hóa chuỗi cung ứng với thông tin thời gian và khoảng cách chính xác
- Tự động hóa toàn bộ quá trình tính toán mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã kích hoạt
- API Key từ Open Route Service (miễn phí)
- File Google Sheet chứa dữ liệu tuyến đường (thành phố xuất phát, kinh độ/vĩ độ xuất phát, thành phố đích, kinh độ/vĩ độ đích)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: `https://n8n.io/workflows/4564`
3. Hoặc tải file JSON từ link trên và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When clicking ‘Test workflow’" (manualTrigger)**:
   - Không cần cấu hình gì, chỉ cần nhấn "Test workflow" để kích hoạt

2. **Node "Collect Routes" (googleSheets)**:
   - Thêm credentials Google Sheets OAuth2 API
   - Chọn file Google Sheet chứa dữ liệu tuyến đường
   - Chọn sheet chứa dữ liệu
   - Map các trường dữ liệu: `city_departure`, `longitude_departure`, `latitude_departure`, `city_destination`, `longitude_destination`, `latitude_destination`, `distance`, `duration`, `n_steps`

3. **Node "Request Open Route API" (httpRequest)**:
   - Thêm API Key từ Open Route Service
   - Chọn phương thức lái xe: `driving-car` (xe cá nhân) hoặc `driving-hgv` (xe thương mại)

4. **Node "Save Results" (googleSheets)**:
   - Sử dụng cùng credentials với node "Collect Routes"
   - Chọn file và sheet tương tự
   - Map các trường dữ liệu: `city_departure`, `longitude_departure`, `latitude_departure`, `city_destination`, `longitude_destination`, `latitude_destination`, `distance`, `duration`, `n_steps`

#### 3. Kích hoạt ⚡️
1. Nhấn "Test workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn "Activate workflow" để chạy workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log hoạt động vào Google Sheets để theo dõi lịch sử
- Tự động gửi báo cáo hàng ngày về các tuyến đường quan trọng
- Tích hợp với hệ thống quản lý logistics để cập nhật thông tin thời gian và khoảng cách

### 📌 Kết luận
Workflow này giúp các sếp logistics tiết kiệm thời gian đáng kể trong việc tính toán thời gian và khoảng cách lái xe. Dữ liệu chính xác và tự động hóa toàn bộ quá trình sẽ giúp tối ưu hóa chuỗi cung ứng và nâng cao hiệu quả hoạt động. Hãy áp dụng ngay để thấy kết quả ngay lập tức!