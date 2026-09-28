---
title: "🚀 Tự Động Hóa Nội Dung Twitter Với Gemini AI: Tweet, Hình Ảnh & Tương Tác"
description: "Giải pháp không code giúp các sếp tự động tạo tweet, hình ảnh AI và tương tác trên Twitter chỉ bằng một form."
slug: "twitter-content-automation-gemini-ai"
tags: [n8n, automation, no-code, social-media, AI]
keywords: [n8n workflow, tự động hóa Twitter, Gemini AI, tạo nội dung, AI multimodal]
---

# 🚀 Tự Động Hóa Nội Dung Twitter Với Gemini AI: Tweet, Hình Ảnh & Tương Tác

Bạn có bao giờ phải ngồi gõ tweet, tìm hình ảnh, rồi mới nhấn “Post” rồi lại phải trả lời DM, thích, retweet…?  
Công việc này vừa tốn thời gian, vừa dễ sai sót, còn khiến thương hiệu mất đi tính nhất quán.  

**Workflow này** sẽ giải quyết toàn bộ quy trình chỉ bằng một form duy nhất:  
- **AI Gemini** viết nội dung tweet theo tone & mục tiêu bạn chọn.  
- **AI tạo hình ảnh** dựa trên prompt tùy chỉnh.  
- **Twitter Tool** tự động đăng tweet, gửi DM, hoặc thực hiện “like”/retweet.  

Tất cả chạy **100 % không code** trên n8n, giúp các sếp tập trung vào chiến lược, không còn lo “đánh máy”.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ vài phút viết tweet → vài giây tự động.  
- **Độ chính xác cao**: Nội dung, hình ảnh và CTA luôn đồng nhất với brand guide.  
- **Tự động tương tác**: Like, retweet, DM được thực hiện ngay sau khi tweet.  
- **Hoạt động 24/7**: Không cần nhân sự giám sát, workflow tự chạy liên tục.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Twitter/X** (có quyền đăng tweet, gửi DM, thực hiện like).  
- **API Key Google Gemini** (để sử dụng các node `lmChatGoogleGemini`).  
- **API Endpoint cho tạo hình ảnh** (mặc định dùng Pollinations; có thể thay bằng DALL·E, Stable Diffusion, …).  
- **n8n** được cài đặt (Self‑hosted hoặc Cloud) và có **đủ quyền tạo webhook**.  
- (Tùy chọn) **Google Sheets OAuth2** nếu muốn lưu lịch sử tweet.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [đây](https://n8n.io/workflows/10322).  
2. Mở n8n → **Workflows** → **Import** → Chọn file JSON hoặc **Paste JSON** vào ô.  
3. Nhấn **Import**, workflow sẽ xuất hiện trên canvas.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
#### Node quan trọng & cách cấu hình

| Node | Vai trò | Cấu hình cần chỉnh |
|------|---------|--------------------|
| **Twitter Content Form** (`formTrigger`) | Form công khai để nhập nội dung (Tone, Action Type, Prompt hình ảnh). | - Đặt **Webhook Path**: `twitter-content-form` <br> - Bảo mật: bật **IP allow‑list** hoặc **secret**. |
| **Workflow Configuration** (`set`) | Đặt hằng số chung (ví dụ `maxTweetLength = 280`). | - Kiểm tra và thay đổi giá trị nếu cần. |
| **Twitter AI Agent** (`agent`) | Kết nối Gemini để sinh tweet. | - Chọn **Credential**: Google Gemini API Key.<br> - Đảm bảo **Model** là `gemini-pro`. |
| **Process AI Response** (`code`) | Định dạng lại phản hồi AI thành JSON chuẩn. | - Không cần thay đổi nếu bạn dùng prompt mặc định. |
| **Fields - Set Values** (`set`) | Đặt các trường cho việc tạo hình ảnh (prompt, size…). | - Kiểm tra `imagePrompt` và `imageSize` phù hợp với API hình ảnh. |
| **AI Agent - Create Image From Prompt** (`agent`) | Dùng Gemini (hoặc LLM hỗ trợ) để tạo prompt cho API hình ảnh. | - Credential: Google Gemini.<br> - Model: `gemini-pro-vision` (nếu hỗ trợ). |
| **Code - Clean Json** (`code`) | Làm sạch JSON trả về từ API hình ảnh. | - Kiểm tra `item.imageUrl` hoặc `binary` key. |
| **Code - Get Prompt** (`code`) | Trích xuất prompt cuối cùng cho HTTP Request. | - Đảm bảo biến `prompt` đúng định dạng. |
| **HTTP Request - Create Image** (`httpRequest`) | Gọi API Pollinations (hoặc dịch vụ khác) để tạo ảnh. | - URL: `https://image.pollinations.ai/...` <br> - Header: `Authorization` nếu cần.<br> - Kết quả sẽ lưu ở **binary → imageData**. |
| **Code - Set Filename** (`code`) | Đặt tên file cho ảnh (vd: `tweet-image-{{ $now }}`). | - Không cần thay đổi, chỉ thay `extension` nếu dùng định dạng khác. |
| **Twitter Post Tool** (`twitterTool`) | Công cụ “Post” được AI gọi khi Action = **Post**. | - Chọn **Credential** Twitter.<br> - Kiểm tra **resource** = `tweet`. |
| **Twitter DM Tool** (`twitterTool`) | Gửi tin nhắn trực tiếp (DM). | - `resource` = `directMessage`.<br> - Cấu hình **recipientId** (có thể lấy từ form). |
| **Twitter Engagement Tool** (`twitterTool`) | Thực hiện “like” hoặc “retweet”. | - `operation` = `like` (hoặc `retweet`). |
| **Create Tweet** (`twitter`) | Đăng tweet cuối cùng (có hoặc không ảnh). | - Đảm bảo **binary** `imageData` được truyền nếu muốn đính kèm ảnh. |
| **Merge Tweet Text and Image** (`merge`) | Gộp nội dung tweet + binary ảnh. | - Kiểu **Mode**: `Combine`.<br> - Input 1: Text, Input 2: Binary `imageData`. |
| **Google Gemini Chat Model2 & Model3** (`lmChatGoogleGemini`) | Các model phụ trợ cho prompt nâng cao. | - Credential: Google Gemini.<br> - Kiểm tra **temperature**, **maxTokens** nếu muốn tùy chỉnh. |

> **Lưu ý:** Mỗi node `twitterTool` phải được **kích hoạt** (Enable) và **được cấp quyền** trong tài khoản Twitter của bạn. Kiểm tra quota API để tránh bị block.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → nhập dữ liệu mẫu vào form (tone = “Professional”, action = “Post”).  
2. Kiểm tra **Execution Log**:  
   - Xem **Binary → imageData → View** ở node `HTTP Request - Create Image` để xác nhận ảnh được tạo.  
   - Kiểm tra **Twitter** → xem tweet đã xuất hiện trên tài khoản.  
3. Khi mọi thứ ổn, bật **Active** (Toggle ở góc phải) để workflow chạy tự động khi webhook được gọi.

## ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `Create Tweet` để gửi thông báo nội bộ mỗi khi có tweet mới.  
- **Lưu lịch sử**: Dùng node `Google Sheets` hoặc `Airtable` để ghi lại nội dung, link tweet, thời gian.  
- **Kiểm soát nội dung**: Thêm node `IF` trước `Create Tweet` để kiểm tra độ dài tweet (`{{ $json["text"].length }}` ≤ `maxTweetLength`).  
- **Đa ngôn ngữ**: Sử dụng thêm một `Google Gemini Chat Model` để dịch tweet sang các ngôn ngữ khác và đăng đồng thời trên các tài khoản quốc tế.  
- **Thay API hình ảnh**: Thay URL trong `HTTP Request - Create Image` bằng DALL·E, Stable Diffusion hoặc Midjourney API để có chất lượng ảnh cao hơn.

## 📌 Kết luận
Với workflow **Twitter Content Automation with Gemini AI**, các sếp có thể biến việc tạo nội dung, hình ảnh và tương tác trên Twitter thành một chuỗi tự động, nhanh chóng và không lỗi. Hãy import ngay, cấu hình các credential, và để n8n làm việc thay bạn – tiết kiệm thời gian, tăng hiệu quả và duy trì thương hiệu nhất quán trên mọi kênh xã hội!