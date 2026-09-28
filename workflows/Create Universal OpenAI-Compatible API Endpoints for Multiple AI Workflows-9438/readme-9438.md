---
title: "🚀 Tạo API OpenAI Tương Thích Đa Năng cho Nhiều Workflow AI"
description: "Giải pháp không code giúp bạn biến mọi workflow n8n thành các endpoint OpenAI /models và /chat/completions chỉ trong vài phút."
slug: "tao-api-openai-tuong-thich-nhiem-vu-ai"
tags: [n8n, automation, no-code, AI, OpenAI, workflow]
keywords: [n8n workflow, tự động hóa, OpenAI API, AI workflow, no-code integration]
---

# 🚀 Tạo API OpenAI Tương Thích Đa Năng cho Nhiều Workflow AI

Bạn có bao giờ phải **tự tay viết code** để đưa các workflow AI của n8n lên thành các endpoint giống OpenAI?  
Mỗi khi muốn mở rộng, phải sửa lại URL, định dạng JSON, xử lý streaming… công việc tẻ nhạt, tốn thời gian và dễ gây lỗi.  

**Workflow này** là giải pháp “**plug‑and‑play 100 % không code**” giúp bạn:

* Tạo một endpoint **GET /youragents/models** liệt kê tất cả các mô hình (workflow) được gắn thẻ `aimodel`.  
* Tạo một endpoint **POST /youragents/chat/completions** thực hiện chat completion, tự động phát hiện **stream** hay **non‑stream** và trả về định dạng chuẩn OpenAI.  
* Tất cả chỉ cần **import** file JSON và cấu hình vài credential – không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: chỉ vài phút để có 2 endpoint OpenAI chuẩn.  
- **Độ chính xác cao**: dữ liệu luôn được map đúng schema, giảm lỗi client.  
- **Tích hợp liền mạch**: các ứng dụng hiện có (ChatGPT UI, Postman, VSCode) có thể gọi ngay mà không thay đổi code.  
- **Hoạt động liên tục**: chạy trên n8n server, hỗ trợ streaming và non‑stream đồng thời.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **n8n instance** (Self‑hosted hoặc Cloud) với quyền tạo webhook.  
- **OpenAI Credential** trong n8n (để cấu hình Base URL trỏ tới n8n của bạn).  
- **Tag `aimodel`** được gắn vào các workflow muốn expose dưới dạng mô hình.  
- **API Key** (nếu bạn muốn bảo vệ endpoint bằng authentication).  
- **Node “lmChatOpenAi”** đã được cài đặt (`@n8n/n8n-nodes-langchain`).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file **Create‑Universal‑OpenAI‑API‑Endpoints.json** (được cung cấp trong mục “Download”).  
2. Vào **n8n → Workflows → Import**, kéo file vào hoặc dán nội dung JSON.  
3. Đặt tên workflow: *Create Universal OpenAI‑Compatible API Endpoints*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|---------|--------------------|
| **GET models** (Webhook) | Endpoint `GET /youragents/models` | - `Path`: `youragents/models` <br> - `HTTP Method`: `GET` (mặc định) |
| **POST ChatCompletions** (Webhook) | Endpoint `POST /youragents/chat/completions` | - `Path`: `youragents/chat/completions` <br> - `HTTP Method`: `POST` |
| **Get many workflows** (n8n) | Lấy danh sách workflow có tag `aimodel` | - `Operation`: **Get All** <br> - `Filters → Tags`: `aimodel` |
| **Edit Fields** (Set) | Định dạng lại dữ liệu workflow thành schema OpenAI | - Đặt các trường `id`, `object`, `owned_by`, `permission` … theo mẫu OpenAI. |
| **Remap to Response API Schema** (Code) | Chuyển đổi kết quả từ `Get many workflows` sang dạng JSON `/models`. | - Không cần thay đổi code nếu bạn giữ nguyên cấu trúc. |
| **Is Stream?** (If) | Kiểm tra header `stream` trong request để quyết định trả về `text/plain` hay JSON. | - Điều kiện: `{{$json["stream"]}} === true` |
| **Format Completion Response** (Code) | Định dạng response cho **non‑stream** (JSON). | - Kiểm tra và chỉnh `return` nếu muốn tùy biến. |
| **Format Stream Response** (Code) | Định dạng response cho **stream** (plain text). | - Đảm bảo `Content-Type: text/event-stream`. |
| **Call workflow webhook** / **Call workflow webhook1** (HTTP Request) | Gửi request tới workflow nội bộ để thực thi mô hình. | - `URL`: `{{ $node["When chat message received"].webhookUrl }}` <br> - `Method`: `POST` |
| **n8n Webhooks** (lmChatOpenAi) | Kết nối mô hình OpenAI (được gọi bởi endpoint). | - `Model`: nhập tên mô hình (ví dụ: `youragentname`) <br> - **Credential**: chọn **OpenAI** → **Custom Base URL** = `https://<your‑n8n‑domain>/webhook`. |
| **When chat message received** (chatTrigger) | Bắt đầu quá trình chat khi có tin nhắn tới. | - Không cần thay đổi, chỉ cần bật. |
| **Powered By n8n Workflow Models** (agent) | Đánh dấu nguồn mô hình. | - Để mặc định. |
| **Simple Memory** (memoryBufferWindow) | Lưu trữ lịch sử chat ngắn hạn. | - `Size`: 10 (hoặc tùy chỉnh). |
| **Models Response** & **JSON Response** / **Text Response** (respondToWebhook) | Trả về kết quả cuối cùng cho client. | - Đảm bảo `Response Mode` = **JSON** hoặc **RAW** tùy vào `Is Stream?`. |

> **Lưu ý:** Sau khi import, **đừng quên** gán **credential OpenAI** cho node `lmChatOpenAi`. Đặt **Base URL** thành `https://<domain‑của‑bạn>/webhook` để các request tới `/youragents/*` được chuyển tiếp đúng.

#### 3. Kích hoạt ⚡️
1. **Test**: Gửi request `GET https://<domain>/webhook/youragents/models` → bạn sẽ nhận danh sách mô hình.  
2. **Test chat**: `POST https://<domain>/webhook/youragents/chat/completions` với payload OpenAI chuẩn. Kiểm tra cả **stream** (`"stream": true`) và **non‑stream**.  
3. Khi mọi thứ ổn, bật **Active** cho workflow (nút **Activate** góc trên bên phải).

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `When chat message received` để nhận tin nhắn từ kênh chat nội bộ.  
- **Lưu log**: Dùng node `Write Binary File` hoặc `Google Sheets` để ghi lại mỗi request/response, hỗ trợ audit.  
- **Báo cáo định kỳ**: Thêm trigger `Cron` để chạy `GET models` mỗi ngày, gửi báo cáo qua email.  
- **Bảo mật**: Đặt **API Key** trong header `Authorization` và kiểm tra trong node `If` trước khi thực hiện workflow.  

### 📌 Kết luận
Với workflow **“Create Universal OpenAI‑Compatible API Endpoints for Multiple AI Workflows”**, các sếp có thể nhanh chóng biến mọi workflow n8n thành các endpoint chuẩn OpenAI, hỗ trợ cả streaming và non‑stream, mà không cần viết một dòng code nào. Hãy **import**, **cấu hình credential**, **test** và **đưa vào production** ngay hôm nay – tiết kiệm thời gian, giảm lỗi và mở rộng khả năng tích hợp AI của doanh nghiệp! 🚀