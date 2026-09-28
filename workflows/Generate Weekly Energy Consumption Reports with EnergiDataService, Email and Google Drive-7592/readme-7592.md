---
title: "🚀 Tự động hóa Báo cáo Tiêu thụ Năng lượng Hàng tuần với EnergiDataService, Google Drive và Email"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy dữ liệu tiêu thụ năng lượng từ EnergiDataService, xuất file CSV, lưu trữ trên Google Drive và gửi email báo cáo vào mỗi thứ Hai hàng tuần."
slug: "tu-dong-hoa-bao-cao-nang-luong-hang-tuan-n8n"
tags: [n8n, automation, no-code, energy-report, google-drive, api-integration]
keywords: [n8n workflow, tự động hóa báo cáo năng lượng, EnergiDataService, Google Drive API, email automation, n8n cron trigger]
---

# 🚀 Tự động hóa Báo cáo Tiêu thụ Năng lượng Hàng tuần

Việc tổng hợp và báo cáo dữ liệu tiêu thụ năng lượng định kỳ thủ công thường ngốn rất nhiều thời gian của đội ngũ vận hành hoặc quản lý tòa nhà/nhà máy. Chưa kể nguy cơ sai sót khi xử lý dữ liệu thô từ các API bên ngoài. 

Giải pháp hoàn hảo là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: gọi API lấy dữ liệu từ **EnergiDataService**, chuẩn hóa cấu trúc dữ liệu, chuyển đổi thành file báo cáo chuyên nghiệp, lưu trữ an toàn trên **Google Drive** và gửi trực tiếp qua **Email** vào mỗi sáng thứ Hai hàng tuần. Tất cả diễn ra hoàn toàn tự động mà không cần một dòng code thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn cảnh loay hoay vào đầu tuần để tổng hợp số liệu năng lượng thủ công.
- **Dữ liệu luôn sẵn sàng:** Báo cáo dạng file CSV được cập nhật và lưu trữ ngăn nắp trên Google Drive đúng giờ hẹn.
- **Minh bạch và chính xác:** Loại bỏ hoàn toàn sai sót do con người nhờ quy trình chuẩn hóa dữ liệu tự động từ API.
- **Chủ động thông tin:** Tự động gửi email đính kèm báo cáo đến các bên liên quan mỗi sáng thứ Hai lúc 8:00 AM.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Hệ thống n8n:** Đã được cài đặt và đang hoạt động (Self-hosted hoặc n8n Cloud).
- **Tài khoản Google Drive:** Để cấu hình kết nối OAuth2 lưu trữ file báo cáo.
- **Tài khoản/Máy chủ SMTP (Email):** Để cấu hình node gửi email tự động (Gmail, SendGrid, SMTP riêng...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện chính thức của n8n (Workflow ID: `7592` của tác giả *WeblineIndia*) hoặc copy mã JSON và paste thẳng vào màn hình n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Schedule Weekly (Mon 8AM) (`cron`):** 
  - Node này đóng vai trò kích hoạt (Trigger). Mặc định chạy vào lúc 8:00 AM mỗi thứ Hai hàng tuần. Các sếp có thể điều chỉnh lại lịch trình nếu muốn đổi giờ hoặc ngày chạy.
- **Fetch Energy Data (`httpRequest`):** 
  - Node này thực hiện gọi API đến `EnergiDataService.dk`. Hãy kiểm tra lại endpoint API trong node này xem có cần truyền thêm token xác thực (nếu API yêu cầu) hoặc thay đổi tham số khoảng thời gian lấy dữ liệu cho phù hợp với nhu cầu thực tế.
- **Normalize Records (`code`):** 
  - Sử dụng JavaScript để xử lý và làm phẳng cấu trúc JSON phức tạp từ API (chuyển đổi từ định dạng `records` sang `items`). Node này đã được viết sẵn logic, các sếp chỉ cần kiểm tra lại output xem đã khớp với cấu trúc mong muốn chưa.
- **Convert to File (`convertToFile`):** 
  - Chuyển đổi các items đã chuẩn hóa thành định dạng file CSV (đầu ra là binary `data`). Các sếp có thể đổi tên file đầu ra tại đây (ví dụ: `energy-report-week-[date].csv`).
- **Report File Upload to Google Drive (`googleDrive`):** 
  - **Credentials:** Cần kết nối tài khoản Google cá nhân hoặc Workspace thông qua `googleDriveOAuth2Api`.
  - **Tham số:** Chọn thư mục đích (Folder ID) trên Google Drive nơi các sếp muốn lưu trữ các file báo cáo hàng tuần.
- **Send Email Weekly Report (`emailSend`):** 
  - Cấu hình thông tin máy chủ SMTP hoặc dịch vụ gửi mail, điền địa chỉ Email người nhận (Recipient), tiêu đề và nội dung thư. Đảm bảo đã gắn file binary từ node chuyển đổi CSV vào phần đính kèm (Attachments).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu thực tế từ API và kiểm tra xem file đã được đẩy lên Google Drive và email đã được gửi đi thành công chưa.
- Sau khi test mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm định kỳ hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp ChatOps:** Thêm node **Slack** hoặc **Telegram** ngay sau bước gửi email để bắn thông báo dạng *"Đã tạo và gửi báo cáo năng lượng tuần thành công!"* vào nhóm chat chung của công ty.
- **Lưu lịch sử chạy:** Lưu thông tin đường dẫn file Google Drive vào một bảng **Google Sheets** để làm log theo dõi dài hạn.
- **Cảnh báo ngưỡng năng lượng:** Thêm một node `If` sau bước chuẩn hóa dữ liệu, nếu lượng tiêu thụ vượt quá mức giới hạn cho phép, hệ thống sẽ gửi cảnh báo khẩn cấp ngay lập tức thay vì đợi đến thứ Hai.

### 📌 Kết luận
Workflow tự động hóa báo cáo tiêu thụ năng lượng này là một mảnh ghép tuyệt vời giúp tối ưu hóa quy trình quản trị tài nguyên cho doanh nghiệp. Chỉ với vài phút thiết lập ban đầu, các sếp đã có ngay một trợ lý ảo làm việc chăm chỉ 24/7 không bao giờ quên việc. Triển khai ngay thôi nào!