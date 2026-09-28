---
title: "🚀 Tự động phân tích đánh giá Google Play Store, lưu Google Sheets và cảnh báo Telegram với Bright Data"
description: "Hướng dẫn xây dựng hệ thống tự động cào dữ liệu đánh giá ứng dụng từ Google Play bằng Bright Data API, tự động lưu trữ vào Google Sheets và gửi cảnh báo khẩn cấp qua Telegram khi nhận đánh giá thấp."
slug: "google-play-review-intelligence-bright-data-telegram"
tags: [n8n, automation, no-code, bright-data, google-sheets, telegram]
keywords: [n8n workflow, cào google play review, bright data api, tự động hóa google sheets, telegram alert]
keywords: [n8n workflow, cào google play review, bright data api, tự động hóa google sheets, telegram alert]
---

# 🚀 Tự động phân tích đánh giá Google Play Store, lưu Google Sheets và cảnh báo Telegram

Các sếp có đang đau đầu vì phải thủ công vào Google Play Store đọc từng review của người dùng để nắm bắt phản hồi về ứng dụng của mình hoặc đối thủ? Việc này không chỉ tốn hàng giờ đồng hồ mà còn rất dễ bỏ lỡ các đánh giá tiêu cực (1-3 sao) cần xử lý khẩn cấp.

Giải pháp là đây! Workflow n8n tự động hóa 100% giúp các sếp kích hoạt cào dữ liệu đánh giá từ Google Play Store thông qua Bright Data, tự động lưu toàn bộ vào Google Sheets để phân tích dài hạn, và đặc biệt sẽ **bắn tin nhắn cảnh báo ngay lập tức qua Telegram** khi phát hiện đánh giá thấp. Không cần biết lập trình, chỉ cần kéo thả và kết nối!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhập link ứng dụng và số lượng review qua form, phần còn lại hệ thống lo.
- **Lưu trữ khoa học:** Tự động đồng bộ toàn bộ review và thông tin ứng dụng vào Google Sheets để làm báo cáo.
- **Phản ứng chớp nhoáng:** Phát hiện ngay các review thấp điểm (dưới 4 sao) và đẩy cảnh báo trực tiếp về nhóm Telegram để đội ngũ CSKH/Tech xử lý kịp thời.
- **Tiết kiệm thời gian:** Thay vì mất hàng giờ lướt store mỗi ngày, các sếp nhận báo cáo tổng hợp chỉ sau vài phút.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Bright Data Account:** Tài khoản Bright Data để sử dụng API cào dữ liệu Google Play.
- **Google Account:** Tài khoản Google Sheets để lưu trữ dữ liệu.
- **Telegram Bot:** Một Telegram Bot Token và Chat ID để nhận tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node sau:

- **✅ Trigger Input Form**: Cấu hình form nhận đầu vào gồm URL của ứng dụng trên Google Play Store và số lượng review muốn cào.
- **🚀 Start Scraping Request** & **🔄 Check Scrape Status**: Điền API Key và endpoint của Bright Data API để khởi tạo yêu cầu cào dữ liệu và kiểm tra trạng thái snapshot ID.
- **⏱️ Wait for Response 45 sec** & **🧩 Verify Completion**: Node chờ 45 giây và vòng lặp kiểm tra xem dataset đã sẵn sàng (`status: "ready"`) hay chưa.
- **📥 Fetch Scraped Data**: Node lấy kết quả dữ liệu thô (reviews và thông tin app) sau khi Bright Data xử lý xong.
- **📊 Save to Google Sheet**: Kết nối tài khoản `googleSheetsOAuth2Api`, chọn file Google Sheets và cấu hình operation `append` để lưu dữ liệu vào bảng tính.
- **⚠️ Check Low Ratings** & **📣 Send Alert to Telegram**: Cấu hình điều kiện lọc review (ví dụ: rating < 4) và kết nối `telegramApi` để gửi thông báo khẩn cấp đến nhóm Telegram khi có review kém chất lượng.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** và điền thử URL ứng dụng vào Form để kiểm tra toàn bộ luồng chạy.
- Nếu dữ liệu đổ về Google Sheets và Telegram thành công, các sếp hãy bật **Active workflow** để hệ thống hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI phân loại lỗi:** Thêm một node OpenAI/Anthropic sau bước cào dữ liệu để tự động phân tích xem review tiêu cực thuộc lỗi kỹ thuật, lỗi thanh toán hay phàn nàn về tính năng.
- **Báo cáo định kỳ:** Kết hợp thêm node Schedule Trigger để tự động cào dữ liệu của đối thủ mỗi tuần một lần và gửi báo cáo tóm tắt qua Telegram/Email.
- **Lưu lịch sử lỗi:** Thêm nhánh Error Trigger để nếu Bright Data API lỗi, hệ thống sẽ tự động thông báo về Telegram để các sếp biết và kiểm tra credit tài khoản.

### 📌 Kết luận
Với workflow **Google Play Review Intelligence**, việc theo dõi sức khỏe ứng dụng và phản hồi của người dùng trên chợ ứng dụng chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay hôm nay để không bỏ lỡ bất kỳ tín hiệu nào từ khách hàng!