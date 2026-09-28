---
title: "🚀 Tự động tìm việc làm trên Indeed qua Telegram với BrowserAct và Gemini"
description: "Xây dựng trợ lý tìm việc ảo thông minh qua Telegram: Tự động cào dữ liệu từ Indeed bằng BrowserAct, xử lý và lọc tin tuyển dụng bằng AI Gemini/OpenRouter rồi gửi báo cáo chi tiết đến điện thoại."
slug: "tim-viec-lam-indeed-qua-telegram-browseract-gemini"
tags: [n8n, automation, no-code, telegram, ai-agent, web-scraping]
keywords: [n8n workflow, tìm việc Indeed, BrowserAct, Gemini AI, Telegram bot tự động, AI agent n8n]
---

# 🚀 Tự động tìm việc làm trên Indeed qua Telegram với BrowserAct và Gemini

Việc tìm kiếm công việc mơ ước trên các trang tuyển dụng lớn như Indeed thường tốn rất nhiều thời gian lọc thủ công, lướt qua hàng trăm tin rác và trùng lặp. Các sếp có bao giờ ước gì mình chỉ cần nhắn một tin nhắn đơn giản qua Telegram như *"Tuyển dụng Marketing Manager tại Austin"* và ngay lập tức nhận được danh sách việc làm đã được chọc lọc, phân tích kỹ lưỡng gửi thẳng vào điện thoại không?

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp các sếp giải quyết triệt để bài toán săn việc làm tự động nhờ sự kết hợp mạnh mẽ giữa **Telegram Bot**, công cụ cào web **BrowserAct** và các mô hình AI thông minh như **Gemini** & **OpenRouter**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác liền mạch:** Chỉ cần chat với Telegram Bot để ra lệnh tìm kiếm việc làm mọi lúc mọi nơi.
- **Tự động hóa toàn diện:** Tự động nhận diện từ khóa (Vị trí công việc & Địa điểm), tự động điền giá trị mặc định (ví dụ: *Brooklyn*) nếu người dùng quên nhập địa điểm.
- **Cào dữ liệu thông minh:** Sử dụng BrowserAct để bóc tách dữ liệu việc làm thực tế từ Indeed (tiêu đề, mức lương, phúc lợi...) một cách mượt mà.
- **AI xử lý tinh gọn:** AI Agent (Gemini/OpenRouter) tự động loại bỏ tin rác, lọc trùng lặp và định dạng tin tuyển dụng thành các thông điệp HTML trực quan, dễ đọc trên di động.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram.
- **BrowserAct Account & API:** Cần có tài khoản và template **"The Indeed Smart Job Scout"** được lưu sẵn trên hệ thống BrowserAct.
- **Google Gemini API / OpenRouter API:** Để cung cấp "bộ não" phân tích ngôn ngữ tự nhiên cho các AI Agent.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **User Sends Message to Bot (`telegramTrigger`):** Kết nối với thông tin Credentials của Telegram Bot của các sếp để nhận lệnh chat từ người dùng.
- **Extract Job Data (`n8n-nodes-browseract.browserAct`):** 
  - Chọn Credentials cho BrowserAct.
  - Đảm bảo các sếp đã cài sẵn template **"The Indeed Smart Job Scout"** trong tài khoản BrowserAct của mình để node này có thể gọi đúng kịch bản cào dữ liệu Indeed.
- **Analyze user Input (`agent`) & OpenRouter Chat Model / Gemini (`lmChatOpenRouter`, `lmChatGoogleGemini`):** 
  - Cấu hình API Key của OpenRouter hoặc Google Palm/Gemini.
  - Node này chịu trách nhiệm bóc tách ý định người dùng (Role & Location). Nếu thiếu địa điểm, AI sẽ tự động gán mặc định là *Brooklyn*.
- **Send Job Post to Telegram (`telegram`):** Node cuối cùng nhận dữ liệu đã được xử lý (qua node `Split Out Generated Data`) và bắn kết quả định dạng HTML đẹp mắt về lại chat Telegram cho các sếp.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test workflow** và thử nhắn một tin nhắn mẫu tới Telegram Bot của các sếp (ví dụ: *"Python Developer in New York"*).
- Kiểm tra kết quả trả về, nếu mọi thứ hoạt động trơn tru thì gạt công tắc sang **Active** để đưa bot vào vận hành chính thức 24/7.

---
### ⚙️ Quy trình hoạt động chi tiết qua 3 bước:
1. **🗣️ Bước 1: Trích xuất ý định & tham số:** Workflow phân tích tin nhắn Telegram, tách ra chức danh nghề nghiệp và địa điểm. Nếu thiếu, AI tự động thêm giá trị mặc định.
2. **🕵️ Bước 2: Cào dữ liệu trực tuyến:** BrowserAct thực thi phiên tự động trên Indeed dựa trên tham số đã lọc, thu thập các thông tin mới nhất về việc làm.
3. **🧠 Bước 3: Phân tích AI & Định dạng:** AI Agent xử lý thô dữ liệu, lọc bỏ tin trùng lặp/spam và trình bày lại thành dạng bản tin gọn gàng, nhiều emoji.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hơn nữa con bot tìm việc này, các sếp có thể cân nhắc:
- **Tích hợp Google Sheets / Airtable:** Thêm một node lưu trữ lại toàn bộ các tin tuyển dụng đã tìm được vào bảng tính để dễ dàng theo dõi tiến trình ứng tuyển.
- **Cảnh báo qua Slack/Discord:** Thay vì chỉ gửi Telegram cá nhân, có thể mở rộng nhánh gửi tin vào kênh tuyển dụng chung của team.
- **Lịch chạy định kỳ (Cron):** Kết hợp thêm `Schedule Trigger` để bot chủ động tìm việc mới mỗi sáng gửi cho các sếp mà không cần phải ra lệnh thủ công.

### 📌 Kết luận
Workflow **Find jobs on Indeed via Telegram using BrowserAct and Gemini** là một minh chứng tuyệt vời cho việc ứng dụng AI và No-Code vào đời sống hàng ngày. Hãy cài đặt ngay hôm nay để biến chiếc Telegram của các sếp thành một "Headhunter" cá nhân chuyên nghiệp và tận tụy!