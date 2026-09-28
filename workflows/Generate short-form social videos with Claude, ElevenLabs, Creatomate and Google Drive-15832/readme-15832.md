---
title: "🚀 Tự động tạo video ngắn (Shorts/Reels/TikTok) với Claude AI, ElevenLabs và Creatomate trong n8n"
description: "Hướng dẫn chi tiết cách xây dựng pipeline tự động hóa tạo video ngắn hoàn chỉnh từ một chủ đề bất kỳ: viết kịch bản bằng Claude, lồng tiếng ElevenLabs, dựng video qua Creatomate và lưu trữ tự động."
slug: "tu-dong-tao-video-ngan-claude-elevenlabs-creatomate-n8n"
tags: [n8n, automation, ai-video, claude, elevenlabs, creatomate]
keywords: [n8n workflow, tạo video tự động, claude ai, elevenlabs voiceover, creatomate render, tiktok automation]
---

# 🚀 Tự động tạo video ngắn (Shorts/Reels/TikTok) bằng AI qua n8n

Các sếp có đang tốn hàng giờ mỗi ngày chỉ để lên ý tưởng, viết kịch bản, thu âm giọng đọc, chỉnh sửa capcut và xuất video ngắn cho TikTok, Instagram Reels hay YouTube Shorts không? Việc sản xuất nội dung thủ công liên tục thực sự là một "cực hình" ngốn rất nhiều thời gian và năng lượng.

Hãy để workflow n8n này giúp các sếp giải phóng 100% thời gian! Chỉ với một chủ đề đầu vào đơn giản, hệ thống sẽ tự động hóa toàn bộ quy trình: từ viết kịch bản chuyên nghiệp, tạo giọng đọc AI siêu thực, render video kèm hiệu ứng chữ chạy (captions) cho đến việc lưu trữ lên Google Drive và thông báo về Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến một từ khóa/chủ đề thành video hoàn chỉnh sẵn sàng đăng tải mà không cần đụng tay vào khâu edit.
- **Chất lượng AI đỉnh cao:** Kịch bản hút khách chuẩn cấu trúc 3 giây đầu gây chú ý từ Claude Sonnet, giọng đọc AI tự nhiên từ ElevenLabs.
- **Đồng bộ thương hiệu:** Video được render tự động qua Creatomate với màu sắc, font chữ và phong cách riêng của doanh nghiệp.
- **Quản lý tập trung:** Tự động lưu video vào Google Drive, gửi cảnh báo qua Slack và ghi log chi tiết vào Google Sheets.
:::

---

### 🔧 Yêu cầu cần thiết
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Anthropic API Key:** Để sử dụng Claude Sonnet viết kịch bản.
- **ElevenLabs API Key & Voice ID:** Để tạo giọng đọc AI.
- **Creatomate Account & API Key + Template ID:** Công cụ render video tự động.
- **Google Account:** Kết nối Google Drive (lưu video) và Google Sheets (lưu log).
- **Slack Account (Tùy chọn):** Nhận thông báo khi video render xong.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn gốc hoặc copy trực tiếp mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng 3 chấm ở góc trên bên phải -> **Import from File / Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm **13 nodes** chính được thiết kế mượt mà. Các sếp cần cấu hình các điểm mấu chốt sau:

- **Submit Video Topic (`formTrigger`):** Node khởi chạy bằng form nhập liệu thủ công. Các sếp có thể thay thế bằng *Schedule Trigger* nếu muốn lấy ý tưởng tự động từ Google Sheets.
- **Configure Brand Settings (`code`):** Node cực kỳ quan trọng! Hãy mở node này và điền thông tin thương hiệu của các sếp gồm: Tên thương hiệu, lĩnh vực, đối tượng mục tiêu, giọng văn, ElevenLabs Voice ID, Creatomate Template ID và tên thư mục lưu trữ. Đây là nơi duy nhất các sếp cần cấu hình cài đặt chung.
- **Write Script (`chainLlm`) & Claude Sonnet (`lmChatAnthropic`):** Thêm Anthropic Credentials và dán API Key lấy từ `console.anthropic.com`.
- **Generate Voiceover (`httpRequest`):** Nhập ElevenLabs API Key và cấu hình Voice ID muốn sử dụng.
- **Render Video (`httpRequest`) & Wait for Render / Get Render Status:** Cập nhật Creatomate API Key và Template ID để định hình phong cách video, hiệu ứng chữ và tỉ lệ khung hình (9:16 cho video ngắn).
- **Upload Audio to Drive & Upload Video to Drive (`googleDrive`):** Kết nối tài khoản Google và chỉ định thư mục lưu trữ file.
- **Notify Team - Video Ready (`slack`):** Kết nối kênh Slack của team. *(Lưu ý: Nếu không dùng Slack, các sếp có thể chuột phải vào node này và chọn Disable).*
- **Log Video Run (`googleSheets`):** Tạo sẵn một Google Sheet với tên `Video Log` gồm các cột: `Timestamp`, `Topic`, `Script Preview`, `Status`, `Drive Link`, `Duration`, sau đó kết nối tài khoản Google Sheets vào node này ở chế độ `append`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form qua Form Trigger.
- Kiểm tra kết quả trả về ở Google Drive và Google Sheets.
- Nếu mọi thứ chạy trơn tru, hãy gạt công tắc sang **Active** để hệ thống chính thức hoạt động tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa hoàn toàn:** Thay thế *Form Trigger* bằng *Schedule Trigger* kết hợp với một bảng Google Sheets chứa hàng loạt ý tưởng video để hệ thống tự sản xuất content hàng ngày mà không cần chạm tay.
- **Mở rộng đa nền tảng:** Thêm các node gọi API của TikTok, Instagram Graph API hoặc YouTube Data API vào nhánh sau node *Upload Video to Drive* để tự động đăng tải video lên các nền tảng xã hội.
- **Đổi công cụ Render:** Có thể thay thế Creatomate bằng Shotstack hoặc JSON2Video tùy theo sở thích và chi phí tối ưu của doanh nghiệp.

---

### 📌 Kết luận
Việc sản xuất video ngắn hàng loạt chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của Claude AI, ElevenLabs và Creatomate trong n8n. Hãy cài đặt ngay workflow này để tiết kiệm hàng chục giờ làm việc mỗi tuần và bứt phá kênh truyền thông xã hội của các sếp!