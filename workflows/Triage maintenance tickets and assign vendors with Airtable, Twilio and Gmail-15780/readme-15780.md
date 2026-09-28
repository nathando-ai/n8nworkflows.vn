---
title: "🚀 Tự động phân loại và phân công nhà cung cấp bảo trì với Airtable, Twilio và Gmail"
description: "Hướng dẫn tự động hóa quy trình phân loại và phân công nhà cung cấp bảo trì cho các yêu cầu của người thuê, giúp tiết kiệm thời gian và tăng hiệu quả quản lý tài sản"
slug: "tu-dong-phan-loai-phan-cong-nha-cung-cap-bao-tri"
tags: [n8n, automation, no-code, property management, maintenance tickets]
keywords: [n8n workflow, tự động hóa bảo trì, quản lý tài sản, phân loại yêu cầu]
---

# 🚀 Tự động phân loại và phân công nhà cung cấp bảo trì với Airtable, Twilio và Gmail

[Các sếp quản lý bất động sản] thường phải đối mặt với hàng trăm yêu cầu bảo trì hàng ngày từ người thuê. Quy trình thủ công này tốn thời gian, dễ gây nhầm lẫn và làm chậm quá trình giải quyết vấn đề. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ nhận yêu cầu đến phân công nhà cung cấp, giảm thiểu công việc thủ công và tăng hiệu quả quản lý tài sản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động phân loại và phân công nhà cung cấp trong vòng vài giây
- **Giảm thiểu lỗi**: Phân tích yêu cầu và tìm nhà cung cấp phù hợp nhất
- **Tăng hiệu quả**: Giảm thời gian chờ đợi của người thuê và nhà cung cấp
- **Tạo hồ sơ**: Ghi lại toàn bộ quá trình xử lý yêu cầu trong Airtable
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtable với hai bảng: **Vendors** và **Maintenance Tickets**
- Tài khoản Gmail để gửi email thông báo
- Tài khoản Twilio với số điện thoại đã xác thực để gửi SMS
- Các thông tin cần thiết:
  - Airtable Personal Access Token
  - Gmail OAuth2 credentials
  - Twilio API credentials
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15780](https://n8n.io/workflows/15780)
2. Nhấn nút "Import" để tải workflow về máy
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Watch for New Records** (airtableTrigger):
   - Chọn credentials "airtableTokenApi"
   - Cấu hình base ID và table ID cho bảng Maintenance Tickets

2. **Search Records** (airtable):
   - Chọn credentials "airtableTokenApi"
   - Cấu hình base ID và table ID cho bảng Vendors
   - Đảm bảo các trường dữ liệu phù hợp: Name, Email, Phone, Categories, Service Areas, Response Time, Active

3. **Send SMS to Vendor** (twilio):
   - Chọn credentials "twilioApi"
   - Cập nhật số điện thoại nguồn (from) đã xác thực trong Twilio

4. **Tất cả các node Gmail**:
   - Chọn credentials "gmailOAuth2"
   - Cập nhật địa chỉ email nguồn và các thông tin khác trong template email

5. **Extract Postcode District** (code):
   - Kiểm tra logic xử lý mã bưu điện để đảm bảo chuyển đổi đúng định dạng

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để kiểm tra toàn bộ quy trình
2. Kích hoạt workflow bằng cách nhấn nút "Active"

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo khi có yêu cầu bảo trì mới
- Cấu hình gửi SMS cho người thuê khi yêu cầu được tiếp nhận
- Thêm chức năng đánh giá chất lượng dịch vụ từ nhà cung cấp
- Tích hợp với hệ thống quản lý tài sản (PMS) hiện tại của các sếp
- Cấu hình gửi email nhắc nhở cho người thuê khi yêu cầu đang chờ xử lý

### 📌 Kết luận
Workflow này giúp các sếp quản lý bất động sản tự động hóa toàn bộ quy trình xử lý yêu cầu bảo trì, từ nhận yêu cầu đến phân công nhà cung cấp và thông báo cho người thuê. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian, giảm thiểu lỗi và tăng hiệu quả quản lý tài sản một cách đáng kể. Hãy thử ngay để trải nghiệm sự khác biệt!