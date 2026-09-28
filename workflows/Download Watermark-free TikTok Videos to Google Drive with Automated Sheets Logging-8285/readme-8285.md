---
title: "🚀 Tự động tải video TikTok không logo lên Google Drive và ghi log Google Sheets bằng n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa việc nhận link TikTok qua Form, tải video không watermark, lưu trữ lên Google Drive và quản lý trạng thái trên Google Sheets."
slug: "tu-dong-tai-video-tiktok-khong-logo-google-drive-n8n"
tags: [n8n, automation, tiktok-downloader, google-drive, google-sheets, rapidapi]
keywords: [n8n workflow, tải video tiktok không logo, tự động hóa n8n, google drive api, rapidapi tiktok downloader]
---

# 🚀 Tự động tải video TikTok không logo lên Google Drive và quản lý qua Google Sheets

Các sếp làm sáng tạo nội dung (Content Creator), marketer hay agency có mệt mỏi mỗi khi cần tải hàng loạt video TikTok về để dựng lại, làm reup hoặc lưu trữ tài nguyên không? Việc copy link, dùng các trang web bên thứ ba đầy quảng cáo, tải về máy rồi lại up lên Google Drive thủ công cực kỳ tốn thời gian và dễ bị sót link.

Giải pháp hoàn hảo đây các sếp ơi! Workflow **n8n** tự động hóa 100% quy trình này: Chỉ cần dán link TikTok vào một chiếc Form gọn gàng, hệ thống sẽ tự động gọi API lấy video **không có watermark (không dính logo)**, lưu trực tiếp vào Google Drive, cấu hình quyền chia sẻ công khai và tự động ghi log trạng thái thành công hay thất bại vào Google Sheets. Không cần code phức tạp, chạy mượt mà 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập nguồn hay mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn thao tác thủ công tải xuống và tải lên từng video.
- **Video chuẩn nét, không logo:** Tải video TikTok sạch sẽ không dính watermark nhờ tích hợp RapidAPI chuyên nghiệp.
- **Lưu trữ khoa học:** Tự động đẩy file lên Google Drive, tạo sẵn link chia sẻ (`Anyone with the link can view`).
- **Quản lý minh bạch:** Mọi yêu cầu thành công hay lỗi đều được ghi log chi tiết vào Google Sheets để dễ dàng theo dõi lại.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n:** Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
- **Tài khoản RapidAPI:** Đăng ký một tài khoản miễn phí trên [RapidAPI](https://rapidapi.com/) và lấy API Key cho [TikTok Download Audio Video API](https://rapidapi.com/PrineshPatel/api/tiktok-download-audio-video).
- **Google Account:** 
  - Đã chuẩn bị sẵn một Google Drive Folder để chứa video tải về.
  - Một file Google Sheets có sẵn các cột ghi nhận thông tin (URL, Drive_URL...).
- **Credentials trong n8n:** Kết nối tài khoản Google API và Google Drive OAuth2 API với n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào n8n Editor chọn **Add workflow** -> Nhấp vào menu 3 chấm ở góc trên bên phải -> Chọn **Import from JSON** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các node sau để workflow chạy trơn tru:

- **On form submission (`formTrigger`):** Node này đóng vai trò giao diện nhập liệu. Sau khi active, n8n sẽ cung cấp một URL công khai. Các sếp có thể truy cập link này để nhập URL video TikTok bất cứ lúc nào.
- **TikTok RapidAPI Request (`httpRequest`):** Điền RapidAPI Key của các sếp vào header xác thực của node này để kết nối với dịch vụ tải video.
- **Upload To Google Drive (`googleDrive`):** Chọn kết nối Google Drive OAuth2 của sếp, sau đó chọn thư mục đích (Folder ID) trên Drive nơi video sẽ được lưu trữ.
- **Google Drive Set Permission (`googleDrive`):** Cấu hình quyền chia sẻ file thành dạng công khai (`Anyone with the link can view`) để lấy ra liên kết (`webViewLink`) chia sẻ trực tiếp.
- **Google Sheets & Google Sheets Append Row (`googleSheets`):** Kết nối tài khoản Google Sheets, chọn đúng file bảng tính và Sheet Name để ghi nhận dữ liệu:
  - Trường hợp **Thành công**: Ghi lại `URL` gốc và `Drive_URL` chứa link video trên Drive.
  - Trường hợp **Thất bại**: Sau khi đi qua node **Wait** (chống spam ghi dữ liệu liên tục), node này sẽ ghi lại `URL` và đánh dấu `Drive_URL` là `N/A`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền một link TikTok vào form.
- Kiểm tra xem video đã được tải về Google Drive và ghi dòng mới vào Google Sheets chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để bật chế độ tự động 24/7!

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở thành một trợ thủ đắc lực hơn nữa, các sếp có thể mở rộng thêm:
- **Tích hợp Telegram/Slack Bot:** Thêm node gửi thông báo về nhóm chat ngay khi video được tải lên Drive thành công hoặc khi có lỗi xảy ra.
- **Tự động đổi tên file:** Sử dụng thêm JavaScript node để đặt tên file video trên Drive theo đúng ID hoặc tiêu đề gốc của TikTok video cho dễ quản lý.
- **Tải hàng loạt (Batch Processing):** Thay vì dùng Form Trigger đơn lẻ, các sếp có thể đổi thành Google Sheets Trigger (đọc một danh sách link có sẵn trong bảng tính và chạy vòng lặp xử lý hàng loạt).

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa cực kỳ hữu ích cho những ai làm việc với nội dung video ngắn. Chỉ với vài phút thiết lập ban đầu, các sếp đã giải phóng bản thân khỏi những thao tác chân tay nhàm chán. Chúc các sếp cài đặt thành công và hẹn gặp lại ở các bài hướng dẫn tiếp theo!