---
title: "🚀 Tự động tạo nội dung AI cho dịch vụ ô tô – Đăng bài trên mạng xã hội tự động"
description: "Workflow n8n tự động lấy dữ liệu từ Google Sheets, sinh bài viết và hình ảnh bằng AI, sau đó đăng lên Twitter, LinkedIn, Facebook và Telegram, giúp doanh nghiệp ô tô duy trì presença online 24/7 mà không cần can thiệp thủ công."
slug: "tu-dong-tai-noi-dung-ai-cho-dich-vu-o-to"
tags: [n8n, automation, no-code, AI content generation, social media automation, auto service]
keywords: [n8n workflow, tự động hóa, AI content, social media, auto service, marketing automation]
---

# 🚀 Tự động tạo nội dung AI cho dịch vụ ô tô – Đăng bài trên mạng xã hội tự động

Làm việc trong ngành ô tô đòi hỏi bạn phải luôn cập nhật tin tức, chia sẻ kiến thức về bảo dưỡng, sửa chữa và các chương trình khuyến mãi. Nhưng việc viết bài, tìm hình ảnh và đăng lên từng kênh mạng xã hội mỗi ngày tốn nhiều thời gian và dễ bị lỗi. Workflow **AI content generation for Auto Service** giải quyết triệt để vấn đề này: nó tự động lấy ý tưởng từ Google Sheets, sử dụng các mô hình LLM và AI sinh ảnh để tạo bài viết + hình ảnh chất lượng, rồi đăng ngay lên Twitter, LinkedIn, Facebook và Telegram – tất cả mà không cần viết một dòng code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ mỗi tuần**: Không cần nghĩ nội dung, tìm ảnh hoặc đăng tay.
- **Độ nhất quán cao**: Bài viết và hình ảnh được tạo theo quy trình chuẩn, giảm lỗi chính tả hoặc hình ảnh không phù hợp.
- **Cá nhân hóa linh hoạt**: Dễ dàng thay đổi prompt, model LLM hoặc nguồn dữ liệu để phù hợp với từng chiến dịch.
- **Hoạt động liên tục**: Kích hoạt bằng Schedule Trigger hoặc Manual Trigger, đăng bài ngay cả khi bạn đang nghỉ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, bạn cần chuẩn bị các credentials / API keys sau (tương ứng với các node trong workflow):

- **Telegram** – `telegramApi` (Bot Token)
- **Google Sheets** – `googleSheetsTriggerOAuth2Api` (OAuth2 Zugang tới Google Sheets)
- **Mistral Cloud** – `mistralCloudApi` (API Key Mistral)
- **OpenRouter** – `openRouterApi` (API Key OpenRouter)
- **Anthropic** – `anthropicApi` (API Key Claude) – *node được liệt kê nhưng cần credential*
- **Google Gemini** – `googleGeminiApi` (API Key Gemini)
- **xAI Grok** – `xAiGrokApi` (API Key Grok)
- **DeepSeek** – `deepSeekApi` (API Key DeepSeek)
- **Hugging Face Inference** – `huggingFaceApi` (Access Token HuggingFace)
- **HTTP Bearer Auth** – `httpBearerAuth` (Bearer Token cho Clipdrop API)
- **APITemplate.io** – `apiTemplateIoApi` (API Key APITemplate)
- **Tavily** – `tavilyApi` (API Key Tavily Internet Search)
- **OpenAI** – `openAiApi` (API Key OpenAI – dùng cho GPT‑4.1 và GPT Image 1)
- **Facebook Graph API** – `facebookOAuth2Api` (Access Token Fanpage)
- **Twitter (X)** – `twitterOAuth2Api` (OAuth2 Token / API Key + Secret)
- **LinkedIn** – `linkedInOAuth2Api` (Access Token)

Ngoài ra, nếu bạn muốn sử dụng các dịch vụ sinh ảnh khác (Freepik, Runware, Ideogram, Replicate, Imagen Google, Runway, Minimax, Kling, Leonardo…) cần chuẩn bị API keys tương ứng và thêm vào các node **HTTP Request** nếu chưa có sẵn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Trong n8n Editor, nhấn **Import** → **From URL** hoặc **Upload file** và chọn file JSON của workflow.
2. Hoặc sao chép toàn bộ JSON từ trang workflow và dán vào ô **Import from Clipboard**.
3. Nhấn **Import** – n8n sẽ tự động tạo tất cả các node và kết nối.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, bạn **phải** kiểm tra và cấu hình các node sau:

| Node | Cần cấu hình | Ghi chú |
|------|--------------|---------|
| **Schedule Trigger** | Đặt cron (ví dụ: `0 9 * * *` để chạy hàng ngày 9h sáng) hoặc chọn interval. | Nếu muốn chạy thủ công, giữ Manual Trigger và tắt Schedule Trigger. |
| **Google Sheets Trigger** | Chọn **Spreadsheet ID** và **Worksheet** chứa cột: `Topic`, `Keywords`, `Preferred Tone` (hoặc bất kỳ cột nào bạn dùng). | Đảm bảo sheet có quyền truy cập cho OAuth2 credential đã cấu hình. |
| **Split Out** | Kiểm tra trường **Input** là `$json` từ Google Sheets Trigger để tách từng hàng thành một item. | Thường không cần thay đổi nếu cấu trúc sheet không đổi. |
| **LLM Nodes** (Mistral Cloud, OpenRouter, Anthropic, Google Gemini, xAI Grok, DeepSeek, Ollama, Azure OpenAI, HuggingFace) | - Chọn **Credential** tương ứng.<br>- Đặt **Model** (nếu node cho phép) – ví dụ Mistral: `pixtral-large-latest`, OpenAI: `gpt-4.1`.<br>- Điều chỉnh **Temperature**, **Max Tokens** nếu cần. | Bạn có thể bật/tắt bất kỳ node nào để chọn model ưu tiên. |
| **OPENAI WRITES PROMPTS** & **OPENAI WRITES POSTS** (lmChatOpenAi) | Credential `openAiApi`; Model `gpt-4.1` (đã được preselect). | Edit **System Message** và **Prompt** để phù hợp với ngành ô tô (ví dụ: “Bạn là chuyên gia nội dung ô tô, viết bài ngắn, hấp dẫn, không chứa văn bản trên hình ảnh”). |
| **GENERATE TEXT** & **GENERATE PROMPT** (Agent) | - Kết nối với **Tavily Internet Search** (cần credential `tavilyApi`) để truy xuất thông tin mới nhất.<br>- Đặt **System Prompt** cho agent (ví dụ: “Tìm kiếm thông tin mới nhất về xe ô tô và tóm tắt thành 2‑3 câu”). | Đảm bảo node Tavily được kết nối đúng vào agent. |
| **OPENAI GENERATES IMAGE** (openAi) | Credential `openAiApi`; Resource `Image`; Model `gpt-image-1`.<br>Prompt: `= IMPORTANT! DONT WRITE TEXT ON A PICTURE! Create perfect visual for\n{{ $json.output }}` – đây là chuỗi lấy từ node trước (bài viết hoặc prompt). | Kiểm tra xem `{{ $json.output }}` thực sự chứa mô tả hình ảnh bạn muốn. |
| **Các node HTTP Request ảnh** (Freepik, Runware, Clipdrop, Ideogram, Replicate, Imagen Google, Runway, Minimax, Kling, Leonardo…) | - Điền **Endpoint URL** (đã có sẵn trong node).<br>- Thêm **Headers** (Authorization Bearer, API Key) nếu cần – thường đã được cấu hình qua credential `httpBearerAuth` hoặc riêng.<br>- Đặt **Body** (JSON) chứa prompt từ node trước. | Nếu không dùng dịch vụ nào, bạn có thể xóa node đó hoặc bỏ qua kết nối. |
| **APITemplate.io** | Credential `apiTemplateIoApi`; chọn template đã chuẩn bị sẵn (nếu có). | Dùng để kết hợp hình ảnh và văn bản thành một file cuối cùng trước khi đăng. |
| **Twitter (X)**, **LinkedIn**, **Facebook** | - Credential tương ứng (`twitterOAuth2Api`, `linkedInOAuth2Api`, `facebookOAuth2Api`).<br>- Trong node: map **Message** = `{{ $json.output }}` (bài viết từ OPENAI WRITES POSTS).<br>- Đính kèm **Image URL** từ node sinh ảnh (thường là output của APITemplate.io hoặc trực tiếp từ OpenAI Image). | Đảm bảo bạn đã cấp quyền đăng bài cho trang/ Fanpage tương ứng. |
| **Telegram** | Credential `telegramApi`; Operation `Send Photo`.<br>- **Chat ID**: ID kênh hoặc nhóm bạn muốn đăng.<br>- **Photo**: URL hình ảnh từ node trước.<br>- **Caption**: Bài viết từ OPENAI WRITES POSTS. | Test bằng nút “Execute Node” để xem tin nhắn gửi đúng chưa. |

> **Lưu ý quan trọng**: Sau mỗi thay đổi credential hoặc prompt, hãy nhấn **Execute Workflow** (Manual Trigger) để chạy thử với một dòng dữ liệu từ Google Sheets trước khi bật lịch.

#### 3. Kích hoạt ⚡️
1. Chọn một hàng trong Google Sheets (hoặc dùng nút **Execute Workflow** để chạy với dữ liệu mẫu).  
2. Kiểm tra từng bước qua thanh thực thi (Execution List) – đảm bảo không có node lỗi.  
3. Nếu mọi thứ ổn, bật toggle **Active** ở góc trên‑phải workflow.  
4. workflow sẽ chạy tự động theo lịch bạn đã đặt ( hoặc bạn có thể kích hoạt thủ công khi cần ).

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack sau mỗi đăng thành công để팀 được thông báo