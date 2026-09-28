---
title: "🚀 Tự động tải video Instagram lưu Google Drive và gửi Email cho khách hàng"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa việc nhận link Instagram qua form, tải video MP4, lưu vào Google Drive và gửi link tải qua email cho người dùng."
slug: "tai-video-instagram-google-drive-tu-dong-n8n"
tags: [n8n, automation, instagram-downloader, google-drive, email-automation, rapid-api]
keywords: [n8n workflow, tải video instagram, lưu google drive tự động, n8n form trigger, rapidapi instagram downloader]
---

# 🚀 Tự động tải video Instagram lưu Google Drive và gửi Email cho khách hàng

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công sao chép link video Instagram, tìm công cụ bên ngoài để chuyển đổi sang MP4, tải về máy rồi lại up lên Google Drive và gửi email thủ công cho khách hàng hoặc đối tác? Quy trình này ngốn rất nhiều thời gian và dễ xảy ra sai sót.

Giải pháp hoàn hảo cho các sếp đây: Workflow n8n tự động hóa 100% quy trình từ A-Z. Người dùng chỉ cần điền link Instagram và email vào một biểu mẫu (Form) đơn giản, hệ thống sẽ tự động xử lý tất cả phần việc còn lại!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần thao tác thủ công, tiết kiệm hàng chục giờ làm việc mỗi tuần.
- **Trải nghiệm khách hàng chuyên nghiệp:** Khách hàng nhận được link tải video qua email chỉ sau vài giây gửi yêu cầu.
- **Lưu trữ khoa học:** Tự động đồng bộ toàn bộ video đã tải vào Google Drive cá nhân hoặc của doanh nghiệp.
- **Hoạt động 24/7:** Hệ thống tự động túc trực và xử lý mọi yêu cầu mọi lúc, mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **RapidAPI Account:** Cần có tài khoản và API Key cho dịch vụ *Instagram Video Downloader* trên RapidAPI.
- **Google API Credentials:** Kết nối Google Drive (OAuth2 hoặc Service Account) để tải tệp lên.
- **SMTP/Email Credentials:** Tài khoản SMTP (Gmail, SendGrid, v.v.) để gửi email tự động cho người dùng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n Workflow #6921](https://n8n.io/workflows/6921), sau đó chọn **Import from File** hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **n8n Form Trigger:** Node khởi chạy. Sau khi kích hoạt, n8n sẽ cung cấp một đường link Web Form công khai. Các sếp có thể chia sẻ link này cho khách hàng để họ nhập Link Instagram và Email.
- **API Request (RapidAPI):** Cần điền RapidAPI Key của các sếp vào phần Headers để node này có thể gửi URL Instagram sang bên thứ ba lấy link tải MP4.
- **Check for API Error:** Node điều kiện (IF) giúp kiểm tra xem API trả về có lỗi hay không. Nếu `error === false`, workflow mới tiếp tục chạy.
- **Download Instagram Video:** Node tải file MP4 về n8n dựa trên đường link mà RapidAPI cung cấp.
- **Upload To Google Drive:** Cần chọn đúng Credentials Google Drive đã kết nối. Node này sẽ thực hiện đẩy file MP4 lên thư mục chỉ định trên Drive.
- **Set permissions Google Drive (Share):** Cấu hình chia sẻ file ở chế độ công khai (Anyone with the link can view/download) để người nhận có thể bấm vào tải về dễ dàng.
- **Deliver Download Link to User (Email Send):** Cấu hình thông tin SMTP gửi mail. Sử dụng biểu thức động `={{ $json.email }}` làm người nhận và chèn link file `={{ $json.webViewLink }}` vào nội dung email.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền form mẫu để kiểm tra xem email và file trên Google Drive đã hoạt động trơn tru chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node thông báo về kênh chat nội bộ (Slack/Telegram) mỗi khi có khách hàng yêu cầu tải video mới để đội ngũ sales dễ dàng nắm bắt.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử gồm: Thời gian, Email khách hàng và Link video Instagram.
- **Xử lý hàng đợi (Queue):** Nếu lượng request quá lớn, có thể tối ưu thêm cấu hình worker của n8n để tránh bị giới hạn tốc độ (Rate Limit) từ RapidAPI.

### 📌 Kết luận
Workflow "Download Instagram Videos to Google Drive with Auto-Email Delivery" là một công cụ cực kỳ mạnh mẽ giúp cá nhân hóa trải nghiệm người dùng và tự động hóa các tác vụ quản lý file video. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa hiệu suất làm việc!