---
title: "🚀 Tự Động Hóa Thông Báo Video Mới Từ Các Kênh YouTube Theo RSS & Email (Không Cần Code)"
description: "Workflow tự động hóa theo dõi video mới từ tất cả kênh YouTube đăng ký của bạn, lọc bỏ Shorts và gửi thông báo email chi tiết mỗi khi có video mới phát hành. Giúp các sếp không bỏ lỡ bất kỳ nội dung nào quan trọng mà không cần phải kiểm tra thủ công hàng ngày."
slug: "tu-dong-hoa-thong-bao-video-moi-youtube-rss-email"
tags: [n8n, automation, youtube, email, rss, no-code, tự động hóa]
keywords: [tự động hóa youtube, thông báo video mới, rss youtube, email tự động, n8n workflow youtube, theo dõi kênh youtube tự động]
---

# 🚀 **Tự Động Hóa Thông Báo Video Mới Từ YouTube: Không Cần Kiểm Tra Thủ Công Hàng Ngày**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải **tốn thời gian hàng giờ** mỗi ngày để:
- Theo dõi **tất cả các kênh YouTube** đăng ký.
- Lọc bỏ **Shorts** (video ngắn) không quan trọng.
- **Bỏ lỡ video mới** vì quên hoặc không có thời gian kiểm tra.
- **Không biết video nào mới** mà phải scroll vô tận trên trang chủ.

**Workflow này giải quyết tất cả vấn đề đó bằng cách:**
✅ **Tự động lấy video mới** từ tất cả kênh đăng ký.
✅ **Lọc bỏ Shorts** và video cũ.
✅ **Gửi email chi tiết** với thumbnail, tiêu đề và liên kết trực tiếp.
✅ **Chạy 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra YouTube hàng ngày.
- **Không bỏ lỡ video**: Tất cả video mới được gửi email ngay lập tức.
- **Lọc bỏ Shorts**: Chỉ nhận thông báo về video dài (phù hợp với nội dung chuyên sâu).
- **Dễ dàng truy cập**: Email chứa **thumbnail + liên kết trực tiếp** để xem ngay.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình (mặc định 1 giờ/lần).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản YouTube OAuth 2.0 API**:
   - [Cài đặt API YouTube](https://developers.google.com/youtube/v3/getting-started) và tạo **OAuth 2.0 Client ID**.
   - **Quota**: Mỗi lần chạy lấy danh sách kênh đăng ký sẽ tiêu thụ **1 quota/50 kênh** (an toàn với giới hạn 10.000/ngày).
2. **Tài khoản Email SMTP** (để gửi thông báo):
   - Các dịch vụ hỗ trợ: Gmail (SMTP), SendGrid, Mailgun, hoặc SMTP của nhà cung cấp hosting.
   - **Tham số cần thiết**: Host, Port, Username, Password, và **Enable SSL/TLS**.
3. **Danh sách kênh YouTube** (nếu muốn lọc thêm):
   - Các sếp có thể **tìm ID kênh** bằng cách:
     - Mở kênh → **Mô tả** → **Chia sẻ kênh** → **Copy Channel ID**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/3216](https://n8n.io/workflows/3216) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **12 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu Hình OAuth 2.0 YouTube**
- **Node**: *"Get my subscriptions"* và *"Get video details"*
- **Thao tác**:
  1. Vào **Credentials** → Tạo mới **YouTube OAuth 2.0 API**.
  2. Điền **Client ID** và **Client Secret** từ Google Cloud Console.
  3. **Chọn scope**: `https://www.googleapis.com/auth/youtube.readonly`.

##### **B. Cấu Hình Email SMTP**
- **Node**: *"Send an email for each new video"*
- **Thao tác**:
  1. Vào **Credentials** → Tạo mới **SMTP**.
  2. Điền thông tin SMTP của tài khoản email (ví dụ Gmail):
     - **Host**: `smtp.gmail.com`
     - **Port**: `465` (hoặc `587` nếu không SSL)
     - **Username**: `email@gmail.com`
     - **Password**: **App Password** (nếu sử dụng Gmail, tạo ở [My Account > Security](https://myaccount.google.com/security))
     - **Enable SSL/TLS**: **Bật**.

##### **C. Cấu Hình Lọc Kênh (Nếu Có Yêu Cầu)**
- **Node**: *"Filter out channels"*
- **Thao tác**:
  - Nếu muốn **bỏ kênh nào đó**, thêm điều kiện lọc trong **Filter Expression**:
    ```json
    {{ $node["Get my subscriptions"].json["items"].channelId }} !== "CHANNEL_ID_TO_REMOVE"
    ```

##### **D. Thiết Lập Lịch Triggers**
- **Node**: *"Schedule Trigger"*
- **Thao tác**:
  - Mặc định **là 1 giờ/lần**, các sếp có thể thay đổi theo nhu cầu (ví dụ: 2 giờ/lần).
  - **Không cần chỉnh sửa các node khác** khi thay đổi tần suất.

##### **E. Lọc Bỏ Shorts**
- **Node**: *"Filter out shorts"*
- **Thao tác**:
  - Workflow đã tự động **lọc bỏ video có duration < 60 giây** (Shorts).
  - Nếu muốn thay đổi ngưỡng, chỉnh **Filter Expression** trong node này:
    ```json
    {{ $node["Get video details"].json["items"][0].duration }} > "PT60S"
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Run Workflow** và kiểm tra email có nhận được thông báo không.
  - Nếu có lỗi, kiểm tra **Log** và **Credentials**.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Kết hợp với **Slack Webhook** hoặc **Telegram Bot** để nhận thông báo ngay khi có video mới.
   - **Cách làm**:
     - Thêm node **Slack** hoặc **Telegram** sau node **emailSend**.
     - Gửi thông báo cùng nội dung email (thumbnail + tiêu đề).

2. **Lưu Log Lịch Sử**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử video đã được thông báo.
   - **Cách làm**:
     - Sau node **emailSend**, thêm node **Google Sheets** với action **Create Row**.
     - Lưu thông tin: **Tiêu đề video, kênh, thời gian, liên kết**.

3. **Gửi Báo Cáo Tuần/Tháng**:
   - Sử dụng **node Schedule Trigger** để chạy tuần/month và gửi **tóm tắt video mới** qua email.
   - **Cách làm**:
     - Tạo một workflow mới với **Schedule Trigger** (ví dụ: ngày đầu tuần).
     - Lấy dữ liệu từ **Google Sheets/Notion** và gửi báo cáo tổng hợp.

4. **Tự Động Xóa Video Cũ**:
   - Nếu muốn **xóa video đã xem** khỏi danh sách, thêm node **Google Drive** để lưu danh sách video đã xem và lọc trong **Filter**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách:
✔ **Tự động theo dõi tất cả kênh YouTube**.
✔ **Lọc bỏ Shorts và video cũ**.
✔ **Gửi email chi tiết** với thumbnail và liên kết.
✔ **Chạy 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình OAuth 2.0 + SMTP.
2. **Test run** và kiểm tra email.
3. **Bật Active** để bắt đầu tự động hóa!

**Nếu có vấn đề**, các sếp có thể:
- **Xem log** trong n8n để debug.
- **Tìm ID kênh** bằng cách chia sẻ kênh trên YouTube.
- **Tùy chỉnh tần suất** theo nhu cầu (ví dụ: 2 giờ/lần).

---
**Chúc các sếp tự động hóa thành công!** 🚀