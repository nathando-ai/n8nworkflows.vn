---
title: "🚀 Nhắc Nhở Nhiệm Vụ Hàng Ngày Tự Động Với Google Sheets & SMTP"
description: "Tự động gửi email nhắc nhở công việc trong ngày dựa trên Google Sheets, giảm 100% công việc thủ công và đảm bảo không bỏ sót."
slug: "email-nhac-nhiem-vu-hang-ngay-google-sheets-smtp"
tags: [n8n, automation, no-code, email, google-sheets, smtp]
keywords: [n8n workflow, tự động hóa, email nhắc nhiệm vụ, Google Sheets, SMTP]
---

# 🚀 Nhắc Nhở Nhiệm Vụ Hàng Ngày Tự Động Với Google Sheets & SMTP

Doanh nghiệp thường phải dành hàng giờ mỗi ngày để kiểm tra danh sách công việc, lọc ra những việc cần thực hiện trong ngày và gửi email nhắc nhở cho từng thành viên. Công việc này không chỉ tốn thời gian mà còn dễ gây sai sót, dẫn đến việc bỏ lỡ deadline quan trọng.  

**Workflow này** sẽ tự động:

1. Lấy dữ liệu công việc từ Google Sheets (lịch nội dung).  
2. Lọc ra những nhiệm vụ có ngày thực hiện là **hôm nay**.  
3. Gửi email nhắc nhở qua SMTP tới người chịu trách nhiệm.  
4. Cập nhật trạng thái trong Google Sheets để tránh gửi lại.  

Kết quả: **100% tự động**, không cần viết code, giảm thiểu lỗi và tiết kiệm thời gian.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn phải mở Sheet, lọc, copy email thủ công.  
- **Độ chính xác 100%**: Email chỉ gửi cho những nhiệm vụ có ngày hôm nay.  
- **Cá nhân hoá**: Nội dung email được tạo động dựa trên dữ liệu từng hàng.  
- **Hoạt động liên tục**: Workflow chạy tự động mỗi ngày, không cần can thiệp.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Google** có quyền **đọc/ghi** Google Sheet chứa lịch công việc.  
- **Google Sheets API credentials** (OAuth2 hoặc Service Account) được cấu hình trong n8n.  
- **SMTP server** (Gmail, Outlook, SendGrid, …) và **API Key / Username & Password** để gửi email.  
- **Sheet ID** và **tên sheet** (ví dụ: `Task Calendar`).  
- **Cột ngày** (định dạng `YYYY-MM-DD`) và **cột email người chịu trách nhiệm** trong Sheet.  
- **n8n** đã được cài đặt (Docker, VPS, hoặc n8n.cloud).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.  
2. Click **Import** → **From File** và chọn file JSON của workflow (được đính kèm trong phần **Tải xuống**).  
   *Hoặc* copy toàn bộ JSON và dán vào **Import → From Clipboard**.  

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Hướng dẫn chi tiết |
|------|-------------------|--------------------|
| **Daily Reminder Trigger** (cron) | - **Cron Expression**: `0 8 * * *` (gửi lúc 08:00 mỗi ngày) hoặc tùy chỉnh thời gian phù hợp. | Mở node → **Cron** → nhập biểu thức. |
| **Read Content Calendar** (googleSheets) | - **Credentials**: Chọn Google API credentials.<br>- **Spreadsheet ID**: ID của Google Sheet.<br>- **Sheet Name**: Tên sheet chứa dữ liệu (ví dụ `Task Calendar`).<br>- **Range**: `A:Z` (hoặc phạm vi thực tế). | Đảm bảo quyền **Read** được cấp. |
| **Filter Today's Tasks** (filter) | - **Condition**: `dateColumn` (cột ngày) **equals** `{{$today}}` (hoặc `{{ $json["date"] }}` tùy cách đặt). | Sử dụng biểu thức `{{$now.format("YYYY-MM-DD")}}` để so sánh. |
| **Code** (code) | - **Language**: JavaScript.<br>- **Code**: Tạo nội dung email HTML dựa trên dữ liệu hàng (ví dụ: `return { subject: \`Nhắc nhở: ${item.task}\`, html: \`<p>Chào ${item.assignee},</p><p>... </p>\` };`). | Kiểm tra lại biến `item` tương ứng với output của node filter. |
| **Send Reminder Email** (emailSend) | - **Credentials**: Chọn SMTP credentials.<br>- **To**: `{{$json["assigneeEmail"]}}`.<br>- **Subject**: `{{$json["subject"]}}` (được trả về từ node Code).<br>- **HTML Body**: `{{$json["html"]}}`. | Đảm bảo **From** được cấu hình đúng domain để tránh spam. |
| **Update row in sheet** (googleSheets) | - **Credentials**: Google API credentials.<br>- **Spreadsheet ID** & **Sheet Name**: giống node đọc.<br>- **Row ID**: `{{$json["rowId"]}}` (hoặc `{{$node["Read Content Calendar"].json["rowNumber"]}}`).<br>- **Values to Update**: Đánh dấu cột `Status` = `Sent`. | Đặt **Operation** = `Update`. |

> **Lưu ý:** Các tên cột trong Sheet (Date, Task, Assignee, Email, Status) phải khớp chính xác với cấu hình node.

#### 3. Kích hoạt ⚡️
1. **Test run**: Click **Execute Workflow** → kiểm tra log để chắc chắn email được tạo đúng nội dung và chỉ gửi cho các nhiệm vụ hôm nay.  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải). Workflow sẽ tự động chạy mỗi ngày theo cron đã thiết lập.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo tổng hợp**: Thêm node **Google Docs** hoặc **PDF** để tạo báo cáo ngày và gửi tới quản lý.  
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để đồng thời gửi tin nhắn nhanh cho nhóm.  
- **Lưu log**: Dùng node **Write Binary File** hoặc **MongoDB** để lưu lịch sử email đã gửi, hỗ trợ audit.  
- **Xử lý lỗi**: Sử dụng node **Error Trigger** để nhận thông báo khi có lỗi gửi email (ví dụ quota SMTP hết).  

### 📌 Kết luận
Với workflow **Automated Daily Task Reminder Emails**, các sếp có thể hoàn toàn loại bỏ công việc kiểm tra và gửi email nhắc nhở thủ công. Chỉ cần một lần thiết lập, hệ thống sẽ tự động chạy 24/7, đảm bảo mọi nhiệm vụ được nhắc nhở đúng thời điểm, giảm thiểu rủi ro và tăng năng suất làm việc. Hãy triển khai ngay hôm nay để cảm nhận sự khác biệt!