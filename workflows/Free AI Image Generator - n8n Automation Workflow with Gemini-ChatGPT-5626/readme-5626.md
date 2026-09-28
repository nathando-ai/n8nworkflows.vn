---
title: "🚀 Tạo ảnh AI tự động miễn phí qua Telegram và Chat với n8n Workflow"
description: "Hướng dẫn xây dựng hệ thống tự động tạo ảnh bằng AI siêu tốc sử dụng Google Gemini, Telegram Bot và n8n hoàn toàn miễn phí, không cần code."
slug: "tao-anh-ai-tu-dong-mien-phi-qua-telegram-n8n"
tags: [n8n, automation, no-code, ai-image-generator, google-gemini, telegram]
keywords: [n8n workflow, tạo ảnh ai tự động, google gemini image generation, telegram bot ai, tự động hóa n8n]
---

# 🚀 Tạo ảnh AI tự động miễn phí qua Telegram và Chat với n8n Workflow

Các sếp có đang tốn hàng giờ để viết prompt, tạo ảnh thủ công trên các công cụ trả phí rồi tải về đăng mạng xã hội? Quy trình đó vừa mất thời gian, vừa ngắt quãng mạch sáng tạo của anh em làm nội dung. 

Đừng lo! Bài viết này sẽ hướng dẫn các sếp triển khai ngay một **Workflow n8n tự động hóa 100%**, giúp biến mọi ý tưởng văn bản thành những bức ảnh tuyệt đẹp chỉ bằng một câu lệnh chat qua Telegram hoặc n8n Chat Interface. Giải pháp này kết hợp sức mạnh của **Google Gemini** và **AI Agent** để tạo ảnh tự động mà không tốn một đồng chi phí vận hành phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo ảnh tự động theo yêu cầu:** Chỉ cần nhắn tin qua Telegram hoặc khung chat, AI sẽ tự động hiểu và vẽ ảnh.
- **Tùy biến linh hoạt kích thước & mô hình:** Dễ dàng thay đổi kích thước ảnh (mặc định 1080x1920 cho TikTok/Reels) và đổi model AI (Flux, Kontext, Turbo...).
- **Đa kênh trả kết quả:** Ảnh tạo ra có thể gửi trực tiếp về chat Telegram hoặc lưu tự động vào ổ cứng (Disk) máy chủ.
- **Tiết kiệm chi phí tối đa:** Vận hành trên nền tảng self-hosted n8n kết hợp các mô hình AI mạnh mẽ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Self-hosted hoặc Cloud).
- **Google Gemini API Key:** Tài khoản Google AI Studio có quyền truy cập mô hình tạo ảnh/chat.
- **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram (nếu muốn nhận ảnh qua Telegram).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ Agent Circle hoặc copy mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp JSON vào màn hình làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 11 nodes thông minh, các sếp cần chú ý cấu hình các điểm sau:
- **Fields - Set Values**: Nơi quy định kích thước ảnh (`1080 x 1920` pixels) và loại model (`flux`, `kontext`, `turbo`, `gptimage`). Hãy sửa lại thông số này nếu muốn đổi kích thước hoặc phong cách ảnh.
- **Google Gemini Chat Model**: Kết nối với credential tài khoản Google của sếp (Google Palm/Gemini API key).
- **Telegram Trigger** & **Telegram Response**: Cấu hình Telegram Bot Token để bot có thể lắng nghe tin nhắn và gửi ảnh trả về.
- **AI Agent - Create Image From Prompt**: Nơi điều phối prompt từ người dùng gửi tới mô hình AI. Các sếp có thể thay đổi model chat tại đây nếu muốn chuyển sang OpenAI ChatGPT hoặc Microsoft Copilot.
- **Save Image To Disk**: (Tùy chọn) Cấu hình đường dẫn thư mục lưu file trên ổ cứng nếu muốn lưu bản sao cục bộ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một tin nhắn mẫu (ví dụ: *"A futuristic cyberpunk city at night"*).
- Kiểm tra kết quả trả về qua khung chat hoặc Telegram.
- Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** góc trên cùng bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Drive / Cloud Storage:** Thay vì chỉ lưu local trên Disk, các sếp có thể nối thêm node Google Drive để tự động lưu trữ và phân loại toàn bộ ảnh AI tạo ra.
- **Thông báo qua Slack / Discord:** Thêm node gửi thông báo về kênh nhóm khi có một bức ảnh mới được tạo thành công.
- **Tự động đăng mạng xã hội:** Kết hợp thêm các node Facebook, Twitter/X hoặc Instagram để tự động hóa toàn bộ quy trình "Tạo ảnh -> Đăng bài".

### 📌 Kết luận
Workflow tạo ảnh AI tự động này là trợ thủ đắc lực cho các nhà sáng tạo nội dung, marketer hay bất kỳ ai muốn ứng dụng AI vào công việc hằng ngày mà không cần biết lập trình. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa hiệu suất làm việc ngay hôm nay!