---
title: "🚀 Tự động gửi email cảnh báo lỗi n8n qua Gmail (Execution & Trigger Errors)"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động phát hiện và gửi email cảnh báo chi tiết khi workflow gặp lỗi ở cả cấp độ thực thi (execution) lẫn kích hoạt (trigger)."
slug: "tu-dong-gui-email-can-bao-loi-n8n-qua-gmail"
tags: [n8n, automation, error-handling, gmail, monitoring, devops]
keywords: [n8n error handling, canh bao loi n8n, gui email loi n8n, gmail automation n8n, error trigger n8n]
---

# 🚀 Tự động gửi email cảnh báo lỗi n8n qua Gmail (Execution & Trigger Errors)

Các sếp đã bao giờ đau đầu khi một workflow quan trọng bỗng nhiên "lăn đùng ra chết" giữa đêm, nhưng mãi đến hôm sau khi khách hàng phàn nàn mới tá hoả nhận ra? Việc kiểm tra log thủ công mỗi ngày cực kỳ tốn thời gian và dễ bỏ sót lỗi.

Giải pháp ở đây là để n8n tự động "la làng" cho các sếp ngay lập tức! Workflow này sẽ giúp bắt mọi lỗi xảy ra trong hệ thống n8n của các sếp — bao gồm cả lỗi trong quá trình thực thi (**Execution errors**) lẫn lỗi ở tầng kích hoạt (**Trigger-level errors**) — sau đó tự động tổng hợp thông tin và gửi một email chi tiết qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow giám sát lỗi này chạy ổn định 24/7 bảo vệ hệ thống, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cảnh báo tức thì 24/7:** Nhận email ngay khi workflow gặp lỗi bất kể ngày đêm.
- **Bắt trọn mọi loại lỗi:** Xử lý tốt cả lỗi lúc chạy (execution) lẫn lỗi lúc nhận trigger đầu vào.
- **Thông tin chi tiết, trực quan:** Tiêu đề email hiển thị rõ ID, tên workflow, nguồn lỗi và thông điệp lỗi. Nội dung email đính kèm sẵn link trực tiếp tới workflow lỗi và dữ liệu JSON chi tiết giúp debug nhanh chóng.
- **Tái sử dụng cao:** Chỉ cần cài đặt 1 lần và gán cho toàn bộ các workflow quan trọng khác trong hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản Google/Gmail để cấu hình kết nối gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy đoạn mã JSON của workflow này hoặc import file trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Node `Config` (Set):** Điền các thông số cơ bản như URL của ứng dụng n8n (`base url`), email nhận thông báo (`recipient email`), và tên hiển thị của người gửi (`sender name` để dễ tạo bộ lọc trong Gmail).
- **Node `Gmail`:** Tạo và chọn **Credentials** sử dụng Gmail OAuth2 để cho phép n8n gửi email từ tài khoản của các sếp.
- **Cấu hình Error Workflow:** Vào phần Settings của các workflow chính mà các sếp muốn giám sát, tại trường **Error Workflow**, chọn chính workflow xử lý lỗi này ([Tham khảo tài liệu n8n](https://docs.n8n.io/flow-logic/error-handling/#create-and-set-an-error-workflow)).

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) với dữ liệu giả lập lỗi để kiểm tra xem email đã đổ về hòm thư hay chưa.
- Bật công tắc **Active** cho workflow xử lý lỗi này.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack song song với Gmail để nhận thông báo tức thời trên điện thoại.
- **Lưu lịch sử lỗi:** Thêm node Google Sheets hoặc Notion để lưu lại toàn bộ lịch sử lỗi nhằm thống kê tỷ lệ ổn định của hệ thống theo tuần/tháng.
- **Tự động tạo Task:** Kết hợp Jira hoặc Trello để tự động tạo ticket giao việc cho đội ngũ kỹ thuật khi có lỗi nghiêm trọng xảy ra.

### 📌 Kết luận
Hệ thống tự động hóa chỉ thực sự vững mạnh khi có cơ chế giám sát và cảnh báo thông minh. Hãy cài đặt ngay workflow này để chủ động nắm bắt mọi sự cố trước khi khách hàng kịp nhận ra nhé các sếp!