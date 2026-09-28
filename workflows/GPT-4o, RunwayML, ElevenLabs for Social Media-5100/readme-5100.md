---
title: "🚀 Tự động hóa sản xuất video mạng xã hội với GPT-4o, RunwayML và ElevenLabs trên n8n"
description: "Hướng dẫn xây dựng hệ thống AI Agent tự động biến ý tưởng văn bản thành video chuyên nghiệp, lồng tiếng sống động và đăng tải hoàn toàn tự động."
slug: "tu-dong-hoa-tao-video-gpt4o-runwayml-elevenlabs"
tags: [n8n, automation, no-code, ai-video, gpt-4o, runwayml, elevenlabs]
keywords: [n8n workflow, tao video tu dong, gpt-4o, runwayml, elevenlabs, ai content creation]
---

# 🚀 Xây dựng hệ thống "Nhà máy" sản xuất video tự động bằng GPT-4o, RunwayML & ElevenLabs

Các sếp có đang mệt mỏi vì tốn hàng giờ lên ý tưởng, viết kịch bản, tạo hình ảnh, dựng video và thu âm giọng đọc cho các kênh mạng xã hội (TikTok, Reels, Shorts)? Việc sản xuất nội dung đa phương tiện (Multimodal AI) thủ công cực kỳ ngốn thời gian và chi phí.

Hôm nay, em xin giới thiệu một siêu phẩm workflow n8n được thiết kế bởi chuyên gia Mohan Gopal. Workflow này sẽ tự động hóa **100% quy trình sản xuất video đa phương tiện**: Từ một ý tưởng sơ khai trong Google Sheets, AI sẽ tự động viết prompt, tạo hình ảnh, tạo giọng đọc (ElevenLabs), dựng video (RunwayML), lưu trữ Google Drive và sẵn sàng bùng nổ traffic trên mạng xã hội!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến 1 dòng ý tưởng thành video hoàn chỉnh kèm âm thanh chỉ bằng vài cú click hoặc chạy theo lịch trình (Schedule Trigger).
- **Ứng dụng AI đỉnh cao:** Kết hợp sức mạnh của GPT-4o, Google Gemini, RunwayML (Video AI) và ElevenLabs (Voice AI).
- **Quản lý tập trung:** Theo dõi trạng thái ý tưởng, cập nhật link video trực tiếp trên Google Sheets và Google Drive.
- **Tiết kiệm 95% thời gian:** Giải phóng đội ngũ Marketing khỏi các tác vụ dựng hình và thu âm thủ công lặp đi lặp lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản self-hosted).
- **Tài khoản & API Keys:**
  - OpenAI API (cho GPT-4o)
  - Google Gemini API (Google Palm API)
  - RunwayML API (hoặc dịch vụ tạo video tương ứng qua HTTP Request)
  - ElevenLabs API (cho giọng đọc)
- **Google Workspace:** Tài khoản Google Sheets (lưu ý tưởng và trạng thái) và Google Drive (lưu trữ và chia sẻ video).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ n8n.
- Mở n8n Editor -> Chọn **Workflows** -> **Add workflow** -> Dấu `...` (Options ở góc trên bên phải) -> **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 29 nodes được chia thành các cụm chức năng rõ ràng. Các sếp cần cấu hình kỹ các điểm sau:

- **Grab Idea & Google Sheets nodes (`Grab Idea`, `Video Status`, `Update Sheet`):** Kết nối tài khoản Google Sheets của các sếp. Chuẩn bị sẵn một file Google Sheets chứa các cột: *Idea*, *Status*, *Video URL*... để node đọc và ghi dữ liệu.
- **AI Agents (`Image Prompt Agent`, `Sound Agent`):** Liên kết với model LLM tương ứng là **GPT 4o** (`GPT 4o` node) và **Google Gemini Chat Model**. Đảm bảo đã điền OpenAI API Key và Google AI Studio API Key hợp lệ trong Credentials.
- **HTTP Request nodes (`Generate Image`, `Get Images`, `Generate Audio`, `Generate Videos`, `Render Video`, v.v.):** Đây là các node gọi API bên thứ ba (RunwayML, ElevenLabs, v.v.). Các sếp cần cấu hình đúng Header Auth (API Key của từng dịch vụ) và kiểm tra lại Endpoint URL theo tài liệu API mới nhất của các nền tảng đó.
- **Schedule Trigger / Manual Trigger:** Sếp có thể dùng nút `When clicking ‘Test workflow’` để test thủ công hoặc bật `Schedule Trigger` để hệ thống tự động quét ý tưởng và sản xuất video định kỳ mỗi ngày.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với 1 dòng ý tưởng mẫu trên Google Sheets để test từng bước (đặc biệt theo dõi các node `Wait`, `Limit`, `Merge` để đảm bảo luồng chạy mượt mà không bị timeout).
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào cuối workflow (`Share File` / `Update Sheet`) để gửi thông báo ngay cho sếp kèm link Google Drive khi video render xong.
- **Tự động đăng mạng xã hội:** Dựa trên gợi ý sẵn có trên canvas (*"Connect to Social media and post the video automatically"*), các sếp có thể gắn thêm các node API của TikTok, YouTube Shorts hoặc Facebook Reels để video tự động publish ngay sau khi render xong.
- **Tối ưu thời gian chờ:** Các node `Wait` (như 90 seconds, 2 minutes, 25 seconds) được thiết lập để chờ các API AI bên ngoài render xong video/ảnh. Các sếp có thể tinh chỉnh lại thời gian này dựa trên tốc độ phản hồi thực tế của các dịch vụ AI.

### 📌 Kết luận
Workflow **GPT-4o, RunwayML, ElevenLabs for Social Media** là một cỗ máy tự động hóa cực kỳ mạnh mẽ, đưa năng lực sản xuất content của các sếp lên một tầm cao mới. Hãy setup ngay hôm nay để tối ưu hóa chi phí nhân sự và phủ sóng thương hiệu trên mọi nền tảng video ngắn!