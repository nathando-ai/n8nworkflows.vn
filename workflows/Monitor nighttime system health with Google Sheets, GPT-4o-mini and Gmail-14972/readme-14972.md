---
title: "🚀 Tự động giám sát sức khỏe hệ thống ban đêm với Google Sheets, GPT-4o-mini và Gmail"
description: "Xây dựng hệ thống tự động kiểm tra uptime API, ghi log vào Google Sheets, phân tích lỗi bằng AI GPT-4o-mini và gửi cảnh báo qua Gmail khi có sự cố."
slug: "giam-sat-suc-khoe-he-thong-ban-dem-n8n"
tags: [n8n, automation, devops, openai, google-sheets, gmail, ai-monitoring]
keywords: [n8n workflow, giám sát hệ thống, health check tự động, gpt-4o-mini devops, tự động hóa devops n8n]
---

# 🚀 Tự động giám sát sức khỏe hệ thống ban đêm với Google Sheets, GPT-4o-mini và Gmail

Các sếp làm DevOps, quản trị hệ thống hay IT Operations chắc chắn đã không ít lần "nín thở" lo lắng cho các dịch vụ, API chạy ngầm ban đêm. Việc ngồi thức trắng hay lật đật bật laptop mỗi lần server sập là một nỗi ám ảnh thực sự. 

Giải pháp thủ công vừa tốn nhân lực, vừa chậm trễ trong việc phát hiện sự cố. Workflow n8n này sẽ thay các sếp "gác đêm" 100% tự động: tự động quét hệ thống, ghi log chi tiết, sử dụng trí tuệ nhân tạo **GPT-4o-mini** để viết thông báo lỗi chi tiết và bắn tin báo động thẳng vào **Gmail** của các sếp ngay khi dịch vụ "hắt xì hơi".

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát tự động 24/7:** Chủ động kiểm tra các endpoint, API, service theo lịch trình cài sẵn mà không cần con người can thiệp.
- **Báo động tức thì bằng AI:** Khi có lỗi (non-200), GPT-4o-mini sẽ phân tích và tạo nội dung cảnh báo chi tiết, rõ ràng gửi trực tiếp qua Gmail.
- **Lưu trữ log minh bạch:** Mọi trạng thái OK hay ERROR đều được ghi nhận đầy đủ vào Google Sheets để tiện kiểm tra, thống kê.
- **Tiết kiệm thời gian & An tâm ngủ ngon:** Giảm thiểu tối đa thời gian downtime của hệ thống mà không cần tẻ nhạt canh trực ban đêm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google Sheets & Google Drive:** Dùng để lưu danh sách URL cần kiểm tra và bảng log lịch sử.
- **Tài khoản Google / Gmail:** Đã kết nối OAuth2 với n8n để gửi email cảnh báo.
- **OpenAI API Key:** Kích hoạt mô hình GPT-4o-mini để xử lý nội dung cảnh báo thông minh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các thành phần sau:

- **Google Sheets Template:** 
  1. Tạo bản sao của bảng tính mẫu tại đây: [Google Sheets Template](https://docs.google.com/spreadsheets/d/1OIo7K64HGvfUFufGYvAqxElVc0Ot65x3g-D5_w7ulLs/copy)
  2. Lấy **Spreadsheet ID** từ URL của file vừa copy (`https://docs.google.com/spreadsheets/d/【THIS IS THE ID】/edit`).
  3. Cập nhật Spreadsheet ID này vào các node: `Read Monitor Targets`, `Log to Check Log (OK)`, `Log to Check Log (ERROR)`, và `Update alert_sent to TRUE`.
  4. Điền các dịch vụ/URL cần giám sát vào sheet `Monitor Targets` với các cột `name`, `url`, `active` (đặt là `TRUE` để bật, `FALSE` để tạm tắt).

- **Credentials cần thiết:**
  - `Read Monitor Targets`, `Log to Check Log (OK/ERROR)`, `Update alert_sent to TRUE`: Kết nối **Google Sheets OAuth2**.
  - `Send Alert Email`: Kết nối **Gmail OAuth2** và điền email nhận cảnh báo vào trường `sendTo`.
  - `Generate Alert Message (GPT-4o-mini)`: Thêm **OpenAI API Key**.

- **Cấu hình thời gian (Schedule Setting):**
  - Mặc định node `Monitoring Schedule` chạy định kỳ 10 phút một lần, từ 1:00 đến 4:59 sáng các ngày trong tuần (Thứ Hai - Thứ Sáu) với biểu thức Cron: `*/10 1-4 * * 1-5`. Các sếp có thể thay đổi tùy theo múi giờ hệ thống (Settings -> Default Timezone) và nhu cầu thực tế.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test workflow) bằng cách nhấn nút **Execute Workflow** để kiểm tra việc đọc sheet và gọi API.
- Sau khi kiểm tra mọi thứ hoạt động ổn định, gạt công tắc sang **Active** để workflow chính thức làm nhiệm vụ gác đêm cho các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack song song với Gmail để nhận thông báo khẩn cấp ngay trên điện thoại.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp tỷ lệ uptime của các dịch vụ ra một sheet riêng.
- **Tùy chỉnh thời gian timeout:** Tại node `Health Check` (HTTP Request), điều chỉnh thời gian timeout phù hợp với tốc độ phản hồi thực tế của ứng dụng (mặc định 3000ms).

### 📌 Kết luận
Một hệ thống tự động hóa nhỏ gọn nhưng cực kỳ thiết thực cho các kỹ sư hệ thống. Thiết lập ngay hôm nay để có những giấc ngủ ban đêm trọn vẹn và an tâm tuyệt đối về hạ tầng của mình các sếp nhé!