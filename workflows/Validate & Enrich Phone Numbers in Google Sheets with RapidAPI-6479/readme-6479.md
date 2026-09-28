---
title: "📞 Tự động hóa xác thực số điện thoại từ Google Sheets với RapidAPI"
description: "Hướng dẫn tự động hóa xác thực và bổ sung thông tin số điện thoại từ Google Sheets sử dụng RapidAPI, tiết kiệm thời gian và nâng cao chất lượng dữ liệu khách hàng."
slug: "tu-dong-hoa-xac-thuc-so-dien-thoai-google-sheets-rapidapi"
tags: [n8n, automation, no-code, google-sheets, rapidapi]
keywords: [n8n workflow, tự động hóa, xác thực số điện thoại, google sheets, rapidapi]
---

# 📞 Tự động hóa xác thực số điện thoại từ Google Sheets với RapidAPI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình xác thực số điện thoại thay vì làm thủ công.
- Nâng cao chất lượng dữ liệu: Bổ sung thông tin chi tiết về quốc gia, vị trí và múi giờ.
- Giảm thiểu lỗi: Xác thực chính xác số điện thoại trước khi sử dụng.
- Xử lý hàng loạt: Xử lý nhiều số điện thoại cùng một lúc.
- Tính bền bỉ: Tiếp tục xử lý ngay cả khi gặp lỗi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API Key từ RapidAPI để xác thực số điện thoại.
- Google Sheets đã có dữ liệu số điện thoại cần xác thực.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/6479](https://n8n.io/workflows/6479).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When clicking ‘Execute workflow’"**:
   - Không cần cấu hình gì, chỉ cần nhấn "Execute workflow" để bắt đầu.

2. **Node "Google Sheets"**:
   - Cấu hình credentials cho Google API.
   - Chọn Spreadsheet ID và Sheet Name chứa dữ liệu số điện thoại.
   - Đảm bảo cột chứa số điện thoại được đặt tên là "phone_number".

3. **Node "Loop Over Items"**:
   - Không cần cấu hình gì, node này tự động lặp qua từng số điện thoại.

4. **Node "HTTP Request"**:
   - Cấu hình credentials cho RapidAPI.
   - Đảm bảo URL và phương thức là POST.
   - Thêm header "Content-Type" với giá trị "application/json".
   - Thêm body JSON với cấu trúc: `{"phone_number": "{{$node["Google Sheets"].json["phone_number"]}}"}`

5. **Node "Google Sheets1"**:
   - Cấu hình credentials cho Google API.
   - Chọn Spreadsheet ID và Sheet Name chứa dữ liệu số điện thoại.
   - Đảm bảo cột chứa số điện thoại được đặt tên là "phone_number".
   - Thêm các cột mới để lưu kết quả: "is_valid", "country", "location", "timezone".
   - Cấu hình "Update" operation và sử dụng "phone_number" làm khóa chính.

#### 3. Kích hoạt ⚡️
- Nhấn "Execute workflow" để kiểm tra dữ liệu mẫu.
- Kiểm tra kết quả trong Google Sheets để đảm bảo dữ liệu đã được cập nhật đúng.
- Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có số điện thoại không hợp lệ.
- Lưu log các số điện thoại đã xử lý vào một sheet khác.
- Gửi báo cáo định kỳ về tỷ lệ số điện thoại hợp lệ.
- Kết hợp với các công cụ khác như CRM để cập nhật trạng thái khách hàng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình xác thực số điện thoại từ Google Sheets, tiết kiệm thời gian và nâng cao chất lượng dữ liệu khách hàng. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!