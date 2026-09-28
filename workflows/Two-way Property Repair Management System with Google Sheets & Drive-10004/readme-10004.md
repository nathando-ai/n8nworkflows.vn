---
title: "🏠 Hệ thống quản lý sửa chữa bất động sản hai chiều với Google Sheets & Drive"
description: "Tự động hóa hoàn toàn quá trình quản lý sửa chữa bất động sản từ yêu cầu đến cập nhật, giúp tiết kiệm thời gian và giảm lỗi con người"
slug: "he-thong-quan-ly-sua-chua-bat-dong-san-google-sheets-drive"
tags: [n8n, automation, no-code, bất động sản, quản lý sửa chữa]
keywords: [n8n workflow, tự động hóa sửa chữa, quản lý bất động sản, google sheets, google drive]
---

# 🏠 Hệ thống quản lý sửa chữa bất động sản hai chiều với Google Sheets & Drive

[Các sếp quản lý bất động sản] thường phải đối mặt với những thách thức lớn khi xử lý các yêu cầu sửa chữa từ cư dân. Từ việc ghi nhận yêu cầu đến theo dõi tiến độ và cập nhật thông tin, quá trình này thường tốn nhiều thời gian và dễ xảy ra lỗi. Hệ thống tự động hóa này sẽ giúp các sếp quản lý toàn bộ quy trình sửa chữa một cách hiệu quả, từ lúc nhận yêu cầu đến khi hoàn thành công việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý yêu cầu sửa chữa lên đến 80%
- Giảm lỗi con người trong quá trình ghi nhận và cập nhật thông tin
- Tạo ra hệ thống quản lý sửa chữa thống nhất và dễ theo dõi
- Tự động hóa toàn bộ quy trình từ lúc nhận yêu cầu đến khi hoàn thành
- Tăng tính minh bạch trong quá trình quản lý sửa chữa
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để sử dụng Google Sheets và Google Drive)
- Tài khoản email (để gửi thông báo qua Gmail)
- Tạo một Google Form để nhận yêu cầu sửa chữa từ cư dân
- Tạo một Google Sheet để lưu trữ thông tin sửa chữa
- Tạo một thư mục trong Google Drive để lưu trữ ảnh sửa chữa
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [workflow gốc trên n8n.io](https://n8n.io/workflows/10004)
2. Click vào nút "Copy Workflow" để sao chép JSON của workflow
3. Trong n8n Editor của bạn, click vào nút "Import from Clipboard" và dán JSON vừa sao chép vào

Hoặc các sếp cũng có thể tải file JSON của workflow về máy và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

##### Workflow 1: Nhận yêu cầu sửa chữa mới
1. **New repair form submitted** (googleSheetsTrigger):
   - Thêm Google Sheets credential
   - Chọn tài liệu, sheet và thời gian poll phù hợp

2. **Format Data** (set):
   - Cấu hình các trường dữ liệu cần hiển thị (địa chỉ, đơn vị, mức độ khẩn cấp, liên hệ, v.v.) và nội dung tin nhắn
   - Thêm biểu thức đầu vào cho "địa chỉ"+"đơn vị" để tạo "UUID"

3. **Add UUID #** (googleSheets):
   - Thêm Google Sheets credential
   - Chọn tài liệu và sheet phù hợp
   - Sử dụng TIMESTAMP làm "Cột để khớp"

4. **Report Alert + Info** (gmail):
   - Thêm Gmail/email credential
   - Định dạng thông tin tóm tắt gửi cho quản lý tòa nhà
   - Bao gồm liên kết đến biểu mẫu cập nhật sửa chữa (tìm thấy trong **N8N Form Trigger** trong Workflow 2)

##### Workflow 2: Cập nhật tiến độ sửa chữa
1. **REPLACE w/ N8N FORM trigger.** (manualTrigger):
   - Thay thế bằng N8N Form trigger cho biểu mẫu cập nhật sửa chữa
   - Liên kết đến biểu mẫu cập nhật sửa chữa phải được dán vào nút Email ở cuối Workflow 1

2. **Get row(s) in sheet** (googleSheets):
   - Thêm Google Sheets credential
   - Sử dụng **UUID** để thu thập thông tin hiện có từ hàng trong bảng tính

3. **Existing Details** (set):
   - Thiết lập các trường dữ liệu bắt buộc

4. **Upload Repair Photo** (googleDrive):
   - Thêm Drive credential
   - Thiết lập thư mục để lưu trữ ảnh sửa chữa

5. **Update w/ Repair** (googleSheets):
   - Thêm credential
   - Chọn tài liệu và sheet phù hợp
   - Ánh xạ biểu thức Java đến các cột
   - Phải có các cột trong bảng tính khớp chính xác với tất cả các tên trường, bao gồm cập nhật sửa chữa

6. **Send a message** (gmail):
   - Tùy chọn: để cảnh báo cư dân hoặc người khác về cập nhật sửa chữa

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình tất cả các node cần thiết, các sếp nên:
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu tự động hóa quy trình

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Teams**: Thêm các node để gửi thông báo qua Slack hoặc Microsoft Teams để tăng tính minh bạch và phản hồi nhanh hơn
2. **Lưu log hoạt động**: Thêm các node để ghi lại tất cả các hoạt động quan trọng vào một bảng tính riêng để theo dõi và phân tích
3. **Gửi báo cáo định kỳ**: Tạo một workflow phụ để tự động gửi báo cáo tổng hợp về tình hình sửa chữa hàng tuần hoặc hàng tháng
4. **Tích hợp với hệ thống CRM**: Kết nối với hệ thống quản lý quan hệ khách hàng để lưu trữ thông tin cư dân và lịch sử sửa chữa

### 📌 Kết luận
Hệ thống quản lý sửa chữa bất động sản hai chiều với Google Sheets & Drive này sẽ giúp các sếp quản lý tòa nhà tiết kiệm thời gian, giảm lỗi và tạo ra một hệ thống quản lý sửa chữa thống nhất và minh bạch. Bằng cách tự động hóa toàn bộ quy trình từ lúc nhận yêu cầu đến khi hoàn thành công việc, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn và cung cấp dịch vụ tốt hơn cho cư dân.