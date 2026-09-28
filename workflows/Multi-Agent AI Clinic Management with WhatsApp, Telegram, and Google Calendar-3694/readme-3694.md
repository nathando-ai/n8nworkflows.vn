---
title: "🚀 Xây Dựng Hệ Thống Quản Lý Phòng Khám AI Đa Tác Vụ (Multi-Agent) Với WhatsApp, Telegram và Google Calendar"
description: "Hướng dẫn chi tiết triển khai workflow n8n tự động hóa phòng khám y tế: tự động xác nhận lịch hẹn WhatsApp, xử lý âm thanh/hình ảnh bằng AI, tích hợp Google Calendar và quản lý nội bộ qua Telegram."
slug: "quan-ly-phong-kham-ai-da-tac-vu-n8n"
tags: [n8n, automation, ai-agent, whatsapp, telegram, google-calendar]
keywords: [n8n workflow, quan ly phong kham ai, multi-agent n8n, evolution api whatsapp, google calendar n8n, telegram bot n8n]
---

# 🚀 Xây Dựng Hệ Thống Quản Lý Phòng Khám AI Đa Tác Vụ (Multi-Agent) Với WhatsApp, Telegram và Google Calendar

Việc vận hành một phòng khám thủ công thường đối mặt với vô vàn áp lực: nhân viên tiếp tân quá tải vì phải nghe điện thoại, nhắn tin xác nhận lịch hẹn thủ công qua WhatsApp, xử lý các file ghi âm giọng nói hay hình ảnh đơn thuốc từ bệnh nhân, và dễ dẫn đến sai sót lịch hẹn trên Google Calendar. 

Workflow n8n **Multi-Agent AI Clinic Management** này giải quyết triệt để các vấn đề trên bằng cách xây dựng một đội ngũ Trợ lý AI (Multi-Agent) hoạt động tự động 24/7. Hệ thống tích hợp đa kênh (WhatsApp cho bệnh nhân, Telegram cho đội ngũ nội bộ), tự động hóa từ khâu nhắc lịch, nhận diện tin nhắn văn bản/audio/hình ảnh cho đến cập nhật lịch hẹn thông minh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn lịch hẹn:** Bot tự động quét Google Calendar mỗi ngày vào 08:00 sáng và gửi tin nhắn nhắc nhở/xác nhận qua WhatsApp cho bệnh nhân.
- **Xử lý đa phương tiện thông minh:** AI tự động nghe file audio (chuyển voice thành text qua Whisper), đọc ảnh chụp đơn thuốc/tài liệu (OCR) gửi qua WhatsApp.
- **Quản lý nội bộ qua Telegram:** Đội ngũ y bác sĩ, nhân viên phòng khám có thể ra lệnh cho trợ lý ảo để đổi lịch hẹn hoặc thêm danh sách mua sắm vào Google Tasks.
- **Bộ nhớ ngữ cảnh bền vững (Postgres Memory):** Giữ xuyên suốt lịch sử trò chuyện của bệnh nhân để AI phản hồi tự nhiên, chuẩn xác như nhân viên thật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để vận hành trơn tru workflow này, các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
- **n8n Instance** (Khuyên dùng bản Self-hosted trên VPS).
- **OpenAI API Key** (Dùng cho GPT-4o-mini/nano và Whisper transcribe).
- **OpenRouter API Key** (Dùng cho các model phụ trợ như Gemini).
- **Evolution API** (Instance WhatsApp để nhận/gửi tin nhắn tự động).
- **Telegram Bot Token** (Cho trợ lý nội bộ và cảnh báo).
- **Google OAuth2 Credentials** (Truy cập Google Calendar & Google Tasks).
- **PostgreSQL Database** (Lưu trữ bộ nhớ hội thoại chat memory cho AI Agent).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp (hoặc copy trực tiếp).
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) -> **Import from File** / **Import from JSON** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 31 nodes được chia thành nhiều phân khu chức năng rõ rệt. Các sếp cần lưu ý cấu hình kỹ các điểm sau:

- **Webhook1 & Evolution API Nodes (`Webhook1`, `Evolution API`, `Evolution API2`, `REMINDER`):** 
  - Cấu hình thông tin kết nối tới **Evolution API** của sếp (URL và Global API Key).
  - Trỏ Webhook URL từ n8n vào phần Webhook settings trên bảng điều khiển Evolution API để nhận tin nhắn WhatsApp đến (`evolutionAPIKORE`).
- **OpenAI & OpenRouter Chat Models (`OpenAI Chat Model`, `OpenRouter Chat Model1`, v.v.):**
  - Đảm bảo đã liên kết đúng thông tin xác thực API Key của OpenAI và OpenRouter.
  - Kiểm tra lại các biến thể model LLM được chọn (như `gpt-4.1-mini` hoặc `google/gemini-2.0-flash-exp`) để đảm bảo không bị lỗi model không tồn tại.
- **Postgres Chat Memory Nodes (`Postgres Chat Memory`, `Postgres Chat Memory1`):**
  - Kết nối tới cơ sở dữ liệu PostgreSQL của sếp để Agent ghi nhớ ngữ cảnh cuộc trò chuyện với bệnh nhân.
- **MCP Google Calendar & Google Tasks Tools:**
  - Cấu hình OAuth2 cho tài khoản Google cá nhân/tập thể của phòng khám để các Agent có quyền đọc/ghi lịch hẹn và tạo task mua sắm.
- **Gạt nút Kích hoạt Daily Trigger (`Gatilho diário`):**
  - Node này mặc định chạy lúc 08:00 sáng từ thứ Hai đến thứ Sáu để kích hoạt "Appointment Confirmation Assistant" quét lịch hẹn ngày mai và gửi tin nhắn nhắc nhở.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm với một tin nhắn webhook mẫu hoặc chạy thử trigger lịch trình.
- Kiểm tra log hoạt động của các AI Agent.
- Sau khi mọi thứ chạy ổn định, gạt công tắc **Active** góc trên bên phải để hệ thống chính thức tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo lỗi:** Có thể bổ sung node gửi thông báo qua Telegram hoặc Slack cho quản lý phòng khám nếu hệ thống gặp lỗi kết nối Evolution API hoặc OpenAI.
- **Mở rộng kênh giao tiếp:** Ngoài WhatsApp và Telegram, các sếp có thể mở rộng thêm Web Chat hoặc Messenger tích hợp chung vào luồng Multi-Agent này.
- **Tự động lưu log vào Google Sheets:** Lưu trữ toàn bộ lịch sử tương tác và yêu cầu đặt lịch của bệnh nhân vào một Google Sheet để đội ngũ marketing hoặc CS chăm sóc lại dễ dàng hơn.

### 📌 Kết luận
Hệ thống **Multi-Agent AI Clinic Management** là giải pháp đỉnh cao giúp phòng khám tối ưu hóa vận hành, giảm tải 80% công việc thủ công cho lễ tân và mang lại trải nghiệm chuyên nghiệp, tức thì cho bệnh nhân. Hãy triển khai ngay trên hệ thống n8n của các sếp để nâng tầm chất lượng dịch vụ y tế thời đại số!