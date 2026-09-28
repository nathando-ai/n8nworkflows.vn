---
title: "🚀 Tự động hóa bản tin thời tiết cá nhân hóa với OpenWeatherMap, Python và GPT-4.1-mini"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy dữ liệu thời tiết, sử dụng AI tạo nội dung hài hước và gửi email báo cáo cá nhân hóa cho người dùng qua Gmail."
slug: "tao-ban-tin-thoi-tiet-ca-nhan-hoa-n8n-openai"
tags: [n8n, automation, no-code, openai, python, productivity]
keywords: [n8n workflow, tự động hóa thời tiết, openweathermap, gpt-4.1-mini, ai agent, gui email tu dong]
---

# 🚀 Tự động hóa bản tin thời tiết cá nhân hóa với OpenWeatherMap, Python và GPT-4.1-mini

Các sếp có bao giờ cảm thấy việc cập nhật thời tiết mỗi ngày để chuẩn bị trang phục hay lịch trình khá nhàm chán? Việc phải tự tra cứu rồi tự viết email nhắc nhở hoặc chuẩn bị nội dung cho khách hàng/đội ngũ thủ công thực sự tốn nhiều thời gian và thiếu sự sinh động. 

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Chỉ với một cú click điền tên thành phố qua form, hệ thống sẽ tự động lấy dữ liệu thời tiết thời gian thực, xử lý dữ liệu qua Python, nhờ AI (GPT-4.1-mini) viết một lời khuyên kèm câu đùa dí dỏm, sau đó tự động gửi một email cực kỳ cá nhân hóa đến hộp thư của các sếp. Hoàn toàn tự động 100% và không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Tự động hóa hoàn toàn quy trình từ tra cứu, xử lý đến gửi email chỉ trong vài giây.
- **Cá nhân hóa cao:** Kết hợp sức mạnh của AI Agent để tạo ra nội dung độc đáo, hài hước dựa trên tình hình thời tiết thực tế tại thành phố được chọn.
- **Hoạt động liên tục:** Form trigger giúp kích hoạt workflow bất cứ lúc nào người dùng có nhu cầu tra cứu.
- **Quy trình chuyên nghiệp:** Kết hợp linh hoạt giữa HTTP Request, Python script và mô hình ngôn ngữ lớn (LLM).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenWeatherMap API Key:** Tài khoản miễn phí để lấy dữ liệu thời tiết.
- **OpenAI API Key:** Để sử dụng model `gpt-4.1-mini` thông qua AI Agent.
- **Gmail Account / Credentials:** Tài khoản Gmail để cấp quyền cho n8n gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor để hệ thống tự động dựng các nodes.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 7 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **On form submission (`formTrigger`):** Node khởi chạy bằng giao diện form. Các sếp có thể tuỳ chỉnh trường nhập liệu để người dùng điền tên thành phố muốn xem thời tiết.
- **Fetch Weather Data (`httpRequest`):** 
  - Cấu hình gọi API đến OpenWeatherMap.
  - Thay thế đoạn `<your_API_key>` bằng OpenWeatherMap API Key thực tế của các sếp.
- **Process Weather Data (`code`):** Node sử dụng Python script để xử lý dữ liệu thô nhận được từ API thời tiết thành dạng dễ đọc.
- **AI Agent & OpenAI Chat Model (`agent` & `lmChatOpenAi`):**
  - Điền OpenAI API Key vào credentials của model `gpt-4.1-mini`.
  - Nhiệm vụ của AI Agent là phân tích thời tiết và viết một câu đùa/lời khuyên hài hước liên quan đến thành phố vừa nhập để làm phong phú nội dung email.
- **Generate Email Content (`code`):** Node code tiếp tục tổng hợp dữ liệu thời tiết và phần nội dung do AI tạo ra để đóng gói thành một template email hoàn chỉnh.
- **Send a message (`gmail`):** 
  - Kết nối tài khoản Gmail của các sếp.
  - Cập nhật tiêu đề (Subject) và phần thân email (Body) lấy từ kết quả của các bước trước để gửi đến người nhận mong muốn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền tên một thành phố bất kỳ vào form để kiểm tra toàn bộ luồng dữ liệu.
- Sau khi test thành công và email đã bay vào inbox mượt mà, các sếp nhớ bật công tắc **Active** ở góc trên bên phải để chính thức đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi qua Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack để bắn thông báo thời tiết ngay lập tức lên nhóm chat làm việc mỗi sáng.
- **Lưu lịch sử tra cứu:** Thêm node Google Sheets để ghi lại lịch sử các thành phố mà người dùng đã tra cứu nhằm phục vụ việc phân tích nhu cầu.
- **Lên lịch tự động (Cron):** Thay thế `Form Trigger` bằng `Schedule Trigger` để hệ thống tự động gửi bản tin thời tiết mỗi 7:00 sáng cho danh sách người đăng ký sẵn.

### 📌 Kết luận
Workflow tích hợp OpenWeatherMap, Python và GPT-4.1-mini là một ví dụ tuyệt vời cho việc ứng dụng AI và No-code vào đời sống và công việc hàng ngày. Hãy cài đặt ngay hôm nay để trải nghiệm sự tiện lợi mà tự động hóa mang lại cho các sếp!