---
title: "🚀 Tự động tạo video ngắn từ YouTube bằng Reka Vision AI và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn việc trích xuất, phân tích và cắt dựng video ngắn từ kênh YouTube sử dụng Reka Vision AI."
slug: "tu-dong-tao-video-ngan-tu-youtube-reka-vision-n8n"
tags: [n8n, automation, reka-ai, video-creation, youtube, ai-agent]
keywords: [n8n workflow, tạo video tự động, reka vision, youtube automation, ai video clips]
---

# 🚀 Tự động tạo video ngắn từ YouTube bằng Reka Vision AI

Các sếp làm sáng tạo nội dung (Content Creator) chắc hẳn đều hiểu cảm giác "ngợp" thế nào khi phải xem từng video dài trên YouTube, thủ công chọn khoảnh khắc hay, cắt dựng lại thành các đoạn ngắn (Shorts/Reels) để đăng mạng xã hội. Quá trình này ngốn hàng tá thời gian!

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình đó. Ngay khi kênh YouTube yêu thích của các sếp có video mới, hệ thống sẽ tự động dùng sức mạnh của **Reka Vision AI** để phân tích, cắt dựng video ngắn theo đúng ý muốn và gửi thông báo qua Gmail khi hoàn tất. Không cần tốn một phút cắt thủ công nào nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động bắt trend:** Theo dõi sát sao các video mới từ bất kỳ kênh YouTube nào thông qua RSS Feed.
- **Biên tập bằng AI thông minh:** Reka Vision tự động xử lý, chọn góc máy, phân tích nội dung và tạo video ngắn tối ưu cho TikTok/Reels/Shorts.
- **Quy trình khép kín:** Vòng lặp kiểm tra trạng thái thông minh kèm cơ chế an toàn chống lặp vô hạn (infinite loop).
- **Nhận kết quả tận tay:** Gửi email thông báo chứa link video sẵn sàng đăng tải ngay khi hoàn thành.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Reka AI API Key** (Miễn phí! Các sếp lấy tại [đây](https://link.reka.ai/free)).
- **Tài khoản Gmail** (hoặc cấu hình lại sang dịch vụ email khác nếu muốn).
- **Link RSS Feed** của kênh YouTube muốn theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ template gốc (ID: 12829).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node cốt lõi cần cấu hình lại cho đúng nhu cầu thực tế:

- **When New Video (`rssFeedReadTrigger`)**: 
  - Thay đổi đường dẫn Feed URL thành kênh YouTube các sếp muốn theo dõi. 
  - *Ví dụ:* `https://www.youtube.com/feeds/videos.xml?channel_id=UCAr20GBQayL-nFPWFnUHNAA`
- **Create a clip (`@reka-ai/n8n-nodes-reka.rekaVision`)**: 
  - Thêm Reka API Credential của các sếp.
  - Tùy chỉnh prompt, chọn template, bật/tắt phụ đề (captions), độ dài tối thiểu/tối đa của clip theo sở thích.
- **Check clip job status & Loop To Check the Status (`@reka-ai/n8n-nodes-reka.rekaVision`, `wait`, `splitInBatches`)**: 
  - Hệ thống mất thời gian để Reka tải video, phân tích và render. Mặc định node **Wait 10 minutes** sẽ hoãn 10-15 phút tùy độ dài video gốc. Các sếp có thể điều chỉnh thời gian chờ này cho phù hợp.
  - Node **If MAX Reached** giới hạn tối đa 10 lần kiểm tra (tránh vòng lặp vô tận nếu AI gặp sự cố).
- **Send Clip Ready EMail & Send Failure EMail (`gmail`)**: 
  - Kết nối tài khoản Gmail OAuth2 của các sếp.
  - Tùy chỉnh nội dung tiêu đề và body email thông báo nhận video thành phẩm hoặc cảnh báo lỗi.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test Step / Execute workflow**) với một video mẫu để kiểm tra kết quả trả về từ Reka Vision.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ nhận email, các sếp có thể gắn thêm node **Telegram** hoặc **Slack** để nhận thông báo ngay lập tức trên điện thoại.
- **Tự động hóa đăng bài:** Kết nối đầu ra của email hoặc node hoàn thành với các công cụ lên lịch đăng bài (Buffer, Hootsuite hoặc qua API chính thức của TikTok/YouTube Shorts) để automation đạt mức 200%.
- **Lưu trữ Log:** Thêm một node **Google Sheets** để ghi lại lịch sử các video đã được AI xử lý, tránh việc trùng lặp nội dung.

### 📌 Kết luận
Tự động hóa sản xuất video ngắn chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n và Reka Vision AI. Hãy cài đặt ngay workflow này để tối ưu hóa thời gian sáng tạo nội dung của các sếp ngay hôm nay!