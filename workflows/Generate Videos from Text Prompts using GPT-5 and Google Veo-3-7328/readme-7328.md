---
title: "🚀 Tự động tạo video điện ảnh từ văn bản bằng GPT-5 và Google Veo-3 trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình sáng tạo video: biến một từ khóa đơn giản thành video chất lượng điện ảnh bằng AI/ML API, GPT-5 và Google Veo-3."
slug: "tao-video-tu-van-ban-gpt-5-google-veo-3-n8n"
tags: [n8n, automation, ai, video-generation, gpt-5, google-veo-3]
keywords: [n8n workflow, tạo video tự động, ai video generator, gpt-5, google veo-3, aimlapi]
---

# 🚀 Tự động tạo video điện ảnh từ văn bản bằng GPT-5 và Google Veo-3

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ viết prompt chi tiết, chọn góc máy, ánh sáng, màu sắc rồi lại phải chờ đợi, kiểm tra trạng thái render video thủ công từng cái một? Việc sản xuất nội dung video ngắn, cinematic cho marketing hay social media tốn rất nhiều thời gian nếu làm theo cách truyền thống.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: Các sếp chỉ cần nhập một từ khóa ngắn gọn (ví dụ: *"hoàng hôn trên biển"*, *"cyberpunk"*), hệ thống sẽ dùng **GPT-5** để "phù phép" thành một prompt điện ảnh chuyên nghiệp, sau đó gọi **Google Veo-3** để khởi tạo video, tự động lặp (polling) kiểm tra trạng thái và trả về link tải video hoàn thiện ngay trong khung chat!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu thời gian:** Biến ý tưởng 1 chữ thành prompt video điện ảnh chi tiết chỉ trong vài giây.
- **Tự động hóa hoàn toàn:** Tự động gọi API khởi tạo, tự động chờ (poll status) và lấy file video về mà không cần thao tác thủ công.
- **Chất lượng đỉnh cao:** Kết hợp sức mạnh của GPT-5 trong việc mở rộng ngôn ngữ và Google Veo-3 trong việc tạo hình ảnh/video chuyển động mượt mà.
- **Hoạt động linh hoạt:** Tích hợp sẵn qua giao diện Chat Trigger, dễ dàng mở rộng lưu về Google Drive hoặc đăng lên YouTube.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **AI/ML API Account:** Tài khoản từ [AIMLAPI](https://aimlapi.com/app/keys) để lấy API Key sử dụng cho cả GPT-5 và Google Veo-3.
- **Credentials:** Tạo 1 credential kiểu `aimlApi` trong n8n với Bearer Token từ tài khoản trên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nền tảng n8n và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 10 nodes chính xử lý từ bước nhận input đến khi hoàn thành video. Các sếp cần chú ý cấu hình các điểm sau:

- **When chat message received (`chatTrigger`):** Điểm khởi đầu nhận câu lệnh/ý tưởng (`chatInput`) và URL ảnh gốc (`image_url` bắt buộc cho tính năng image-to-video).
- **Cinematic Prompt (GPT‑5) (`n8n-nodes-aimlapi.aimlApi`):**
  - Model: Chọn `openai/gpt-5-mini-2025-08-07`.
  - Cần gán **AI/ML API Credentials** đã chuẩn bị.
  - Prompt hệ thống đã được cấu hình sẵn để biến ý tưởng thô thành mô tả chi tiết về góc máy, ánh sáng, nhịp điệu và màu sắc.
- **Create Video with AI/ML API1 (`httpRequest`):**
  - Node gửi request khởi tạo video tới Google Veo-3 thông qua AIMLAPI.
  - Yêu cầu cấu hình đúng credentials `aimlApi`.
- **Wait 30 sec.1 (`wait`):** Khoảng thời gian chờ giữa các lần gọi kiểm tra trạng thái render video (có thể điều chỉnh tùy thuộc vào thời gian xử lý thực tế).
- **Get status1 & Completed? / Error? (`httpRequest` & `if`):** Hệ thống sẽ liên tục polling trạng thái video. Nếu hoàn thành (`completed`), luồng sẽ chuyển sang node **Get Video File** để tải video; nếu lỗi sẽ chuyển sang **Stop and Error**.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng một từ khóa ngắn gọn qua Chat Trigger để kiểm tra quá trình tạo prompt và render video.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình làm content video, các sếp có thể mở rộng workflow với các bước sau:
1. **Lưu trữ tự động:** Thêm node HTTP hoặc Google Drive để tự động tải file từ `video_url` và lưu vào thư mục lưu trữ riêng.
2. **Tạo tiêu đề SEO:** Dùng một node GPT-5 phụ để tự động tạo tiêu đề ngắn gọn (dưới 60 ký tự) mô tả nội dung video.
3. **Log dữ liệu:** Lưu thông tin `prompt`, `generation_id`, `video_url`, `title` vào Google Sheets hoặc Database để dễ dàng quản lý kho tư liệu.
4. **Tự động đăng tải:** Kết nối trực tiếp với API của YouTube Shorts hoặc TikTok để tự động xuất bản video sau khi render xong.

### 📌 Kết luận
Việc tự động hóa sản xuất video chưa bao giờ dễ dàng đến thế khi kết hợp n8n, GPT-5 và Google Veo-3. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất sáng tạo nội dung của các sếp!