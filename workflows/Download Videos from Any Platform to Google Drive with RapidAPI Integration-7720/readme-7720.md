---
title: "🚀 Tự động tải video từ mọi nền tảng lên Google Drive với n8n và RapidAPI"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa việc nhận link video qua form, tải file MP4, lưu trữ vào Google Drive, cấp quyền chia sẻ và ghi log lỗi tự động."
slug: "tu-dong-tai-video-tu-moi-nen-tang-len-google-drive"
tags: [n8n, automation, no-code, google-drive, rapidapi, video-downloader]
keywords: [n8n workflow, tải video tự động, google drive automation, rapidapi video downloader, n8n form trigger]
---

# 🚀 Tự động tải video từ mọi nền tảng lên Google Drive với n8n và RapidAPI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công đi tìm các công cụ bên ngoài để tải video từ Facebook, Instagram, LinkedIn... rồi lại phải tải về máy và upload lên Google Drive để lưu trữ chưa? Quá tốn thời gian và gián đoạn công việc phải không nào!

Giải pháp ở đây là tự động hóa toàn bộ quy trình này với **n8n**. Workflow này sẽ giúp các sếp tạo ra một trang form gọn gàng để dán link video vào, hệ thống sẽ tự động xử lý từ A-Z: gọi API tải video, lưu thẳng lên Google Drive, cấp quyền public link, và thậm chí ghi log lại nếu có lỗi xảy ra. Không cần code phức tạp, chỉ cần vài cú click!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn thao tác thủ công copy link, tải về, upload lên cloud.
- **Lưu trữ tập trung:** Mọi video yêu thích từ các nền tảng mạng xã hội đượcgom gọn gàng vào một thư mục Google Drive cố định.
- **Cá nhân hóa trải nghiệm:** Cung cấp sẵn link xem dạng public ngay sau khi tải xong để dễ dàng chia sẻ.
- **Quản lý lỗi thông minh:** Tự động ghi nhận các URL lỗi vào Google Sheets để các sếp dễ dàng kiểm tra lại khi cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **RapidAPI Account & API Key:** Đăng ký gói sử dụng cho *All in One Video Downloader API*.
- **Google Drive Account:** Chuẩn bị sẵn thư mục lưu trữ video.
- **Google Sheets:** Tạo sẵn một trang tính để ghi log các link tải lỗi (nếu có).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow này, dán trực tiếp vào n8n Editor hoặc tải file JSON về và chọn **Import from File** trong n8n là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp nhớ cấu hình kỹ các node sau:

- **On form submission (`formTrigger`):** Node này tạo sẵn một giao diện form có trường `URL`. Các sếp có thể mở link form do n8n cung cấp để bắt đầu test nhập link video.
- **All in one video downloader (`httpRequest`):** Điền API Endpoint của RapidAPI vào, kèm theo RapidAPI Key và RapidAPI Host trong phần Headers của yêu cầu POST.
- **If (`if`):** Node này kiểm tra xem JSON trả về từ API có chứa trường `error` hay không. 
  - Đường True ➡️ Chuyển sang tải file MP4.
  - Đường False ➡️ Chuyển sang quy trình xử lý lỗi.
- **Upload To Google Drive (`googleDrive`) & Google Drive Set Permission (`googleDrive`):** 
  - Kết nối `googleDriveOAuth2Api`.
  - Chọn thư mục đích trên Google Drive để lưu video trả về từ node `Download mp4`.
  - Ở node cấp quyền, chọn thao tác `share` để tự động bật chế độ `Anyone with the link can view`.
- **Google Sheets Append Row (`googleSheets`):** Kết nối tài khoản Google Sheets qua `googleApi`, trỏ tới file log lỗi để ghi lại các URL không tải được (kết hợp cùng node `Wait` để tránh spam request liên tục vào sheet).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và test thử bằng một URL video bất kỳ trên form.
- Kiểm tra kết quả trên Google Drive và Google Sheets.
- Nếu mọi thứ mượt mà, bật công tắc **Active** góc trên cùng bên phải để workflow hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack sau bước *Google Drive Set Permission* để bot bắn thông báo kèm link Google Drive trực tiếp về máy mỗi khi video được tải xong.
- **Tự động đặt tên file:** Sử dụng biểu thức (expression) của n8n để đổi tên file video theo tiêu đề lấy từ API thay vì tên mặc định.
- **Mở rộng nguồn dữ liệu:** Có thể thay thế form trigger bằng việc nhận link từ tin nhắn Telegram, Slack hoặc Google Sheets có sẵn để tự động tải hàng loạt (batch processing).

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các sếp làm sáng tạo nội dung, marketing hoặc đơn giản là muốn lưu trữ video yêu thích một cách tự động. Hãy cài đặt ngay lên hệ thống n8n của mình và tận hưởng sức mạnh của tự động hóa nhé! Chúc các sếp thao tác thành công!