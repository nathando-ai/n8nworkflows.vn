---
title: "🚀 Tự động hóa quản lý khách hàng tiềm năng: Đồng bộ từ Google Sheets đến Instantly với n8n"
description: "Hướng dẫn chi tiết cách tự động hóa việc quản lý khách hàng tiềm năng bằng cách đồng bộ dữ liệu từ Google Sheets đến Instantly email campaigns thông qua n8n, giúp tiết kiệm thời gian và tăng hiệu quả làm việc."
slug: "tu-dong-hoa-quan-ly-khach-hang-tiem-nang-google-sheets-instantly-n8n"
tags: [n8n, automation, no-code, email-marketing, crm]
keywords: [n8n workflow, tự động hóa, quản lý khách hàng tiềm năng, email marketing, crm]
---

# 🚀 Tự động hóa quản lý khách hàng tiềm năng: Đồng bộ từ Google Sheets đến Instantly với n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý khách hàng tiềm năng thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý khách hàng tiềm năng thủ công
- Tăng hiệu quả làm việc bằng cách tự động hóa quy trình
- Giảm thiểu lỗi và tăng độ chính xác trong quản lý khách hàng
- Tích hợp liền mạch giữa Google Sheets và Instantly email campaigns
- Xử lý hàng loạt khách hàng tiềm năng một cách hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản Instantly với API key
- Dữ liệu khách hàng tiềm năng trong Google Sheets theo định dạng đã chỉ định
- Biết cách tạo và cấu hình Data Table trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Node "When clicking 'Execute workflow'"**: Đây là điểm khởi đầu của workflow. Các sếp có thể kích hoạt workflow thủ công bằng cách nhấp vào nút "Execute workflow" trong giao diện n8n.

- **Node "Get row(s) in sheet"**: Cấu hình node này để lấy dữ liệu từ Google Sheets. Các sếp cần:
  - Chọn credentials Google Sheets OAuth2 đã được thiết lập
  - Chỉ định ID của Google Sheet và tên của sheet chứa dữ liệu khách hàng tiềm năng
  - Đảm bảo các cột cần thiết (Firstname, Email, Website, Company, Title) được bao gồm trong dữ liệu

- **Node "Create a lead"**: Cấu hình node này để tạo khách hàng tiềm năng trong Instantly. Các sếp cần:
  - Chọn credentials Instantly API đã được thiết lập
  - Chỉ định ID của chiến dịch Instantly mà các sếp muốn gửi email
  - Đảm bảo các trường dữ liệu được ánh xạ chính xác giữa Google Sheets và Instantly

- **Node "Get row(s)"**: Cấu hình node này để lấy dữ liệu từ Data Table trong n8n. Các sếp cần:
  - Chọn Data Table đã được tạo trước đó
  - Thiết lập bộ lọc để chỉ lấy các khách hàng tiềm năng chưa được xử lý (campaign = "start")

- **Node "Update row(s)"**: Cấu hình node này để cập nhật trạng thái của khách hàng tiềm năng trong Data Table. Các sếp cần:
  - Chọn Data Table đã được tạo trước đó
  - Thiết lập các trường dữ liệu cần cập nhật (campaign = "added to instantly")

- **Node "Loop Over Items1" và "Loop Over Items"**: Cấu hình các node này để xử lý dữ liệu theo lô. Các sếp cần:
  - Thiết lập kích thước lô (batch size) là 30 để tránh vượt quá giới hạn API
  - Đảm bảo các node xử lý dữ liệu theo lô được kết nối đúng cách

- **Node "Update row(s)1"**: Cấu hình node này để cập nhật trạng thái của khách hàng tiềm năng trong Data Table sau khi đã xử lý. Các sếp cần:
  - Chọn Data Table đã được tạo trước đó
  - Thiết lập các trường dữ liệu cần cập nhật (campaign = "added to instantly")

- **Node "Schedule Trigger"**: Cấu hình node này để chạy workflow theo lịch. Các sếp cần:
  - Thiết lập lịch chạy workflow theo nhu cầu của doanh nghiệp
  - Đảm bảo workflow được kích hoạt đúng thời gian để xử lý dữ liệu mới nhất

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể thêm node Slack/Telegram để nhận thông báo khi workflow chạy thành công hoặc gặp lỗi.
- Các sếp có thể lưu log hoạt động của workflow để theo dõi và phân tích hiệu suất.
- Các sếp có thể gửi báo cáo định kỳ về hoạt động của workflow để quản lý và tối ưu hóa hiệu quả.

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc quản lý khách hàng tiềm năng bằng cách tự động hóa quy trình đồng bộ dữ liệu từ Google Sheets đến Instantly email campaigns thông qua n8n. Với workflow này, các sếp có thể tiết kiệm thời gian, tăng hiệu quả làm việc và giảm thiểu lỗi trong quản lý khách hàng tiềm năng.