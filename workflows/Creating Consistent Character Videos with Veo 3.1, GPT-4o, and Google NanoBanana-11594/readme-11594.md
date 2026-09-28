---
title: "🚀 Tạo Video Nhân Vật Đồng Nhất Tự Động 100% với Veo 3.1, GPT-4o và Google NanoBanana trong n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động hóa hoàn toàn quy trình tạo video nhân vật đồng nhất qua AI, từ tạo kịch bản, khung hình đến đăng TikTok/Instagram."
slug: "tao-video-nhan-vat-dong-nhat-voi-veo-3-1-gpt-4o-n8n"
tags: [n8n, automation, ai-video, veovideo, openai, telegram, social-media]
keywords: [n8n workflow, tao video ai, veo 3.1 n8n, openai gpt-4o, google nanobanana, tu dong hoa video]
---

# 🚀 Tự Động Hóa Tạo Video Nhân Vật Đồng Nhất Với Veo 3.1, GPT-4o & Google NanoBanana

Các sếp đang làm nội dung số, TikTok hay Instagram chắc chắn hiểu cảm giác "vắt óc" nghĩ kịch bản, loay hoay giữ nét mặt nhân vật xuyên suốt các phân cảnh, rồi tốn hàng giờ đồng hồ render video thủ công. Việc này vừa tẻ nhạt, vừa tốn kém thời gian nhân sự mà hiệu suất lại không cao.

Giải pháp ở đây là gì? Hãy để **n8n** gánh hết! Workflow đỉnh cao này sẽ tự động hóa toàn bộ từ A-Z: Lên kịch bản thông minh bằng **GPT-4o**, tạo khung hình đầu/cuối đồng nhất bằng **Google NanoBanana**, render video điện ảnh bằng **Veo 3.1**, gửi thông báo qua **Telegram**, và tự động đăng tải lên **TikTok** cùng **Instagram** thông qua **Blotato**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập giữa chừng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nhân vật đồng nhất 100%:** Giữ nguyên khuôn mặt, trang phục và bối cảnh qua các khung hình nhờ công nghệ AI tiên tiến.
- **Tự động hóa toàn diện:** Từ khâu sinh ý tưởng ngẫu nhiên (100 địa điểm, 15 tư thế) đến render video chất lượng điện ảnh.
- **Đa nền tảng mạng xã hội:** Tự động tối ưu tiêu đề, mô tả, hashtag và đăng trực tiếp lên TikTok, Instagram kèm thông báo kiểm duyệt qua Telegram.
- **Tiết kiệm 95% thời gian:** Không cần can thiệp thủ công, vận hành liên tục theo lịch trình (Schedule Trigger).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để hệ thống mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
1. **OpenAI API Key:** Cho các node `OpenAI Chat Model` (GPT-4o) viết kịch bản và tạo metadata.
2. **KIE.AI API Key:** Dùng để gọi mô hình Google NanoBanana Edit (tạo ảnh) và Veo 3.1 (tạo video).
3. **Blotato API:** Kết nối tài khoản mạng xã hội (TikTok, Instagram) để tự động đăng bài.
4. **Telegram Bot Token:** Nhận ảnh preview khung hình và video trực tiếp về Telegram cá nhân/nhóm.
5. **5 Ảnh tham chiếu (Reference Images):** Chuẩn bị sẵn link của 5 bức ảnh khuôn mặt nhân vật để đưa vào node `Create Start Frame`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn cấp.
- Mở giao diện n8n của các sếp, chọn **Workflows** -> **Import from File** (hoặc paste trực tiếp mã JSON vào).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **OpenAI Chat Model / OpenAI Chat Model1:** Chọn credentials `openAiApi` và trỏ đúng model `gpt-4.1-mini` (hoặc GPT-4o tùy cấu hình).
- **Veo 3.1, Get Start Frame, Create End Frame,... (Các HTTP Request nodes):** Thay thế `YOUR_KIE_AI_API_KEY` bằng API Key thực tế của các sếp hoặc cấu hình `HTTP Bearer Auth`.
- **Create Start Frame:** Cập nhật 5 URL ảnh tham chiếu nhân vật của các sếp vào phần prompt/body của node này để đảm bảo AI nhận diện đúng nhân vật.
- **Telegram (Send Start Frame, Send End Frame, Send Video):** Nhúng Telegram Bot Token vào credentials và điền chính xác Chat ID của các sếp để nhận ảnh/video test.
- **Instagram & Tiktok1:** Kết nối tài khoản Blotato thông qua `blotatoApi` credentials để hệ thống có quyền đăng bài tự động.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thủ công lần đầu để test luồng từ `Schedule Trigger` qua các bước tạo ảnh và video.
- Kiểm tra xem Telegram đã nhận được ảnh khung hình và video chưa.
- Khi mọi thứ mượt mà, gạt công tắc **Active** góc trên cùng bên phải để workflow tự động chạy ngầm theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước lưu trữ:** Kết nối thêm node Google Drive hoặc Google Sheets để lưu lại lịch sử kịch bản, prompt và link video đã render nhằm phục vụ việc tracking.
- **Tích hợp Slack/Discord:** Thay thế hoặc bổ sung thông báo qua kênh chat nội dung của công ty thay vì chỉ dùng Telegram cá nhân.
- **Kiểm duyệt thủ công (Human-in-the-loop):** Chèn thêm node `Wait` kèm Webhook xác nhận trước khi đẩy video lên TikTok/Instagram để tránh những lỗi hiển thị đáng tiếc.

### 📌 Kết luận
Workflow tự động hóa kết hợp giữa Veo 3.1, GPT-4o và Google NanoBanana là "vũ khí tối tân" giúp các sếp sản xuất nội dung video hàng loạt mà không tốn nhiều nhân lực. Hãy triển khai ngay lên VPS của mình và tận hưởng sức mạnh của AI tự động hóa!