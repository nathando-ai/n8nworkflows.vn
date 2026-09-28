---
title: "🚀 Tự động tạo báo cáo tiến độ học sinh từ LMS tới phụ huynh qua Gmail & Google Sheets"
description: "Workflow n8n lấy danh sách học sinh, truy xuất dữ liệu LMS, tạo báo cáo HTML và gửi email cho phụ huynh mỗi tuần, giúp nhà trường tiết kiệm thời gian và tăng độ chính xác."
slug: "tu-dong-bao-cao-tien-do-hoc-sinh-lms-gmail-google-sheets"
tags: [n8n, automation, no-code, education, email, google-sheets]
keywords: [n8n workflow, tự động hóa, báo cáo học sinh, LMS, Gmail, Google Sheets]
---

# 🚀 Tự động tạo báo cáo tiến độ học sinh từ LMS tới phụ huynh qua Gmail & Google Sheets

Trong môi trường giáo dục, việc **tạo và gửi báo cáo tiến độ học tập** cho phụ huynh thường tốn rất nhiều công sức: phải mở LMS, sao chép dữ liệu, dán vào bảng tính, soạn email, rồi gửi từng người. Công việc lặp đi lặp lại này không chỉ **tiêu tốn thời gian** mà còn dễ gây sai sót, khiến phụ huynh không nhận được thông tin kịp thời.

**Workflow n8n** này sẽ **tự động hoá 100%** quy trình trên:
1. Lấy danh sách học sinh từ Google Sheets.  
2. Gọi API LMS để lấy dữ liệu học tập của từng học sinh.  
3. Xử lý, phân tích và tạo báo cáo HTML.  
4. Gửi email báo cáo tới phụ huynh qua Gmail.  
5. Ghi lại lịch sử gửi vào Google Sheets và gửi bản tóm tắt cho admin.  

Kết quả: **Báo cáo được gửi đúng lịch, chính xác, không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gửi báo cáo mỗi tuần mà không cần thao tác thủ công.  
- **Độ chính xác cao**: Dữ liệu lấy trực tiếp từ LMS, giảm lỗi nhập liệu.  
- **Cá nhân hoá**: Mỗi phụ huynh nhận báo cáo riêng, kèm link chi tiết học sinh.  
- **Hoạt động liên tục**: Workflow chạy trên server 24/7, không phụ thuộc vào máy cá nhân.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Account** với quyền **Google Sheets API** (để đọc danh sách học sinh và ghi log).  
- **Gmail OAuth2 credentials** (để gửi email từ tài khoản Gmail của nhà trường).  
- **LMS API endpoint & API Key** (cung cấp bởi nhà cung cấp LMS).  
- **Google Sheet ID** cho danh sách học sinh và sheet ID cho log báo cáo.  
- **Địa chỉ email admin** nhận bản tóm tắt hàng tuần.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Dashboard.  
2. Click **"Import" → "From File"** và tải file JSON của workflow (hoặc copy toàn bộ JSON và dán vào **"Import from Clipboard"**).  
3. Nhấn **"Import"**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hướng dẫn cấu hình chi tiết |
|------|-----------------------------|
| **Weekly Schedule Trigger** | - **Cron**: `0 9 * * 1` (Mỗi Thứ Hai 09:00). |
| **Get Students List** (Google Sheets) | - **Credentials**: chọn `Google API`. <br> - **Spreadsheet ID**: thay `YOUR_STUDENT_SHEET_ID`. <br> - **Sheet Name**: tên sheet chứa danh sách (ví dụ `Students`). |
| **Split Students for Processing** | - **Batch Size**: `10` (tùy theo số lượng học sinh, tránh quá tải API LMS). |
| **Fetch LMS Academic Data** (HTTP Request) | - **Method**: `GET`. <br> - **URL**: `https://api.yourlms.com/v1/student/{{ $json["studentId"] }}/progress`. <br> - **Authentication**: Header `Authorization: Bearer <YOUR_LMS_API_KEY>`. |
| **Process Academic Data** (Code) | - **Language**: JavaScript. <br> - **Input**: dữ liệu JSON từ node trên. <br> - **Output**: đối tượng chứa `studentName`, `grade`, `subjects`, `trend`. (Mã mẫu đã có trong workflow, chỉ cần kiểm tra biến `$json`). |
| **Generate HTML Report** (Code) | - **Output**: chuỗi HTML báo cáo. <br> - **Tham số**: tùy chỉnh mẫu HTML (logo trường, màu sắc). |
| **Send Email to Parents** (Gmail) | - **Credentials**: chọn `gmailOAuth2`. <br> - **To**: `{{ $json["parentEmail"] }}`. <br> - **Subject**: `Báo cáo tiến độ học tập tuần {{ $today }}`. <br> - **HTML Body**: `{{ $json["htmlReport"] }}`. |
| **Log Report Delivery** (Google Sheets) | - **Credentials**: `Google API`. <br> - **Spreadsheet ID**: `YOUR_LOG_SHEET_ID`. <br> - **Sheet Name**: `Log`. <br> - **Operation**: `Append`. <br> - **Columns**: `Timestamp, Student ID, Parent Email, Status`. |
| **Send Admin Summary** (Gmail) | - **To**: địa chỉ email admin (cấu hình trong node). <br> - **Subject**: `Tổng hợp báo cáo tuần {{ $today }}`. <br> - **Body**: tóm tắt số lượng email thành công/failed (được tính trong node trước). |

> **Lưu ý:** Đảm bảo mọi **credential** đều được tạo và cấp quyền đầy đủ trước khi kích hoạt workflow.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chọn **"Execute Workflow"** → **"Run Once"**, nhập một vài bản ghi mẫu để kiểm tra email và log.  
2. Kiểm tra **Inbox phụ huynh** và **Google Sheet log** để xác nhận dữ liệu.  
3. Khi mọi thứ ổn, bật **"Active"** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy vào 09:00 mỗi Thứ Hai.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: dùng node Slack hoặc Telegram để gửi thông báo nhanh cho giáo viên khi có lỗi gửi email.  
- **Lưu trữ log chi tiết**: tạo sheet riêng để lưu toàn bộ payload JSON, giúp debug khi LMS thay đổi cấu trúc.  
- **Báo cáo định kỳ**: sao chép workflow và thay đổi cron thành `0 9 * * 5` để gửi báo cáo cuối tuần cho toàn bộ lớp.  
- **Phân đoạn theo lớp**: sử dụng thêm node **IF** để lọc học sinh theo lớp và gửi email riêng cho từng giáo viên chủ nhiệm.

### 📌 Kết luận
Với workflow **“Automated Student Progress Reports from LMS to Parents”**, các sếp trong ngành giáo dục có thể **loại bỏ công việc thủ công, giảm lỗi và tăng mức độ tương tác** với phụ huynh chỉ trong vài phút thiết lập. Hãy **import ngay**, cấu hình các credential cần thiết và để n8n lo phần còn lại – để bạn có thời gian tập trung vào việc giảng dạy và phát triển chương trình học!