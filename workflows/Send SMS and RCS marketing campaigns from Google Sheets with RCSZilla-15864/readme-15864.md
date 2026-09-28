---
title: "🚀 Tự động hóa chiến dịch SMS/RCS từ Google Sheets với RCSZilla"
description: "Hướng dẫn tự động hóa chiến dịch SMS/RCS từ Google Sheets với n8n và RCSZilla, giúp tiết kiệm thời gian và tăng hiệu quả truyền thông"
slug: "tu-dong-hoa-chien-dich-sms-rcs-google-sheets-rcszilla"
tags: [n8n, automation, no-code, sms, rcs, marketing]
keywords: [n8n workflow, tự động hóa, sms marketing, rcs marketing, google sheets]
---

# 🚀 Tự động hóa chiến dịch SMS/RCS từ Google Sheets với RCSZilla

[Các sếp] đang gặp khó khăn khi quản lý và gửi hàng loạt tin nhắn SMS/RCS cho khách hàng? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ chuẩn bị nội dung đến gửi tin nhắn, chỉ với vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý hàng loạt tin nhắn
- Tăng hiệu quả truyền thông với nội dung cá nhân hóa
- Đảm bảo tuân thủ quy định về quyền riêng tư và quảng cáo
- Giảm thiểu lỗi trong quá trình gửi tin nhắn
- Tự động hóa toàn bộ quy trình từ chuẩn bị nội dung đến gửi tin nhắn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản RCSZilla và thiết bị Android đã kết nối
- Google Sheets với các tab: Campaign Queue, Send Log, và Opt Outs
- Các thông tin cần thiết cho các node trong workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor của các sếp
2. Nhấn vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/15864`
4. Nhấn "Import" để hoàn tất quá trình import

Hoặc các sếp có thể tải file JSON của workflow từ link trên và import trực tiếp từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Node "Every 15 minutes"**: Đây là node kích hoạt workflow chạy mỗi 15 phút. Các sếp có thể điều chỉnh thời gian chạy theo nhu cầu.

- **Node "Read campaign queue"**: Node này đọc dữ liệu từ tab "Campaign Queue" trong Google Sheets. Các sếp cần cấu hình:
  - Chọn credentials Google Sheets đã tạo trước đó
  - Nhập ID của Google Sheet (thay thế PASTE_SMS_RCS_MARKETING_SHEET_ID)
  - Đảm bảo tab "Campaign Queue" có cấu trúc đúng với các cột yêu cầu

- **Node "Prepare marketing messages"**: Node này xử lý và chuẩn bị nội dung tin nhắn. Các sếp cần kiểm tra và điều chỉnh code nếu cần thiết.

- **Node "Eligible for campaign send?"**: Node này kiểm tra xem tin nhắn có đủ điều kiện để gửi hay không. Các sếp có thể điều chỉnh logic kiểm tra nếu cần.

- **Node "Queue marketing message with RCSZilla"**: Node này gửi tin nhắn qua RCSZilla. Các sếp cần cấu hình:
  - Chọn credentials RCSZilla đã tạo trước đó
  - Đảm bảo tài khoản RCSZilla đã được kết nối với thiết bị Android

- **Node "Mark row queued"**: Node này cập nhật trạng thái của hàng đã được gửi trong tab "Campaign Queue". Các sếp cần cấu hình:
  - Chọn credentials Google Sheets đã tạo trước đó
  - Nhập ID của Google Sheet (thay thế PASTE_SMS_RCS_MARKETING_SHEET_ID)

- **Node "Log queued message"**: Node này ghi lại thông tin của tin nhắn đã được gửi trong tab "Send Log". Các sếp cần cấu hình:
  - Chọn credentials Google Sheets đã tạo trước đó
  - Nhập ID của Google Sheet (thay thế PASTE_SMS_RCS_MARKETING_SHEET_ID)

- **Node "Log skipped row"**: Node này ghi lại thông tin của hàng bị bỏ qua trong tab "Send Log". Các sếp cần cấu hình:
  - Chọn credentials Google Sheets đã tạo trước đó
  - Nhập ID của Google Sheet (thay thế PASTE_SMS_RCS_MARKETING_SHEET_ID)

- **Node "Marketing opt-out webhook"**: Node này xử lý các yêu cầu opt-out từ khách hàng. Các sếp cần cấu hình:
  - Đảm bảo đường dẫn webhook là duy nhất và không bị trùng lặp
  - Kiểm tra phương thức HTTP (POST)

- **Node "Normalize opt-out reply"**: Node này chuẩn hóa các phản hồi opt-out từ khách hàng. Các sếp cần kiểm tra và điều chỉnh code nếu cần thiết.

- **Node "Is opt-out keyword?"**: Node này kiểm tra xem phản hồi từ khách hàng có phải là từ khóa opt-out hay không. Các sếp có thể điều chỉnh logic kiểm tra nếu cần.

- **Node "Save opt-out to sheet"**: Node này lưu thông tin opt-out vào tab "Opt Outs". Các sếp cần cấu hình:
  - Chọn credentials Google Sheets đã tạo trước đó
  - Nhập ID của Google Sheet (thay thế PASTE_SMS_RCS_MARKETING_SHEET_ID)

- **Node "Respond opt-out saved"**: Node này trả lời lại khách hàng khi thông tin opt-out đã được lưu. Các sếp có thể điều chỉnh nội dung trả lời nếu cần.

- **Node "Respond ignored reply"**: Node này trả lời lại khách hàng khi phản hồi của họ không được xử lý. Các sếp có thể điều chỉnh nội dung trả lời nếu cần.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp có thể thực hiện các bước sau để kích hoạt workflow:

1. Kiểm tra và chạy thử workflow với một số dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheets để đảm bảo workflow hoạt động đúng
3. Khi đã chắc chắn về tính chính xác của workflow, các sếp có thể kích hoạt workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với các công cụ khác như Slack hoặc Telegram để nhận thông báo khi có tin nhắn mới được gửi hoặc khi có yêu cầu opt-out.
- Các sếp có thể lưu log chi tiết của các tin nhắn đã gửi để theo dõi hiệu quả của chiến dịch.
- Các sếp có thể gửi báo cáo định kỳ về hiệu quả của chiến dịch SMS/RCS để tối ưu hóa chiến dịch tiếp theo.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình từ chuẩn bị nội dung đến gửi tin nhắn SMS/RCS, tiết kiệm thời gian và tăng hiệu quả truyền thông. Các sếp chỉ cần chuẩn bị dữ liệu và cấu hình các node quan trọng, sau đó kích hoạt workflow để chạy tự động. Hãy áp dụng ngay workflow này để tối ưu hóa quá trình truyền thông của các sếp!