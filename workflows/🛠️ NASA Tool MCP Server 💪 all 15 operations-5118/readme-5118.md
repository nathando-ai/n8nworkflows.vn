---
title: "🚀 Tự động hóa 15 chức năng NASA với n8n - Giải pháp toàn diện cho dữ liệu thiên văn học"
description: "Tự động hóa 15 chức năng NASA bao gồm dữ liệu thiên thạch, ảnh thiên văn hàng ngày và cảnh báo thiên văn học với n8n. Tiết kiệm thời gian và tự động hóa quy trình dữ liệu thiên văn học."
slug: "tu-dong-hoa-15-chuc-nang-nasa-voi-n8n"
tags: [n8n, automation, no-code, NASA, thiên văn học, dữ liệu khoa học]
keywords: [n8n workflow, tự động hóa NASA, dữ liệu thiên văn học, thiên thạch, ảnh thiên văn hàng ngày]
---

# 🚀 Tự động hóa 15 chức năng NASA với n8n - Giải pháp toàn diện cho dữ liệu thiên văn học

[Đoạn mở đầu: Các sếp đang làm việc với dữ liệu thiên văn học và cảnh báo thiên văn học có thể gặp phải nhiều thách thức như xử lý dữ liệu thủ công, mất thời gian và không thể tự động hóa. Workflow này giúp các sếp tự động hóa 15 chức năng NASA bao gồm dữ liệu thiên thạch, ảnh thiên văn hàng ngày và cảnh báo thiên văn học với n8n.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa 15 chức năng NASA bao gồm dữ liệu thiên thạch, ảnh thiên văn hàng ngày và cảnh báo thiên văn học.
- Tiết kiệm thời gian và tự động hóa quy trình dữ liệu thiên văn học.
- Tăng tính chính xác và giảm thiểu lỗi trong quá trình xử lý dữ liệu.
- Tự động hóa quy trình dữ liệu thiên văn học và cảnh báo thiên văn học.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản NASA Tool và API key để truy cập dữ liệu thiên văn học.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **NASA Tool MCP Server**: Node này là điểm bắt đầu của workflow. Các sếp cần cấu hình path là "nasa-tool-mcp".
- **Get many asteroid neos**: Node này dùng để lấy dữ liệu thiên thạch. Các sếp cần cấu hình resource là "asteroidNeoBrowse".
- **Get an asteroid neo feed**: Node này dùng để lấy dữ liệu thiên thạch. Các sếp cần cấu hình resource là "asteroidNeoFeed".
- **Get an asteroid neo lookup**: Node này dùng để lấy dữ liệu thiên thạch. Các sếp cần cấu hình resource là "asteroidNeoLookup".
- **Get the astronomy picture of the day**: Node này dùng để lấy ảnh thiên văn hàng ngày. Các sếp không cần cấu hình gì thêm.
- **Get a DONKI coronal mass ejection**: Node này dùng để lấy dữ liệu cảnh báo thiên văn học. Các sếp cần cấu hình resource là "donkiCoronalMassEjection".
- **Get a DONKI high speed stream**: Node này dùng để lấy dữ liệu cảnh báo thiên văn học. Các sếp cần cấu hình resource là "donkiHighSpeedStream".
- **Get a DONKI interplanetary shock**: Node này dùng để lấy dữ liệu cảnh báo thiên văn học. Các sếp cần cấu hình resource là "donkiInterplanetaryShock".
- **Get a DONKI magnetopause crossing**: Node này dùng để lấy dữ liệu cảnh báo thiên văn học. Các sếp cần cấu hình resource là "donkiMagnetopauseCrossing".
- **Get a DONKI notifications**: Node này dùng để lấy dữ liệu cảnh báo thiên văn học. Các sếp cần cấu hình resource là "donkiNotifications".
- **Get a DONKI radiation belt enhancement**: Node này dùng để lấy dữ liệu cảnh báo thiên văn học. Các sếp cần cấu hình resource là "donkiRadiationBeltEnhancement".
- **Get a DONKI solar energetic particle**: Node này dùng để lấy dữ liệu cảnh báo thiên văn học. Các sếp cần cấu hình resource là "donkiSolarEnergeticParticle".
- **Get a DONKI solar flare**: Node này dùng để lấy dữ liệu cảnh báo thiên văn học. Các sếp cần cấu hình resource là "donkiSolarFlare".
- **Get a DONKI wsa enlil simulation**: Node này dùng để lấy dữ liệu cảnh báo thiên văn học. Các sếp cần cấu hình resource là "donkiWsaEnlilSimulation".
- **Get Earth assets**: Node này dùng để lấy dữ liệu tài sản trên trái đất. Các sếp cần cấu hình resource là "earthAssets".
- **Get Earth imagery**: Node này dùng để lấy dữ liệu ảnh trái đất. Các sếp cần cấu hình resource là "earthImagery".

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với các công cụ khác như Slack, Telegram, Google Sheets để gửi cảnh báo thiên văn học và dữ liệu thiên văn học.
- Các sếp có thể lưu log dữ liệu thiên văn học và cảnh báo thiên văn học vào Google Sheets để theo dõi và phân tích.
- Các sếp có thể gửi báo cáo định kỳ về dữ liệu thiên văn học và cảnh báo thiên văn học qua email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa 15 chức năng NASA bao gồm dữ liệu thiên thạch, ảnh thiên văn hàng ngày và cảnh báo thiên văn học với n8n. Các sếp có thể tiết kiệm thời gian và tự động hóa quy trình dữ liệu thiên văn học. Các sếp có thể kết hợp workflow này với các công cụ khác để gửi cảnh báo thiên văn học và dữ liệu thiên văn học. Các sếp có thể lưu log dữ liệu thiên văn học và cảnh báo thiên văn học vào Google Sheets để theo dõi và phân tích. Các sếp có thể gửi báo cáo định kỳ về dữ liệu thiên văn học và cảnh báo thiên văn học qua email.