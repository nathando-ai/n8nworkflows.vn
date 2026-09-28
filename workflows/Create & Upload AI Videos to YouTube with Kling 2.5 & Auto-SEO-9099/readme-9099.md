---
title: "🚀 Tự động tạo & tải video AI lên YouTube với Kling 2.5 & Auto‑SEO"
description: "Workflow n8n tự động chuyển prompt thành video AI, tối ưu SEO và đăng lên YouTube chỉ trong vài phút, không cần viết mã."
slug: "tu-dong-tao-video-ai-youtube-kling-2-5-auto-seo"
tags: [n8n, automation, no-code, AI, SEO, video]
keywords: [n8n workflow, tự động hóa, AI video, YouTube SEO, Kling 2.5]
---

# 🚀 Tự động tạo & tải video AI lên YouTube với Kling 2.5 & Auto‑SEO

Bạn đã từng tốn hàng giờ để viết kịch bản, tìm keyword, tạo video, rồi mới tới bước đăng lên YouTube?  
Quá trình này không chỉ mất thời gian mà còn dễ gây sai sót, không đồng nhất về tiêu chuẩn SEO.  

**Workflow này** sẽ giải quyết toàn bộ chuỗi công việc **từ nhập prompt → sinh nội dung, video AI, tối ưu SEO → đăng lên YouTube** chỉ bằng một cú click, hoàn toàn không cần viết code.  

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ 2‑3 tiếng giảm còn < 5 phút cho mỗi video.  
- **SEO chuẩn**: Tự động tạo tiêu đề, mô tả, tag, thumbnail chuẩn YouTube.  
- **Chất lượng video AI**: Dùng Kling 2.5 tạo video đa phương tiện, đồng bộ âm thanh & hình ảnh.  
- **Hoạt động liên tục**: Workflow chạy 24/7, tự động xử lý hàng loạt prompt.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Google** với quyền **Google Sheets** và **YouTube Data API** (OAuth2).  
- **API Key** của **OpenRouter** (hoặc bất kỳ LLM hỗ trợ).  
- **API Key** của **Kling 2.5** (hoặc dịch vụ video AI tương đương).  
- **Google Sheet** để lưu trữ prompt và kết quả (ID, tên sheet).  
- **Webhook URL** (nếu muốn trigger từ form bên ngoài).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `Create-Upload-AI-Videos-YouTube-Kling-2.5.json` (được cung cấp kèm).  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard** và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là danh sách các node quan trọng và cách cấu hình:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|-------------------|
| **Store Data** | Google Sheets | - **Credentials**: Google OAuth2 <br> - **Spreadsheet ID**: ID của sheet lưu prompt <br> - **Sheet Name**: `Prompts` (hoặc tùy chỉnh) |
| **Type Prompt** | Form Trigger | - **Form Fields**: `title`, `description` (hoặc tùy ý) <br> - **Webhook URL**: URL được n8n tạo tự động, chia sẻ cho người nhập prompt |
| **Wait 5 mins** | Wait | - Thời gian chờ **5 minutes** để LLM trả về kết quả đầy đủ |
| **Structured Output** | Output Parser Structured | - **Schema**: Định nghĩa JSON output (title, script, keywords, thumbnailPrompt, …) – dùng schema có sẵn trong workflow |
| **AI Brain** | LM Chat OpenRouter | - **Credentials**: OpenRouter API Key <br> - **Model**: `gpt‑4o-mini` (hoặc model bạn muốn) <br> - **Prompt**: Dùng biến `{{$json["prompt"]}}` từ Form Trigger |
| **Get Keywords** | Code | - **Code**: JavaScript để tách keyword từ script (đã có sẵn). <br> - Không cần thay đổi, chỉ kiểm tra **Input** là `script` từ AI Brain |
| **YT Video SEO** | Agent (LangChain) | - **Prompt**: Dùng `{{$json["script"]}}` + `{{$json["keywords"]}}` để tạo **title**, **description**, **tags**, **thumbnailPrompt**. <br> - **Credentials**: OpenRouter API Key |
| **AI_Brain** (second) | LM Chat OpenRouter | - **Prompt**: Gửi `thumbnailPrompt` tới LLM để nhận **thumbnail description** (để dùng trong FAL.AI). |
| **Fetch Video Credentials** | HTTP Request | - **Method**: `POST` <br> - **URL**: Endpoint của Kling 2.5 (ví dụ `https://api.kling.ai/v2/video`) <br> - **Authentication**: API Key trong Header `Authorization: Bearer <YOUR_KLING_KEY>` <br> - **Body**: JSON chứa `script`, `voice`, `style`… (được truyền từ node trước) |
| **Videography** | Chain LLM | - **Chain**: Kết hợp LLM và FAL.AI để tạo video cuối cùng. <br> - **Credentials**: OpenRouter + FAL.AI API Key. |
| **Download Video** | HTTP Request | - **Method**: `GET` <br> - **URL**: Link tải video trả về từ Kling. <br> - **Output**: Binary data (`video.mp4`). |
| **Make FAL.AI Request** | HTTP Request | - **Method**: `POST` <br> - **URL**: `https://api.fal.ai/v1/generate-thumbnail` <br> - **Headers**: `Authorization: Bearer <YOUR_FALAI_KEY>` <br> - **Body**: `thumbnailPrompt` từ node **AI_Brain**. |
| **Post on YouTube** | YouTube | - **Credentials**: YouTube OAuth2 (cần quyền **YouTube Data API**). <br> - **Video File**: Binary data từ **Download Video**. <br> - **Title / Description / Tags**: Lấy từ **YT Video SEO** output. <br> - **Thumbnail**: Binary từ **Make FAL.AI Request**. |

> **Lưu ý:**  
> - Đảm bảo **OAuth2 scopes** bao gồm `https://www.googleapis.com/auth/youtube.upload` và `https://www.googleapis.com/auth/spreadsheets`.  
> - Kiểm tra **quota** của OpenRouter và Kling; nếu vượt giới hạn, tăng gói hoặc giảm tần suất chạy.  

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhập một prompt mẫu qua Form Trigger → Kiểm tra từng node có trả về dữ liệu mong muốn không.  
2. Khi mọi thứ ổn, bật **Active** ở góc trên bên phải.  
3. Đặt **Cron** (nếu muốn tự động chạy định kỳ) hoặc để **Webhook** luôn chờ.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** ngay sau node **Post on YouTube** để thông báo tự động cho team.  
- **Lưu log vào Google Cloud Logging**: Dùng node **HTTP Request** gửi log JSON tới Cloud Logging để theo dõi KPI (số video, lượt view).  
- **Batch processing**: Sử dụng **Google Sheets** để đưa nhiều prompt vào một sheet, sau đó dùng **Loop** (SplitInBatches) để tạo video hàng loạt.  
- **A/B testing tiêu đề**: Tạo một node **Code** để sinh 2‑3 tiêu đề, rồi dùng **YouTube API** để thử nghiệm CTR.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình sản xuất video AI**, từ ý tưởng đến SEO và đăng tải, giảm chi phí nhân lực và tăng tốc độ ra nội dung. Hãy import ngay, cấu hình các credential, và để n8n làm việc thay bạn! 🚀