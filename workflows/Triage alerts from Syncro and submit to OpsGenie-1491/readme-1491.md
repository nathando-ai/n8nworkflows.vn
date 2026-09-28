---
title: "🚨 Tự động xử lý cảnh báo từ Syncro và gửi đến OpsGenie"
description: "Hướng dẫn tự động hóa xử lý cảnh báo từ Syncro đến OpsGenie bằng n8n, tiết kiệm thời gian và nâng cao hiệu quả quản lý sự cố"
slug: "tu-dong-xu-ly-canh-bao-syncro-opsgenie"
tags: [n8n, automation, no-code, it-ops, secops]
keywords: [n8n workflow, tự động hóa cảnh báo, syncro, opsgenie, quản lý sự cố]
---

# 🚨 Tự động xử lý cảnh báo từ Syncro và gửi đến OpsGenie

[Các sếp IT/SecOps thường phải xử lý hàng loạt cảnh báo hàng ngày từ các hệ thống giám sát. Việc này tốn thời gian và dễ gây lỗi khi phải làm thủ công. Workflow này sẽ giúp các sếp tự động phân loại và gửi cảnh báo từ Syncro đến OpsGenie một cách nhanh chóng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại cảnh báo từ Syncro
- Tự động gửi cảnh báo đến OpsGenie với mức độ ưu tiên phù hợp
- Giảm thời gian xử lý cảnh báo từ 30-50%
- Tăng tính chính xác trong việc quản lý sự cố
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpsGenie với API key có quyền tạo và đóng cảnh báo
- URL webhook từ Syncro để nhận cảnh báo
- Biết cách cấu hình webhook trong Syncro
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/1491)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook**:
   - Đảm bảo đường dẫn `/fromsyncro` phù hợp với cấu hình webhook của Syncro
   - Kiểm tra phương thức HTTP là POST

2. **Node Create Alert**:
   - Cấu hình credentials với API key của OpsGenie
   - Kiểm tra URL endpoint của OpsGenie (thường là `https://api.opsgenie.com/v2/alerts`)
   - Đảm bảo body request chứa các trường bắt buộc: `message`, `description`, `priority`

3. **Node Close Alert**:
   - Cấu hình tương tự như Node Create Alert
   - Đảm bảo có trường `identifier` để xác định cảnh báo cần đóng

4. **Node IF**:
   - Điều chỉnh điều kiện phân loại cảnh báo theo nhu cầu của các sếp
   - Có thể thêm các điều kiện mới dựa trên các trường dữ liệu từ Syncro

5. **Node Switch**:
   - Cấu hình các trường dữ liệu cần gửi đến OpsGenie
   - Đảm bảo ánh xạ đúng giữa các trường dữ liệu từ Syncro và OpsGenie

#### 3. Kích hoạt ⚡️
1. Kiểm tra workflow bằng cách gửi dữ liệu mẫu từ Syncro
2. Kiểm tra kết quả trên OpsGenie
3. Bật Active workflow sau khi đã kiểm tra và xác nhận hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node gửi thông báo đến Slack/Teams khi có cảnh báo mới
2. Thêm node lưu log các cảnh báo đã xử lý vào Google Sheets
3. Cấu hình gửi báo cáo hàng ngày về các cảnh báo đã xử lý
4. Thêm node xử lý các cảnh báo lặp lại từ Syncro

### 📌 Kết luận
Workflow này giúp các sếp IT/SecOps tự động hóa quy trình xử lý cảnh báo từ Syncro đến OpsGenie, tiết kiệm thời gian và nâng cao hiệu quả quản lý sự cố. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!