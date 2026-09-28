---
title: "🚀 Tự động hóa tạo và quản lý thư mời nhận việc (Offer Letter) với Google Suite & n8n"
description: "Xây dựng hệ thống tự động hóa toàn diện quy trình gửi offer letter, chuyển đổi PDF, gửi email kèm nút bấm xác nhận và tự động theo dõi phản hồi của ứng viên."
slug: "tu-dong-hoa-tao-va-quan-ly-offer-letter-voi-google-suite-va-n8n"
tags: [n8n, automation, no-code, hr, google-workspace, gmail]
keywords: [n8n workflow, tự động hóa nhân sự, offer letter automation, google sheets n8n, quan ly ung vien tu dong]
---

# 🚀 Tự động hóa quy trình tạo và theo dõi Offer Letter từ A-Z

Trong công tác tuyển dụng, việc soạn thảo từng thư mời nhận việc (Offer Letter) thủ công, chuyển đổi file, gửi email và theo dõi phản hồi của ứng viên (Đồng ý/Từ chối/Hết hạn) ngốn rất nhiều thời gian của đội ngũ HR. Thậm chí, việc chậm trễ phản hồi có thể khiến doanh nghiệp bỏ lỡ những nhân tài sáng giá.

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100% vòng đời của một offer letter. Hệ thống sẽ tự động bắt sự kiện từ Google Sheets, sinh file PDF từ Google Docs, gửi email có kèm nút bấm tương tác (Accept/Decline), ghi nhận phản hồi qua Webhook và cập nhật trạng thái liên tục mà không cần con người nhúng tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Từ lúc thêm dòng ứng viên mới trên Google Sheet đến khi gửi thư mời chuyên nghiệp định dạng PDF.
- **Tương tác mượt mà:** Email gửi đi tích hợp sẵn nút bấm "Chấp nhận" hoặc "Từ chối", giúp ứng viên thao tác cực kỳ nhanh chóng.
- **Theo dõi thời gian thực (Real-time tracking):** Webhook tự động bắt phản hồi của ứng viên, kiểm tra hạn chót (Deadline) và tự động cập nhật trạng thái "Accepted", "Rejected" hoặc "Timeout" lên Google Sheets.
- **Thông báo đa chiều:** Tự động gửi email cảm ơn, thông báo kết quả cho cả ứng viên lẫn bộ phận HR ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google Workspace / Google Account:** Kết nối các credentials cho:
  - Google Sheets (Cấp quyền đọc/ghi dữ liệu và Trigger)
  - Google Docs (Cấp quyền cập nhật template)
  - Google Drive (Cấp quyền copy template, lưu file PDF, phân quyền chia sẻ file)
- **Gmail Account:** Để gửi email offer và các email thông báo, xác nhận.
- **Google Sheets Template & Google Docs Template:** Chuẩn bị sẵn các file mẫu với các trường thông tin placeholder cần thiết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow hoặc tải file JSON về máy, sau đó vào giao diện n8n Editor chọn **Add workflow** -> **Import from File** (hoặc Paste JSON trực tiếp).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 21 nodes hoạt động nhịp nhàng với nhau, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Google Sheets Trigger & Google Sheets nodes (`Get row(s) in sheet2`, `Update status in sheet1`, v.v.):** Kết nối tài khoản Google của các sếp, trỏ đến đúng Spreadsheet ID và Sheet Name. Đảm bảo bảng tính có các cột cơ bản như: `Id`, `Name`, `Email`, `Status`, `Date`.
- **Copy Template1 & Google Drive nodes:** Trỏ đến File ID của Google Docs Template mẫu offer letter và Folder ID trên Google Drive nơi sẽ lưu trữ các bản PDF offer được xuất ra.
- **Webhook1:** Đảm bảo đường dẫn webhook (`b04a8eb4-a672-41bd-9c8a-8cb538aaf3b4` hoặc URL tự sinh trên hệ thống n8n của các sếp) trỏ chính xác vào nút bấm nhận phản hồi từ email của ứng viên.
- **Gmail nodes (`Send a message1`, `Thank you to Candidate2`, `Ack. Hr1`, v.v.):** Kết nối tài khoản Gmail gửi đi, cấu hình lại nội dung chữ ký, tiêu đề email và template nút bấm Accept/Decline cho phù hợp với thương hiệu công ty.
- **Code in JavaScript3:** Kiểm tra lại logic tính toán thời hạn phản hồi (deadline) của offer letter cho phù hợp với chính sách nhân sự (ví dụ: hạn phản hồi trong vòng 3 ngày kể từ ngày gửi).

#### 3. Kích hoạt ⚡️
- **Test run:** Thử thêm một dòng dữ liệu mới vào Google Sheet với trạng thái ban đầu là **Pending** để test toàn bộ luồng chạy xem file PDF có được sinh ra và email có được gửi đi đúng hạn không.
- **Active workflow:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo nội bộ:** Kết nối thêm node Slack hoặc Telegram để bắn thông báo ngay lập tức vào group của HR khi có ứng viên bấm nút Accept/Decline offer.
- **Lưu trữ bảo mật:** Đặt quyền chia sẻ file offer PDF trên Google Drive ở chế độ "Anyone with the link can view" nhưng chỉ cho phép ứng viên cụ thể có quyền truy cập dựa trên email của họ.
- **Mở rộng quy trình:** Sau khi ứng viên Accept, có thể tự động tạo tiếp tài khoản email công ty, gửi lịch hẹn onboarding hoặc tạo task trên Trello/Jira cho team IT chuẩn bị thiết bị làm việc.

### 📌 Kết luận
Tự động hóa quy trình quản lý Offer Letter không chỉ giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tháng cho đội ngũ HR mà còn nâng tầm chuyên nghiệp của doanh nghiệp trong mắt nhân tài ngay từ điểm chạm đầu tiên. Hãy triển khai ngay workflow này trên hệ thống n8n của các sếp!