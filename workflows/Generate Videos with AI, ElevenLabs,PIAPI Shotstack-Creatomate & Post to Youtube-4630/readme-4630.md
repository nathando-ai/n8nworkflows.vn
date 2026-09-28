---
title: "🚀 Tự động hóa sản xuất video AI từ A-Z với OpenAI, ElevenLabs, Shotstack và đăng YouTube"
description: "Hướng dẫn xây dựng hệ thống tạo video tự động hoàn toàn bằng n8n, kết hợp OpenAI AI Agent, ElevenLabs, PIAPI/Shotstack/Creatomate và tự động đăng lên YouTube."
slug: "tu-dong-hoa-san-xuat-video-ai-openai-elevenlabs-shotstack-youtube"
tags: [n8n, automation, no-code, ai-video, youtube-automation, openai]
keywords: [n8n workflow, tạo video ai tự động, elevenlabs n8n, shotstack creatomate, tự động đăng youtube]
---

# 🚀 Tự động hóa sản xuất video AI từ A-Z với OpenAI, ElevenLabs, Shotstack và đăng YouTube

Các sếp có đang chật vật tốn hàng giờ mỗi ngày để nghĩ ý tưởng, viết kịch bản, thu âm giọng đọc, dựng video và đăng lên YouTube? Việc làm thủ công này cực kỳ ngốn thời gian và khó duy trì tần suất ra video đều đặn.

Giải pháp ở đây chính là **Workflow n8n "Generate Videos with AI"** – một hệ thống tự động hóa khép kín (All-in-One) giúp các sếp biến các ý tưởng thô sơ thành video hoàn chỉnh, lồng tiếng AI, chèn nhạc, dựng hình bằng AI và tự động xuất bản lên kênh YouTube mà không cần động tay vào bất kỳ công đoạn dựng hình thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các tác vụ nặng (gọi API LLM, render video, chờ đợi các node Wait) chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình sản xuất nội dung**: Từ khâu lên ý tưởng, viết kịch bản, tạo hình ảnh/giọng nói/âm nhạc cho đến dựng video và đăng YouTube.
- **Tiết kiệm 95% thời gian & chi phí nhân sự**: Thay vì thuê cả đội ngũ biên tập, voiceover, designer, hệ thống AI sẽ làm thay toàn bộ.
- **Sản lượng video vượt trội**: Dễ dàng duy trì lịch đăng bài đều đặn mỗi ngày, giúp kênh YouTube tăng trưởng nhanh chóng nhờ thuật toán ưu tiên tần suất.
- **Quản lý dữ liệu chuyên nghiệp**: Tích hợp chặt chẽ với Google Sheets và Airtable để lưu trữ, theo dõi trạng thái kịch bản và asset video minh bạch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Khuyên dùng bản Self-hosted trên VPS).
- **OpenAI API Key** (Dành cho các node AI Agent & Chat Model để lên ý tưởng, viết kịch bản, tạo prompt).
- **ElevenLabs API Key** (Tạo giọng đọc AI lồng tiếng).
- **PIAPI / Shotstack / Creatomate API** (Dành cho việc render và dựng video tự động).
- **Airtable & Google Sheets** (Lưu trữ dữ liệu ý tưởng, kịch bản, link media).
- **Google Drive API** (Lưu trữ file âm thanh, hình ảnh và video thô/thành phẩm).
- **YouTube Data API / Credentials** (Để tự động upload video lên kênh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu `...` (Menu) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì đây là một siêu workflow gồm tới 71 nodes, các sếp cần chú ý cấu hình kỹ các phần sau:
- **Credentials**: Kết nối toàn bộ các tài khoản OpenAI, Google Sheets, Airtable, Google Drive, ElevenLabs, YouTube và các dịch vụ render video vào n8n credentials.
- **Schedule Trigger & Schedule Trigger1**: Cài đặt lịch chạy tự động (ví dụ: chạy mỗi sáng lúc 8:00 để tạo video mới trong ngày).
- **Generate Idea & Generate Script (AI Agent)**: Kiểm tra lại Model OpenAI được chọn (`OpenAI Chat Model`, `OpenAI Chat Model1`, `OpenAI Chat Model2`) và tuỳ chỉnh System Prompt nếu muốn đổi phong cách nội dung/chủ đề video của kênh.
- **Store in Airtable / Google Sheets / Google Drive**: Trỏ chính xác đến các Base/Table trong Airtable, Sheet ID trong Google Sheets và Folder ID trên Google Drive của các sếp để dữ liệu không bị lưu nhầm chỗ.
- **ShotStack Render Video / Video Creatomate**: Cấu hình API endpoint và template ID phù hợp để hệ thống dựng hình theo đúng định dạng video mong muốn (Shorts hoặc Long-form).
- **Post YouTube**: Chọn đúng tài khoản kênh YouTube đích và cấu hình mặc định (Visibility, Tags, Description) khi video được xuất bản.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với 1 bản ghi mẫu ở bước *Schedule Trigger* để kiểm tra luồng chạy qua các node AI, tạo voice, tạo ảnh và dựng video xem có bị lỗi API hay thiếu trường dữ liệu nào không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước thông báo qua Telegram/Slack**: Chèn thêm node thông báo qua Telegram ngay sau node `Youtube Video Created` hoặc `Failed Creation` để nhận tin nhắn báo cáo tức thì khi video lên sóng hoặc gặp lỗi render.
- **Mở rộng đa nền tảng**: Ngoài YouTube, có thể kết hợp thêm các node HTTP Request để auto-repurpose video đăng chéo sang TikTok, Facebook Reels và Instagram.
- **Kiểm duyệt thủ công (Human-in-the-loop)**: Thay vì tự động đăng ngay sau khi render xong, các sếp có thể dùng node Wait hoặc dừng ở trạng thái `Draft` trên Airtable, chờ duyệt bằng 1 cú click rồi mới đẩy sang luồng đăng YouTube.

### 📌 Kết luận
Workflow tự động hóa sản xuất video AI này là một vũ khí cực kỳ mạnh mẽ cho các nhà sáng tạo nội dung và Digital Marketer thời đại số. Hãy cài đặt ngay lên VPS của các sếp để tối ưu hóa thời gian và bứt phá lượng traffic cho kênh ngay hôm nay!