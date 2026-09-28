---
title: "🚀 Tự động hóa Zendesk: Theo dõi vé chờ xử lý với Gmail, Google Sheets & ClickUp"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp theo dõi vé chờ xử lý trong Zendesk, ghi log vào Google Sheets, tạo nhiệm vụ ClickUp và gửi email nhắc nhở khách hàng."
slug: "tu-dong-hoa-zendesk-pending-ticket-follow-up"
tags: [n8n, automation, no-code, zendesk, google-sheets, clickup, gmail]
keywords: [n8n workflow, tự động hóa, zendesk, google sheets, clickup, gmail]
---

# 🚀 Tự động hóa Zendesk: Theo dõi vé chờ xử lý với Gmail, Google Sheets & ClickUp

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi vé chờ xử lý trong Zendesk thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình theo dõi vé chờ xử lý hàng ngày.
- Chính xác: Lọc và xử lý dữ liệu vé một cách tự động và chính xác.
- Cá nhân hóa: Gửi email nhắc nhở khách hàng với nội dung phù hợp.
- Hoạt động liên tục: Workflow chạy tự động từ thứ Hai đến thứ Sáu lúc 20:00.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zendesk với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets và Gmail.
- Tài khoản ClickUp với quyền tạo nhiệm vụ.
- API keys và credentials cho các dịch vụ trên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8743](https://n8n.io/workflows/8743).
2. Nhấn nút "Download" để tải file JSON.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Schedule Trigger**: Đặt lịch chạy workflow từ thứ Hai đến thứ Sáu lúc 20:00.
- **Get Pending Tickets**: Cấu hình credentials cho Zendesk API và đảm bảo chỉ lấy vé có trạng thái "pending".
- **Filter Pending Tickets**: Đảm bảo logic lọc chỉ xử lý vé có trạng thái "pending".
- **Format Ticket Data**: Kiểm tra và điều chỉnh mã code để định dạng dữ liệu vé theo yêu cầu.
- **Log to Google Sheets**: Cấu hình credentials cho Google Sheets OAuth2 và chỉ định sheet và phạm vi cần ghi dữ liệu.
- **Create ClickUp Task**: Cấu hình credentials cho ClickUp API và đảm bảo tạo nhiệm vụ với thông tin chi tiết đầy đủ.
- **Generate Follow-up Emails**: Kiểm tra và điều chỉnh mã code để tạo email nhắc nhở khách hàng với nội dung phù hợp.
- **Send Follow-up Email**: Cấu hình credentials cho Gmail OAuth2 và đảm bảo gửi email với định dạng HTML.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để chạy tự động theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để thông báo khi có vé mới.
- Lưu log chi tiết vào Google Sheets để theo dõi lịch sử vé.
- Gửi báo cáo định kỳ về tình trạng vé chờ xử lý qua email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình theo dõi vé chờ xử lý trong Zendesk, ghi log vào Google Sheets, tạo nhiệm vụ ClickUp và gửi email nhắc nhở khách hàng. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!