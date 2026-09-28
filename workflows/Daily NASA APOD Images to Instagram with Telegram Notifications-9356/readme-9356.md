---
title: "🚀 Tự Động Đăng Ảnh Thiên Văn NASA APOD Lên Instagram Kèm Thông Báo Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy ảnh thiên văn APOD từ NASA mỗi ngày, xử lý tiêu đề/mô tả và đăng lên Instagram, đồng thời gửi thông báo qua Telegram."
slug: "tu-dong-dang-anh-nasa-apod-len-instagram-n8n"
tags: [n8n, automation, no-code, instagram, telegram, nasa-api]
keywords: [n8n workflow, tu dong dang anh instagram, nasa apod api, telegram notification n8n, meta graph api]
---

# 🚀 Tự Động Đăng Ảnh Thiên Văn NASA APOD Lên Instagram Kèm Thông Báo Telegram

Các sếp có bao giờ đau đầu vì việc phải tìm kiếm nội dung khoa học chất lượng, chỉnh sửa hình ảnh và đăng bài đều đặn mỗi ngày lên mạng xã hội không? Việc duy trì nội dung đều đặn cho các kênh chủ đề khoa học, vũ trụ (như NASA APOD) tốn rất nhiều thời gian thủ công.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách **tự động hóa 100%**: mỗi ngày tự động lấy ảnh thiên văn từ NASA, tinh chỉnh nội dung, đẩy lên Instagram và gửi báo cáo kết quả về Telegram cho các sếp mà không cần đụng tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần tìm kiếm ảnh hay copy/paste thủ công mỗi ngày.
- **Đúng giờ & Chính xác**: Chạy theo lịch trình được cài sẵn (Schedule Trigger), đăng ảnh sắc nét kèm chú thích đầy đủ từ NASA.
- **Giám sát thông minh**: Tự động kiểm tra trạng thái xử lý media của Instagram trước khi xuất bản, tránh lỗi bài đăng bị hỏng.
- **Cảnh báo tức thì**: Nhận thông báo trạng thái thành công hoặc thất bại qua Telegram ngay sau khi quy trình kết thúc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã sẵn sàng hoạt động (Cloud hoặc Self-hosted).
- **NASA API Key**: Đăng ký miễn phí tại [api.nasa.gov](https://api.nasa.gov/).
- **Meta / Instagram Business Account**: Đã liên kết tài khoản Instagram với Trang Facebook (Facebook Page) và có Access Token từ Meta Graph API với các quyền `instagram_basic` và `pages_manage_posts`.
- **Telegram Bot Token & Chat ID**: Để nhận tin nhắn thông báo kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số trong các node sau để workflow hoạt động trơn tru:

- **Get APOD (`httpRequest`)**: Cấu hình Authentication bằng `httpQueryAuth` sử dụng NASA API Key của các sếp.
- **Prepare IG Post (`httpRequest`)**: 
  - Tạo ứng dụng trên Meta Developer, lấy `{YOUR_APP_ID}` điền vào URL endpoint: `https://graph.facebook.com/v23.0/{YOUR_APP_ID}/media`.
  - Cấu hình Facebook Graph API Credentials bằng Access Token được tạo từ Graph API Explorer.
- **Get Status For Publish (`httpRequest`)**: Cấu hình chung Facebook Graph API Credentials để kiểm tra trạng thái media container đã sẵn sàng chưa.
- **Publish Post (`httpRequest`)**: Cấu hình URL endpoint xuất bản: `https://graph.facebook.com/v23.0/{YOUR_APP_ID}/media_publish` và chọn đúng Facebook Graph API Credentials.
- **Send Finish Message (`telegram`)** & **Send Fail Message (`telegram`)**: Kết nối Telegram API Credentials, điền Chat ID (`{YOUR_CHAT_ID}`) của các sếp để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử công đoạn thủ công để kiểm tra ảnh có lên Instagram và thông báo có về Telegram hay không.
- Nếu mọi thứ mượt mà, bật công tắc **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy biến Caption**: Chỉnh sửa node `Prepare Caption` để thêm hashtag `#Space #NASA #Astronomy` hoặc chèn link website của các sếp vào bài viết.
- **Đa kênh mạng xã hội**: Mở rộng workflow bằng cách kết nối thêm node Facebook Pages, Twitter/X hoặc LinkedIn để đăng chéo nội dung cùng lúc.
- **Lưu trữ đám mây**: Thêm node Google Drive hoặc S3 để lưu lại toàn bộ ảnh gốc NASA tải về làm tư liệu riêng.

### 📌 Kết luận
Với workflow này, việc xây dựng nội dung tự động cho các trang mạng xã hội về chủ đề khoa học vũ trụ trở nên vô cùng nhẹ nhàng. Chúc các sếp cài đặt thành công và sở hữu một kênh Instagram tự động triệu view!