---
title: "🚀 Tự động hóa dữ liệu từ Form n8n sang Google Sheet, Airtable và gửi Email"
description: "Hướng dẫn chi tiết cách tự động hóa dữ liệu từ form n8n sang Google Sheet, Airtable và gửi email thông qua workflow n8n. Tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-hoa-du-lieu-tu-form-n8n-sang-google-sheet-airtable-va-gui-email"
tags: [n8n, automation, no-code, google-sheets, airtable]
keywords: [n8n workflow, tự động hóa, google sheets, airtable, gửi email]
---

# 🚀 Tự động hóa dữ liệu từ Form n8n sang Google Sheet, Airtable và gửi Email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi các sếp phải xử lý dữ liệu từ form n8n thủ công, việc này tốn nhiều thời gian và dễ xảy ra lỗi. Workflow này giúp tự động hóa toàn bộ quy trình từ khi nhận dữ liệu đến khi lưu trữ và gửi email thông báo, tiết kiệm thời gian đáng kể và đảm bảo tính chính xác cao.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý dữ liệu thủ công.
- Đảm bảo dữ liệu được lưu trữ đồng bộ trên Google Sheets và Airtable.
- Tự động gửi email thông báo đến người dùng, tăng tính chuyên nghiệp.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã cài đặt và cấu hình.
- Tài khoản Google với quyền truy cập vào Google Sheets.
- Tài khoản Airtable với quyền tạo bảng và thêm bản ghi.
- Tài khoản Gmail với quyền gửi email.
- Các credentials cho Google Sheets, Airtable và Gmail đã được cấu hình trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **n8n Form Trigger**:
  - Cấu hình form với các trường Name, City, và Email.
  - Đảm bảo đường dẫn (path) của form là duy nhất và chính xác.

- **Extracting Date and Time Fields from 'submittedAt' Field**:
  - Kiểm tra mã JavaScript trong node này để đảm bảo nó trích xuất đúng Date và Time từ trường submittedAt.

- **Format the Fields**:
  - Cấu hình các trường dữ liệu để đảm bảo định dạng đúng (Name, City, Date, Time, Email).

- **Airtable**:
  - Cấu hình credentials và tham số để tạo bản ghi mới trong Airtable.
  - Đảm bảo bảng và các trường trong Airtable đã được tạo trước đó.

- **Google Sheets**:
  - Cấu hình credentials và tham số để thêm dữ liệu vào Google Sheets.
  - Đảm bảo bảng và các trường trong Google Sheets đã được tạo trước đó.

- **Gmail**:
  - Cấu hình credentials và nội dung email để gửi thông báo đến người dùng.
  - Đảm bảo chủ đề và nội dung email đã được định dạng đúng với các trường dữ liệu.

- **Gmail1**:
  - Cấu hình credentials và nội dung email để gửi thông báo khác đến người dùng.
  - Đảm bảo chủ đề và nội dung email đã được định dạng đúng với các trường dữ liệu.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi có dữ liệu mới.
- Lưu log các hoạt động để theo dõi và phân tích hiệu suất.
- Gửi báo cáo định kỳ về dữ liệu đã được xử lý.

### 📌 Kết luận
Workflow này giúp tự động hóa toàn bộ quy trình từ khi nhận dữ liệu từ form n8n đến khi lưu trữ và gửi email thông báo. Các sếp có thể áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả làm việc.