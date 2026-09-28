---
title: "📄 Tự động hóa xử lý hóa đơn PDF từ Gmail với PDF Vector và thông báo Slack"
description: "Hướng dẫn chi tiết cách tự động hóa việc xử lý hóa đơn PDF từ Gmail, trích xuất thông tin bằng AI và thông báo kết quả qua Slack"
slug: "tu-dong-hoa-xu-ly-hoa-don-pdf-tu-gmail-voi-pdf-vector-va-thong-bao-slack"
tags: [n8n, automation, no-code, pdf, invoice, ai]
keywords: [n8n workflow, tự động hóa hóa đơn, xử lý PDF, PDF Vector, Slack alert]
---

# 📄 Tự động hóa xử lý hóa đơn PDF từ Gmail với PDF Vector và thông báo Slack

[Các sếp] có bao giờ phải xử lý hàng chục hóa đơn PDF mỗi ngày từ Gmail không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhận email đến xác thực và thông báo kết quả - hoàn toàn không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý hàng chục hóa đơn mỗi ngày mà không cần chạm tay
- **Chính xác cao**: Kiểm tra tự động tất cả các số liệu trên hóa đơn
- **Theo dõi thực tế**: Log hóa đơn hợp lệ và báo cáo lỗi ngay trên Google Sheets
- **Thông báo tức thì**: Nhận cảnh báo qua Slack khi có hóa đơn không hợp lệ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ
- API Key từ [PDF Vector](https://pdfvector.com/api-keys)
- Google Sheet với 2 tab: "Invoices" và "Flagged Invoices"
- Kênh Slack để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13069](https://n8n.io/workflows/13069)
2. Click "Import" và chọn "Import from URL"
3. Dán URL vào ô nhập liệu và nhấn "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Gmail Trigger**:
   - Kết nối với tài khoản Gmail cần theo dõi
   - Đảm bảo đã cấp quyền đầy đủ cho n8n

2. **PDF Vector - Extract invoice**:
   - Thêm API Key từ PDF Vector
   - Có thể điều chỉnh prompt nếu cần trích xuất thông tin khác

3. **Log valid** và **Log flagged**:
   - Kết nối với Google Sheet đã tạo
   - Đảm bảo tên tab khớp với "Invoices" và "Flagged Invoices"

4. **Slack success** và **Slack alert**:
   - Kết nối với kênh Slack mong muốn
   - Có thể tùy chỉnh nội dung thông báo

#### 3. Kích hoạt ⚡️
1. Chạy test với một hóa đơn mẫu để kiểm tra toàn bộ quy trình
2. Sau khi xác nhận hoạt động bình thường, bật chế độ Active

### ✍️ Mẹo & gợi ý nâng cao
1. **Điều chỉnh độ chính xác**: Trong node "Validate invoice", các sếp có thể thay đổi giá trị ±$0.01 để phù hợp với yêu cầu kiểm tra
2. **Kết hợp thêm dịch vụ**: Thay thế Slack bằng email hoặc Microsoft Teams
3. **Tự động hóa thêm**: Kết nối với hệ thống kế toán để tự động hóa việc nhập liệu
4. **Báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp hàng tuần qua email

### 📌 Kết luận
Với workflow này, các sếp có thể hoàn toàn tự động hóa quy trình xử lý hóa đơn PDF từ Gmail, từ việc trích xuất thông tin đến xác thực và thông báo kết quả. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu lỗi trong quá trình xử lý hóa đơn hàng ngày!