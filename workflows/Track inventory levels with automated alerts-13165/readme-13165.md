---
title: "🚀 Theo dõi mức tồn kho với cảnh báo tự động - Workflow n8n hoàn chỉnh"
description: "Giải pháp tự động hóa quản lý tồn kho với cảnh báo thời gian thực qua Slack và Email, giúp các sếp tiết kiệm thời gian và tránh thiếu hàng"
slug: "theo-doi-ton-kho-voi-canh-bao-tu-dong"
tags: [n8n, automation, inventory, project-management, no-code]
keywords: [n8n workflow, tự động hóa tồn kho, cảnh báo tồn kho, quản lý kho, n8n template]
---

# 🚀 Theo dõi mức tồn kho với cảnh báo tự động - Workflow n8n hoàn chỉnh

[Các sếp] có bao giờ phải mất hàng giờ mỗi ngày để kiểm tra tồn kho, tính toán mức cảnh báo và gửi thông báo thủ công? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong vòng 15 phút, hoàn toàn không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình quản lý tồn kho
- **Chính xác 100%**: Không còn sai sót do thủ công
- **Cảnh báo thời gian thực**: Nhận thông báo ngay khi tồn kho đạt ngưỡng cảnh báo
- **Hoạt động liên tục**: Theo dõi 24/7 mà không cần can thiệp
- **Dễ dàng mở rộng**: Kết nối thêm các hệ thống khác như ERP, CRM...
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack (hoặc Teams, Telegram)
- Tài khoản Gmail (để gửi email cảnh báo)
- API endpoint cho hệ thống quản lý tồn kho của các sếp
- Credentials cho các dịch vụ trên (Slack, Gmail, API)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/13165)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

Hoặc có thể copy/paste JSON từ trang web vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook - Inventory Movement**:
   - Đặt tên webhook (ví dụ: "inventory-movement")
   - Chọn phương thức HTTP (thường là POST)
   - Điền đường dẫn webhook (ví dụ: `/webhook/inventory`)

2. **Node Slack - Critical Alert, Slack - Urgent Alert, Slack - Warning Alert**:
   - Tạo Slack App và lấy API token
   - Chọn channel để gửi thông báo
   - Cấu hình thông điệp cảnh báo (có thể chỉnh sửa trong node Format Critical/Urgent/Warning Alert)

3. **Node Gmail - Critical Alert**:
   - Cấu hình tài khoản Gmail
   - Điền địa chỉ email người nhận
   - Chỉnh sửa nội dung email trong node Format Critical Alert

4. **Node API - Record Movement, API - Get Current Stock, API - Log Audit Trail**:
   - Cấu hình URL endpoint của hệ thống quản lý tồn kho
   - Điền các headers cần thiết (Authorization, Content-Type...)
   - Chỉnh sửa body request trong các node Prepare API Body và Prepare Audit Entry

5. **Node Check Stock Levels**:
   - Chỉnh sửa logic kiểm tra ngưỡng cảnh báo trong code node
   - Thay đổi các giá trị ngưỡng cảnh báo (ví dụ: critical < 10, urgent 10-20, warning 20-30)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
3. Kiểm tra các kênh Slack và Email để xác nhận nhận được thông báo

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết nối với hệ thống ERP/CRM**: Thêm node để đồng bộ dữ liệu tồn kho với hệ thống quản lý khác
2. **Gửi báo cáo định kỳ**: Thêm node để tổng hợp dữ liệu tồn kho và gửi báo cáo hàng ngày
3. **Tích hợp với Telegram**: Thay thế node Slack bằng node Telegram để nhận thông báo
4. **Lưu log chi tiết**: Thêm node để lưu log chi tiết các giao dịch tồn kho

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình quản lý tồn kho, từ ghi nhận giao dịch đến cảnh báo khi đạt ngưỡng tồn kho. Với việc triển khai chỉ trong 15 phút, các sếp có thể tiết kiệm hàng giờ mỗi ngày và tránh những rủi ro thiếu hàng. Hãy áp dụng ngay để nâng cao hiệu quả quản lý kho của các sếp!