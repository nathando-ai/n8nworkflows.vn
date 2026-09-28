---
title: "📊 [Tự động hóa] Theo dõi và phân tích kết quả giao dịch Forex từ MyFxBook và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa phân tích kết quả giao dịch Forex bằng n8n, kết hợp MyFxBook và Google Sheets để tối ưu hóa chiến lược giao dịch."
slug: "tu-dong-hoa-phan-tich-ket-qua-giao-dich-forex"
tags: [n8n, automation, forex, trading, google-sheets]
keywords: [n8n workflow, tự động hóa giao dịch forex, phân tích kết quả giao dịch, google sheets forex, myfxbook automation]
---

# 📊 [Tự động hóa] Theo dõi và phân tích kết quả giao dịch Forex từ MyFxBook và Google Sheets

[Các sếp giao dịch Forex thường phải mất nhiều thời gian để theo dõi và phân tích kết quả giao dịch hàng ngày. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian phân tích kết quả giao dịch hàng ngày
- Tự động cập nhật dữ liệu High/Low từ MyFxBook
- Phân tích tự động lợi nhuận/lỗ lẻm của các giao dịch
- Tối ưu hóa chiến lược giao dịch dựa trên dữ liệu thực tế
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt
- Tài khoản MyFxBook để truy cập dữ liệu giá
- File Google Sheets mẫu (có thể tải từ [đây](https://docs.google.com/spreadsheets/d/1OhrbUQEc_lGegk5pRWWKz5nrnMbTZGT0lxK9aJqqId4/edit?usp=drive_link))
- Credentials cho Google Sheets và MyFxBook trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8522](https://n8n.io/workflows/8522)
2. Click vào nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get row(s) in sheet"**:
   - Chọn credentials Google Sheets đã cấu hình
   - Điền thông tin Sheet ID và tên sheet chứa dữ liệu giao dịch

2. **Node "HTTP Request"**:
   - Cấu hình endpoint API MyFxBook để lấy dữ liệu giá
   - Đảm bảo có API key hợp lệ cho MyFxBook

3. **Nodes cập nhật Google Sheets**:
   - Tất cả các node Google Sheets cần được cấu hình với cùng credentials
   - Kiểm tra Sheet ID và tên sheet để đảm bảo trùng khớp với file dữ liệu

4. **Node "Schedule Trigger"**:
   - Cấu hình lịch chạy workflow (thường là hàng ngày vào cuối phiên giao dịch)

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả trên Google Sheets để đảm bảo dữ liệu được cập nhật đúng
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Telegram/Slack để nhận thông báo kết quả giao dịch
2. Thêm node để lưu log các giao dịch có lợi nhuận cao
3. Tự động gửi báo cáo hàng tuần về hiệu suất giao dịch
4. Kết nối với các công cụ phân tích kỹ thuật khác để tối ưu hóa chiến lược

### 📌 Kết luận
Workflow này giúp các sếp giao dịch Forex tiết kiệm thời gian đáng kể trong việc phân tích kết quả giao dịch hàng ngày. Bằng cách tự động hóa toàn bộ quá trình, các sếp có thể tập trung vào việc tối ưu hóa chiến lược giao dịch và cải thiện hiệu suất đầu tư. Hãy thử ngay và nâng cao hiệu quả giao dịch của mình!