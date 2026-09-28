---
title: "🚀 Tự động tạo Video và Hình ảnh bằng AI từ Telegram Chat với Nano Banana & Veo-3"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc nhận tin nhắn văn bản hoặc giọng nói trên Telegram, xử lý bằng AI Agent và tạo ra hình ảnh, video chất lượng cao gửi ngược lại cho người dùng."
slug: "tao-video-ai-tu-telegram-voi-nano-banana-va-veo-3"
tags: [n8n, automation, telegram, ai-agent, openai, video-generation]
keywords: [n8n workflow, tạo video ai telegram, nano banana veo 3, openai whisper gpt4, tự động hóa n8n]
---

# 🚀 Tự động tạo Video và Hình ảnh bằng AI từ Telegram Chat với Nano Banana & Veo-3

Các sếp có bao giờ cảm thấy việc sản xuất nội dung hình ảnh và video theo yêu cầu (on-demand) tốn quá nhiều thời gian chuyển đổi giữa các nền tảng? Thay vì phải gõ prompt lên web, rồi tải về, rồi chỉnh sửa, workflow n8n này sẽ biến tài khoản **Telegram** của các sếp thành một "Studio sản xuất media AI" tự động 100%. 

Chỉ cần gửi một tin nhắn văn bản hoặc một đoạn ghi âm (audio) mô tả ý tưởng, AI sẽ tự động phân tích, tạo hình ảnh gốc bằng Nano Banana, sau đó dựng thành video động tuyệt đẹp qua Veo-3 và trả kết quả trực tiếp về Telegram cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác đa phương thức (Multimodal):** Hỗ trợ cả tin nhắn văn bản lẫn tin nhắn thoại (Voice note) trên Telegram.
- **Sản xuất media tự động:** Kết hợp AI thông minh để tinh chỉnh prompt, tạo ảnh chất lượng cao và chuyển đổi thành video mượt mà.
- **Tiết kiệm 90% thời gian:** Không cần thao tác thủ công trên các trang web tạo ảnh/video riêng lẻ, mọi thứ diễn ra ngay trong khung chat Telegram quen thuộc.
- **Hoạt động 24/7:** Bot luôn sẵn sàng nhận lệnh bất cứ lúc nào, bất cứ nơi đâu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram để làm cổng giao tiếp.
2. **OpenAI API Key:** Dùng cho model GPT-4o-mini (AI Agent xử lý logic, tạo prompt) và dịch vụ Whisper (transcribe audio).
3. **API Access:** Tài khoản dịch vụ tạo ảnh (Nano Banana) và tạo video (Veo-3) tương thích với các HTTP Request trong workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n (hoặc tải file JSON từ nguồn cung cấp), sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **Telegram Trigger:** Kết nối với Credentials Telegram Bot của các sếp để lắng nghe tin nhắn đến.
- **Download Audio1 & Transcribe a recording:** Nếu các sếp gửi tin nhắn thoại, node này sẽ tải file về và gọi OpenAI Whisper để chuyển đổi giọng nói thành văn bản chính xác.
- **AI Agent & OpenAI Chat Model (GPT-4o-mini):** Đóng vai trò bộ não phân tích ý định người dùng, kết hợp với *Structured Output Parser* để xuất ra prompt chuẩn cho việc tạo ảnh và video.
- **Image Gen (Nano Banana) & Generate Video (Veo-3):** Cấu hình đúng Endpoint API, Header và Body theo tài liệu API của nhà cung cấp dịch vụ tạo ảnh/video mà các sếp đang sử dụng.
- **Telegram: Send Photo & Telegram: Send Video:** Đảm bảo trường Chat ID được trỏ đúng đến người dùng vừa gửi tin nhắn (`{{ $json.message.chat.id }}`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tin nhắn hoặc voice note bất kỳ vào bot Telegram của các sếp để test luồng chạy.
- Kiểm tra xem ảnh và video có được trả về khung chat Telegram thành công hay không.
- Nếu mọi thứ ổn định, bật công tắc **Active** góc trên bên phải để bot hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước lưu trữ:** Gắn thêm node Google Drive hoặc Supabase để lưu lại toàn bộ ảnh và video AI đã tạo làm tư liệu lưu trữ.
- **Bổ sung kiểm duyệt:** Thêm điều kiện `If` để lọc từ khóa nhạy cảm trước khi gọi API tạo ảnh/video, tránh lãng phí token/credit.
- **Tích hợp thông báo lỗi:** Kết nối thêm nhánh lỗi (Error Trigger) gửi cảnh báo về Telegram cá nhân của các sếp nếu API tạo video gặp sự cố.

### 📌 Kết luận
Với workflow tự động hóa này, việc tạo ra các content trực quan bằng AI chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay hôm nay để biến chiếc bot Telegram thành trợ lý sản xuất media siêu tốc cho các sếp!