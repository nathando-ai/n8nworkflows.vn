---
title: "🚀 Tự động hóa đánh giá và so sánh CV ứng viên bằng OpenAI, Google Sheets và Telegram"
description: "Xây dựng hệ thống HR thông minh trên n8n giúp tự động lọc CV, so sánh ứng viên bằng OpenAI AI và gửi báo cáo chi tiết qua Telegram ngay lập tức."
slug: "tao-bao-cao-so-sanh-cv-tu-dong-voi-openai-google-sheets-telegram"
tags: [n8n, automation, hr-tech, openai, google-sheets, telegram]
keywords: [n8n workflow, loc cv tu dong, openai hr, so sanh cv ung vien, telegram bot n8n]
---

# 🚀 Tự động hóa đánh giá và so sánh CV ứng viên bằng OpenAI, Google Sheets và Telegram

Các sếp làm trong ngành nhân sự (HR) chắc hẳn đã quá quen thuộc với "cực hình" mỗi mùa tuyển dụng: hàng trăm bộ CV đổ về, việc đọc lướt, tổng hợp thông tin, so sánh ưu nhược điểm của từng ứng viên để chọn ra người phù hợp tốn rất nhiều thời gian và dễ xảy ra sai sót.

Đừng để đội ngũ nhân sự của các sếp phải chôn vùi thời gian vào những tác vụ thủ công đó nữa! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ, kết hợp giữa **Google Sheets**, **OpenAI (LLM)** và **Telegram**. Hệ thống này sẽ tự động đọc dữ liệu ứng viên, phân tích, lập báo cáo so sánh chi tiết và gửi thẳng kết quả về Telegram cho các sếp chỉ trong vài giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian sàng lọc:** Không cần phải mở từng file CV hay bảng tính để so sánh thủ công.
- **Đánh giá khách quan, chuyên sâu:** OpenAI sẽ phân tích và so sánh các ứng viên dựa trên tiêu chí rõ ràng, giúp các sếp không bỏ lỡ nhân tài.
- **Tương tác linh hoạt qua Telegram:** Kích hoạt và nhận báo cáo mọi lúc mọi nơi ngay trên điện thoại thông qua Telegram Bot.
- **Vận hành 24/7:** Quy trình tự động 100% từ lúc nhận lệnh đến khi trả kết quả báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Telegram Bot Token** (tạo qua BotFather) để nhận lệnh và gửi báo cáo.
- **Google Sheets** chứa danh sách thông tin và dữ liệu CV của các ứng viên.
- **OpenAI API Key** để kích hoạt mô hình AI phân tích và tạo báo cáo so sánh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ chính thức của n8n (Link: `https://n8n.io/workflows/15288`), sau đó chọn **Import from File** hoặc copy và paste trực tiếp đoạn JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình các node quan trọng sau:

- **When Telegram Message Received (`telegramTrigger`):** 
  - Kết nối với tài khoản Telegram thông qua `telegramApi` credentials của sếp.
  - Node này sẽ lắng nghe câu lệnh (command) từ Telegram để bắt đầu tiến trình tạo báo cáo.
- **Parse Telegram Command (`code`) & Transform Candidate Data (`code`):** 
  - Các node mã hóa bằng JavaScript này làm nhiệm vụ bóc tách cú pháp lệnh từ tin nhắn Telegram và chuẩn bị cấu trúc dữ liệu trước khi ném vào AI. (Thường không cần sửa code trừ khi các sếp muốn đổi cú pháp lệnh).
- **Read Candidates from Sheets (`googleSheets`):** 
  - Chọn tài khoản `googleSheetsOAuth2Api`.
  - Trỏ tới file Google Sheets chứa dữ liệu ứng viên của các sếp và chọn đúng Sheet Name / Range phù hợp.
- **Generate Comparative Report (`openAi`):** 
  - Cấu hình `openAiApi` credentials.
  - Tinh chỉnh Prompt bên trong node LLM này để OpenAI hiểu rõ tiêu chí tuyển dụng (ví dụ: yêu cầu kinh nghiệm, kỹ năng lập trình, ngoại ngữ...) nhằm đưa ra bản so sánh chính xác nhất.
- **Send Report via Telegram (`telegram`):** 
  - Sử dụng lại `telegramApi` credentials để gửi báo cáo hoàn thiện về chat ID của sếp hoặc group chat nhân sự.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một lệnh mẫu qua Telegram Bot để kiểm tra xem dữ liệu từ Google Sheets có được AI xử lý và trả về chính xác không.
- Nếu mọi thứ mượt mà, hãy gạt nút **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tuyển dụng thông minh hơn nữa, các sếp có thể mở rộng workflow bằng cách:
- **Tích hợp Slack/Microsoft Teams:** Thay vì chỉ gửi Telegram, hãy bắn thông báo đồng thời lên kênh HR trên Slack.
- **Lưu lịch sử báo cáo:** Thêm một bước ghi ngược lại kết quả đánh giá của AI vào một sheet mới trong Google Sheets để lưu trữ hồ sơ.
- **Phân loại tự động:** Dựa vào điểm số từ OpenAI, tự động gắn nhãn "Đạt" hoặc "Cần phỏng vấn vòng 2" cho ứng viên.

### 📌 Kết luận
Việc ứng dụng AI và tự động hóa vào quy trình tuyển dụng chưa bao giờ dễ dàng đến thế với n8n. Hãy thiết lập ngay workflow này để giải phóng sức lao động cho đội ngũ HR và tìm kiếm những mảnh ghép hoàn hảo cho doanh nghiệp một cách nhanh chóng nhất!