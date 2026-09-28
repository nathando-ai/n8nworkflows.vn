---
title: "🚀 Tự động cắt video YouTube bằng Claude AI & Apify từ yêu cầu tự nhiên"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình trích xuất transcript, dùng Claude AI phân tích đoạn hay và cắt video YouTube theo yêu cầu."
slug: "tu-dong-cat-video-youtube-claude-apify"
tags: [n8n, automation, no-code, youtube, claude-ai, apify, ai-agent]
keywords: [n8n workflow, cắt video youtube tự động, claude ai apify, tự động hóa nội dung, ai agent n8n]
---

# 🚀 Tự động cắt video YouTube bằng Claude AI & Apify từ yêu cầu tự nhiên

Các sếp có bao giờ cảm thấy mệt mỏi khi phải ngồi cày cuốc hàng giờ đồng hồ chỉ để tìm và cắt ra vài đoạn video YouTube tâm đắc làm Reels, TikTok hay Shorts? Việc xem lại toàn bộ video dài, dò thời gian (timestamp), rồi dùng phần mềm cắt ghép thủ công vừa tốn thời gian, vừa ảnh hưởng đến năng suất sáng tạo nội dung.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100% không cần code. Sự kết hợp giữa **Apify** (cào dữ liệu/transcript YouTube), **Claude AI (Anthropic)** (thông minh phân tích ngữ nghĩa và tìm khoảnh khắc vàng) và **n8n** sẽ giúp các sếp biến một câu lệnh tự nhiên thành những đoạn clip hoàn chỉnh chỉ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công xem video và dò mốc thời gian (timestamp).
- **AI thông minh chọn lọc:** Claude AI tự động đọc transcript và tìm ra chính xác các đoạn nội dung hấp dẫn, đúng với yêu cầu bằng ngôn ngữ tự nhiên của các sếp.
- **Tự động hóa toàn diện:** Từ lấy transcript, cắt video qua Apify, lưu link vào Google Sheets cho đến tải file về máy.
- **Linh hoạt mở rộng:** Dễ dàng tích hợp thêm các bước thông báo qua Telegram, Slack hoặc đăng trực tiếp lên mạng xã hội.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Apify Account:** Tài khoản Apify để gọi API lấy transcript và cắt video YouTube.
- **Anthropic API Key:** Khóa API để kết nối với mô hình Claude AI.
- **Google Sheets:** Tài khoản Google để lưu trữ danh sách các clip đã cắt thành công.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc tải file từ nguồn cấp) và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:

- **YouTube Clip Request Form**: Form đầu vào để người dùng nhập link video YouTube và câu lệnh (prompt) tự nhiên mô tả đoạn clip cần cắt.
- **Workflow Configuration**: Thiết lập các biến cấu hình chung cho toàn bộ luồng xử lý.
- **Get Video Transcript from Apify & Create Clips via Apify**: Kết nối tài khoản Apify thông qua API Token. Đảm bảo cấu hình đúng Actor của Apify chuyên xử lý YouTube transcript và video cutting.
- **Find Clips from Transcript (Agent) & Anthropic Chat Model**: Chọn đúng credential của Anthropic (Claude AI). Cấu hình prompt cho Agent hiểu cách đọc transcript và trả về kết quả theo định dạng.
- **Structured Output Parser**: Đảm bảo schema đầu ra khớp với cấu trúc mốc thời gian (bắt đầu, kết thúc) mà bước cắt video yêu cầu.
- **Save Clip Links to Google Sheets**: Chọn tài khoản Google Sheets của các sếp, kết nối tới file Google Sheet đích và trỏ đúng tên Sheet để hệ thống ghi log kết quả (Link clip, tiêu đề...).
- **Download Clip Files & Save Files Locally**: Cấu hình đường dẫn thư mục lưu trữ file trên server n8n (đối với bản self-hosted) nếu các sếp muốn tải hẳn file video về máy.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form yêu cầu với một video YouTube ngắn để kiểm tra xem toàn bộ các node có chạy xanh (thành công) hay không.
- Sau khi test ngon lành, hãy bật nút **Active** ở góc trên bên phải để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Thông báo:** Thêm node Telegram hoặc Slack ngay sau bước lưu Google Sheets để bot bắn tin nhắn báo cáo kèm link video ngay khi cắt xong.
- **Tự động đăng Reels/TikTok:** Nối thêm các bước gọi API của TikTok hoặc Meta để tự động lên lịch đăng tải các đoạn clip ngắn vừa cắt.
- **Lưu trữ Cloud Storage:** Thay vì lưu file cục bộ, các sếp có thể kết nối với Google Drive, AWS S3 để lưu trữ video chuyên nghiệp hơn.

### 📌 Kết luận
Việc tạo nội dung ngắn từ video dài nay đã trở nên cực kỳ đơn giản và thông minh nhờ sức mạnh của AI kết hợp cùng n8n. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất làm content cho đội ngũ của mình nhé các sếp!