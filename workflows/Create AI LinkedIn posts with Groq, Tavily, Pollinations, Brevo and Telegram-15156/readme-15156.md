---
title: "🚀 Tự động tạo bài đăng LinkedIn AI với Groq, Tavily, Pollinations, Brevo & Telegram"
description: "Giải pháp không-code giúp các marketer, founder và content creator tạo bài LinkedIn, hình ảnh kèm theo, gửi Telegram, email và lưu Notion chỉ trong vài giây."
slug: "tu-dong-tao-bai-dang-linkedin-ai-groq-tavily-pollinations-brevo-telegram"
tags: [n8n, automation, no-code, AI, content-creation, LinkedIn]
keywords: [n8n workflow, tự động hóa, LinkedIn AI, tạo nội dung, AI image generation]
---

# 🚀 Tự động tạo bài đăng LinkedIn AI với Groq, Tavily, Pollinations, Brevo & Telegram

Bạn đã từng mất hàng giờ để **nghiên cứu chủ đề**, **viết nội dung**, **tìm hình ảnh phù hợp**, rồi mới **đăng lên LinkedIn**?  
Quá trình này không chỉ tốn thời gian mà còn dễ gây sai sót, thiếu tính nhất quán và không thể tái sử dụng.  

Workflow này sẽ **tự động hoá 100%** quy trình trên **không cần viết một dòng code nào**. Bạn chỉ cần điền đề tài, đối tượng và tông giọng trong một form, hệ thống sẽ:

1. Tìm kiếm thông tin mới nhất qua **Tavily**.  
2. Viết bài LinkedIn chuẩn SEO bằng **Groq LLM**.  
3. Tạo prompt hình ảnh và lấy ảnh chất lượng từ **Pollinations**.  
4. Gửi bài + ảnh tới **Telegram** để bạn duyệt nhanh.  
5. Email bản hoàn thiện qua **Brevo**.  
6. Lưu toàn bộ nội dung vào **Notion** để quản lý và tái sử dụng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 30‑60 phút giảm còn < 5 phút mỗi bài.  
- **Độ chính xác cao**: Dữ liệu được cập nhật từ web ngay lập tức, giảm rủi ro thông tin lỗi thời.  
- **Nội dung nhất quán, cá nhân hoá**: Tông giọng, đối tượng và phong cách được tùy chỉnh theo form.  
- **Hoạt động liên tục 24/7**: Không cần can thiệp thủ công, workflow tự chạy khi có yêu cầu.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Groq API Key** (đăng ký miễn phí tại console.groq.com).  
- **Tavily API Key** (miễn phí tại tavily.com).  
- **Brevo (Sendinblue) SMTP credentials** (đăng ký tại brevo.com).  
- **Telegram Bot Token** + **Chat ID** (tạo bot qua BotFather).  
- **Notion Integration Token** và **Database ID** (cần quyền `Insert` vào database).  
- **Pollinations API endpoint** (không cần key, chỉ URL).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n (self‑hosted hoặc cloud).  
2. Vào **Workflows → Import**.  
3. Chọn **Upload JSON** và tải file `Create AI LinkedIn posts.json` (hoặc copy toàn bộ JSON từ trang gốc).  
4. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Loại | Cấu hình cần chỉnh |
|------|------|-------------------|
| **LinkedIn Post Form** | `formTrigger` | - Thêm 3 trường: **Topic**, **Audience**, **Tone**.<br>- Đặt **Method** = `POST` và **Path** tùy ý (ví dụ: `/linkedin-form`). |
| **Generate LinkedIn Post** | `agent` | - Chọn **LLM** = **Groq LLM**.<br>- Prompt mẫu: `Write a LinkedIn post about {{ $json["topic"] }} for {{ $json["audience"] }} in a {{ $json["tone"] }} tone. Include a hook and a call‑to‑action.` |
| **Create Image Prompt** | `agent` | - Chọn **LLM** = **Groq LLM**.<br>- Prompt mẫu: `Create a concise image prompt for an illustration that matches the LinkedIn post: "{{ $node["Generate LinkedIn Post"].json["content"] }}".` |
| **Groq LLM** | `lmChatGroq` | - **Credentials**: `groqApi` (điền API key).<br>- **Model**: `llama-3.3-70b-versatile` (đã có trong workflow). |
| **Fetch AI Image** | `httpRequest` | - **Method**: `GET`.<br>- **URL**: `https://image.pollinations.ai/prompt/{{ encodeURIComponent($node["Create Image Prompt"].json["prompt"]) }}`.<br>- **Response Format**: `File` (để lấy URL ảnh). |
| **Tavily Web Search** | `httpRequestTool` | - **Method**: `GET`.<br>- **URL**: `https://api.tavily.com/search`.<br>- **Headers**: `Authorization: Bearer <TAVILY_API_KEY>`.<br>- **Query Params**: `query={{ $json["topic"] }}`.<br>- **Parse**: Lấy phần `results` để truyền vào prompt nếu cần. |
| **Send Email via Brevo** | `emailSend` | - **Credentials**: `smtp` (điền host, port, user, password).<br>- **To**: email của bạn.<br>- **Subject**: `LinkedIn Post – {{ $json["topic"] }}`.<br>- **HTML Body**: chèn nội dung bài và `<img src="{{ $node["Fetch AI Image"].json["url"] }}">`. |
| **Log Post in Notion** | `notion` | - **Credentials**: `notionApi`.<br>- **Resource**: `databasePage`.<br>- **Database ID**: ID của database lưu bài.<br>- **Properties Mapping**: Title → `Post Title`, Rich Text → `Content`, URL → `Image URL`, Date → `Created`. |
| **Send Image to Telegram** | `telegram` | - **Credentials**: `telegramApi` (Bot Token).<br>- **Operation**: `sendPhoto`.<br>- **Chat ID**: ID của kênh/nhóm.<br>- **Photo**: `{{ $node["Fetch AI Image"].json["url"] }}`.<br>- **Caption**: `{{ $node["Generate LinkedIn Post"].json["content"] }}`. |
| **Send Post to Telegram** | `telegram` | - **Credentials**: `telegramApi`.<br>- **Operation**: `sendMessage`.<br>- **Chat ID**: cùng chat ID trên.<br>- **Text**: `{{ $node["Generate LinkedIn Post"].json["content"] }}`. |

> **Lưu ý:** Đảm bảo các node **agent** (Generate LinkedIn Post & Create Image Prompt) đều được liên kết tới **Groq LLM** để sử dụng cùng model và credentials.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → nhập dữ liệu mẫu (ví dụ: Topic = “AI trong marketing”, Audience = “Marketers”, Tone = “Professional”).  
2. Kiểm tra:  
   - Kết quả trả về từ Groq có nội dung hợp lý.  
   - Ảnh từ Pollinations hiển thị đúng.  
   - Email, Telegram và Notion nhận được dữ liệu.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ sẵn sàng nhận yêu cầu từ form.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack**: Thêm node `Slack` để gửi bản nháp tới kênh nội bộ trước khi đăng LinkedIn.  
- **Lưu log chi tiết**: Dùng node `Google Sheets` hoặc `Airtable` để ghi lại thời gian chạy, số lần tìm kiếm Tavily, và token chi phí.  
- **Định kỳ báo cáo**: Thêm `Cron` trigger (hàng tuần) để tổng hợp các bài đã đăng và gửi báo cáo PDF qua Brevo.  
- **Tối ưu prompt**: Sử dụng `Prompt Engineering` trong node `agent` để tùy chỉnh độ dài, số lượng hashtag, hoặc CTA cụ thể cho từng ngành.  

### 📌 Kết luận
Với workflow này, **các sếp** có thể biến việc tạo nội dung LinkedIn thành một chuỗi tự động, nhanh chóng và chuẩn xác, đồng thời lưu trữ, chia sẻ và theo dõi mọi bài viết một cách chuyên nghiệp. Hãy **import ngay**, cấu hình các credential và để n8n lo phần còn lại – bạn sẽ có thêm thời gian tập trung vào chiến lược và sáng tạo! 🚀