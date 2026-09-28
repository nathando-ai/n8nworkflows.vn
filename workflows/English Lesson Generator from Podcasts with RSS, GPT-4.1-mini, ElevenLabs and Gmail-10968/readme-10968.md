---
title: "🚀 Tự động tạo bài học tiếng Anh từ Podcast với n8n, OpenAI và ElevenLabs"
description: "Xây dựng hệ thống tự động hóa trích xuất podcast RSS, sử dụng GPT-4.1-mini tạo nội dung học tập và ElevenLabs chuyển văn bản thành giọng nói để gửi email học tiếng Anh hàng tuần."
slug: "tu-dong-tao-bai-hoc-tieng-anh-tu-podcast-n8n"
tags: [n8n, automation, no-code, openai, elevenlabs, gmail, ai-agents]
keywords: [n8n workflow, tự động hóa podcast, học tiếng anh ai, elevenlabs n8n, gpt-4 mini, rss feed automation]
---

# 🚀 Tự động tạo bài học tiếng Anh từ Podcast với n8n, OpenAI và ElevenLabs

Các sếp có muốn mỗi tuần tự động nhận được một bản tin (newsletter) học tiếng Anh cực kỳ chất lượng được tổng hợp trực tiếp từ các chương trình Podcast nổi tiếng như *BBC 6 Minute English*, kèm theo cả file nghe phát âm từ vựng chuẩn giọng bản xứ do AI đọc không? 

Thay vì phải ngồi nghe podcast, chép từ vựng và tự soạn bài tập thủ công hàng giờ đồng hồ, workflow n8n này sẽ thay các sếp làm tất cả từ A-Z hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Hệ thống tự động quét tập podcast mới nhất mỗi tuần, lọc bỏ các tập đã học.
- **Học tập toàn diện:** Tự động sinh nội dung hook mở đầu, câu hỏi thảo luận, bài tập điền vào chỗ trống nhờ sức mạnh của OpenAI.
- **Cải thiện kỹ năng nghe:** Tự động trích xuất danh sách từ vựng và sử dụng ElevenLabs để tạo file audio phát âm chậm rãi, dễ nghe đính kèm theo email.
- **Giao diện chuyên nghiệp:** Nhận toàn bộ bài học qua email cá nhân được thiết kế chuẩn HTML đẹp mắt.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Cloud hoặc Self-hosted).
- **OpenAI API Key:** Kết nối cho các node AI Agent (sử dụng model `gpt-4.1-mini`).
- **ElevenLabs API Key:** Để tạo file âm thanh đọc từ vựng.
- **Gmail Account / Credentials:** Để gửi email chứa nội dung bài học và file đính kèm.
- **n8n Data Table:** Dùng để lưu lịch sử các tập podcast đã được xử lý (tránh bị lặp lại).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON theo hướng dẫn từ kho lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần chú ý cấu hình các node quan trọng sau:
- **Node `Archived Podcasts` (Data Table):** Tạo một Data Table mới trên n8n với các trường dữ liệu: `guid`, `title`, `link`, `processed_date`. Sau đó kết nối node này với các node `Archived Podcasts`, `Unique guid(s)` và `Combine with archived guid(s)`.
- **Các Model AI (`Model: Email Hook`, `Model: Practice Exercises`, `Model: Discussion Questions`):** Nhập OpenAI API Credentials và cấu hình model `gpt-4.1-mini`.
- **Node `Generate Audio Transcript` (ElevenLabs):** Thêm ElevenLabs credentials, chọn resource là `speech` và chọn giọng đọc (Voice) yêu thích.
- **Node `Send Email` (Gmail):** Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp để hệ thống có quyền gửi email tự động kèm file ghi âm.
- **Node `Trigger Sunday 20:00`:** Có thể thay đổi lịch chạy (thời gian/tần suất) tùy theo nhu cầu cá nhân.

#### 3. Kích hoạt ⚡️
- Chạy thử thủ công (Test step-by-step hoặc Test workflow) để kiểm tra luồng dữ liệu từ RSS đến lúc gửi email.
- Sau khi kiểm tra mọi thứ hoạt động ổn định, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì chỉ gửi qua Gmail, các sếp có thể mở rộng workflow để gửi thẳng bản tin tóm tắt này vào nhóm Telegram hoặc Slack của team học tiếng Anh.
- **Lưu trữ Google Drive:** Thêm bước lưu file audio `.mp3` từ ElevenLabs vào Google Drive để dễ dàng nghe lại trên điện thoại bất cứ lúc nào.
- **Tùy biến Prompts:** Các sếp có thể chỉnh sửa prompt trong các AI Agent node để điều chỉnh độ khó (Beginner, Intermediate, Advanced) hoặc thay đổi phong cách bài học cho phù hợp với sở thích.

### 📌 Kết luận
Một workflow tuyệt vời kết hợp giữa RSS Feed, AI thông minh và công nghệ chuyển văn bản thành giọng nói hàng đầu. Hãy triển khai ngay hôm nay để xây dựng cho mình một trợ lý học ngoại ngữ tự động hóa 24/7 các sếp nhé!