---
title: "🚀 Tự động hóa đánh giá Google 5 sao qua Telegram và Google Sheets với n8n"
description: "Hướng dẫn xây dựng hệ thống quản lý danh tiếng tự động: lọc đánh giá tích cực lên Google, giữ lại phản hồi tiêu cực và chăm sóc khách hàng qua Telegram."
slug: "tu-dong-hoa-danh-gia-google-telegram-google-sheets"
tags: [n8n, automation, telegram, google-sheets, crm, reputation-management]
keywords: [n8n workflow, tự động hóa đánh giá google, telegram bot n8n, google sheets automation, quản lý review doanh nghiệp]
---

# 🚀 Tự động hóa bộ lọc đánh giá Google và chăm sóc khách hàng qua Telegram

Các sếp có đang đau đầu vì những đánh giá 1-2 sao trên Google làm sụt giảm uy tín của cửa hàng/doanh nghiệp? Việc thu thập feedback thủ công vừa tốn thời gian, vừa bỏ lỡ cơ hội biến khách hàng hài lòng thành các đánh giá 5 sao công khai.

Workflow n8n tuyệt vời này do tác giả **Anirudh Aeran** thiết kế sẽ giải quyết triệt để bài toán trên. Hệ thống hoạt động như một "quản lý danh tiếng" tự động: tương tác với khách hàng qua **Telegram**, gửi ưu đãi hấp dẫn, điều hướng khách hàng hài lòng (4-5 sao) lên trang đánh giá Google, đồng thời giữ lại các phản hồi tiêu cực một cách riêng tư để các sếp xử lý nội bộ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo vệ danh tiếng thương hiệu:** Tự động lọc và hướng khách hàng có trải nghiệm tốt viết review 5 sao lên Google.
- **Xử lý khủng hoảng khéo léo:** Khách hàng không hài lòng sẽ gửi feedback riêng tư qua Web Form, giúp các sếp cải thiện dịch vụ trước khi họ bực bội lên mạng xã hội.
- **Chăm sóc tự động 24/7:** Tự động gửi ưu đãi (mã giảm giá, quà tặng), tự động nhắc nhở sau 2 giờ và theo dõi lịch sử tương tác của từng khách hàng.
- **Đồng bộ dữ liệu thời gian thực:** Mọi thông tin khách hàng, trạng thái click link hay nội dung feedback đều được lưu trữ gọn gàng vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted VPS).
- **Telegram Bot Token** (Tạo miễn phí qua `@BotFather`).
- **Google Sheets** (Tạo sẵn một file Sheet lưu trữ dữ liệu).
- **Trang web lọc đánh giá (Web Form):** Source code mẫu của tác giả có thể host miễn phí lên Netlify (Chi tiết ở phần hướng dẫn bên dưới).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **New** -> **Import from Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các điểm sau:

- **Chuẩn bị Web Form lọc đánh giá:** 
  Tải source code mẫu từ [GitHub của tác giả](https://github.com/anirudhaeran/Google-Review-Feedback-Form) và deploy lên Netlify miễn phí (Xem hướng dẫn [tại đây](https://youtu.be/9srnyNC1e_o?si=nSFDZRks_19p43jc)). Trang web này sẽ phân loại đánh giá của khách.
- **Cấu hình Google Sheets:**
  Tạo Google Sheet với các cột chính xác: `ID`, `First Name`, `Last Name`, `Status`, `Feedback Message`, `Timestamp`. Lấy Sheet ID từ URL và dán vào tất cả các node Google Sheets (`Fetch Rows from sheet`, `Updates customer details`, `Updates Status`, `Get row(s) in sheet1`, `update status to follow up sent`, `Update Status to 'Clicked'`, `Save Private Feedback to Sheet`).
- **Cấu hình Telegram Credentials:**
  Kết nối tài khoản Telegram Bot của các sếp vào tất cả các node Telegram (`Already claimed offer msg`, `Send Review Page Link`, `Send Incentive Offer`, `Send Review Link Reminder`).
- **Tùy chỉnh Link Web Form động:**
  Trong node **Send Review Page Link** và **Send Review Link Reminder**, hãy trỏ URL về website lọc đánh giá của các sếp, gắn thêm tham số `?userId={{ $json.id }}` ở cuối URL để hệ thống nhận diện đúng khách hàng (ví dụ: `https://yourwebsite.com?userId=123456789`).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và quét mã QR Bot Telegram của các sếp để test thử luồng nhắn tin, nhận ưu đãi và nhận link review.
- Kiểm tra Google Sheets xem dữ liệu khách hàng đã đổ về chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo nội bộ:** Nối thêm node Telegram hoặc Slack ở node `Save Private Feedback to Sheet` để ngay khi có khách để lại feedback tiêu cực, nhân viên CSKH hoặc quản lý sẽ nhận được cảnh báo ngay lập tức.
- **Mở rộng kênh chăm sóc:** Có thể thay thế Telegram bằng WhatsApp hoặc Zalo ZNS nếu khách hàng mục tiêu của các sếp sử dụng các nền tảng đó nhiều hơn.
- **Tùy biến ưu đãi:** Thay vì mã giảm giá 5%, các sếp có thể thay đổi chiến lược quà tặng (tặng voucher cafe, E-book, tài liệu hướng dẫn...) để kích thích khách hàng tương tác nhiều hơn.

### 📌 Kết luận
Một hệ thống quản lý danh tiếng tự động hoàn toàn bằng n8n sẽ giúp doanh nghiệp tiết kiệm hàng giờ đồng hồ mỗi tuần, đồng thời tối ưu hóa lượng đánh giá 5 sao trên Google Maps một cách tự nhiên nhất. Chúc các sếp cài đặt thành công và bùng nổ doanh số!