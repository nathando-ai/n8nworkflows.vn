---
title: "🚀 Tự động đồng bộ mẫu email từ Dartagnan sang Braze với n8n - Giải pháp tiết kiệm thời gian 100% không code"
description: "Hướng dẫn chi tiết cách tự động đồng bộ các mẫu email từ hệ thống Dartagnan sang nền tảng Braze chỉ trong 5 phút mỗi lần, giúp tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-mau-email-dartagnan-braze-n8n"
tags: [n8n, automation, no-code, email-marketing, braze]
keywords: [n8n workflow, tự động hóa email, đồng bộ mẫu email, Dartagnan, Braze]
---

# 🚀 Tự động đồng bộ mẫu email từ Dartagnan sang Braze với n8n - Giải pháp tiết kiệm thời gian 100% không code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải đồng bộ thủ công các mẫu email từ hệ thống Dartagnan sang nền tảng Braze hàng ngày. Giới thiệu workflow như giải pháp tự động hóa hoàn chỉnh 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ tất cả mẫu email từ Dartagnan sang Braze chỉ trong 5 phút mỗi lần
- Giảm 100% lỗi thủ công trong quá trình đồng bộ
- Tiết kiệm thời gian đáng kể cho đội ngũ marketing
- Đồng bộ liên tục 24/7 với lịch trình tự động
- Tự động xử lý cả việc tạo mới và cập nhật mẫu email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Dartagnan với quyền truy cập API
- Tài khoản Braze với quyền quản trị
- API Key từ cả hai nền tảng (Dartagnan và Braze)
- Quyền truy cập vào hệ thống n8n để import và cấu hình workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/3081
3. Hoặc tải file JSON về máy và import từ local file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Token Request** (httpRequest):
   - Cấu hình endpoint API để lấy token từ Dartagnan
   - Điền thông tin xác thực (client_id, client_secret) trong credentials

2. **Assign Credentials** (set):
   - Thiết lập các credentials cho cả Dartagnan và Braze
   - Đảm bảo các thông tin xác thực được lưu trữ an toàn

3. **Dartagnan Project list** (httpRequest):
   - Cấu hình endpoint API để lấy danh sách project từ Dartagnan
   - Điền các tham số cần thiết cho API request

4. **List Available Email Template Braze** (httpRequest):
   - Cấu hình endpoint API để lấy danh sách mẫu email hiện có trong Braze
   - Điền thông tin xác thực Braze trong credentials

5. **Every 5 minutes start** (scheduleTrigger):
   - Có thể điều chỉnh thời gian chạy theo nhu cầu (mặc định là 5 phút/lần)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, nhấn "Activate Workflow"
2. Chạy test với dữ liệu mẫu để kiểm tra hoạt động
3. Kiểm tra kết quả đồng bộ trên cả hai nền tảng

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo Slack/Telegram khi đồng bộ hoàn thành
- Lưu log chi tiết các lần đồng bộ vào Google Sheets
- Tự động gửi báo cáo hàng ngày về số lượng mẫu email đã đồng bộ
- Kết hợp với workflow khác để tự động kích hoạt các chiến dịch email sau khi đồng bộ hoàn tất
- Thiết lập cảnh báo khi có lỗi trong quá trình đồng bộ

### 📌 Kết luận
Workflow này là giải pháp hoàn chỉnh để tự động hóa quá trình đồng bộ mẫu email giữa Dartagnan và Braze, giúp các sếp tiết kiệm thời gian và giảm thiểu lỗi thủ công. Với cấu hình đơn giản và hoạt động liên tục 24/7, đây là công cụ không thể thiếu cho đội ngũ marketing hiện đại. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!