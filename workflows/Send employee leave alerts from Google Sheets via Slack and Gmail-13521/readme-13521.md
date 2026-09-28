---
title: "🚀 Tự động hóa thông báo nghỉ phép nhân viên từ Google Sheets qua Slack và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra lịch nghỉ phép, gửi thông báo Slack cho HR và email nhắc nhở nhân viên khi bắt đầu/kết thúc kỳ nghỉ mà không cần code."
slug: "tu-dong-hoa-thong-bao-nghi-phep-nhan-vien"
tags: [n8n, automation, no-code, hr, google-sheets, slack, gmail]
keywords: [n8n workflow, tự động hóa nghỉ phép, quản lý nhân sự n8n, google sheets slack gmail automation]
---

# 🚀 Tự động hóa thông báo nghỉ phép nhân viên từ Google Sheets qua Slack và Gmail

Trong vận hành doanh nghiệp, việc theo dõi lịch nghỉ phép (Annual Leave, OOO) của nhân sự và thông báo cho các bên liên quan thường tốn nhiều thời gian thủ công. HR phải nhớ ngày nhân viên nghỉ để thông báo lên kênh chung, nhắc nhở nhân viên set trạng thái, rồi lại theo dõi ngày đi làm lại để chào mừng. 

Workflow n8n này do chuyên gia **Rahul Joshi** thiết kế sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: Quét lịch nghỉ từ Google Sheets mỗi ngày, gửi thông báo qua Slack và tự động gửi email nhắc nhở nhân viên, đồng thời cập nhật trạng thái ngay trên bảng tính.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian nhân sự:** Tự động hóa hoàn toàn việc thông báo nghỉ phép mà HR không cần nhớ hay canh ngày thủ công.
- **Cập nhật minh bạch:** Kênh Slack chung luôn nắm rõ nhân sự nào đang nghỉ, ai đã đi làm lại.
- **Cá nhân hóa trải nghiệm:** Tự động gửi email nhắc nhở nhân viên thiết lập trạng thái OOO (Out of Office) khi nghỉ và email chào mừng "Welcome Back" khi quay lại làm việc.
- **Chống trùng lặp thông minh:** Tự động cập nhật trạng thái trong Google Sheets sau khi xử lý để tránh gửi thông báo lặp lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Google Sheets:** File Google Sheets chứa danh sách dữ liệu nghỉ phép của nhân viên.
- **Slack Workspace:** Tài khoản có quyền kết nối và gửi tin nhắn vào kênh HR/Operations.
- **Gmail Account:** Tài khoản Gmail dùng để gửi email tự động cho nhân viên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow hoặc import file trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các phần sau:

- **Daily Leave Check Trigger (`scheduleTrigger`):** Mặc định chạy định kỳ mỗi ngày. Các sếp có thể tùy chỉnh lại giờ chạy phù hợp với giờ làm việc của công ty (ví dụ: 8:00 sáng mỗi ngày).
- **Fetch Leave Records & Mark Leave Nodes (`googleSheets`):** 
  - Kết nối tài khoản qua `googleSheetsOAuth2Api`.
  - Trỏ đúng tới File Google Sheet và Sheet Name chứa dữ liệu nghỉ phép của công ty.
  - Các node cập nhật trạng thái (`Mark Leave As Inactive`, `Mark Leave as Active`) cần được map chính xác cột trạng thái (Status) trong sheet.
- **Validate & Normalize Leave Data (`code`):** Node này dùng Javascript để chuẩn hóa định dạng ngày tháng và lọc dữ liệu đầu vào. Các sếp giữ nguyên code logic.
- **Check Needs Activation / Check Needs Reset (`if`):** Phân loại xem hôm nay có nhân viên nào bắt đầu nghỉ hoặc kết thúc kỳ nghỉ hay không.
- **Notify HR Channel & Notify HR Leave Reset (`slack`):** 
  - Kết nối với `slackOAuth2Api`.
  - Chọn kênh Slack nhận thông báo (ví dụ: `#hr-updates`, `#general` hoặc `#operations`).
- **Send OOO Reminder Email & Send Welcome Back Email (`gmail`):**
  - Kết nối với tài khoản `gmailOAuth2`.
  - Tùy chỉnh nội dung tiêu đề và mẫu email nhắc nhở nhân viên set trạng thái hoặc email chào mừng ngày trở lại.
- **Process Activations/Resets Sequentially (`splitInBatches`):** Đảm bảo dữ liệu được xử lý tuần tự, tránh tình trạng gọi quá nhiều API cùng lúc gây lỗi Rate Limit.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử với dữ liệu hiện tại trong Google Sheets.
- Kiểm tra lại kết quả trên Slack và Gmail xem đã chuẩn chỉnh chưa.
- Gạt nút **Active** để workflow chính thức tự động vận hành hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram:** Ngoài Slack, các sếp có thể gắn thêm node Telegram để bắn tin nhắn vào group chat nội bộ của công ty.
- **Lưu Log vào Database:** Thêm bước ghi lịch sử vào Airtable hoặc PostgreSQL để dễ dàng thống kê ngày nghỉ của nhân viên cuối năm.
- **Tạo bảng quản lý nghỉ phép tự động:** Kết hợp thêm Google Calendar node để tự động block lịch (Create Event) trên lịch chung của công ty khi nhân viên nghỉ.

### 📌 Kết luận
Workflow tự động hóa thông báo nghỉ phép này là một mảnh ghép tuyệt vời giúp tối ưu hóa vận hành HR, mang lại sự chuyên nghiệp và tiết kiệm hàng giờ làm việc thủ công mỗi tuần. Hãy import ngay vào hệ thống n8n của các sếp và trải nghiệm sự tiện lợi này nhé!