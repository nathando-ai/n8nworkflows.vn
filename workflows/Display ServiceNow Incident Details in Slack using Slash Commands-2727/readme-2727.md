---
title: "🚀 Tích hợp ServiceNow Incident trực tiếp lên Slack với n8n Slash Command"
description: "Tự động hóa tra cứu và hiển thị thông tin sự cố ServiceNow ngay trong Slack bằng Slash Command, giúp đội ngũ IT xử lý sự cố nhanh chóng mà không cần chuyển đổi tab."
slug: "hien-thi-serviceNow-incident-trong-slack-bang-slash-command"
tags: [n8n, automation, servicenow, slack, support, no-code]
keywords: [n8n workflow, servicenow slack integration, slash command n8n, tu dong hoa it support]
---

# 🚀 Tích hợp ServiceNow Incident trực tiếp lên Slack với n8n Slash Command

Các sếp trong đội ngũ IT Support hay DevOps chắc hẳn đã quá quen thuộc với cảnh phải liên tục chuyển đổi qua lại giữa Slack và ServiceNow để tra cứu thông tin các sự cố (incident). Việc này vừa tốn thời gian, vừa làm gián đoạn nhịp độ làm việc. 

Giải pháp là đây! Workflow n8n tuyệt vời này (được thiết kế bởi chuyên gia Angel Menendez) sẽ giúp các sếp tạo ngay một **Slack Slash Command** để tra cứu và trả về chi tiết incident của ServiceNow ngay lập tức trong đoạn chat Slack. Tự động hóa 100%, không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu tốc độ:** Gõ lệnh Slash Command trên Slack là lấy được thông tin sự cố ngay lập tức.
- **Tập trung làm việc:** Không cần đăng nhập vào ServiceNow hay rời khỏi không gian chat Slack.
- **Phản hồi thông minh:** Tự động xử lý các trường hợp tìm thấy incident, không tìm thấy hoặc lỗi kết nối hệ thống với thông báo thân thiện.
- **Vận hành 24/7:** Hoạt động tự động liên tục, tiết kiệm hàng giờ thao tác thủ công mỗi tuần cho đội ngũ support.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **n8n Instance:** Đã chạy và sẵn sàng (Self-hosted hoặc n8n Cloud).
- **Slack Workspace:** Quyền cấu hình App và tạo Slash Command.
- **ServiceNow Instance:** Tài khoản có quyền truy cập API để query Incident (chuẩn bị thông tin `ServiceNow Basic API Credentials`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống liên thông mượt mà giữa Slack và ServiceNow, các sếp cần cấu hình chính xác các node sau:

- **Webhook Node:**
  - Nhận request từ Slack Slash Command (phương thức `POST`).
  - Lấy Production/Test Webhook URL này để dán vào cấu hình của Slack App (phần Slash Commands).
- **Extract Incident ID from Response Node (`Set`):**
  - Xử lý payload từ Slack gửi lên để bóc tách mã Incident ID mà người dùng vừa nhập.
- **Search For Incident in ServiceNow Node (`ServiceNow`):**
  - Chọn credentials `serviceNowBasicApi` của doanh nghiệp các sếp.
  - Cấu hình Resource là `incident` và Operation là `getAll` để tìm kiếm theo ID đã trích xuất.
- **Parse ServiceNow Response Node (`Switch`):**
  - Phân loại kết quả trả về từ ServiceNow: có tìm thấy incident hay không, hay gặp lỗi hệ thống.
- **Các node phản hồi (`Respond to Webhook`):**
  - Gồm `Send Incident Details to Slack`, `Notify User no Incident was Found`, và `Notify User of Error with ServiceNow` để trả về thông báo phù hợp nhất cho người dùng trên Slack.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test run** bằng cách gọi lệnh Slash Command từ Slack để kiểm tra luồng dữ liệu.
- Sau khi test thành công, bật trạng thái **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài việc trả kết quả về cho cá nhân gọi lệnh, các sếp có thể cấu hình gửi bản tóm tắt incident vào một channel chung của team DevOps/IT khi có sự cố nghiêm trọng.
- **Lưu lịch sử tra cứu:** Kết nối thêm một node **Google Sheets** hoặc **Airtable** để lưu log mỗi khi có nhân sự tra cứu incident, giúp dễ dàng kiểm tra nội bộ.
- **Tích hợp AI:** Kết hợp thêm n8n AI node để tóm tắt nhanh nội dung sự cố bằng AI trước khi đẩy lên Slack.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ hữu ích giúp tối ưu hóa quy trình quản 3 trị sự cố (Incident Management) của doanh nghiệp. Hãy cài đặt ngay hôm nay để giải phóng thời gian cho đội ngũ IT support của các sếp!