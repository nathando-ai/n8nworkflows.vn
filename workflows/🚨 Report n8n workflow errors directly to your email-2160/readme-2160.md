---
title: "🚨 [Hướng dẫn] Tự động báo lỗi n8n qua email - Giải pháp giám sát workflow"
description: "Hướng dẫn chi tiết cách tự động nhận thông báo lỗi của workflow n8n qua email, giúp quản lý và khắc phục sự cố nhanh chóng hơn"
slug: "tu-dong-bao-loi-n8n-qua-email"
tags: [n8n, automation, no-code, email, error-handling]
keywords: [n8n workflow, tự động hóa, báo lỗi, email, error handling]
---

# 🚨 [Hướng dẫn] Tự động báo lỗi n8n qua email - Giải pháp giám sát workflow

[Các sếp đang gặp khó khăn khi phải theo dõi và xử lý lỗi của các workflow n8n một cách thủ công. Với giải pháp này, các sếp sẽ nhận được thông báo lỗi trực tiếp qua email ngay khi xảy ra sự cố, giúp tiết kiệm thời gian và nâng cao hiệu quả quản lý hệ thống.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận thông báo lỗi ngay lập tức qua email
- Giảm thời gian phát hiện và xử lý lỗi
- Tăng tính ổn định của hệ thống tự động hóa
- Giảm tải công việc quản lý workflow
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để nhận thông báo lỗi
- Quyền truy cập vào n8n instance để cấu hình workflow
- Đã cài đặt và cấu hình n8n trên hệ thống
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/2160](https://n8n.io/workflows/2160)
3. Hoặc tải file JSON từ link trên và import thông qua "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On Error"**:
   - Không cần cấu hình gì thêm, node này sẽ tự động kích hoạt khi có lỗi xảy ra trong bất kỳ workflow nào

2. **Node "Gmail"**:
   - Chọn credentials "gmailOAuth2" đã được cấu hình trước đó
   - Điền địa chỉ email nhận thông báo vào trường "To"
   - Có thể tùy chỉnh tiêu đề email trong trường "Subject"
   - Nội dung email sẽ tự động bao gồm thông tin lỗi chi tiết

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn "Activate" để kích hoạt workflow
2. Để kiểm tra hoạt động, có thể tạo một workflow khác và gây ra lỗi (ví dụ: kết nối API không thành công)
3. Kiểm tra hộp thư email đã cấu hình để nhận thông báo lỗi

### ✍️ Mẹo & gợi ý nâng cao
- Để sử dụng workflow này cho nhiều workflow khác nhau, bạn có thể sao chép nó và gắn vào các workflow cần giám sát
- Có thể tùy chỉnh nội dung email để bao gồm thông tin bổ sung như tên workflow, thời gian xảy ra lỗi, v.v.
- Kết hợp với các dịch vụ như Slack hoặc Telegram để nhận thông báo lỗi đa kênh
- Đặt lịch gửi báo cáo tổng hợp lỗi hàng ngày/tháng để theo dõi xu hướng lỗi

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa việc giám sát lỗi của hệ thống n8n, giúp tiết kiệm thời gian và nâng cao hiệu quả quản lý. Hãy áp dụng ngay để nâng cao tính ổn định của hệ thống tự động hóa của bạn!