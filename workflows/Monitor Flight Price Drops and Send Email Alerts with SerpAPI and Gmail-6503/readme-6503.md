---
title: "✈️ Tự Động Theo Dõi Giá Vé Máy Bay & Gửi Email Cảnh Báo Giảm Giá Với SerpAPI và Gmail"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động săn vé máy bay giá rẻ 24/7 thông qua SerpAPI và gửi email thông báo tức thì qua Gmail khi có biến động."
slug: "tu-dong-theo-doi-gia-ve-may-bay-va-gui-email-canh-bao-n8n"
tags: [n8n, automation, no-code, travel, serpapi, gmail, productivity]
keywords: [n8n workflow, theo dõi giá vé máy bay, serpapi n8n, tự động gửi email, săn vé máy bay giá rẻ, n8n viet nam]
---

# ✈️ Tự Động Theo Dõi Giá Vé Máy Bay & Gửi Email Cảnh Báo Giảm Giá

Các sếp có bao giờ mệt mỏi vì phải ngày đêm "canh" giá vé máy bay, F5 liên tục các trang web đặt vé chỉ để chờ một cơ hội giảm giá sâu cho chuyến du lịch hay công tác sắp tới? Việc kiểm tra thủ công này vừa tốn thời gian, dễ bỏ lỡ khung giờ vàng, lại cực kỳ phiền toái.

Đừng lo, workflow n8n **Monitor Flight Price Drops and Send Email Alerts with SerpAPI and Gmail** do tác giả *Yash Choudhary* xây dựng sẽ giải quyết triệt để bài toán này. Workflow này hoạt động như một "trợ lý ảo" tự động 100%, thay các sếp quét giá vé định kỳ, đối chiếu biến động và tự động bắn email cảnh báo ngay lập tức khi phát hiện giá vé giảm.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 săn vé mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7:** Không cần tốn một phút thủ công nào để mở web tra cứu giá vé mỗi ngày.
- **Bắt đáy kịp thời:** Nhận email thông báo ngay khi giá vé giảm, giúp book vé với mức giá tối ưu nhất.
- **Tiết kiệm chi phí tối đa:** Giúp tối ưu ngân sách đi lại cho cá nhân hoặc doanh nghiệp.
- **Hoạt động bền bỉ:** Chạy ngầm liên tục trên hệ thống n8n của các sếp mà không sợ quên.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- Một hệ thống n8n đang hoạt động ổn định.
- **SerpAPI Account & API Key:** Dùng để lấy dữ liệu tìm kiếm chuyến bay từ Google Flights.
- **Gmail Account (OAuth2):** Dùng để cấp quyền cho n8n gửi email thông báo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [link gốc n8n](https://n8n.io/workflows/6503) hoặc copy mã JSON tương ứng, sau đó dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Cron (Node lịch trình):** 
  - Thiết lập tần suất quét giá vé (ví dụ: chạy 1 lần/ngày vào lúc 8:00 sáng hoặc tùy chỉnh theo nhu cầu).
- **Fetch Price - SerpAPI (Node HTTP Request):** 
  - Cần tạo và liên kết `serpApi` credentials bằng API Key cá nhân của các sếp.
  - Cấu hình tham số đường dẫn (API parameters) cho chặng bay, điểm đi, điểm đến và ngày khởi hành mong muốn theo tài liệu của SerpAPI.
- **Check Price Drop (Node Function):** 
  - Nơi chứa đoạn mã Javascript dùng để lưu trữ lịch sử giá cũ, so sánh với mức giá mới vừa fetch về từ SerpAPI xem có giảm hay không.
- **IF Price Dropped? (Node điều kiện):** 
  - Kiểm tra kết quả trả về từ node function. Nếu giá mới thấp hơn giá cũ (Điều kiện `True`), workflow sẽ chuyển sang bước tiếp theo.
- **Send a message (Node Gmail):** 
  - Cấu hình `gmailOAuth2` credentials.
  - Điền email nhận thông báo, tiêu đề email (ví dụ: *"🔥 Cảnh báo: Giá vé máy bay chặng X vừa giảm!"*) và nội dung chi tiết kèm mức giá mới.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm (Test run) xem dữ liệu có trả về đúng và email có bắn thành công không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Nâng cấp & gợi ý mở rộng
Để workflow trở nên "xịn xò" hơn, các sếp có thể tùy biến thêm:
- **Đa kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack để nhận thông báo ngay trên điện thoại thay vì chỉ check email.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử biến động giá vé theo từng ngày, giúp phân tích xu hướng giá.
- **Theo dõi nhiều chặng bay:** Nhân bản các nhánh workflow để theo dõi đồng thời nhiều hành trình khác nhau.

### 📌 Kết luận
Việc săn vé máy bay giá rẻ chưa bao giờ dễ dàng đến thế khi đã có tự động hóa hỗ trợ. Hãy triển khai ngay workflow này lên n8n của các sếp để tối ưu hóa thời gian và không bao giờ bỏ lỡ những chuyến đi với mức giá hời nhất! Chúc các sếp thao tác thành công!