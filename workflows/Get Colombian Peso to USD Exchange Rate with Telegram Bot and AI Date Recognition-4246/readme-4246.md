---
title: "🚀 Tra cứu tỷ giá Peso Colombia sang USD tự động qua Telegram Bot kết hợp AI"
description: "Hướng dẫn xây dựng chatbot Telegram thông minh tích hợp OpenAI để nhận diện ngày tháng từ văn bản hoặc tin nhắn thoại, tự động tra cứu tỷ giá TRM chính xác."
slug: "tra-cuu-ty-gia-peso-colombia-usd-telegram-bot-ai"
tags: [n8n, automation, telegram, openai, ai-agent, finance]
keywords: [n8n workflow, telegram bot tra cuu ty gia, ai nhan dien ngay thang, openai whisper n8n, ty gia peso usd]
---

# 🚀 Tra cứu tỷ giá Peso Colombia sang USD tự động qua Telegram Bot kết hợp AI

Các sếp có bao giờ gặp khó khăn khi phải liên tục tra cứu thủ công tỷ giá quy đổi tiền tệ từ các nguồn dữ liệu chính phủ, hoặc mất thời gian xử lý các yêu cầu tra cứu lịch sử tỷ giá từ khách hàng/đội ngũ nội bộ chưa? Việc tra cứu thủ công vừa tốn thời gian, vừa dễ sai sót, lại thiếu tính linh hoạt khi người dùng gửi tin nhắn bằng văn bản tự nhiên hoặc tin nhắn thoại.

Giải pháp hoàn hảo cho bài toán này chính là **Workflow n8n tích hợp Telegram Bot và Trí tuệ nhân tạo (OpenAI)** do tác giả Juan Sanchez thiết kế. Workflow này cho phép người dùng gửi tin nhắn (dạng chữ hoặc giọng nói) chứa mốc thời gian bất kỳ lên Telegram, AI sẽ tự động phân tích và bóc tách ngày tháng, sau đó truy vấn hệ thống dữ liệu mở (datos.gov.co) để trả về tỷ giá TRM (Representative Market Rate) chính xác nhất, kể cả vào các ngày cuối tuần hay ngày lễ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn 24/7:** Người dùng chỉ cần chat với Telegram Bot bất cứ lúc nào để lấy tỷ giá Peso Colombia (COP) sang USD (TRM).
- **AI thông minh hiểu ngữ nghĩa:** Tích hợp OpenAI Agent để nhận diện ngày tháng từ văn bản tự nhiên hoặc chuyển đổi giọng nói (Audio) thành văn bản qua OpenAI Whisper.
- **Xử lý thông minh ngày nghỉ/lễ:** Tự động quét lùi lại 10 ngày trước đó để tìm ra mức TRM có hiệu lực gần nhất (vì tỷ giá thường giữ nguyên vào cuối tuần/ngày lễ).
- **Trải nghiệm mượt mà:** Phản hồi tức thì, chính xác và có cơ chế cảnh báo khi người dùng nhập sai định dạng hoặc chọn ngày trong tương lai.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản Cloud hoặc Self-hosted).
- **Telegram Bot Token:** Tạo một bot mới thông qua `@BotFather` trên Telegram để lấy API Token.
- **OpenAI API Key:** Cần thiết cho các node AI Agent, Chat Model và Transcribe Audio.
- **Nguồn dữ liệu:** Hệ thống tự động gọi API mở từ `datos.gov.co` (không cần API Key riêng cho nguồn này).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ trang chủ n8n (ID: 4246) hoặc tải file JSON về máy, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các thành phần sau:
- **Node `Once a Telegram Message is received` & các node Telegram khác:** Cấu hình **Credentials** bằng Telegram Bot Token đã tạo từ `@BotFather`.
- **Node `OpenAI Chat Model` & `Transcribe Audio`:** Cấu hình **Credentials** bằng OpenAI API Key. Tại node Chat Model, chọn model phù hợp (ví dụ: `gpt-4.1-nano` hoặc `gpt-4o-mini`).
- **Node `Extractor Agent` & `Structured Output Parser`:** Đảm bảo cấu hình đúng schema đầu ra để AI trả về định dạng ngày chuẩn `YYYY-MM-DD`.
- **Logic Vòng lặp (Loop):** Workflow sử dụng các node `Generate an array with 10 numbers`, `Split Items for the loop` và `Get the last 10 responses` nhằm giải quyết bài toán ngày lễ/cuối tuần (khi không có tỷ giá mới, hệ thống sẽ tự động quét lùi 10 ngày để lấy giá trị gần nhất).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và thử gửi một tin nhắn đến Telegram Bot (ví dụ: *"Cho tôi xin tỷ giá ngày hôm qua"* hoặc gửi một tin nhắn thoại).
- Kiểm tra các luồng dữ liệu chạy qua các node `Validate Text or Audio`, `Extractor Agent`, và `Get TRM`.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để bot chính thức hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử tra cứu:** Kết nối thêm node Google Sheets hoặc Airtable ngay trước bước gửi phản hồi để lưu lại lịch sử câu hỏi của người dùng và kết quả trả về, tiện cho việc phân tích nhu cầu.
- **Đa ngôn ngữ:** Tỉnh chỉnh System Prompt trong AI Agent để bot có thể hiểu và phản hồi bằng cả tiếng Tây Ban Nha, tiếng Anh hoặc tiếng Việt tùy theo đối tượng sử dụng.
- **Mở rộng kênh chat:** Dễ dàng thay thế hoặc bổ sung node kích hoạt từ WhatsApp, Messenger hoặc Slack bằng cách cấu hình lại Trigger tương ứng.

### 📌 Kết luận
Workflow này là một minh họa tuyệt vời cho việc kết hợp sức mạnh của No-code (n8n), Chatbot (Telegram) và Trí tuệ nhân tạo (OpenAI). Giờ đây, việc tra cứu tỷ giá tài chính đã trở nên đơn giản hơn bao giờ hết chỉ bằng vài câu lệnh tự nhiên. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa quy trình làm việc nhé!