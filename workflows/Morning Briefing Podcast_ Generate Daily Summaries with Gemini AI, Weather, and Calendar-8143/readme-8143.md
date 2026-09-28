---
title: "🚀 Tự động tạo bản tin Podcast buổi sáng với Gemini AI, Thời tiết và Lịch cá nhân trên n8n"
description: "Xây dựng hệ thống tự động tổng hợp tin tức, lịch họp Google Calendar và thời tiết, sau đó chuyển đổi thành file audio Podcast phát qua Telegram nhờ Gemini AI."
slug: "tao-podcast-buoi-sang-gemini-ai-n8n"
tags: [n8n, automation, ai, gemini, telegram, google-calendar, podcast]
keywords: [n8n workflow, podcast tự động, gemini ai, google calendar, openweathermap, newsapi, telegram bot]
---

# 🚀 Tự động tạo bản tin Podcast buổi sáng với Gemini AI, Thời tiết và Lịch cá nhân trên n8n

Mỗi buổi sáng, các sếp thường mất bao nhiêu thời gian để mở lịch xem hôm nay họp hành ra sao, lướt app thời tiết xem mưa nắng thế nào, rồi lại lướt các trang tin tức công nghệ để cập nhật thông tin? Việc này vừa tốn thời gian lại dễ bị phân tâm. 

Thay vì làm thủ công mỗi ngày, tại sao không để n8n "lên đồ" một hệ thống tự động hóa hoàn toàn? Workflow này sẽ thay các sếp gom nhặt **Lịch làm việc (Google Calendar)**, **Thời tiết (OpenWeatherMap)** và **Tin tức nóng hổi (NewsAPI)**, sau đó dùng sức mạnh của **Gemini AI** để viết kịch bản trò chuyện, tổng hợp thành một bản tin Podcast âm thanh cực kỳ chuyên nghiệp và tự động gửi thẳng vào **Telegram** cá nhân mỗi sáng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tệp âm thanh mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Nhận trọn bộ bản tin tóm tắt thời tiết, lịch họp, tin tức công nghệ chỉ bằng một file audio ngay khi thức dậy.
- **Cá nhân hóa thông minh:** Gemini AI biên tập lại nội dung thành văn phong trò chuyện gần gũi, dễ nghe như một người trợ lý thực thụ.
- **Tự động hóa 100%:** Kết hợp nhịp nhàng giữa các API bên thứ ba (Google, NewsAPI, OpenWeatherMap) và AI mà không cần viết một dòng code phức tạp nào.
- **Tiện lợi mọi lúc mọi nơi:** Podcast được gửi trực tiếp qua Telegram, các sếp có thể nghe trong lúc tập thể dục, lái xe hoặc pha cà phê sáng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (phiên bản Cloud hoặc Self-hosted).
- **Google Calendar Account** (để lấy lịch họp trong ngày).
- **Google Gemini API Key** (Google AI Studio / PaLM API) cho các node LangChain LLM.
- **NewsAPI Key** (để lấy tiêu điểm tin tức công nghệ).
- **OpenWeatherMap API Key** (để lấy dự báo thời tiết).
- **Telegram Bot Token & Chat ID** (để gửi file audio Podcast về máy).
- Một dịch vụ chuyển đổi text-to-speech (hoặc cấu hình HTTP Request tới API tạo giọng đọc tương ứng trong node `Generate Podcast Audio`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow từ nguồn cung cấp.
- Mở n8n Editor, tạo một workflow mới và chọn **Import from JSON**, sau đó dán đoạn code vào và nhấn lưu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này có tới 27 nodes chia thành các nhánh xử lý song song và gom tụ lại. Các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Get Today Meetings (`Get Today Meetings`)**: Kết nối tài khoản Google Calendar OAuth2, cấu hình lấy danh sách sự kiện trong ngày hiện tại.
- **Open Weather Map (`Open Weather Map`)**: Điền OpenWeatherMap API Key và cấu hình tọa độ (hoặc tên thành phố) của các sếp vào node HTTP Request này.
- **Get Headlines from NewsApi (`Get Headlines from NewsApi`)**: Cấu hình NewsAPI Key qua Header Auth để hệ thống cào tin tức từ các trang công nghệ hàng đầu.
- **Gemini AI Agents (`Calendar Summary`, `Weather Summary`, `News Summary`)**: Kết nối các node `Gemini_Calendar`, `Gemini_Weather`, `Gemini_News` với **Google Gemini API Credentials**. Tại đây, các sếp có thể tùy chỉnh Prompt trong các Agent để AI định hình phong cách đọc (ví dụ: vui vẻ, nghiêm túc, ngắn gọn...).
- **Generate Podcast Audio (`Generate Podcast Audio`)**: Node này chịu trách nhiệm gọi API Text-to-Speech (TTS) để biến kịch bản văn bản thành âm thanh. Cần điền đúng thông tin xác thực (HTTP Basic/Header Auth) của dịch vụ âm thanh mà các sếp sử dụng.
- **Send Podcast to Telegram (`Send Podcast to Telegram`)**: Kết nối Telegram Bot Credentials và điền Chat ID của các sếp để hệ thống bắn file Audio hoàn chỉnh về.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `When clicking ‘Execute workflow’` để test thử toàn bộ chuỗi xử lý (từ lấy dữ liệu -> qua AI -> sinh file audio -> gửi Telegram).
- Kiểm tra xem file audio đã nhảy vào Telegram của các sếp chưa.
- Sau khi test ngon lành, hãy đổi `Manual Trigger` thành `Schedule Trigger` (đặt lịch chạy 6:00 sáng mỗi ngày) và gạt công tắc **Active** lên màu xanh là xong!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn tin:** Các sếp có thể bổ sung thêm các RSS Feed báo chí Việt Nam vào phần `News Sources` để bản tin gần gũi hơn với thị trường trong nước.
- **Thêm bước lưu trữ:** Lưu bản ghi âm podcast vào Google Drive hoặc Notion Database để có thể nghe lại bất cứ lúc nào.
- **Tích hợp giọng đọc AI tiếng Việt:** Sử dụng các dịch vụ Text-to-Speech hỗ trợ giọng đọc tiếng Việt mượt mà (như FPT.AI, VinBigdata, hoặc ElevenLabs) để bản tin Podcast nghe tự nhiên nhất.

### 📌 Kết luận
Một trợ lý ảo điểm tin buổi sáng cá nhân hóa không chỉ giúp các sếp tiết kiệm khối lượng lớn thời gian mà còn khởi đầu ngày mới đầy hứng khởi với thông tin được chắt lọc tinh gọn. Hãy import workflow này ngay lên hệ thống n8n của các sếp và tận hưởng sức mạnh tự động hóa!