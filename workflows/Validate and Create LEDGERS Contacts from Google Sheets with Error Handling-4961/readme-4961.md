---
title: "🚀 Tự động hóa tạo liên hệ LEDGERS từ Google Sheets với xử lý lỗi"
description: "Hướng dẫn tự động hóa tạo liên hệ LEDGERS từ Google Sheets với xử lý lỗi, tiết kiệm thời gian và giảm sai sót trong quản lý khách hàng"
slug: "tu-dong-hoa-tao-lien-he-ledgers-tu-google-sheets"
tags: [n8n, automation, no-code, ledgers, google-sheets]
keywords: [n8n workflow, tự động hóa, ledgers, google sheets, quản lý khách hàng]
---

# 🚀 Tự động hóa tạo liên hệ LEDGERS từ Google Sheets với xử lý lỗi

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý khách hàng thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian quản lý khách hàng thủ công
- Giảm 90% sai sót khi nhập liệu
- Tự động hóa toàn bộ quy trình từ Google Sheets đến LEDGERS
- Nhận thông báo lỗi ngay khi có vấn đề xảy ra
- Dữ liệu luôn được đồng bộ và chính xác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản LEDGERS với quyền tạo liên hệ mới
- Tài khoản Gmail để nhận thông báo lỗi
- Google Sheets đã được cấu hình với các cột: Tên, Email, Số điện thoại, Địa chỉ...
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4961](https://n8n.io/workflows/4961)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets Trigger**:
   - Chọn credentials Google Sheets của bạn
   - Cấu hình Spreadsheet ID và Sheet Name chứa dữ liệu khách hàng

2. **LEDGERS Node**:
   - Chọn credentials LEDGERS của bạn
   - Đảm bảo tài khoản có quyền tạo liên hệ mới

3. **Gmail Nodes** (3 nodes):
   - Chọn credentials Gmail của bạn
   - Cấu hình email nhận thông báo lỗi
   - Tùy chỉnh nội dung email theo nhu cầu của bạn

4. **Code Nodes** (3 nodes):
   - **Email & Mobile Format Checker**: Có thể điều chỉnh regex để phù hợp với định dạng email/số điện thoại của bạn
   - **Mobile Formatter**: Có thể điều chỉnh logic định dạng số điện thoại
   - **Get Created Time**: Có thể điều chỉnh định dạng thời gian

5. **Google Sheets Update Node**:
   - Chọn credentials Google Sheets
   - Cấu hình Spreadsheet ID và Sheet Name để lưu kết quả
   - Đảm bảo có quyền ghi vào sheet này

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu trước khi kích hoạt
2. Kiểm tra tất cả các node đã được cấu hình đúng
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo lỗi ngay lập tức
- Tạo bản sao dữ liệu trước khi chạy workflow để phòng trường hợp lỗi
- Thiết lập lịch chạy workflow định kỳ để đồng bộ dữ liệu hàng ngày
- Kết hợp với workflow khác để tự động hóa toàn bộ quy trình bán hàng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình tạo liên hệ LEDGERS từ Google Sheets, giảm thiểu sai sót và tiết kiệm thời gian đáng kể. Hãy thử ngay để trải nghiệm hiệu quả của tự động hóa!