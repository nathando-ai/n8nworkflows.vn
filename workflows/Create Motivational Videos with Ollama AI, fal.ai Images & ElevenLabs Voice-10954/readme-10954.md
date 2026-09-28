---
title: "🚀 Tự động tạo video truyền cảm hứng với Ollama AI, fal.ai & ElevenLabs"
description: "Workflow n8n tạo video động lực từ văn bản, sinh ảnh fal.ai, lồng tiếng ElevenLabs và ghép video chỉ trong vài phút, không cần viết code."
slug: "tu-dong-tao-video-truyen-cam-hung-ollama-fal-ai-elevenlabs"
tags: [n8n, automation, no-code, content-creation, multimodal-ai]
keywords: [n8n workflow, tự động tạo video, AI video, Ollama, ElevenLabs, fal.ai]
---

# 🚀 Tự động tạo video truyền cảm hứng với Ollama AI, fal.ai & ElevenLabs

Bạn đã bao giờ muốn sản xuất **video truyền cảm hứng** cho fanpage, kênh YouTube hay newsletter nhưng lại bị kẹt ở bước viết kịch bản, tạo hình ảnh, lồng tiếng và ghép video?  
Việc thực hiện thủ công mất hàng giờ, dễ sai sót và chi phí thuê dịch vụ thiết kế quá cao.  

**Workflow này** sẽ giải quyết toàn bộ chuỗi công việc **tự động 100 %** chỉ bằng một cú click:  
1️⃣ Nhập nội dung (câu châm ngôn, lời khuyên…) vào Google Sheet.  
2️⃣ Ollama AI viết kịch bản, fal.ai sinh hình ảnh minh hoạ, ElevenLabs tạo giọng nói tự nhiên.  
3️⃣ Các API video xử lý (concatenate, trim, caption) tự động ghép thành video hoàn chỉnh, sẵn sàng tải xuống hoặc đăng lên mạng xã hội.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ 2‑3 giờ thủ công giảm còn <5 phút.  
- **Độ chính xác cao**: Nội dung, hình ảnh và giọng nói luôn đồng nhất nhờ AI.  
- **Tùy biến linh hoạt**: Thay đổi prompt, màu sắc, phong cách giọng nói chỉ bằng một ô trong Sheet.  
- **Hoạt động liên tục**: Workflow có thể chạy tự động mỗi ngày, tạo video mới mỗi sáng.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản n8n** (Self‑hosted hoặc Cloud).  
- **API key Ollama** (đối với `lmChatOllama`).  
- **API key fal.ai** (image generation).  
- **API key ElevenLabs** (voice synthesis).  
- **API key video service** (concatenate, trim, caption – tùy nhà cung cấp).  
- **Google Sheet** chứa cột: `Prompt`, `Status`, `Video URL` (có quyền chỉnh sửa).  
- **Kết nối internet ổn định** cho các request HTTP.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n > Workflows > Import**.  
2. Tải file JSON của workflow (được cung cấp ở phần cuối README) hoặc **Copy/Paste** toàn bộ JSON vào ô **Import from Clipboard**.  
3. Nhấn **Import** → workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần thay đổi |
|------|---------|-----------------------|
| **When clicking ‘Execute workflow’** | Manual trigger – khởi động workflow. | Không cần thay đổi. |
| **Set Variables** | Đặt các biến toàn cục (API URLs, model names…). | Cập nhật `Ollama URL`, `fal.ai URL`, `ElevenLabs URL` và các key. |
| **Get row(s) in sheet** | Lấy dữ liệu từ Google Sheet. | Chọn **Google Sheets Credential**, nhập **Spreadsheet ID** và **Sheet Name**. |
| **Basic LLM Chain** | Gọi Ollama Chat Model để viết kịch bản. | Chọn **Ollama Credential**, nhập **Model Name** (vd: `llama2`). |
| **Structured Output Parser** | Chuyển đổi output Ollama thành JSON (title, script…). | Đảm bảo **Schema** khớp với prompt. |
| **Image Gen** | Gửi prompt tới fal.ai để sinh ảnh. | Chọn **fal.ai Credential**, nhập **API Key** và **Model** (vd: `stable-diffusion`). |
| **Voice Gen1** → **Get Voice** | Tạo file âm thanh bằng ElevenLabs. | Chọn **ElevenLabs Credential**, nhập **Voice ID** và **API Key**. |
| **Generate Video**, **Concatenate Video**, **Trim Video**, **Caption Video**, **Combine Audio + Video** | Các request HTTP tới dịch vụ video (ví dụ: **Pexels**, **Shotstack**, **Ziggeo**…). | Cập nhật **Endpoint URL**, **Headers** (Authorization) và **Body** theo tài liệu dịch vụ bạn dùng. |
| **Merge** | Gộp dữ liệu hình ảnh, âm thanh, video lại với nhau. | Kiểm tra **Mode** (e.g., `append`) để đảm bảo thứ tự đúng. |
| **Ollama Chat Model** | Node cuối cùng của chain, dùng để kiểm tra hoặc tạo nội dung phụ. | Không bắt buộc, chỉ cần credential đúng. |

> **⚠️ Lưu ý:** Mỗi node `httpRequest` có thể yêu cầu **multipart/form‑data** hoặc **JSON** tùy API. Kiểm tra lại **Headers** (`Content-Type`) và **Body** mẫu trong tài liệu API.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhập một dòng mẫu vào Google Sheet (ví dụ: “Bạn có thể làm được”).  
2. Click **Execute workflow** → quan sát log từng node trong **Execution List**.  
3. Kiểm tra **Video URL** được ghi lại trong Sheet; mở link để xác nhận video hoàn chỉnh.  
4. Khi mọi thứ ổn, bật **Active** → workflow sẽ sẵn sàng chạy tự động (có thể kết hợp với **Cron** hoặc **Webhook**).

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động lên lịch**: Thêm node **Cron** để chạy mỗi sáng 8h, tự động tạo video “Quote of the Day”.  
- **Kết nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi video ngay sau khi tạo xong.  
- **Lưu log chi tiết**: Dùng node **Google Sheets** hoặc **Airtable** ghi lại thời gian, prompt, token usage của Ollama và ElevenLabs.  
- **Tối ưu chi phí**: Đặt **maxTokens** và **temperature** hợp lý trong Ollama để giảm token tiêu thụ.  
- **Thêm phụ đề đa ngôn ngữ**: Sử dụng **Google Translate API** trước khi gọi `Caption Video` để tạo phụ đề tiếng Anh, tiếng Việt, …  

### 📌 Kết luận
Với workflow **“Create Motivational Videos with Ollama AI, fal.ai Images & ElevenLabs Voice”**, các sếp có thể **biến ý tưởng thành video chất lượng chỉ trong vài phút**, giảm chi phí sản xuất nội dung, tăng tần suất đăng tải và duy trì tương tác người xem. Đừng chần chừ, hãy import ngay, cấu hình các API key và để AI làm việc cho bạn! 🚀

---  

**File JSON workflow** (để import):  
```json
{
  "nodes": [
    {"name":"When clicking ‘Execute workflow’","type":"n8n-nodes-base.manualTrigger","position":[250,300]},
    {"name":"Set Variables","type":"n8n-nodes-base.set","position":[450,300]},
    {"name":"Split Out","type":"n8n-nodes-base.splitOut","position":[650,300]},
    {"name":"Create Array with Videos","type":"n8n-nodes-base.code","position":[850,300]},
    {"name":"Split Items","type":"n8n-nodes-base.splitOut","position":[1050,300]},
    {"name":"Build Video Array","type":"n8n-nodes-base.code","position":[1250,300]},
    {"name":"Generate Video","type":"n8n-nodes-base.httpRequest","position":[1450,300]},
    {"name":"Build Faceless Array","type":"n8n-nodes-base.code","position":[1650,300]},
    {"name":"Concatenate Video","type":"n8n-nodes-base.httpRequest","position":[1850,300]},
    {"name":"Trim Video","type":"n8n-nodes-base.httpRequest","position":[2050,300]},
    {"name":"Get Audio Metadata","type":"n8n-nodes-base.httpRequest","position":[2250,300]},
    {"name":"Caption Video","type":"n8n-nodes-base.httpRequest","position":[2450,300]},
    {"name":"Combine Audio + Video","type":"n8n-nodes-base.httpRequest","position":[2650,300]},
    {"name":"Basic LLM Chain","type":"@n8n/n8n-nodes-langchain.chainLlm","position":[2850,300]},
    {"name":"Structured Output Parser","type":"@n8n/n8n-nodes-langchain.outputParserStructured","position":[3050,300]},
    {"name":"Image Gen","type":"n8n-nodes-base.httpRequest","position":[3250,300]},
    {"name":"Voice Gen1","type":"n8n-nodes-base.httpRequest","position":[3450,300]},
    {"name":"Get Voice","type":"n8n-nodes-base.httpRequest","position":[3650,300]},
    {"name":"Get row(s) in sheet","type":"n8n-nodes-base.googleSheets","position":[3850,300]},
    {"name":"Image Scripts","type":"n8n-nodes-base.set","position":[4050,300]},
    {"name":"Audio Scripts","type":"n8n-nodes-base.set","position":[4250,300]},
    {"name":"Code2","type":"n8n-nodes-base.code","position":[4450,300]},
    {"name":"Code3","type":"n8n-nodes-base.code","position":[4650,300]},
    {"name":"Image Get","type":"n8n-nodes-base.httpRequest","position":[4850,300]},
    {"name":"Code","type":"n8n-nodes-base.code","position":[5050,300]},
    {"name":"Code1","type":"n8n-nodes-base.code","position":[5250,300]},
    {"name":"Merge","type":"n8n-nodes-base.merge","position":[5450,300]},
    {"name":"Ollama Chat Model","type":"@n8n/n8n-nodes-langchain.lmChatOllama","position":[5650,300]}
  ],
  "connections": {}
}
```