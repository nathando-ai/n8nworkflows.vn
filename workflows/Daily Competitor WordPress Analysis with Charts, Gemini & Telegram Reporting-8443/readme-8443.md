---
title: "🚀 Tự động phân tích website đối thủ WordPress hàng ngày với Google Gemini & Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động cào bài viết mới từ RSS đối thủ WordPress, chụp ảnh màn hình, phân tích bằng AI Gemini và gửi báo cáo trực quan qua Telegram."
slug: "tu-dong-phan-tich-doi-thu-wordpress-gemini-telegram"
tags: [n8n, automation, ai, google-gemini, telegram, wordpress, market-research]
keywords: [n8n workflow, phân tích đối thủ, google gemini ai, telegram reporting, tự động hóa n8n, cào rss wordpress]
keywords: [n8n workflow, phân tích đối thủ, google gemini ai, telegram reporting, tự động hóa n8n]
---

# 🚀 Tự động phân tích website đối thủ WordPress hàng ngày với Google Gemini & Telegram

Các sếp có đang đau đầu vì phải tốn hàng giờ mỗi ngày để truy cập vào website của các đối thủ cạnh tranh xem họ có bài viết mới nào, nội dung ra sao, chiến lược thế nào không? Việc theo dõi thủ công này không chỉ mất thời gian mà còn dễ bỏ sót những thông tin quan trọng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh do tác giả Cong Nguyen xây dựng. Workflow này sẽ tự động hóa 100% quy trình: lấy tin từ RSS của đối thủ, chụp ảnh màn hình giao diện, sử dụng AI đa phương thức (Google Gemini) để phân tích hình ảnh và nội dung, lưu trữ vào Google Sheets, cuối cùng là tổng hợp và gửi báo cáo trực quan ngay lập tức qua Telegram. Các sếp chỉ việc nhận thông tin và đưa ra chiến lược!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% định kỳ:** Chạy tự động mỗi ngày nhờ `Schedule Trigger`, không cần can thiệp thủ công.
- **Bắt trọn mọi nội dung:** Theo dõi đồng thời nhiều đối thủ sử dụng nền tảng WordPress thông qua các nguồn `RSS opponent`.
- **Phân tích thông minh bằng AI:** Kết hợp `APIFlash` để chụp ảnh màn hình và sức mạnh thị giác của `Google Gemini` để đánh giá bài viết, giao diện đối thủ.
- **Báo cáo tức thì qua Telegram:** Nhận thông tin tóm tắt và số liệu thống kê được gửi thẳng vào chat Telegram cá nhân hoặc nhóm làm việc.
- **Lưu trữ dữ liệu lịch sử:** Tự động ghi nhận thông tin bài viết vào `Google Sheets` để tiện theo dõi và phân tích xu hướng dài hạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Sheets:** Một trang tính (Google Sheet) dùng để lưu lịch sử phân tích bài viết đối thủ.
- **Google Gemini API Key:** Tài khoản Google Cloud/AI Studio để sử dụng node phân tích hình ảnh (Google Gemini).
- **APIFlash API Key:** Dịch vụ chụp ảnh màn hình website (hoặc dịch vụ tương đương được cấu hình trong HTTP Request).
- **Telegram Bot Token & Chat ID:** Tạo một Bot Telegram qua BotFather để gửi tin nhắn báo cáo.
- **Danh sách RSS của đối thủ:** URL nguồn RSS từ các website WordPress của đối thủ cạnh tranh (thường có dạng `https://domain.com/feed/`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n.
- Trong giao diện n8n Editor, bấm vào menu **Add workflow** -> **Import from File** và chọn file JSON vừa tải, hoặc copy toàn bộ mã JSON và dán trực tiếp vào không gian làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru không lỗi, các sếp cần cấu hình kỹ các node sau:
- **Schedule Trigger:** Thiết lập lại khung giờ chạy tự động hàng ngày (ví dụ: 8:00 sáng mỗi ngày) cho phù hợp với múi giờ và nhu cầu doanh nghiệp.
- **RSS opponent 1, 2, 3 (HTTP Request):** Thay thế các URL mẫu bằng đường dẫn RSS thực tế của các website đối thủ WordPress mà các sếp muốn theo dõi.
- **APIFlash (HTTP Request):** Điền API Key của dịch vụ chụp ảnh màn hình và trỏ đường dẫn tới URL bài viết mới của đối thủ vừa lấy từ RSS.
- **Analyze image (Google Gemini):** Kết nối thông tin Credentials Google Gemini. Tùy chỉnh câu lệnh (Prompt) trong node AI này để hướng dẫn Gemini phân tích hình ảnh giao diện và nội dung theo ý muốn (ví dụ: *“Hãy tóm tắt bố cục, đánh giá tiêu đề và điểm nổi bật của bài viết này qua hình ảnh”*).
- **Append or update row in sheet (Google Sheets):** Kết nối tài khoản Google, chọn đúng file Sheet và Sheet Name đã chuẩn bị để lưu dữ liệu tiêu đề, link, kết quả phân tích.
- **Send a text message (Telegram):** Thêm Telegram Bot Credentials, cấu hình chính xác `Chat ID` nơi nhận báo cáo tổng hợp từ node `Aggregate` và `Merge`.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử thủ công (Test Run) kiểm tra xem dữ liệu có chảy qua từng node suôn sẻ hay không.
- Sau khi test thành công và nhận được tin nhắn trên Telegram, các sếp hãy gạt công tắc sang trạng thái **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn đối thủ:** Dễ dàng nhân bản các node `RSS opponent` và `Limit` để theo dõi từ 5 đến 10 đối thủ cùng lúc.
- **Tích hợp thêm Slack/Teams:** Bên cạnh Telegram, có thể gắn thêm node Slack để gửi báo cáo tự động vào kênh chung của team Marketing.
- **Tạo biểu đồ trực quan:** Kết hợp dữ liệu lưu trong Google Sheets để vẽ biểu đồ tần suất đăng bài của đối thủ theo tuần/tháng.
- **Cảnh báo từ khóa (Keyword Alert):** Thêm điều kiện lọc (If node) trong Gemini để nếu đối thủ nhắc đến từ khóa nhạy cảm hoặc chiến dịch lớn, đẩy thẳng tin nhắn khẩn cấp lên Telegram.

### 📌 Kết luận
Với workflow n8n Daily Competitor WordPress Analysis, việc theo dõi đối thủ cạnh tranh chưa bao giờ trở nên đơn giản và tự động đến thế. Hãy cài đặt ngay hôm nay để nắm bắt từng bước đi của đối thủ, tối ưu hóa chiến lược nội dung và vượt lên dẫn đầu thị trường! Chúc các sếp automation thành công!