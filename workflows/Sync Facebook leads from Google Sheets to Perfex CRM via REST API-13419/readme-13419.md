---
title: "🚀 Tự động đồng bộ dữ liệu khách hàng từ Facebook Lead Ads vào Perfex CRM qua Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ dữ liệu khách hàng từ Facebook Lead Ads vào Perfex CRM thông qua Google Sheets, tránh trùng lặp và tiết kiệm thời gian cho đội ngũ bán hàng và chăm sóc khách hàng."
slug: "tu-dong-dong-bo-du-lieu-khach-hang-facebook-perfex-crm"
tags: [n8n, automation, no-code, crm, google-sheets]
keywords: [n8n workflow, tự động hóa, crm, google sheets, facebook lead ads]
---

# 🚀 Tự động đồng bộ dữ liệu khách hàng từ Facebook Lead Ads vào Perfex CRM qua Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình đồng bộ dữ liệu khách hàng từ Facebook Lead Ads vào Perfex CRM.
- Tránh trùng lặp dữ liệu khách hàng, tiết kiệm thời gian và công sức cho đội ngũ bán hàng và chăm sóc khách hàng.
- Tự động cập nhật trạng thái khách hàng trong Google Sheets và lưu trữ liên kết trực tiếp đến hồ sơ CRM.
- Hoạt động liên tục 24/7 với lịch trình kiểm tra mỗi phút.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- Tài khoản Perfex CRM với quyền truy cập vào REST API.
- API token từ Perfex CRM (cần cài đặt module "Rest API" trong Perfex).
- Google Sheets có ít nhất các cột: `email`, `full_name`, `phone_number`, và `lead_status`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Schedule trigger (every minute)**: Node này sẽ kích hoạt workflow mỗi phút để kiểm tra dữ liệu mới.
- **Google Sheets: Get leads with status CREATED**: Cấu hình credentials Google Sheets và điền thông tin về Sheet ID, tên Sheet, và phạm vi dữ liệu cần lấy (ví dụ: `A:D`).
- **Split in batches**: Cấu hình kích thước batch để xử lý dữ liệu theo từng nhóm (ví dụ: 10 bản ghi mỗi lần).
- **Perfex: Search lead by email**: Cấu hình credentials Perfex CRM và điền URL cơ sở của Perfex CRM.
- **IF: Lead exists**: Node này sẽ kiểm tra xem khách hàng đã tồn tại trong Perfex CRM hay chưa.
- **IF: Lead not found (404)**: Node này sẽ xử lý trường hợp khách hàng chưa tồn tại trong Perfex CRM.
- **Perfex: Create lead**: Cấu hình thông tin cần thiết để tạo khách hàng mới trong Perfex CRM (ví dụ: tên, email, số điện thoại, người phụ trách).
- **Google Sheets: Mark as ADDED (existing)**: Cấu hình cập nhật trạng thái khách hàng trong Google Sheets thành `ADDED` và lưu trữ liên kết trực tiếp đến hồ sơ CRM.
- **Google Sheets: Mark as ADDED (new)**: Tương tự như node trên, nhưng dành cho khách hàng mới được tạo.
- **Wait (rate limit buffer)**: Cấu hình thời gian chờ giữa các yêu cầu để tránh bị giới hạn tốc độ từ Perfex CRM.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có khách hàng mới được thêm vào Perfex CRM.
- Lưu log hoạt động của workflow để theo dõi và giải quyết vấn đề nếu có.
- Gửi báo cáo định kỳ về số lượng khách hàng mới được thêm vào Perfex CRM.

### 📌 Kết luận
Workflow này giúp tự động hóa toàn bộ quy trình đồng bộ dữ liệu khách hàng từ Facebook Lead Ads vào Perfex CRM, tiết kiệm thời gian và công sức cho đội ngũ bán hàng và chăm sóc khách hàng. Các sếp hãy áp dụng ngay để nâng cao hiệu suất làm việc!