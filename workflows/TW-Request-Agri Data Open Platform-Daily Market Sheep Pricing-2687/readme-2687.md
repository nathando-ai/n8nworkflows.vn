---
title: "🐑 Tự động hóa giá thị trường cừu hàng ngày từ Agri Data Open Platform"
description: "Hướng dẫn tự động hóa lấy dữ liệu giá thị trường cừu hàng ngày từ Agri Data Open Platform và lưu vào Google Sheets với n8n"
slug: "tu-dong-hoa-gia-thi-truong-cu-hang-ngay-tu-agri-data-open-platform"
tags: [n8n, automation, no-code, agri-data, google-sheets]
keywords: [n8n workflow, tự động hóa, giá thị trường cừu, Agri Data Open Platform, Google Sheets]
---

# 🐑 Tự động hóa giá thị trường cừu hàng ngày từ Agri Data Open Platform

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động lấy dữ liệu giá thị trường cừu hàng ngày mà không cần can thiệp thủ công.
- Dữ liệu chính xác: Lấy dữ liệu trực tiếp từ Agri Data Open Platform, đảm bảo tính chính xác cao.
- Tích hợp dễ dàng: Lưu dữ liệu vào Google Sheets để phân tích và báo cáo dễ dàng.
- Hoạt động liên tục: Workflow có thể chạy tự động hàng ngày để cập nhật dữ liệu mới nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API key hoặc credentials để truy cập Agri Data Open Platform.
- Tài khoản n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **When clicking ‘Test workflow’**: Node này dùng để kích hoạt workflow. Các sếp có thể sử dụng để kiểm tra workflow trước khi chạy tự động.
- **HTTP Request**: Node này dùng để lấy dữ liệu từ Agri Data Open Platform. Các sếp cần cấu hình URL và phương thức HTTP (GET, POST, v.v.) để lấy dữ liệu.
- **Split Out**: Node này dùng để tách dữ liệu thành các phần nhỏ hơn để xử lý. Các sếp cần cấu hình các trường dữ liệu cần tách.
- **Google Sheets**: Node này dùng để lưu dữ liệu vào Google Sheets. Các sếp cần cấu hình Spreadsheet ID và tên sheet để lưu dữ liệu.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có dữ liệu mới.
- Lưu log hoạt động của workflow để theo dõi và kiểm tra lỗi.
- Gửi báo cáo định kỳ dựa trên dữ liệu đã lưu vào Google Sheets.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc lấy dữ liệu giá thị trường cừu hàng ngày từ Agri Data Open Platform và lưu vào Google Sheets. Với việc tự động hóa này, các sếp có thể tiết kiệm thời gian và đảm bảo dữ liệu luôn được cập nhật mới nhất. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của mình!