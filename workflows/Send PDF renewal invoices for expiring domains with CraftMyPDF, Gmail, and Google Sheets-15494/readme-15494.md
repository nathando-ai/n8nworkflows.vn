---
title: "🚀 Tự động hóa hóa đơn gia hạn tên miền với PDF, Gmail và Google Sheets"
description: "Hướng dẫn tự động hóa gửi hóa đơn gia hạn tên miền PDF qua Gmail và cập nhật Google Sheets - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-hoa-hoa-don-gia-han-ten-mien-pdf-gmail-google-sheets"
tags: [n8n, automation, no-code, pdf, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa hóa đơn, gia hạn tên miền, pdf invoice, google sheets api]
---

# 🚀 Tự động hóa hóa đơn gia hạn tên miền với PDF, Gmail và Google Sheets

[Các sếp] có bao giờ phải tự tay gửi hàng chục, hàng trăm hóa đơn gia hạn tên miền mỗi tháng? Phải kiểm tra từng tên miền, tạo PDF, gửi email, cập nhật bảng tính... quá mệt mỏi phải không? Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa hoàn toàn quy trình gửi hóa đơn
- **Chính xác 100%**: Không sót tên miền nào cần gia hạn
- **Cá nhân hóa**: Mỗi hóa đơn chứa thông tin cụ thể của từng tên miền
- **Hoạt động liên tục**: Chạy tự động mỗi ngày mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail)
- API key của CraftMyPDF (dịch vụ tạo PDF)
- Bảng tính Google Sheets đã chuẩn bị theo mẫu
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15494](https://n8n.io/workflows/15494)
2. Click "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Click "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get domains"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền Sheet ID (lấy từ URL bảng tính)
   - Điền tên sheet (thường là "Sheet1" nếu không đổi tên)
   - Điền range (ví dụ: "A2:E" nếu dữ liệu từ cột A đến E)

2. **Node "Create PDF Invoice"**:
   - Chọn credentials HTTP Header Auth
   - Điền URL API của CraftMyPDF (thường là `https://api.craftmypdf.com/v1/pdf`)
   - Điền Template ID (lấy từ CraftMyPDF sau khi tạo template)

3. **Node "Send invoice"**:
   - Chọn credentials Gmail OAuth2
   - Điền địa chỉ email người nhận (sử dụng biểu thức `{{$node["Get domains"].json["email"]}}`)

4. **Node "Update Sheet"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền Sheet ID và tên sheet như node "Get domains"
   - Điền range để cập nhật trạng thái hóa đơn (ví dụ: "F2")

5. **Node "Add next expire date"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền Sheet ID và tên sheet như node "Get domains"
   - Điền range để thêm ngày hết hạn mới (ví dụ: "A:E")

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để test chạy dữ liệu mẫu
2. Kiểm tra email và bảng tính để xác nhận workflow hoạt động
3. Bật "Active workflow" để chạy tự động theo lịch trình

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo khi có lỗi
- Kết hợp với Telegram để gửi báo cáo hàng tuần
- Tạo bản sao bảng tính mới mỗi tháng để lưu trữ dữ liệu
- Thiết lập nhắc nhở trước 30 ngày cho các tên miền sắp hết hạn

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm hàng giờ mỗi tháng trong việc quản lý tên miền. Bằng cách tự động hóa hoàn toàn quy trình gửi hóa đơn, các sếp có thể tập trung vào công việc quan trọng hơn. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!