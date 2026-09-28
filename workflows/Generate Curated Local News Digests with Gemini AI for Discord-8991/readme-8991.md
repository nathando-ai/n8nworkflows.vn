---
title: "🚀 Tự động tổng hợp và chọn lọc tin tức địa phương bằng Gemini AI gửi trực tiếp lên Discord"
description: "Xây dựng hệ thống tự động cào tin từ RSS/Reddit, dùng Gemini AI chấm điểm độ liên quan và gửi bản tin tóm tắt chất lượng cao lên kênh Discord mỗi ngày."
slug: "tong-hop-tin-tuc-dia-phuong-gemini-ai-discord"
tags: [n8n, automation, no-code, gemini, discord, ai, rss]
keywords: [n8n workflow, tự động hóa tin tức, gemini ai, discord webhook, rss feed, tóm tắt tin tức]
---

# 🚀 Tự động tổng hợp và chọn lọc tin tức địa phương bằng Gemini AI gửi trực tiếp lên Discord

Các sếp có đang tốn hàng giờ mỗi ngày để lướt qua hàng loạt trang báo, mạng xã hội và các kênh tin tức địa phương chỉ để tìm ra vài thông tin thực sự hữu ích? Việc cập nhật tin tức thủ công không chỉ mất thời gian mà còn dễ bỏ sót các sự kiện quan trọng.

Đừng lo, workflow n8n này sẽ giải quyết triệt để vấn đề đó cho các sếp! Hệ thống sẽ tự động gom nhặt tin tức từ các nguồn RSS và Reddit, sử dụng **Gemini AI** để phân tích, chấm điểm mức độ liên quan, chọn lọc ra **Top 5 tin tức đáng chú ý nhất** và bắn thẳng một bản tin tóm tắt cực kỳ chuyên nghiệp lên kênh **Discord** vào mỗi buổi sáng. Hoàn toàn tự động 100%, không tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần tự tay lướt báo hay kiểm tra các trang tin địa phương mỗi ngày.
- **AI thông minh chọn lọc:** Gemini AI sẽ đọc, hiểu và đánh giá mức độ quan trọng của từng bài viết, loại bỏ tin rác, tin trùng lặp.
- **Cá nhân hóa nội dung:** Dễ dàng thay đổi khu vực địa lý, nguồn tin (RSS, Reddit) theo đúng nhu cầu của các sếp.
- **Hoạt động 24/7 tự động:** Cứ đúng 8 giờ sáng mỗi ngày, bản tin sạch sẽ, gọn gàng sẽ xuất hiện trên Discord của nhóm hoặc cá nhân.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n** (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Lấy miễn phí tại [Google AI Studio](https://aistudio.google.com/).
- **Discord Webhook URL:** Để gửi tin nhắn tự động vào kênh Discord mong muốn.
- **Các nguồn tin RSS / Reddit** của khu vực các sếp muốn theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này, dán thẳng vào trình soạn thảo n8n (n8n Editor) hoặc import file JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà theo ý muốn, các sếp cần cấu hình các node sau:
- **Daily 8AM Trigger:** Chỉnh lại múi giờ (Timezone) nếu cần để bot gửi tin đúng giờ địa phương của các sếp.
- **RSS Phoenix New Times, RSS AZ Free News, RSS Reddit Phoenix... (và các node RSS khác):** Thay thế các đường dẫn RSS mẫu bằng các nguồn tin địa phương hoặc lĩnh vực mà các sếp thực sự quan tâm. Có thể tìm kiếm RSS của bất kỳ website nào bằng các công cụ tìm kiếm RSS trực tuyến.
- **Gemini Relevance Scoring (Node HTTP Request):** 
  - Tại phần Header hoặc URL, đảm bảo đã thay thế đoạn `key=YOUR_KEY_HERE` bằng **Google Gemini API Key** thực tế của các sếp.
  - Có thể tinh chỉnh Prompt bên trong payload của request để AI hiểu rõ hơn tiêu chí đánh giá tin tức nào là quan trọng đối với các sếp.
- **Limit to Top 5:** Mặc định hệ thống sẽ lấy 5 bài viết xuất sắc nhất. Các sếp có thể đổi số lượng này nếu muốn nhận nhiều hơn hoặc ít hơn.
- **Send to Discord:** Kết nối credential `discordWebhookApi` bằng Webhook URL của kênh Discord mà các sếp muốn bot bắn tin vào.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute workflow** để chạy thử xem dữ liệu có chảy qua các node Code, AI và bắn về Discord thành công hay không.
- Nếu mọi thứ hiển thị ngon lành, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Discord, các sếp có thể nhân bản node cuối để bắn đồng thời tin tức này sang **Telegram Bot** hoặc **Slack** phục vụ team.
- **Lưu trữ lịch sử:** Thêm node **Google Sheets** hoặc **Airtable** ở gần cuối để lưu lại toàn bộ các bản tin đã gửi, tạo thành một kho tư liệu tra cứu theo ngày tháng.
- **Tùy biến bộ lọc:** Tinh chỉnh node **Deduplicate & Prepare** để lọc bỏ các từ khóa nhạy cảm hoặc tin không liên quan trước khi gửi cho Gemini AI chấm điểm, giúp tiết kiệm token API.

### 📌 Kết luận
Một workflow cực kỳ thiết thực giúp tự động hóa hoàn toàn quy trình đọc báo, điểm tin mỗi ngày bằng sức mạnh của AI. Hãy cài đặt ngay để biến chiếc Discord của các sếp thành một trung tâm tin tức thông minh tự động!