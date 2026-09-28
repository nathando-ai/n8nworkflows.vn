---
title: "🚀 Tự động hóa sản xuất video ngắn AI từ kịch bản với DeepSeek, TTS và Together.ai"
description: "Hướng dẫn xây dựng workflow n8n toàn diện giúp tự động biến ý tưởng thô thành video hoàn chỉnh kèm giọng đọc AI, hình ảnh, phụ đề và nhạc nền."
slug: "tu-dong-hoa-san-xuat-video-ai-deepseek-tts-together-ai"
tags: [n8n, automation, ai-video, deepseek, together-ai, content-creation]
keywords: [n8n workflow, tạo video tự động, deepseek n8n, ai video generation, tts automation]
keywords: [n8n workflow, tự động hóa, tạo video tự động, deepseek, ai video generation]
---

# 🚀 Tự động hóa sản xuất video ngắn AI từ kịch bản với DeepSeek, TTS và Together.ai

Các sếp có đang cảm thấy mệt mỏi khi phải tốn hàng giờ liền để viết kịch bản, tìm kiếm hình ảnh, lồng tiếng, dựng phim và thêm phụ đề cho các video ngắn (Reels, TikTok, Shorts)? Việc làm thủ công này không chỉ ngốn thời gian mà còn cực kỳ khó để duy trì tần suất đăng bài đều đặn.

Đừng lo, workflow n8n "khủng" với 71 nodes này sẽ gánh thay các sếp toàn bộ quy trình từ A-Z! Chỉ cần nhập ý tưởng hoặc kịch bản thô vào một form đơn giản, hệ thống sẽ sử dụng sức mạnh của **DeepSeek** (qua OpenRouter) để viết kịch bản, **Together.ai** để sinh ảnh (Flux/Schnell), kết hợp tạo giọng đọc TTS, lồng nhạc nền, ghép video, chèn phụ đề tự động và trả thẳng kết quả về Telegram hoặc Google Drive. Hoàn toàn tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến một ý tưởng đơn thuần thành video hoàn chỉnh sẵn sàng đăng TikTok/Reels mà không cần đụng tay vào editor.
- **Tiết kiệm thời gian & chi phí:** Thay vì mất nửa ngày dựng 1 video, hệ thống tự động xử lý hàng loạt nhờ cơ chế batching và lưu vết trên Google Sheets.
- **AI thông minh:** Sử dụng DeepSeek viết kịch bản tối ưu, kết hợp Together.ai sinh hình ảnh chất lượng cao và tích hợp sẵn công cụ tạo phụ đề, lồng tiếng, nhạc nền.
- **Quản lý chuyên nghiệp:** Mọi dữ liệu, file, trạng thái render đều được đồng bộ tự động lên Google Drive và Google Sheets để dễ dàng theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (khuyến nghị Self-hosted trên VPS để tránh timeout vì số lượng nodes lớn).
- **OpenRouter API Key** (dùng cho model DeepSeek Chat v3).
- **Together.ai API Key** (dùng cho việc tạo hình ảnh bằng Flux/Schnell).
- Tài khoản **Google Drive** & **Google Sheets** (để lưu trữ tài nguyên và quản lý trạng thái).
- **Telegram Bot Token** (để nhận thông báo và file video hoàn thiện trực tiếp qua chat).
- Các API/Credential liên quan đến dịch vụ Text-to-Speech (TTS), Subtitle/Caption và ghép nhạc nền (được cấu hình qua các HTTP Request nodes).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste Workflow**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Do workflow có tới 71 nodes và được chia thành nhiều module chức năng (Từ *Create script*, *Generate scenes*, *Image Generation*, đến *Create clips*, *Add Captions*, *Add BG Music*), các sếp cần lưu ý cấu hình kỹ các điểm sau:
- **Node `On form submission` (Form Trigger):** Cấu hình form nhận ý tưởng đầu vào từ người dùng.
- **Node `Open Router - Deepseek v3.1` & `Open Router - Deepseek v3.`:** Kết nối tài khoản OpenRouter bằng **openRouterApi** credentials, chọn model DeepSeek v3.
- **Các node Google Sheets (`Google Sheets`, `Google Sheets1`, ...):** Liên kết tài khoản **googleSheetsOAuth2Api**, trỏ tới một file Google Sheets chuẩn bị sẵn để lưu log, kịch bản, và prompt hình ảnh.
- **Các node Google Drive (`Google Drive`, `Google Drive1`, ...):** Kết nối **googleDriveOAuth2Api** để lưu trữ hình ảnh, audio và các video clip cắt nhỏ trước khi ghép.
- **Node `HTTP - Together.ai`:** Cấu hình **httpHeaderAuth** để gọi API sinh ảnh (lưu ý Together.ai bản miễn phí có rate limits, workflow đã được thiết kế cơ chế batching chậm lại để phù hợp).
- **Node `Telegram`, `Telegram1`, `Telegram2`:** Cấu hình **telegramApi** với Bot Token của các sếp để nhận video hoàn chỉnh gửi về tài khoản cá nhân hoặc nhóm.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) bằng cách submit một form mẫu để kiểm tra từng module (Kịch bản -> Prompt ảnh -> Sinh ảnh -> TTS -> Ghép video).
- Sau khi kiểm tra toàn bộ dữ liệu chạy trơn tru từ Google Sheets sang Google Drive và trả về Telegram, các sếp gạt công tắc sang **Active** để vận hành tự động.

### ✍️ Gợi ý & Mẹo nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi về Telegram, các sếp có thể nối thêm node Slack hoặc Discord để team cùng theo dõi tiến độ sản xuất video.
- **Tối ưu tốc độ:** Vì Together.ai bản miễn phí có giới hạn tốc độ (Rate Limit), các sếp có thể cân nhắc nâng cấp tài khoản Together.ai hoặc phân bổ thời gian chạy (chia nhỏ batch) để tránh lỗi timeout trên n8n.
- **Lưu trữ dài hạn:** Thiết lập tự động xóa file tạm trên Google Drive sau 7 ngày để tiết kiệm dung lượng lưu trữ cloud.

### 📌 Kết luận
Workflow "Generate AI Videos from Scripts with DeepSeek, TTS, and Together.ai" là một cỗ máy tự động hóa cực kỳ mạnh mẽ, giúp các nhà sáng tạo nội dung giải phóng sức lao động hoàn toàn khỏi các tác vụ thủ công. Hãy triển khai ngay trên VPS của các sếp để bắt đầu sản xuất hàng loạt video chất lượng cao mỗi ngày!