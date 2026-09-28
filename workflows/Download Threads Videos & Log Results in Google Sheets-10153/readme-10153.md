---
title: "🚀 Tự Động Tải Video Threads, Lưu Google Drive & Ghi Log Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình tải video từ Threads, lưu trữ lên Google Drive và quản lý trạng thái qua Google Sheets."
slug: "tu-dong-tai-video-threads-google-drive-google-sheets"
tags: [n8n, automation, no-code, google-drive, google-sheets, threads]
keywords: [n8n workflow, tải video threads, auto download threads, google drive automation, n8n google sheets]
---

# 🚀 Tự Động Tải Video Threads, Lưu Google Drive & Ghi Log Google Sheets

Các sếp làm sáng tạo nội dung, marketing hay quản lý mạng xã hội chắc hẳn đã từng "đau đầu" khi phải thủ công đi copy từng link video trên Threads, tìm cách tải về máy rồi lại up lên Google Drive để chia sẻ cho team. Việc này vừa mất thời gian, vừa dễ sót link lại tốn dung lượng thiết bị cá nhân.

Giải pháp ở đây là gì? Hãy để chiếc workflow n8n này "gánh" hết! Workflow này sẽ tự động hóa từ A-Z: nhận link từ form, tải video từ Threads, lưu trữ gọn gàng trên Google Drive, bật quyền chia sẻ link công khai và tự động ghi log thành công/thất bại vào Google Sheets một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Chỉ cần dán link vào Web Form, mọi việc còn lại hệ thống tự lo.
- **Lưu trữ khoa học:** Video tự động bay thẳng vào thư mục Google Drive được chỉ định, không rườm rà.
- **Quản lý minh bạch:** Google Sheets sẽ ghi lại toàn bộ lịch sử link gốc kèm theo link Drive hoặc trạng thái lỗi (nếu có) để dễ kiểm tra.
- **Hoạt động không ngừng nghỉ:** Xử lý hàng loạt yêu cầu liên tục mà không lo gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Drive Account:** Để cấp quyền cho n8n upload và cấu hình chia sẻ file (`googleDriveOAuth2Api`).
- **Google Sheets Account:** Để ghi log kết quả (`googleApi`).
- **Threads Downloader API:** Endpoint hoặc dịch vụ API để bóc tách dữ liệu và link tải video từ Threads (được gọi thông qua node HTTP Request).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp bằng phím tắt `Ctrl+V` / `Cmd+V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **On form submission (`formTrigger`):** Node này tạo sẵn một giao diện web form nhỏ. Các sếp có thể tùy chỉnh lại tiêu đề hoặc giao diện form nếu muốn.
- **Fetch Threads Video Data (`httpRequest`):** Cần cấu hình đúng endpoint API tải video Threads và truyền tham số URL từ form vào request.
- **Check If Video Exists (`if`):** Node điều kiện kiểm tra xem API có trả về link video hợp lệ hay không. Nếu có luồng chạy sang nhánh thành công, ngược lại chạy sang nhánh thất bại.
- **Upload Video to Google Drive (`googleDrive`):** Kết nối tài khoản Google Drive của các sếp (`googleDriveOAuth2Api`) và chọn sẵn **Parent Folder ID** nơi lưu trữ video.
- **Set Google Drive Sharing Permissions (`googleDrive`):** Cấu hình thao tác `share` file để cấp quyền ai có link đều xem/tải được, giúp team dễ dàng lấy link sử dụng.
- **Log Success to Google Sheets & Log Failed Download to Google Sheets (`googleSheets`):** Kết nối tài khoản Google Sheets (`googleApi`), trỏ tới file Excel quản lý của các sếp, chọn đúng Sheet Name và map các cột dữ liệu (Link gốc, Link Drive, Trạng thái).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và test thử bằng cách điền một URL Threads bất kỳ vào form để kiểm tra dữ liệu trả về trên Google Drive và Google Sheets.
- Nếu mọi thứ xanh mướt (success), các sếp gạt công tắc sang **Active** để chính thức đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack vào nhánh thành công để bot hú lên mỗi khi có video mới được tải về thành công.
- **Quản lý trùng lặp:** Thêm một bước kiểm tra Google Sheets trước khi tải để đảm bảo không tải lại cùng một URL Threads đã tồn tại trong hệ thống.
- **Báo cáo định kỳ:** Kết hợp thêm trigger theo thời gian (Schedule Trigger) để tổng hợp số lượng video tải được trong ngày gửi về email cho quản lý.

### 📌 Kết luận
Một workflow cực kỳ thiết thực cho các tín đồ làm nội dung video ngắn. Thiết lập một lần, nhàn tênh cả đời. Chúc các sếp cài đặt thành công và "lên đồ" tự động hóa mượt mà!