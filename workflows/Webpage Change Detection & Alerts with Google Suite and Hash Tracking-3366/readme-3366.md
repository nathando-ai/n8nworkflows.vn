---
title: "🚀 Theo dõi thay đổi trang web và cảnh báo với Google Suite và theo dõi Hash"
description: "Hướng dẫn tự động hóa theo dõi thay đổi nội dung trang web và nhận cảnh báo qua email, Google Sheets và Google Drive bằng n8n"
slug: "theo-doi-thay-doi-trang-web-voi-google-suite"
tags: [n8n, automation, no-code, google-suite, web-monitoring]
keywords: [n8n workflow, tự động hóa, theo dõi web, google sheets, google drive]
---

# 🚀 Theo dõi thay đổi trang web và cảnh báo với Google Suite và theo dõi Hash

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi thay đổi nội dung trang web hàng ngày
- Nhận cảnh báo email ngay khi có thay đổi
- Lưu trữ lịch sử thay đổi trong Google Sheets
- Lưu bản snapshot của nội dung thay đổi trong Google Drive
- Tiết kiệm thời gian và công sức theo dõi thủ công
- Đảm bảo không bỏ lỡ bất kỳ thay đổi quan trọng nào
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Gmail, Google Sheets và Google Drive
- URL của trang web cần theo dõi
- Thời gian chạy định kỳ (ví dụ: hàng ngày)
- Múi giờ đúng cho lịch trình chạy
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3366](https://n8n.io/workflows/3366)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Variables"**:
   - Cập nhật URL của trang web cần theo dõi trong trường "url"
   - Đảm bảo múi giờ được đặt chính xác

2. **Node "Extract Contents"**:
   - Cập nhật các selector CSS/XPath để trích xuất nội dung mong muốn từ trang web
   - Kiểm tra lại các selector để đảm bảo chúng trích xuất đúng nội dung cần theo dõi

3. **Node "Notify of Change"**:
   - Cấu hình tài khoản Gmail OAuth2
   - Đặt địa chỉ email nhận cảnh báo trong trường "to"

4. **Node "Log Record"**:
   - Cấu hình tài khoản Google Sheets OAuth2
   - Đặt tên sheet và phạm vi dữ liệu cần ghi

5. **Node "Take a Snapshot"**:
   - Cấu hình tài khoản Google Drive OAuth2
   - Đặt tên thư mục lưu trữ snapshot

6. **Node "Schedule Trigger"**:
   - Đặt lịch chạy định kỳ (ví dụ: hàng ngày lúc 9:00 sáng)
   - Đảm bảo múi giờ được đặt chính xác

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Test Workflow" để kiểm tra với dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn nút "Activate Workflow" để kích hoạt

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node Slack/Teams để nhận cảnh báo ngay trong ứng dụng chat
2. **Lưu log chi tiết hơn**: Thêm thông tin thời gian, URL và nội dung thay đổi vào Google Sheets
3. **Theo dõi nhiều trang web**: Sao chép workflow và cấu hình cho các trang web khác
4. **Cảnh báo chỉ khi có thay đổi quan trọng**: Sử dụng node "If" để lọc các thay đổi không quan trọng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình theo dõi thay đổi nội dung trang web, giảm thiểu công sức thủ công và đảm bảo không bỏ lỡ bất kỳ thay đổi quan trọng nào. Hãy thử ngay và tối ưu hóa theo nhu cầu cụ thể của doanh nghiệp!