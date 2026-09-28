---
title: "🚀 Tự động tạo và đăng video AI Avatar tin tức công nghệ lên đa nền tảng với n8n, HeyGen & Blotato"
description: "Khám phá cách xây dựng hệ thống tự động hóa 100% không cần code: Tự động quét tin tức công nghệ hot, viết kịch bản bằng OpenAI, tạo video AI Avatar qua HeyGen và phân phối lên toàn bộ mạng xã hội bằng Blotato."
slug: "tu-dong-tao-va-dang-video-ai-avatar-len-mang-xa-hoi"
tags: [n8n, automation, ai-avatar, heygen, blotato, content-creation, social-media]
keywords: [n8n workflow, tạo video ai avatar, heygen api, blotato automation, tự động đăng mạng xã hội, ai agent n8n]
---

# 🚀 Tự động hóa sản xuất và phân phối Video AI Avatar tin tức công nghệ đa nền tảng

Các sếp có bao giờ mệt mỏi vì phải liên tục tìm kiếm ý tưởng, viết kịch bản, quay camera, dựng hình rồi lại ì ạch đăng lên từng mạng xã hội chưa? Việc này ngốn hàng tá thời gian mà đôi khi tương tác lại chẳng được bao nhiêu.

Đừng lo, workflow n8n cực kỳ xịn sò này do **Sabrina Ramonov** thiết kế sẽ thay các sếp làm tất cả từ A-Z! Hệ thống sẽ tự động quét tin tức công nghệ hot trên Hacker News, nhờ AI viết kịch bản 30 giây, gọi API HeyGen để tạo video AI Clone của chính các sếp, và cuối cùng tự động "bơm" video đó lên 10 nền tảng mạng xã hội khác nhau thông qua Blotato mỗi ngày. Hoàn toàn tự động, không cần đụng tay chân!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần quay phim, không cần edit video thủ công, mọi thứ chạy tự động hoàn toàn.
- **Sản xuất nội dung đều đặn:** Kênh truyền thông của các sếp sẽ luôn "nóng" với các tin tức công nghệ mới nhất mỗi ngày lúc 10h sáng.
- **Phủ sóng đa nền tảng:** Đăng một phát ăn ngay lên TikTok, LinkedIn, Facebook, Instagram, YouTube, Twitter/X, Threads, Bluesky, Pinterest.
- **Cá nhân hóa cực cao:** Sử dụng chính AI Avatar và giọng nói clone của các sếp (qua HeyGen và ElevenLabs) để tạo sự tin cậy tuyệt đối với khán giả.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **OpenAI API Key:** Dành cho AI Agent và các node viết kịch bản, viết caption (khuyên dùng model GPT-4.1).
- **HeyGen API Plan (Có trả phí):** Tài khoản HeyGen API (gói trả phí vì gói free không hỗ trợ API tạo video avatar). Chuẩn bị sẵn Avatar ID và Voice ID của các sếp.
- **Blotato Account & API:** Tài khoản tại [Blotato.com](https://blotato.com) để kết nối và điều phối đăng bài lên các mạng xã hội.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow này hoặc tải file JSON từ nguồn gốc.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp nhớ cấu hình kỹ các node sau:
- **Schedule Trigger:** Mặc định đang đặt chạy lúc 10:00 AM mỗi ngày. Các sếp có thể đổi lại giờ giấc theo ý thích.
- **Write Script & Viết Caption (OpenAI nodes):** Kết nối credentials OpenAI API của các sếp. Có thể tinh chỉnh system prompt nếu muốn đổi phong cách văn phong (hài hước, chuyên môn, châm biếm...).
- **Setup Heygen (Set node):** Điền các tham số quan trọng như `avatar_id`, `voice_id`. 
  - *Lưu ý nâng cao:* Nếu muốn chèn video nền phía sau avatar (yêu cầu avatar tách nền dạng green screen/matte), hãy cấu hình tham số `has_background_video` thành `true` và trỏ tới link video nền tại `background_video_url`.
- **Get Avatar Video & Create Avatar Video nodes:** Cấu hình HTTP Request gọi đến HeyGen API. Nếu kịch bản dài, hãy chú ý tăng thời gian ở node **Wait** để đảm bảo HeyGen render xong video mới tiến hành bước tiếp theo.
- **Các node mạng xã hội [BLOTATO] (TikTok, LinkedIn, Facebook, Instagram, YouTube, Twitter, Threads, Bluesky, Pinterest):** 
  - Kết nối `blotatoApi` credentials.
  - Mở từng node và chọn đúng tài khoản mạng xã hội đã liên kết trên Blotato. **Tuyệt đối không cần chỉnh sửa gì thêm ở các node này!**

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** để chạy thử nghiệm xem quá trình tạo video và gọi API có mượt mà không.
- Sau khi test xanh mướt, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi ngách nội dung:** Nếu các sếp không làm về tech, hãy thay thế node *Fetch HN Article / Hacker News* bằng **SerpAPI tool** để AI tự động tìm kiếm tin tức về bất kỳ lĩnh vực nào (Crypto, Bất động sản, Marketing, Sức khỏe...).
- **Thêm bước kiểm duyệt (Human-in-the-loop):** Thay vì đăng thẳng lên mạng xã hội, các sếp có thể chèn thêm một node **Telegram** hoặc **Slack** gửi video nháp về để duyệt trước khi ra lệnh cho Blotato phát sóng.
- **Chống spam mạng xã hội:** Hãy tuân thủ lưu ý của tác giả: Không nên đăng hoàn toàn 100% nội dung giống hệt nhau hoặc tần suất quá dày đặc trên cùng một nền tảng để tránh bị quét spam. Luôn bật nhãn gắn nội dung AI (AI-generated content) nếu nền tảng yêu cầu.

### 📌 Kết luận
Workflow này chính là một "vũ khí tối thượng" giúp các sếp xây dựng thương hiệu cá nhân tự động hóa hoàn toàn trên internet mà không tốn một phút quay dựng thủ công nào. Hãy cài đặt ngay hôm nay và để AI làm việc thay các sếp!