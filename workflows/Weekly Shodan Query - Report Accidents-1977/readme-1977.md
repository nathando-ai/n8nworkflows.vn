---
title: "🚀 Tự động hóa theo dõi cổng mở bất thường bằng Shodan và TheHive"
description: "Hướng dẫn tự động hóa kiểm tra hàng tuần các cổng mở bất thường trên hệ thống mạng bằng Shodan và báo cáo lên TheHive để tăng cường bảo mật."
slug: "tu-dong-hoa-theo-doi-cong-mo-bat-thuong-shodan-thehive"
tags: [n8n, automation, no-code, secops, thehive, shodan]
keywords: [n8n workflow, tự động hóa bảo mật, secops, thehive, shodan]
---

# 🚀 Tự động hóa theo dõi cổng mở bất thường bằng Shodan và TheHive

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa kiểm tra hàng tuần các cổng mở bất thường trên hệ thống mạng.
- Tiết kiệm thời gian và công sức cho đội ngũ bảo mật.
- Tăng cường khả năng phản ứng với các mối đe dọa bảo mật.
- Tích hợp liền mạch với hệ thống quản lý sự cố TheHive.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shodan với API key.
- Tài khoản TheHive với API key.
- Danh sách IP và cổng cần theo dõi (định dạng JSON).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/1977).
2. Nhấn nút "Download" để tải file JSON.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Node "Get watched IPs & Ports"**: Cấu hình API endpoint để lấy danh sách IP và cổng cần theo dõi. Đảm bảo dữ liệu trả về đúng định dạng JSON như ví dụ:
  ```json
  [
    {
      "ip": "116.202.106.35",
      "ports": [5678, 80]
    },
    {
      "ip": "188.114.96.9",
      "ports": [8080, 80]
    }
  ]
  ```

- **Node "Scan each IP"**: Cấu hình credentials "httpQueryAuth" với API key của Shodan.

- **Node "Create TheHive alert"**: Cấu hình credentials "theHiveApi" với API key của TheHive.

- **Node "Every Monday"**: Cấu hình lịch chạy hàng tuần (mặc định là mỗi thứ Hai lúc 9:00 AM).

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có cổng mở bất thường.
- Lưu log các kết quả kiểm tra vào Google Sheets hoặc cơ sở dữ liệu.
- Tự động gửi báo cáo hàng tuần qua email cho các thành viên trong đội ngũ bảo mật.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình theo dõi cổng mở bất thường hàng tuần, giảm thiểu rủi ro bảo mật và tăng cường khả năng phản ứng với các mối đe dọa. Hãy áp dụng ngay để nâng cao hiệu quả bảo mật của hệ thống mạng!