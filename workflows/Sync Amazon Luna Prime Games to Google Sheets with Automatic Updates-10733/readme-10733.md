---
title: "🎮 Tự động đồng bộ danh sách game Prime Amazon Luna lên Google Sheets với cập nhật tự động"
description: "Hướng dẫn chi tiết cách tự động đồng bộ danh sách game Prime Amazon Luna lên Google Sheets và nhận thông báo khi có game mới, tiết kiệm thời gian và nâng cao trải nghiệm chơi game"
slug: "tu-dong-dong-bo-game-prime-amazon-luna-len-google-sheets"
tags: [n8n, automation, no-code, amazon, google-sheets, discord]
keywords: [n8n workflow, tự động hóa, amazon luna, google sheets, game prime]
---

# 🎮 Tự động đồng bộ danh sách game Prime Amazon Luna lên Google Sheets với cập nhật tự động

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp game thủ khi phải theo dõi thủ công danh sách game Prime Amazon Luna. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động cập nhật danh sách game Prime hàng ngày mà không cần can thiệp thủ công.
- **Theo dõi dễ dàng**: Tất cả thông tin game được lưu trữ và cập nhật tự động trên Google Sheets.
- **Nhận thông báo tức thì**: Được thông báo ngay khi có game mới được thêm vào danh sách Prime.
- **Quản lý hiệu quả**: Dễ dàng theo dõi và quản lý danh sách game yêu thích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã kích hoạt API.
- Tài khoản Discord (hoặc các dịch vụ thông báo khác như Telegram, Slack).
- API Key và thông tin xác thực cho Amazon Luna (nếu cần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/10733).
2. Nhấn nút "Download" để tải file JSON.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Edit Fields"**:
   - Cấu hình các headers yêu cầu cho yêu cầu Amazon Luna:
     - `x-amz-locale` (ngôn ngữ/địa điểm)
     - `x-amz-marketplace-id` (thị trường cho khu vực của bạn)
     - `Accept-Language`
     - `User-Agent`
     - platform và device type

2. **Node "Get row(s) in sheet"**:
   - Chọn credentials Google API.
   - Nhập ID của Google Sheet và tên sheet chứa danh sách game.

3. **Node "Send a message1"**:
   - Chọn credentials Discord OAuth2 API.
   - Nhập Channel ID để nhận thông báo.

4. **Node "Append or update row in sheet"**:
   - Chọn credentials Google API.
   - Nhập ID của Google Sheet và tên sheet để lưu trữ dữ liệu.

5. **Node "Schedule Trigger"**:
   - Cấu hình lịch chạy workflow (ví dụ: hàng ngày lúc 8:00 sáng).

#### 3. Kích hoạt ⚡️
- Nhấn nút "Execute Workflow" để test với dữ liệu mẫu.
- Sau khi test thành công, nhấn "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Telegram**: Thay thế node Discord bằng node Telegram để nhận thông báo trên ứng dụng ưa thích.
- **Lưu log hoạt động**: Thêm node để lưu log các lần chạy workflow để theo dõi hiệu suất.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo hàng tuần/tuần về danh sách game mới.
- **Tích hợp với Notion**: Thay thế Google Sheets bằng Notion để quản lý danh sách game theo phong cách Notion.

### 📌 Kết luận
Workflow này giúp các sếp game thủ tiết kiệm thời gian và nâng cao trải nghiệm chơi game bằng cách tự động đồng bộ danh sách game Prime Amazon Luna lên Google Sheets và nhận thông báo tức thì khi có game mới. Hãy thử ngay và tận hưởng sự tiện lợi của tự động hóa!