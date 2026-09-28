---
title: "🚀 Tự động hóa gửi tóm tắt cuộc họp với Mailchimp và MongoDB"
description: "Hướng dẫn tự động hóa quy trình ghi âm, chuyển đổi văn bản, tóm tắt và gửi email tóm tắt cuộc họp đến các thành viên tham gia bằng n8n, Mailchimp và MongoDB."
slug: "tu-dong-hoa-gui-tom-tat-cuoc-hop-mailchimp-mongodb"
tags: [n8n, automation, no-code, mailchimp, mongodb]
keywords: [n8n workflow, tự động hóa, mailchimp, mongodb, tóm tắt cuộc họp]
---

# 🚀 Tự động hóa gửi tóm tắt cuộc họp với Mailchimp và MongoDB

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải thủ công ghi âm, chuyển đổi văn bản, tóm tắt và gửi email tóm tắt cuộc họp đến các thành viên tham gia? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code, tiết kiệm thời gian và đảm bảo tính chính xác cao.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ ghi âm đến gửi email.
- **Chính xác cao**: Đảm bảo dữ liệu được xử lý và lưu trữ chính xác.
- **Cá nhân hóa**: Gửi tóm tắt cuộc họp cụ thể đến từng thành viên tham gia.
- **Hoạt động liên tục**: Chạy tự động hàng ngày mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản API của nền tảng cuộc họp nội bộ.
- Tài khoản API của dịch vụ chuyển đổi văn bản (transcription API).
- Tài khoản MongoDB với quyền ghi dữ liệu.
- Tài khoản Mailchimp với quyền tạo campaign và quản lý thành viên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12760](https://n8n.io/workflows/12760).
2. Nhấn nút "Import" và chọn "Import from URL".
3. Dán URL của workflow vào ô nhập liệu và nhấn "OK".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Daily Schedule**: Đặt lịch chạy workflow hàng ngày.
2. **Fetch Meetings**: Cấu hình HTTP Request để lấy dữ liệu cuộc họp từ API của nền tảng cuộc họp nội bộ.
   - Tạo credential **Meetings API** với các thông tin xác thực cần thiết.
3. **Initiate Transcription**: Cấu hình HTTP Request để gửi URL ghi âm đến dịch vụ chuyển đổi văn bản.
   - Tạo credential **Transcription API** với API key của dịch vụ chuyển đổi văn bản.
4. **Summarise Transcript**: Chỉnh sửa logic tóm tắt trong node Code nếu cần.
5. **Insert into MongoDB**: Cấu hình MongoDB credential và chỉ định collection `meeting_summaries`.
6. **Upsert Member**: Cấu hình Mailchimp credential và chỉ định List ID.
7. **Create Campaign**: Chỉnh sửa thông tin campaign như tên, người gửi, v.v.
8. **Set Campaign Content**: Cập nhật nội dung email theo mẫu HTML của công ty.
9. **Send Campaign**: Đảm bảo campaign được gửi đến đúng danh sách thành viên.

#### 3. Kích hoạt ⚡️
1. Chạy workflow một lần để kiểm tra kết quả.
2. Kích hoạt workflow để chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo lỗi**: Thêm node Slack hoặc Telegram để nhận thông báo khi workflow gặp lỗi.
- **Lưu log**: Lưu log chi tiết của từng bước xử lý vào MongoDB để dễ dàng theo dõi và giải quyết vấn đề.
- **Gửi báo cáo định kỳ**: Tạo báo cáo tổng hợp các cuộc họp đã xử lý và gửi qua email hàng tuần.
- **Tích hợp với các công cụ khác**: Kết nối với các công cụ khác như Google Drive để lưu trữ bản ghi âm và transcript.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình từ ghi âm đến gửi email tóm tắt cuộc họp, tiết kiệm thời gian và đảm bảo tính chính xác cao. Hãy áp dụng ngay để nâng cao hiệu suất làm việc và cải thiện trải nghiệm cho các thành viên tham gia cuộc họp.