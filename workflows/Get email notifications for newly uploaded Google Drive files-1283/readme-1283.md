---
title: "🚀 Nhận thông báo qua Email ngay khi có file mới trên Google Drive bằng n8n"
description: "Hướng dẫn thiết lập tự động hóa nhận email cảnh báo tức thì mỗi khi có file mới được tải lên Google Drive, giúp kiểm soát dữ liệu chặt chẽ và không bỏ lỡ thông tin quan trọng."
slug: "nhan-thong-bao-email-file-moi-google-drive-n8n"
tags: [n8n, automation, google-drive, email, productivity]
keywords: [n8n workflow, google drive trigger, tự động hóa google drive, nhận email file mới, n8n viet nam]
---

# 🚀 Nhận thông báo qua Email ngay khi có file mới trên Google Drive

Các sếp có bao giờ rơi vào tình trạng khách hàng hoặc nhân viên tải tài liệu lên thư mục chung của Google Drive nhưng chẳng ai hay biết? Đến khi cần thì phải lục tung các thư mục lên hoặc đi hỏi từng người rất mất thời gian. Quản lý file thủ công kiểu này vừa dễ bỏ sót, vừa thiếu chuyên nghiệp.

Đừng lo, trong bài viết này em sẽ hướng dẫn các sếp tự động hóa 100% quy trình này. Chỉ với 2 nodes đơn giản trong n8n, hệ thống sẽ tự động quét và gửi email thông báo ngay lập tức về hòm thư của các sếp mỗi khi có file mới được "bắn" lên Google Drive!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thông báo tức thì:** Nhận email ngay lập tức trong vài giây sau khi file được tải lên thành công.
- **Kiểm soát chặt chẽ:** Nắm bắt chính xác tên file, thời gian và ai là người tải lên.
- **Tiết kiệm thời gian:** Không cần phải mở Google Drive kiểm tra thủ công mỗi ngày.
- **Hoạt động 24/7:** Chạy ngầm tự động liên tục mà không cần con người can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản Google có quyền truy cập Google Drive.
- Thông tin cấu hình SMTP (Gmail, SendGrid, hoặc SMTP server riêng) để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trong n8n, sau đó copy toàn bộ cấu trúc JSON của workflow này và paste trực tiếp vào giao diện n8n Editor là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này siêu gọn nhẹ với chỉ 2 nodes, các sếp tập trung cấu hình kỹ 2 điểm sau:

- **Google Drive Trigger (Node bắt sự kiện):**
  - Kết nối tài khoản của các sếp thông qua `googleDriveOAuth2Api`.
  - Chọn thư mục (Folder) cụ thể trên Google Drive mà các sếp muốn theo dõi. Nếu để trống, n8n sẽ theo dõi toàn bộ Drive (lưu ý dung lượng và số lượng file có thể gây nhiễu).
  - Cấu hình polling interval (tần suất kiểm tra file mới) cho phù hợp với nhu cầu.

- **Send Email (Node gửi thông báo):**
  - Cấu hình credentials `smtp` bằng thông tin tài khoản gửi email của các sếp (Host, Port, User, Password).
  - Điền địa chỉ email nhận thông báo.
  - Tùy chỉnh tiêu đề và nội dung email, tận dụng các biến dữ liệu từ node Google Drive (như tên file, link truy cập file) để email hiển thị trực quan và dễ bấm xem ngay.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** ở phần Google Drive Trigger và thử tải một file lên thư mục để test xem dữ liệu có đổ về không.
- Kiểm tra hòm thư xem email thông báo đã tới chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức "chạy cơm" tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn xò hơn nữa, các sếp có thể mở rộng workflow này:
- **Bắn tin nhắn vào Telegram/Slack:** Thay vì chỉ gửi email, tích hợp thêm node Telegram để nhận thông báo trực tiếp trên điện thoại cực nhanh.
- **Lưu log vào Google Sheets:** Tự động ghi lại lịch sử ai tải file gì, vào lúc mấy giờ để tiện làm báo cáo cuối tháng.
- **Phân loại file tự động:** Kiểm tra định dạng file (PDF, hình ảnh, video...) để chuyển hướng gửi thông báo đến các phòng ban chuyên trách khác nhau.

### 📌 Kết luận
Một workflow cực kỳ đơn giản nhưng giải quyết triệt để bài toán quản lý file và thông tin trong doanh nghiệp. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ của các sếp nhé!