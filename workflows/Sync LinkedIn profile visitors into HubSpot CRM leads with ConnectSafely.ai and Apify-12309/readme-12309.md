---
title: "🚀 Tự động đồng bộ khách truy cập LinkedIn vào HubSpot với ConnectSafely.ai và Apify"
description: "Hướng dẫn tự động hóa quy trình thu thập và quản lý khách truy cập LinkedIn, giúp tăng hiệu quả chăm sóc khách hàng và tăng doanh thu"
slug: "tu-dong-dong-bo-khach-truy-cap-linkedin-vao-hubspot"
tags: [n8n, automation, no-code, linkedin, hubspot]
keywords: [n8n workflow, tự động hóa, linkedin, hubspot, lead generation]
---

# 🚀 Tự động đồng bộ khách truy cập LinkedIn vào HubSpot với ConnectSafely.ai và Apify

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động thu thập và quản lý khách truy cập LinkedIn trong HubSpot
- Tiết kiệm thời gian và công sức cho đội ngũ sales
- Tăng hiệu quả chăm sóc khách hàng và tăng doanh thu
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ConnectSafely.ai và API key
- Tài khoản Apify để enrich dữ liệu LinkedIn
- Tài khoản HubSpot với quyền tạo và cập nhật contact
- Credentials cho HTTP Bearer Auth
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Run an Actor and get dataset**: Cấu hình credentials `apifyApi` và chọn operation `Run actor and get dataset`.
- **HTTP Request**: Cập nhật Bearer token từ ConnectSafely.ai trong credentials `httpBearerAuth`.
- **Create or update a contact**: Cấu hình credentials `hubspotAppToken` và điền các tham số cần thiết cho HubSpot.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi tần suất chạy workflow theo nhu cầu của doanh nghiệp.
- Thêm các trường dữ liệu bổ sung trong node HubSpot.
- Kết hợp với Slack/Telegram để nhận thông báo khi có khách truy cập mới.
- Lưu log hoạt động của workflow để theo dõi hiệu suất.

### 📌 Kết luận
Workflow này giúp tự động hóa quy trình thu thập và quản lý khách truy cập LinkedIn, giúp các sếp tiết kiệm thời gian và tăng hiệu quả chăm sóc khách hàng. Hãy áp dụng ngay để nâng cao hiệu suất kinh doanh!