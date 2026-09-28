---
title: "🚀 Tự động cập nhật thuộc tính sản phẩm VNTANA từ file Excel định kỳ"
description: "Hướng dẫn tự động hóa cập nhật thuộc tính sản phẩm VNTANA từ file Excel đính kèm định kỳ, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-cap-nhat-thuoc-tinh-san-pham-vntana-tu-excel"
tags: [n8n, automation, no-code, vntana, ecommerce]
keywords: [n8n workflow, tự động hóa, vntana, cập nhật sản phẩm, excel]
---

# 🚀 Tự động cập nhật thuộc tính sản phẩm VNTANA từ file Excel định kỳ

[Các sếp] có biết không? Việc cập nhật thủ công thuộc tính sản phẩm từ file Excel lên hệ thống VNTANA đang tốn thời gian và dễ xảy ra lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động cập nhật hàng loạt sản phẩm mà không cần can thiệp thủ công
- **Giảm lỗi**: Loại bỏ các lỗi nhập liệu do thủ công
- **Tự động hóa hoàn toàn**: Chạy định kỳ mà không cần giám sát
- **Tích hợp liền mạch**: Kết nối trực tiếp với API VNTANA
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản VNTANA với quyền truy cập API
- File Excel định kỳ được đính kèm với định dạng đã được quy định
- API Key và thông tin xác thực VNTANA
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/16129](https://n8n.io/workflows/16129)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Configure Values** (Node Code đầu tiên):
   - Cập nhật các tham số cấu hình:
     ```javascript
     return {
       filenamePrefix: "products_", // Tiền tố file Excel cần xử lý
       productIdColumn: "product_id", // Tên cột chứa ID sản phẩm
       attributeColumns: ["size", "color", "material"], // Các cột thuộc tính cần cập nhật
       vntanaApiUrl: "https://api.vntana.com/v1" // URL API VNTANA
     };
     ```

2. **Post Auth to VNTANA** (Node HTTP Request):
   - Điền thông tin xác thực:
     - URL: `https://api.vntana.com/v1/auth`
     - Method: POST
     - Headers: `Content-Type: application/json`
     - Body: `{"username": "your_username", "password": "your_password"}`

3. **Post Search Attachments** (Node HTTP Request thứ hai):
   - Cập nhật URL API tìm kiếm đính kèm:
     ```json
     {
       "url": "https://api.vntana.com/v1/attachments/search",
       "method": "POST",
       "headers": {
         "Authorization": "Bearer {{ $node["Post Auth to VNTANA"].json["access_token"] }}"
       },
       "body": {
         "prefix": "{{ $node["Configure Values"].json["filenamePrefix"] }}"
       }
     }
     ```

4. **Parse Spreadsheet Data** (Node Spreadsheet File):
   - Đảm bảo file Excel có định dạng phù hợp với cấu hình trong node Configure Values

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Activate" để bật workflow
3. Workflow sẽ tự động chạy mỗi 15 phút theo lịch trình đã cài đặt

### ✍️ Mẹo & gợi ý nâng cao
1. **Thay đổi tần suất chạy**: Điều chỉnh thời gian chạy trong node "When Every 15 Minutes" nếu cần
2. **Thêm thông báo**: Kết nối với Slack/Telegram để nhận thông báo khi cập nhật thành công
3. **Lưu log**: Thêm node lưu log để theo dõi lịch sử cập nhật
4. **Xử lý lỗi**: Thêm node xử lý lỗi để gửi email cảnh báo khi có vấn đề xảy ra

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình cập nhật thuộc tính sản phẩm từ file Excel lên VNTANA, tiết kiệm thời gian và giảm thiểu lỗi. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!