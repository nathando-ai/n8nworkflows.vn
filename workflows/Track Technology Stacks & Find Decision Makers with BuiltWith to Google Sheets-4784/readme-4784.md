---
title: "🚀 Tự động hóa tìm kiếm công nghệ và ghi dữ liệu vào Google Sheets với BuiltWith và n8n"
description: "Hướng dẫn chi tiết cách tự động hóa việc tìm kiếm các trang web sử dụng công nghệ cụ thể và ghi dữ liệu vào Google Sheets để phục vụ lead generation, email marketing và phân tích thị trường."
slug: "tu-dong-hoa-tim-kiem-cong-nghe-voi-builtwith-google-sheets"
tags: [n8n, automation, no-code, lead generation, marketing]
keywords: [n8n workflow, tự động hóa, lead generation, marketing, công nghệ]
---

# 🚀 Tự động hóa tìm kiếm công nghệ và ghi dữ liệu vào Google Sheets với BuiltWith và n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức trong việc tìm kiếm và ghi dữ liệu thủ công.
- Tự động hóa việc thu thập thông tin về các trang web sử dụng công nghệ cụ thể.
- Dữ liệu được lưu trữ và quản lý dễ dàng trong Google Sheets.
- Hỗ trợ lead generation, email marketing và phân tích thị trường.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để kết nối với Google Sheets.
- API Key của BuiltWith để truy cập dữ liệu.
- Biết cách tạo và cấu hình credentials trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Manual Trigger**: Node này cho phép các sếp chạy workflow thủ công khi cần thiết.
- **Set Technology**: Node này cho phép các sếp định nghĩa công nghệ cần tìm kiếm (ví dụ: "Shopify").
- **Fetch BuiltWith Data**: Node này gửi yêu cầu GET đến API của BuiltWith để tìm kiếm các trang web sử dụng công nghệ đã định nghĩa. Các sếp cần thay thế `YOUR_API_KEY` bằng API Key thực tế của mình.
- **Extract Site Info**: Node này xử lý dữ liệu JSON từ BuiltWith và trích xuất các trường thông tin quan trọng như `domain`, `technology`, `firstIndexed`, và `vertical`.
- **Log to Google Sheet**: Node này ghi dữ liệu đã xử lý vào Google Sheets. Các sếp cần cấu hình credentials Google Sheets và chỉ định tên sheet và phạm vi cần ghi.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể sao chép workflow này và sử dụng cho bất kỳ API nào khác, chỉ cần thay đổi API và cấu hình tương ứng.
- Có thể kết hợp với các công cụ khác như Slack hoặc Telegram để thông báo khi workflow hoàn thành.
- Lưu log hoạt động của workflow để theo dõi và phân tích hiệu suất.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc tìm kiếm và ghi dữ liệu thủ công. Dữ liệu được lưu trữ và quản lý dễ dàng trong Google Sheets, hỗ trợ lead generation, email marketing và phân tích thị trường. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của mình!