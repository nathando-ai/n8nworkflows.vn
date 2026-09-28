---
title: "🚀 Tự Động Tạo và Gửi Email Chăm Sóc Khách Hàng Cá Nhân Hóa với Google Sheets, OpenAI và Gmail trên n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động đọc danh sách lead từ Google Sheets, dùng AI viết email HTML cá nhân hóa và gửi đi qua Gmail trong tích tắc."
slug: "tu-dong-tao-va-gui-email-ca-nhan-hoa-voi-google-sheets-openai-gmail"
tags: [n8n, automation, no-code, openai, gmail, google-sheets, ai-agency]
keywords: [n8n workflow, tự động hóa email, openai gmail n8n, google sheets n8n, cá nhân hóa email sale]
---

# 🚀 Tự Động Tạo và Gửi Email Chăm Sóc Khách Hàng Cá Nhân Hóa với OpenAI và Gmail

Viết email chăm sóc (cold email / lead reply) thủ công cho từng khách hàng là nỗi ám ảnh tốn rất nhiều thời gian của đội ngũ sales. Nếu viết nhanh thì thiếu sự cá nhân hóa, còn nếu viết kỹ thì không kịp tiến độ.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: lấy thông tin lead từ Google Sheets, kết hợp chữ ký thực tế từ Gmail, nhờ AI (OpenAI) viết nội dung HTML cực kỳ tinh tế, và tự động gửi email phản hồi mà các sếp không cần tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh copy-paste từng dòng thông tin khách hàng để soạn email.
- **Cá nhân hóa đỉnh cao:** AI dựa trên mục đích (intent) và lý do khách hàng nhắn tin để tạo nội dung cực kỳ chạm đúng "nỗi đau".
- **Chuẩn nhận diện thương hiệu:** Tự động lấy tên hiển thị (displayName) từ tài khoản Gmail để làm chữ ký chuyên nghiệp.
- **Hoạt động liên tục:** Có thể kích hoạt thủ công hoặc cài đặt chạy tự động theo lịch trình (cron job) hàng ngày.
:::

### 📦 Các thành phần trong Workflow (5 Nodes)
1. **When clicking ‘Execute workflow’** (`manualTrigger`): Nút bấm thủ công để bắt đầu chạy thử nghiệm.
2. **Get row(s) in sheet** (`googleSheets`): Đọc danh sách dữ liệu khách hàng từ Google Sheets.
3. **HTTP Request** (`httpRequest`): Lấy thông tin định danh người gửi (Gmail sendAs) để làm chữ ký chuẩn xác.
4. **Message a model** (`openAi`): Sử dụng AI để tạo nội dung HTML cá nhân hóa dựa trên dữ liệu lead.
5. **Send Personalized emails** (`gmail`): Gửi email hoàn chỉnh đến khách hàng qua tài khoản Gmail cá nhân/doanh nghiệp.

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI LÊN ĐỒ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Sheets** có sẵn bảng dữ liệu lead (gồm các cột: *Email ID*, *First Name*, *Intent*, *Why They Sent Email*).
- Tài khoản **OpenAI API Key** (để gọi model sinh nội dung).
- Tài khoản **Google / Gmail** đã kết nối OAuth2 với n8n để đọc thông tin sendAs và gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ mã nguồn JSON của workflow này và dán trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không báo lỗi, các sếp cần cấu hình kỹ các node sau:

* **Node `Get row(s) in sheet` (Google Sheets):**
  - Chọn Credentials kết nối Google Sheets OAuth2.
  - Thay thế **Document ID** và **Sheet Name** bằng file Google Sheets thực tế của các sếp.
  - Đảm bảo các trường dữ liệu trong bảng khớp với prompt: `Email ID`, `First Name`, `Intent`, `Why They Sent Email`.

* **Node `HTTP Request` (Lấy chữ ký Gmail):**
  - Node này dùng để gọi Gmail API lấy thông tin `sendAs` nhằm trích xuất `displayName` làm chữ ký. Cần cấu hình kết nối Gmail OAuth2 credentials có quyền đọc thông tin tài khoản.

* **Node `Message a model` (OpenAI):**
  - Chọn Credentials OpenAI API.
  - Đảm bảo thiết lập prompt nhận vào các biến: `First Name`, `Intent`, `Why They Sent Email` và `sendAs.displayName`.
  - **Lưu ý quan trọng:** Yêu cầu mô hình trả về định dạng **HTML** hoàn toàn và **không kèm theo tiêu đề (subject)** trong nội dung trả về.

* **Node `Send Personalized emails` (Gmail):**
  - Sử dụng chung Credentials Gmail OAuth2.
  - **To:** Trỏ đến trường `Email ID` lấy ra từ Google Sheets.
  - **Subject:** Đặt tiêu đề email động, ví dụ: `"Re: " + {{ $json.Intent }}`.
  - **Body:** Nhận kết quả HTML từ node OpenAI.
  - ⚠️ **CỰC KỲ QUAN TRỌNG:** Phải cài đặt thuộc tính `emailType = html` trong node Gmail này để nội dung hiển thị đúng định dạng HTML thay vì dạng chữ thuần (plain text).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test thử với 1-2 dòng dữ liệu đầu tiên trong Google Sheets xem email gửi đi có chuẩn chỉnh hay chưa.
- Kiểm tra hòm thư người nhận và hộp thư đi (Sent) của Gmail.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống sẵn sàng vận hành tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch:** Thay thế node `Manual Trigger` bằng node `Schedule Trigger` để n8n tự động quét Google Sheets và gửi email chăm sóc vào mỗi 9 giờ sáng hàng ngày.
- **Lưu lại lịch sử:** Thêm một bước cập nhật ngược lại Google Sheets (Google Sheets Node - Update Row) để đánh dấu trạng thái "Đã gửi email" cho từng dòng lead, tránh việc gửi trùng lặp.
- **Thông báo qua Slack/Telegram:** Thêm node thông báo về nhóm chat nội bộ mỗi khi AI gửi thành công email cho một lead tiềm năng.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một "đội ngũ trợ lý AI" làm việc không mệt mỏi, giúp tối ưu hóa quy trình sales outreach, chăm sóc khách hàng cực kỳ chuyên nghiệp và cá nhân hóa ở quy mô lớn. 

Chúc các sếp "lên đồ" thành công và bùng nổ doanh số! Nếu gặp khó khăn gì trong quá trình cài đặt, đừng ngần ngại để lại bình luận trao đổi nhé!