---
title: "🔄 Tự động đồng bộ dữ liệu giữa hai ứng dụng với n8n"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu từ PostgreSQL sang Google Sheets bằng workflow n8n, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-du-lieu-giua-postgresql-va-google-sheets"
tags: [n8n, automation, no-code, postgres, google-sheets]
keywords: [n8n workflow, tự động hóa dữ liệu, đồng bộ dữ liệu, postgres google sheets]
---

# 🔄 Tự động đồng bộ dữ liệu giữa hai ứng dụng với n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ dữ liệu mới từ PostgreSQL sang Google Sheets
- Lọc và xử lý dữ liệu trước khi lưu trữ
- Tiết kiệm thời gian và giảm lỗi thủ công
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Dễ dàng tùy chỉnh cho các trường hợp sử dụng khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản PostgreSQL với quyền truy cập cơ sở dữ liệu
- API keys hoặc credentials cho cả hai dịch vụ
- File Google Sheets mẫu đã được sao chép (hướng dẫn trong phần tiếp theo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc trên n8n.io](https://n8n.io/workflows/1930)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong giao diện n8n của bạn, click vào biểu tượng "+" ở góc trái màn hình
4. Chọn "Import from JSON" và dán JSON đã sao chép vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Postgres Trigger** (Node đầu tiên):
   - Chọn credentials cho PostgreSQL của bạn
   - Cấu hình truy vấn SQL để lấy dữ liệu mới
   - Thiết lập khoảng thời gian kiểm tra mới (polling interval)

2. **Filter** (Node thứ hai):
   - Chỉnh sửa điều kiện lọc để phù hợp với dữ liệu của bạn
   - Ví dụ: `{{ $json.email }} does not contain "@n8n.io"`
   - Có thể thêm nhiều điều kiện lọc khác

3. **Google Sheets** (Node cuối cùng):
   - Tạo credentials mới bằng cách đăng nhập Google
   - Chọn file Google Sheets đã sao chép (hướng dẫn trong phần tiếp theo)
   - Chọn sheet cụ thể trong file
   - Cấu hình các cột để ánh xạ dữ liệu

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách click vào nút "Execute Workflow"
2. Kiểm tra kết quả trong Google Sheets của bạn
3. Nếu mọi thứ hoạt động tốt, bật Active workflow để chạy liên tục

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi có dữ liệu mới được đồng bộ
- Lưu log hoạt động vào cơ sở dữ liệu để theo dõi lịch sử
- Tạo báo cáo định kỳ từ dữ liệu đã đồng bộ
- Kết hợp với các dịch vụ khác như HubSpot, Zendesk để tạo chuỗi tự động hóa hoàn chỉnh

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động đồng bộ dữ liệu giữa PostgreSQL và Google Sheets. Với các bước cấu hình đơn giản và linh hoạt, các sếp có thể áp dụng ngay cho nhiều trường hợp sử dụng khác nhau trong doanh nghiệp. Hãy thử ngay và tiết kiệm thời gian quý giá của bạn!