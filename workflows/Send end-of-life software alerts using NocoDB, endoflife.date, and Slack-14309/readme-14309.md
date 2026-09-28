---
title: "🚀 Tự động cảnh báo phần mềm hết vòng đời (End-of-Life) qua NocoDB và Slack"
description: "Xây dựng hệ thống tự động theo dõi vòng đời phần mềm (End-of-Life), đối chiếu với dự án qua NocoDB và gửi cảnh báo thông minh lên Slack."
slug: "tu-dong-canh-bao-phan-mem-het-vong-doi-nocodb-slack"
tags: [n8n, automation, no-code, devops, nocodb, slack]
keywords: [n8n workflow, end of life alert, nocodb slack integration, tu dong hoa devops, quan ly vong doi phan mem]
---

# 🚀 Tự động cảnh báo phần mềm hết vòng đời (End-of-Life) qua NocoDB và Slack

Trong phát triển phần mềm và quản trị hạ tầng, việc bỏ sót thời điểm hết hạn hỗ trợ (End-of-Life - EOL) của các thư viện, framework hay hệ điều hành có thể tạo ra những lỗ hổng bảo mật nghiêm trọng. Quy trình thủ công kiểm tra hàng loạt công nghệ thực sự tẻ nhạt và dễ sai sót. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hóa 100%, giúp giám sát toàn bộ danh sách phần mềm đang sử dụng, kết nối dữ liệu từ `endoflife.date`, đồng bộ vào NocoDB và chủ động bắn cảnh báo chi tiết lên Slack trước khi quá muộn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần tốn nhân lực kiểm tra thủ công lịch sử EOL của hàng trăm phần mềm.
- **Cảnh báo thông minh**: Phân loại rõ ràng các mức độ (Đã quá hạn, Hết hạn hôm nay, Sắp hết hạn trong X ngày tới).
- **Đồng bộ tập trung**: Quản lý toàn bộ thông tin phần mềm và dự án trực quan ngay trên NocoDB.
- **Thông báo kịp thời**: Gửi thẳng tin nhắn cấu trúc đẹp mắt vào kênh Slack của đội ngũ kỹ thuật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động.
- Tài khoản **NocoDB** (để quản lý dữ liệu phần mềm và dự án).
- Tài khoản **Slack** và quyền cấu hình Bot/App để gửi tin nhắn vào kênh cảnh báo.
- Kết nối internet để truy cập API miễn phí từ `endoflife.date`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần chú ý các điểm sau:
- **Node NocoDB Credentials**: Cấu hình API Token cho toàn bộ các node tương tác với NocoDB (`Get Current Rows`, `Insert New`, `Update Data`, `Get software to check`, v.v.).
- **Node Slack (`Send a message`)**: Kết nối tài khoản Slack (`slackOAuth2Api`) và chọn kênh (channel) nhận thông báo mà team các sếp đang túc trực.
- **Node `Config`**: Tùy chỉnh số ngày cấu hình (ví dụ: cảnh báo trước bao nhiêu ngày trước khi phần mềm chính thức EOL).
- **Khởi tạo dữ liệu ban đầu**: 
  1. Chạy thủ công trigger `Create Tables` để tự động tạo 3 bảng cần thiết trên NocoDB.
  2. Điền thủ công danh sách phần mềm muốn theo dõi vào bảng `EOLSoftware` (tên phải khớp với slug trên `endoflife.date`).
  3. Chạy thủ công trigger `Run daily` một lần để hệ thống đồng bộ dữ liệu vào bảng `EOLDates`.
  4. Cấu hình bảng `EOLProjects` để liên kết dự án với các phiên bản phần mềm tương ứng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một vài bản ghi để kiểm tra dữ liệu trả về từ API và NocoDB.
- Sau khi chắc chắn mọi thứ hoạt động ổn định, hãy bật nút **Active** để workflow tự động chạy định kỳ hàng ngày theo `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Kết hợp thêm node Telegram hoặc Microsoft Teams bên cạnh Slack để đa dạng hóa kênh tiếp nhận thông tin cho quản lý.
- **Ghi log báo cáo**: Lưu lại lịch sử các lần cảnh báo vào một bảng Google Sheets hoặc một bảng riêng trên NocoDB để tiện kiểm tra xu hướng bảo trì hệ thống.
- **Tự động tạo Issue**: Tự động tạo Jira Ticket hoặc GitHub Issue cho đội ngũ Dev ngay khi phát hiện phần mềm sắp hết hạn hỗ trợ.

### 📌 Kết luận
Việc kiểm soát vòng đời phần mềm chưa bao giờ dễ dàng đến thế với sự kết hợp mạnh mẽ giữa n8n, NocoDB và Slack. Hãy thiết lập ngay hôm nay để bảo vệ hệ thống của các sếp khỏi những rủi ro bảo mật tiềm ẩn từ các công nghệ cũ kỹ!