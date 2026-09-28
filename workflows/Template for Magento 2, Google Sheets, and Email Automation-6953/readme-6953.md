---
title: "🚀 Tự động hóa Magento 2 + Google Sheets + Email: Báo cáo tuần tự động cho Shop Online"
description: "Hướng dẫn chi tiết cách tự động hóa báo cáo hàng tuần từ Magento 2 sang Google Sheets và gửi email thông báo. Tiết kiệm 80% thời gian thủ công với workflow n8n."
slug: "tu-dong-hoa-magento-2-google-sheets-email"
tags: [n8n, automation, magento, google-sheets, email]
keywords: [n8n workflow, tự động hóa báo cáo, magento 2, google sheets, email marketing]
---

# 🚀 Tự động hóa Magento 2 + Google Sheets + Email: Báo cáo tuần tự động cho Shop Online

[Các sếp shop online] có biết không? Với việc bán hàng online ngày càng phát triển, việc theo dõi và báo cáo doanh số hàng tuần đang trở thành một công việc tốn thời gian và dễ gây lỗi. Hãy tưởng tượng: mỗi tuần bạn phải:

1. Truy cập Magento 2 để lấy dữ liệu đơn hàng
2. Tính toán thủ công các chỉ số quan trọng
3. Copy-paste dữ liệu sang Google Sheets
4. Soạn email báo cáo gửi cho team

Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này trong vòng 15 phút cài đặt!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian**: Không cần làm thủ công mỗi tuần
- **Dữ liệu chính xác 100%**: Không còn sai sót do copy-paste
- **Báo cáo tự động**: Nhận báo cáo hàng tuần vào đúng giờ
- **Dễ dàng theo dõi**: Dữ liệu được lưu trữ trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Magento 2 (cần quyền truy cập API)
- Tài khoản Google (để tạo và quản lý Google Sheets)
- Tài khoản Gmail (để gửi email báo cáo)
- Thông tin xác thực cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/6953)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Thiết lập lịch chạy hàng tuần (ví dụ: mỗi Chủ Nhật lúc 8h sáng)
   - Chọn múi giờ phù hợp với shop

2. **Node "Get Last Week Orders"**:
   - Cấu hình credentials cho Magento 2 API
   - Điền URL API endpoint của Magento 2 (thường là `https://yourstore.com/rest/V1/orders`)
   - Thêm header `Authorization: Bearer YOUR_MAGENTO_API_TOKEN`

3. **Node "Create spreadsheet"**:
   - Cấu hình credentials cho Google Sheets
   - Điền tên file Google Sheets mong muốn (ví dụ: "Magento Weekly Reports")
   - Thiết lập tên sheet cho báo cáo tuần (ví dụ: "Weekly Summary")

4. **Node "Send a message"**:
   - Cấu hình credentials cho Gmail
   - Điền địa chỉ email người nhận
   - Soạn nội dung email báo cáo (có thể sử dụng biến từ các node trước)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test chạy dữ liệu mẫu
2. Kiểm tra:
   - Dữ liệu đã được lấy từ Magento 2
   - Google Sheets đã được tạo và cập nhật
   - Email báo cáo đã được gửi
3. Nếu mọi thứ ổn, click vào nút "Activate" để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack**: Thêm node Slack để nhận thông báo khi workflow chạy
2. **Báo cáo định kỳ**: Thiết lập lịch chạy hàng tháng cho báo cáo tổng hợp
3. **Báo cáo sản phẩm**: Thêm phân tích chi tiết về sản phẩm bán chạy nhất
4. **Báo cáo khách hàng**: Thêm phân tích về khách hàng mới và khách hàng quay lại

### 📌 Kết luận
Với workflow này, các sếp shop online có thể tự động hóa hoàn toàn báo cáo hàng tuần, tiết kiệm thời gian quý giá và giảm thiểu sai sót. Hãy thử ngay và trải nghiệm sự khác biệt! 🚀