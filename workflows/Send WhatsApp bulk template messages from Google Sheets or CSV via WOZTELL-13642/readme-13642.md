---
title: "🚀 Gửi tin nhắn WhatsApp hàng loạt từ Google Sheets hoặc CSV qua WOZTELL"
description: "Hướng dẫn tự động hóa gửi tin nhắn WhatsApp theo mẫu hàng loạt từ danh sách liên hệ trong Google Sheets hoặc file CSV thông qua WOZTELL"
slug: "gui-tin-nhan-whatsapp-hang-loat-tu-google-sheets-hoac-csv-qua-woztell"
tags: [n8n, automation, no-code, whatsapp, social media]
keywords: [n8n workflow, tự động hóa, whatsapp marketing, gửi tin nhắn hàng loạt, woztell]
---

# 🚀 Gửi tin nhắn WhatsApp hàng loạt từ Google Sheets hoặc CSV qua WOZTELL

[Các sếp đang gặp khó khăn khi phải gửi tin nhắn WhatsApp hàng loạt cho hàng trăm khách hàng thông qua các công cụ truyền thống như Excel hay các ứng dụng nhắn tin thông thường. Việc này tốn thời gian, dễ gây lỗi và không thể theo dõi được quá trình gửi tin. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần viết code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi gửi hàng loạt tin nhắn WhatsApp
- Đảm bảo tin nhắn được gửi theo đúng mẫu đã được phê duyệt
- Theo dõi trạng thái gửi tin (thành công/thất bại) trong Google Sheets
- Tự động hóa toàn bộ quy trình mà không cần can thiệp thủ công
- Giảm thiểu lỗi khi gửi tin nhắn hàng loạt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- File CSV chứa danh sách liên hệ (hoặc sử dụng Google Sheets)
- Tài khoản WOZTELL với WhatsApp Business API đã được cấu hình
- Các mẫu tin nhắn WhatsApp đã được phê duyệt
- Tài khoản n8n để chạy workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/13642](https://n8n.io/workflows/13642)
2. Nhấn nút "Import" để tải workflow về máy
3. Trong n8n Editor, nhấn vào biểu tượng "+" và chọn "Import from File"
4. Chọn file JSON đã tải về và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get row(s) in sheet"**:
   - Cấu hình credentials Google API
   - Chọn Spreadsheet ID và Sheet Name chứa danh sách liên hệ
   - Đảm bảo có cột "Sent" để theo dõi trạng thái gửi tin

2. **Node "Send message template"**:
   - Cấu hình credentials WOZTELL
   - Chọn template WhatsApp đã được phê duyệt
   - Map các trường dữ liệu từ Google Sheets vào các biến trong template

3. **Node "Update row in sheet"**:
   - Đảm bảo cấu hình Google API giống với node "Get row(s) in sheet"
   - Cập nhật đúng Spreadsheet ID và Sheet Name

4. **Node "Extract from File"**:
   - Đảm bảo file CSV có cấu trúc phù hợp (cột Phone number và Name)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn "Execute workflow" để kiểm tra
2. Kiểm tra kết quả trong Google Sheets để xác nhận tin nhắn đã được gửi
3. Nếu mọi thứ hoạt động tốt, nhấn "Active workflow" để kích hoạt tự động hóa

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh mẫu tin nhắn**: Có thể chỉnh sửa template WhatsApp để phù hợp với nhu cầu marketing của doanh nghiệp
2. **Thêm hệ thống xác nhận**: Kết hợp với node "Email" hoặc "SMS" để xác nhận người nhận trước khi gửi tin nhắn
3. **Lập lịch gửi tin**: Sử dụng node "Schedule Trigger" để tự động hóa gửi tin nhắn theo lịch trình
4. **Báo cáo kết quả**: Kết hợp với node "Google Sheets" để tạo báo cáo tổng hợp kết quả gửi tin

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình gửi tin nhắn WhatsApp hàng loạt từ danh sách liên hệ trong Google Sheets hoặc file CSV thông qua WOZTELL. Với việc tự động hóa toàn bộ quy trình, các sếp có thể tiết kiệm thời gian đáng kể và giảm thiểu lỗi khi gửi tin nhắn hàng loạt. Hãy áp dụng ngay workflow này để nâng cao hiệu quả marketing và chăm sóc khách hàng của doanh nghiệp!