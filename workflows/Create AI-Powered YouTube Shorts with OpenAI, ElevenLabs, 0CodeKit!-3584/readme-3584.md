---
title: "🚀 Tự động tạo YouTube Shorts AI với OpenAI, ElevenLabs & 0CodeKit"
description: "Workflow n8n tự động sinh nội dung, hình ảnh, giọng nói và render video Shorts chỉ trong vài phút, không cần viết code."
slug: "tu-dong-tao-youtube-shorts-ai"
tags: [n8n, automation, no-code, AI, marketing]
keywords: [n8n workflow, tự động hóa, YouTube Shorts, OpenAI, ElevenLabs, 0CodeKit]
---

# 🚀 Tự động tạo YouTube Shorts AI với OpenAI, ElevenLabs & 0CodeKit

Bạn có bao giờ phải **ngồi gõ script, tìm hình ảnh, thu âm, dựng video** cho một YouTube Shorts chỉ để rồi nhận được kết quả không ưng?  
Việc này tốn hàng giờ, công sức và thường xuyên gây lỗi sai do con người.  

**Workflow này** sẽ giải quyết toàn bộ chuỗi công việc trên **tự động 100%**, từ ý tưởng, viết kịch bản, tạo hình ảnh, lồng tiếng AI, tới render video cuối cùng – **không cần một dòng code nào**.  

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ ý tưởng đến video chỉ trong < 5 phút.  
- **Độ chính xác cao**: Nội dung được sinh bởi OpenAI, giọng nói chuẩn xác từ ElevenLabs.  
- **Cá nhân hoá**: Thay đổi prompt, giọng nói, màu sắc video chỉ bằng một vài thay đổi trong node.  
- **Hoạt động liên tục**: Đặt lịch chạy tự động, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản n8n** (cài đặt self‑hosted hoặc cloud).  
- **OpenAI API Key** (để dùng GPT‑4/ChatGPT).  
- **ElevenLabs API Key** (để tạo voiceover).  
- **0CodeKit API Key** (để tạo video từ script + hình ảnh).  
- **Cloudinary Account & API credentials** (lưu trữ video tạm thời).  
- **Kết nối internet ổn định** (các request tới API bên ngoài).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file `Create AI-Powered YouTube Shorts.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là các node quan trọng và cách cấu hình chúng:

| Node | Loại | Mục đích | Cấu hình cần thay đổi |
|------|------|----------|-----------------------|
| **When clicking ‘Test workflow’** | `manualTrigger` | Bắt đầu workflow thủ công để test. | Không cần thay đổi. |
| **Ideator** | `openAi` | Dùng GPT‑4 sinh **ý tưởng video** dựa trên prompt của bạn. | - **Credentials**: OpenAI API Key.<br>- **Model**: `gpt-4`.<br>- **Prompt**: “Generate 5 YouTube Shorts ideas about *[chủ đề]*”. |
| **Script** | `set` | Lưu script gốc từ Ideator vào trường `script`. | - **Values**: `script` = `{{$json["choices"][0]["message"]["content"]}}`. |
| **Script Generator** | `httpRequest` | Gửi script tới 0CodeKit để tạo **kịch bản chi tiết** (scene, thời gian). | - **URL**: `https://api.0codekit.com/v1/script`.<br>- **Authentication**: 0CodeKit API Key.<br>- **Body**: `{ "script": "{{$node["Script"].json["script"]}}" }`. |
| **HTTP Request** (đầu vào) | `httpRequest` | Lấy **voiceover** từ ElevenLabs. | - **URL**: `https://api.elevenlabs.io/v1/text-to-speech/{{voice_id}}`.<br>- **Headers**: `xi-api-key: {{elevenlabsApiKey}}`.<br>- **Body**: `{ "text": "{{$node["Script Generator"].json["detailedScript"]}}" }`. |
| **Split Out** | `splitOut` | Tách **các đoạn văn** để tạo ảnh riêng cho mỗi scene. | - **Mode**: `Split by newline`. |
| **Image Prompter** | `openAi` | Dùng DALL·E (hoặc Stable Diffusion) sinh **prompt cho hình ảnh** dựa trên đoạn văn. | - **Credentials**: OpenAI API Key.<br>- **Prompt**: “Create an image prompt for: {{$json["value"]}}”. |
| **Request Image** | `httpRequest` | Gửi prompt tới dịch vụ tạo ảnh (DALL·E). | - **URL**: `https://api.openai.com/v1/images/generations`.<br>- **Body**: `{ "prompt": "{{$node["Image Prompter"].json["generatedPrompt"]}}", "n":1, "size":"1024x1024" }`. |
| **Wait** | `wait` | Đợi một khoảng thời gian để ảnh được tạo (đảm bảo API trả về). | - **Time to wait**: `5 seconds` (có thể tùy chỉnh). |
| **Get Image** | `httpRequest` | Lấy URL ảnh trả về và lưu vào biến `imageUrl`. | - **URL**: `{{$json["data"][0]["url"]}}`. |
| **Request Video** | `httpRequest` | Gửi **danh sách ảnh + voiceover** tới 0CodeKit để tạo video tạm thời. | - **URL**: `https://api.0codekit.com/v1/video`.<br>- **Body**: `{ "images": [{{$node["Get Image"].json["imageUrl"]}}], "audioUrl": "{{$node["HTTP Request"].json["audioUrl"]}}" }`. |
| **Wait for Video** | `wait` | Đợi quá trình render video hoàn tất. | - **Time to wait**: `30 seconds` (tùy thuộc độ dài). |
| **Get Video** | `httpRequest` | Lấy **URL video** đã render. | - **URL**: `{{$json["videoUrl"]}}`. |
| **Upload to Cloudinary** | `httpRequest` | Đẩy video lên Cloudinary để có link chia sẻ công cộng. | - **URL**: `https://api.cloudinary.com/v1_1/{{cloudName}}/video/upload`.<br>- **Form Data**: `file` = `{{$node["Get Video"].json["videoUrl"]}}`, `upload_preset` = `{{presetName}}`. |
| **Aggregate** | `aggregate` | Gom lại **script, voice, ảnh, video URL** thành một object. | - **Mode**: `Keep Only Latest`. |
| **Merge** | `merge` | Kết hợp dữ liệu từ các node trước (script, image, video). | - **Mode**: `Pass Through`. |
| **Create Editor JSON** | `httpRequest` | Tạo **JSON cấu hình cho trình chỉnh sửa** (nếu muốn tùy chỉnh thêm). | - **URL**: `https://api.0codekit.com/v1/editor`.<br>- **Body**: `{ "script": "{{$node["Script Generator"].json["detailedScript"]}}", "images": [...], "audio": "{{$node["HTTP Request"].json["audioUrl"]}}" }`. |
| **Set JSON Variable** | `set` | Lưu JSON cuối cùng vào biến `finalPayload`. | - **Values**: `finalPayload` = `{{$node["Create Editor JSON"].json}}`. |
| **Editor** | `httpRequest` | Gửi payload tới công cụ **Editor** để preview (tùy chọn). | - **URL**: `https://editor.0codekit.com/render`.<br>- **Body**: `{{$node["Set JSON Variable"].json["finalPayload"]}}`. |
| **Rendering** | `wait` | Đợi quá trình preview/render hoàn tất. | - **Time to wait**: `10 seconds`. |
| **Get Final Video** | `httpRequest` | Lấy **video cuối cùng** (đã qua bước chỉnh sửa) và trả về link. | - **URL**: `{{$json["finalVideoUrl"]}}`. |

> **Lưu ý:**  
> - Mỗi node `httpRequest` cần **đặt đúng Credential** (OpenAI, ElevenLabs, 0CodeKit, Cloudinary).  
> - Kiểm tra **quota** của các API (đặc biệt OpenAI và ElevenLabs) để tránh bị gián đoạn.  
> - Nếu muốn **tự động chạy hàng ngày**, thay `manualTrigger` bằng `Cron` node.

#### 3. Kích hoạt ⚡️
1. **Test**: Nhấn nút **Execute Workflow** → Kiểm tra log từng node, đảm bảo không có lỗi.  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Nếu muốn chạy tự động, thêm **Cron** node trước `manualTrigger` và cấu hình lịch (ví dụ: mỗi ngày 09:00).

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` để nhận thông báo khi video đã sẵn sàng.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại tiêu đề, link video, thời gian tạo.  
- **Tối ưu chi phí**: Chỉ dùng **GPT‑3.5** cho ý tưởng, chuyển sang **GPT‑4** cho script chi tiết nếu cần độ sâu.  
- **Tùy chỉnh phong cách video**: Thêm các tham số `style`, `music` vào payload của 0CodeKit để tạo video “vibrant”, “minimalist”, …  

### 📌 Kết luận
Với workflow này, **các sếp** có thể biến một ý tưởng ngẫu nhiên thành YouTube Shorts chuyên nghiệp chỉ trong vài phút, không cần đội ngũ sản xuất video. Hãy **import, cấu hình nhanh**, bật chạy và để AI làm việc cho mình – tiết kiệm thời gian, tăng năng suất và tạo nội dung liên tục cho kênh YouTube! 🚀