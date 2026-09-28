---
title: "🚀 Tự động nhận ảnh Thiên văn NASA (APOD) mỗi ngày qua Email với n8n"
description: "Khám phá workflow n8n tự động lấy hình ảnh thiên văn từ NASA APOD RSS, lọc dữ liệu và gửi vào hộp thư đến của bạn mỗi ngày mà không cần chạm tay."
slug: "tu-dong-nhan-anh-thien-van-nasa-moi-ngay-qua-email"
tags: [n8n, automation, no-code, rss, email, ai]
keywords: [n8n workflow, nasa apod, tu dong hoa email, rss feed n8n, gui anh thien van tu dong]
---

# 🚀 Tự động nhận ảnh Thiên văn NASA (APOD) mỗi ngày qua Email với n8n

Các sếp có bao giờ tò mò muốn chiêm ngưỡng những bức ảnh vũ trụ tuyệt đẹp từ NASA mỗi ngày nhưng lại quên mất việc phải lên trang chủ của họ để tìm kiếm? Việc theo dõi thủ công các nguồn tin tức yêu thích thường tốn thời gian và dễ bị bỏ lỡ. 

Giải pháp là gì? Hãy để n8n thay các sếp làm việc đó! Workflow tuyệt vời này sẽ tự động kết nối với nguồn RSS chính thức của NASA APOD (Astronomy Picture of the Day), lấy những bức ảnh mới nhất, xử lý và gửi thẳng vào hòm thư điện tử của các sếp một cách hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Không cần thao tác thủ công, bức ảnh vũ trụ cùng mô tả sẽ đến hòm thư đúng lịch hẹn.
- **Khơi nguồn cảm hứng:** Bắt đầu ngày mới với những hình ảnh kỳ vĩ và kiến thức khoa học vũ trụ thú vị từ NASA.
- **Tùy biến linh hoạt:** Dễ dàng chỉnh sửa giao diện HTML của email hoặc thay đổi lịch trình gửi theo ý thích.
- **Học hỏi nhanh chóng:** Workflow mẫu hoàn hảo để làm quen với việc kết hợp RSS Feed, xử lý dữ liệu và tự động hóa Email trong n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản hoặc dịch vụ SMTP (ví dụ: Gmail, SendGrid, Mailgun,...) để cấu hình node gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **Schedule Trigger:** Thiết lập mốc thời gian định kỳ (mỗi ngày một lần vào buổi sáng chẳng hạn) để kích hoạt workflow chạy tự động.
- **Get APOD Data (RSS Feed Read):** Node này trỏ tới nguồn RSS feed chính thức của NASA APOD. Các sếp có thể kiểm tra lại URL RSS để đảm bảo dữ liệu trả về đầy đủ.
- **Filter only last 2 days (Filter):** Bộ lọc giúp giữ lại các bản tin từ 1-2 ngày gần nhất, đảm bảo các sếp luôn nhận được bức ảnh mới nhất của ngày hôm đó.
- **Set only important fields / Aggregate data (Set):** Tinh chỉnh và gom nhóm các trường dữ liệu quan trọng như tiêu đề ảnh, nội dung mô tả (description), và đường dẫn hình ảnh (image URL).
- **Send email (Email Send):** 
  - Cần cấu hình **SMTP Credentials** chính xác với tài khoản email của các sếp (ví dụ: App Password của Gmail).
  - Tùy chỉnh phần nội dung HTML bên trong node này để bức thư gửi đến hiển thị đẹp mắt, trực quan và đúng phong cách cá nhân.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công xem email có được gửi về hòm thư hay không.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Kết hợp thêm node **Telegram** hoặc **Slack** để vừa nhận email, vừa nhận ảnh nóng hổi ngay trên điện thoại.
- **Lưu trữ tự động:** Đổ dữ liệu hình ảnh và thông tin vào **Google Sheets** hoặc **Notion** để xây dựng thư viện ảnh vũ trụ cá nhân.
- **Tích hợp AI:** Sử dụng thêm các node AI để dịch tự động phần mô tả tiếng Anh của NASA sang tiếng Việt trước khi gửi email cho các sếp.

### 📌 Kết luận
Một workflow gọn nhẹ nhưng cực kỳ thú vị và hữu ích để bắt đầu hành trình tự động hóa cá nhân với n8n. Hãy thiết lập ngay hôm nay để mang cả vũ trụ bao la về hòm thư của các sếp mỗi sáng!