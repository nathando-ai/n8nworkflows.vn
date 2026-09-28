---
title: "🚀 Tự động hóa hành trình khách sạn với Gmail và Google Sheets trong n8n"
description: "Hướng dẫn thiết lập workflow n8n tự động gửi email chào mừng, yêu cầu đánh giá sau khi trả phòng và báo cáo vận hành hàng ngày cho khách sạn."
slug: "tu-dong-hoa-hanh-trinh-khach-san-gmail-google-sheets"
tags: [n8n, automation, no-code, gmail, google-sheets, hospitality]
keywords: [n8n workflow, tự động hóa khách sạn, hotel guest journey, google sheets gmail n8n, tự động gửi email khách sạn]
---

# 🚀 Tự động hóa toàn bộ hành trình khách sạn (Guest Journey) với n8n

Việc quản lý thủ công các email chào mừng trước khi check-in, xin đánh giá sau khi check-out và tổng hợp báo cáo ca trực hàng ngày cho nhân viên tốn rất nhiều thời gian của đội ngũ lễ tân. Điều này dễ dẫn đến sai sót, bỏ quên khách hàng hoặc gửi trùng lặp thông tin.

Workflow n8n **Hotel Guest Journey Automation with Gmail & Google Sheets** chính là giải pháp tự động hóa 100% không cần code, giúp chăm sóc khách hàng xuyên suốt từ lúc đặt phòng đến sau khi rời đi, đồng thời tối ưu hóa hiệu suất vận hành nội bộ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Gửi email chào mừng trước check-in 1-2 ngày và xin review sau check-out 24 giờ mà không cần can thiệp thủ công.
- **Tránh trùng lặp thông tin:** Hệ thống tự động theo dõi trạng thái (Tracking) và cập nhật Google Sheets ngay sau khi gửi email thành công.
- **Báo cáo vận hành chính xác:** Tự động tạo và gửi báo cáo danh sách khách đến/đi hàng ngày vào lúc 6:00 sáng cho bộ phận lễ tân và buồng phòng.
- **Nâng cao trải nghiệm khách hàng:** Tăng đánh giá 5 sao trên Google/TripAdvisor và kích thích khách hàng quay lại nhờ mã giảm giá cá nhân hóa.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets chứa dữ liệu đặt phòng của khách.
- Tài khoản Gmail (hoặc Google Workspace) để gửi email tự động.
- Một instance n8n (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy file JSON của workflow này và dán trực tiếp vào n8n Editor của các sếp, hoặc import file thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru với dữ liệu thực tế, các sếp cần cấu hình chính xác các node sau:

- **Node `Get Hotel Reservation` & `Get All Reservations` (Google Sheets):** 
  - Kết nối tài khoản Google Sheets của các sếp thông qua `googleSheetsOAuth2Api`.
  - Thay thế Spreadsheet ID bằng bảng tính quản lý đặt phòng thực tế và chọn đúng Sheet Name/Range.
- **Node `Edit Fields` & `Add Information` (Set):** 
  - Điền thông tin tùy chỉnh của khách sạn như tên khách sạn, địa chỉ, số điện thoại liên hệ, thông tin tiện ích.
- **Node `Welcome Email` & `Write Review` & `Send Daily Staff Report` (Gmail):** 
  - Chọn credentials `gmailOAuth2`.
  - Thiết lập email người gửi (Sender) và địa chỉ nhận email báo cáo nội bộ cho nhân viên.
- **Node `Mark Welcome Email as Sent` & `Mark Review Email as Sent` (Google Sheets):** 
  - Đảm bảo cấu hình thao tác `update` để ghi nhận trạng thái (đã gửi email) vào các cột tương ứng trong bảng tính, giúp tránh tình trạng gửi email lặp lại cho cùng một khách.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) với một vài dòng dữ liệu mẫu trong Google Sheets để kiểm tra luồng lọc dữ liệu (`Filter Upcoming Guest`, `Filter Today's Arrivals`,...).
- Sau khi kiểm tra mọi thứ hoạt động hoàn hảo, hãy bật **Active** workflow để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc khác:** Kết hợp thêm node Telegram hoặc Slack để bắn thông báo tức thời cho bộ phận buồng phòng ngay khi có khách check-out.
- **Cá nhân hóa nội dung nâng cao:** Sử dụng thêm các node AI/LLM để viết nội dung email chào mừng sinh động hơn dựa trên sở thích hoặc lịch sử đặt phòng của khách.
- **Lưu log lỗi:** Thêm nhánh Error Trigger để gửi cảnh báo về Telegram cá nhân nếu quá trình gọi API Gmail hoặc Google Sheets gặp sự cố.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo cho các khách sạn, homestay hoặc căn hộ dịch vụ muốn chuyên nghiệp hóa quy trình chăm sóc khách hàng và tiết kiệm tối đa thời gian vận hành. Hãy cài đặt ngay hôm nay để nâng tầm dịch vụ của các sếp!