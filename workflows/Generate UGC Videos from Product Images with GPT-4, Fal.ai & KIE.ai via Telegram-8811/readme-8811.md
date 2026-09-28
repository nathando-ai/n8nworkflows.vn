---
title: "🚀 Tự động tạo video UGC triệu view từ hình ảnh sản phẩm với GPT-4, Fal.ai & KIE.ai qua Telegram"
description: "Hướng dẫn cấu hình workflow n8n tự động hóa toàn bộ quy trình sáng tạo nội dung UGC: nhận ảnh từ Telegram, phân tích bằng GPT-4, tạo ảnh và dựng video AI chuyên nghiệp."
slug: "tao-video-ugc-tu-anh-san-pham-n8n-gpt4-fal-kie-telegram"
tags: [n8n, automation, no-code, ai-video, telegram, openai]
keywords: [n8n workflow, tạo video ugc tự động, gpt-4 vision, fal.ai, kie.ai, telegram bot automation]
---

# 🚀 Tự động tạo video UGC triệu view từ hình ảnh sản phẩm với GPT-4, Fal.ai & KIE.ai qua Telegram

Các sếp có đang đau đầu vì việc sản xuất nội dung video UGC (User Generated Content) để chạy quảng cáo hay làm marketing tốn quá nhiều thời gian, nhân sự và chi phí? Việc thuê diễn giả, setup góc quay, dựng hình đôi khi ngốn hàng tuần liền. 

Giải pháp ở đây là gì? Hãy để AI làm thay các sếp! Workflow n8n siêu việt này sẽ biến một bức ảnh sản phẩm đơn thuần thành một chuỗi video UGC sống động chỉ bằng vài thao tác nhắn tin qua Telegram. Toàn bộ quy trình từ phân tích hình ảnh, viết kịch bản, tạo ảnh ghép nối đến dựng video hoàn chỉnh đều diễn ra tự động 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ AI nặng mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Chỉ cần gửi ảnh và mô tả qua Telegram, hệ thống sẽ tự động nhào nặn ra video hoàn chỉnh.
- **Tiết kiệm chi phí tối đa**: Không cần tốn ngân sách thuê studio hay thuê mẫu quay dựng phức tạp.
- **Đa dạng hóa nội dung (Multimodal AI)**: Kết hợp sức mạnh của GPT-4 Vision, Fal.ai và KIE.ai để tạo ra các góc quay, kịch bản UGC độc quyền, thu hút người xem.
- **Vận hành 24/7**: Bot Telegram luôn sẵn sàng nhận yêu cầu bất cứ lúc nào các sếp cần lên chiến dịch nội dung.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Telegram Bot Token**: Tạo qua `@BotFather` để nhận/gửi tin nhắn và media.
- **OpenAI API Key**: Dành cho GPT-4 Vision phân tích hình ảnh và Agent tạo kịch bản.
- **Fal.ai API Key**: Dùng để xử lý tạo hình ảnh và kết hợp video.
- **KIE.ai API Key**: Dùng để gọi các mô hình sinh video thế hệ mới.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy toàn bộ mã JSON của workflow từ nguồn cung cấp, sau đó paste trực tiếp vào giao diện n8n Editor của mình (Create new workflow -> Import from JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Hệ thống gồm 22 nodes được chia thành các cụm chức năng rõ ràng. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:
- **Telegram Trigger & Send a video / Send a photo message**: Chọn đúng Credentials của Telegram Bot đã tạo. Node Trigger sẽ lắng nghe tin nhắn kèm ảnh gửi đến bot của các sếp.
- **Analyze image & OpenAI Chat Model**: Điền OpenAI API Key và kiểm tra model `gpt-4.1-mini` (hoặc phiên bản GPT-4 Vision phù hợp) để hệ thống nhận diện sản phẩm chính xác.
- **Create Image 1, Get the Image, Combine Video, Get the final Video**: Cấu hình các HTTP Request nodes đi kèm `httpHeaderAuth` để kết nối mượt mà với Fal.ai API.
- **Make video 1 & Get Record Info**: Thiết lập kết nối API tới KIE.ai để bắt đầu tiến trình dựng video từ các prompt đã được cấu hình sẵn.

#### 3. Kích hoạt ⚡️
- Gửi thử một bức ảnh sản phẩm kèm caption yêu cầu qua Telegram Bot để chạy Test run.
- Kiểm tra kết quả trả về trên Telegram. Nếu video đã được gửi về thành công, các sếp hãy bấm nút **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu khách hàng/yêu cầu**: Tích hợp thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các sản phẩm đã tạo video, phục vụ cho việc thống kê và quản lý nội dung.
- **Nhận thông báo qua Slack/Telegram Admin**: Thêm một nhánh gửi thông báo về group nội bộ của team mỗi khi có một video UGC hoàn tất.
- **Tùy biến Prompt**: Tinh chỉnh prompt trong các AI Agent (`Image Prompt` và `Video Prompt`) để kịch bản sát với thị hiếu tệp khách hàng mục tiêu của doanh nghiệp hơn.

### 📌 Kết luận
Workflow tạo video UGC tự động này là một cỗ máy marketing thực thụ, giúp các sếp tối ưu hóa thời gian và nguồn lực trong kỷ nguyên AI. Hãy triển khai ngay hôm nay để bứt phá doanh thu và lượng tương tác trên các nền tảng mạng xã hội!