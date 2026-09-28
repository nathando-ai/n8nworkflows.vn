---
title: "🚀 Tự động trích xuất KPI Mirakl xuất ra file CSV và gửi email qua Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu KPI từ Mirakl API theo lịch trình, chuyển đổi thành file CSV và gửi báo cáo qua Gmail."
slug: "tu-dong-trich-xuat-mirakl-kpi-csv-gmail"
tags: [n8n, automation, no-code, mirakl, gmail, api-integration]
keywords: [n8n workflow, tự động hóa, mirakl api, export csv, gmail automation, báo cáo kpi]
---

# 🚀 Tự động trích xuất KPI Mirakl xuất ra file CSV và gửi email qua Gmail

Các sếp làm trong ngành e-commerce chắc chắn hiểu cảm giác mỗi ngày phải tốn thời gian đăng nhập vào nền tảng Mirakl, tải xuống dữ liệu KPI, xử lý rồi mới gửi báo cáo cho sếp lớn hoặc đội ngũ vận hành. Công việc lặp đi lặp lại này vừa nhàm chán, vừa dễ xảy ra sai sót do thao tác thủ công.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Workflow này sẽ âm thầm làm thay các sếp mọi công đoạn: gọi API Mirakl, gom dữ liệu, đóng gói thành file CSV gọn gàng và gửi thẳng vào hộp thư Gmail định kỳ mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không còn cảnh tải tay, kéo thả Excel mỗi sáng.
- **Báo cáo đúng giờ:** Dữ liệu tự động cập nhật và gửi đi chính xác theo lịch trình cài đặt sẵn (Daily Schedule).
- **Chính xác & Minh bạch:** Loại bỏ hoàn toàn sai sót do con người trong quá trình tổng hợp dữ liệu.
- **Hoạt động 24/7:** Hệ thống tự động chạy ngầm trên n8n mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Mirakl API Access:** URL API của hệ thống Mirakl và khóa xác thực (API Key / Token).
- **Tài khoản Gmail:** Đã kết nối với n8n qua OAuth2 để cấp quyền gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này (ID: `15742` từ n8n template), copy toàn bộ nội dung JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính được sắp xếp khoa học, các sếp cần chú ý cấu hình các điểm sau:

- **Daily Export Trigger (`scheduleTrigger`):** 
  - Cấu hình lại mốc thời gian (ví dụ: chạy vào lúc 8:00 sáng mỗi ngày) tùy theo nhu cầu vận hành của doanh nghiệp.
- **Set Configuration Parameters (`set`):** 
  - Nơi lưu trữ các biến cấu hình quan trọng như: Mirakl API URL, API Key, và địa chỉ email nhận báo cáo. Các sếp nhớ điền chính xác thông tin của hệ thống mình.
- **Fetch Mirakl KPI (`httpRequest`):** 
  - Node này sẽ thực hiện gọi API đến Mirakl dựa trên cấu hình ở bước trên. Hãy kiểm tra lại header xác thực (Authorization/API Key) để đảm bảo kết nối thành công.
- **Edit fields to to keep (`set`):** 
  - Lọc và giữ lại các trường dữ liệu (columns) cần thiết cho báo cáo KPI, loại bỏ các dữ liệu rác không quan trọng.
- **Convert to csv File (`convertToFile`):** 
  - Tự động đóng gói dữ liệu đã lọc thành một tệp tin `.csv` chuẩn chỉnh, sẵn sàng đính kèm.
- **Send Email via Gmail (`gmail`):** 
  - Chọn credentials `gmailOAuth2` của các sếp.
  - Điền tiêu đề email, nội dung thông báo và đính kèm file CSV vừa được chuyển đổi ở bước trước để gửi đi.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm xem email có được gửi về hộp thư thành công hay không.
- Sau khi test mượt mà, gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Thay vì chỉ gửi qua Gmail, các sếp có thể nhân bản nhánh gửi thêm thông báo vào **Telegram Bot** hoặc **Slack Channel** của team để mọi người cùng nắm tình hình KPI.
- **Lưu trữ lịch sử:** Thêm node **Google Drive** hoặc **OneDrive** để lưu trữ tự động các file CSV báo cáo mỗi ngày vào một thư mục riêng phục vụ việc tra cứu sau này.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để nếu API Mirakl lỗi (ví dụ server sập hoặc sai token), hệ thống sẽ lập tức bắn tin nhắn cảnh báo về Telegram cho sếp.

### 📌 Kết luận
Tự động hóa quy trình báo cáo KPI từ Mirakl qua Gmail là một bước tiến nhỏ nhưng giúp tiết kiệm rất nhiều giờ làm việc thủ công mỗi tuần. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất vận hành cho đội ngũ của các sếp!