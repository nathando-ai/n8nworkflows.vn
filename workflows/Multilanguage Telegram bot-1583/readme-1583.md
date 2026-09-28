---
title: "🚀 Bot Telegram Đa Ngôn Ngữ Tự Động - N8N Workflow"
description: "Tự động trả lời đa ngôn ngữ trên Telegram, quản lý người dùng và từ điển bằng NocoDB, giảm 90% thời gian hỗ trợ thủ công."
slug: "bot-telegram-da-ngon-ngu-n8n"
tags: [n8n, automation, no-code, telegram, nocodb]
keywords: [n8n workflow, tự động hóa, bot telegram, đa ngôn ngữ, nocodb]
---

# 🚀 Bot Telegram Đa Ngôn Ngữ Tự Động - N8N Workflow

Bạn đã từng phải trả lời cùng một câu hỏi trên Telegram bằng nhiều ngôn ngữ khác nhau?  
Mỗi lần người dùng chuyển ngôn ngữ, bạn lại phải dừng công việc hiện tại, mở Google Translate, sao chép‑dán…  
Kết quả: **lãng phí thời gian, sai sót khi dịch, và mất cơ hội tương tác nhanh chóng**.

Workflow **Multilanguage Telegram bot** (tác giả Eduard) giải quyết vấn đề này 100% **không cần viết code**:  
- Nhận tin nhắn từ Telegram, tự động phát hiện ngôn ngữ và trả lời bằng ngôn ngữ tương ứng.  
- Quản lý danh sách người dùng và từ điển đa ngôn ngữ trên **NocoDB**.  
- Tự động thêm mới hoặc cập nhật thông tin người dùng khi họ lần đầu trò chuyện.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: trả lời ngay lập tức, không cần mở công cụ dịch.  
- **Độ chính xác cao**: dùng từ điển đã được chuẩn hoá trong NocoDB.  
- **Cá nhân hoá**: lưu lịch sử người dùng, gửi lời chào riêng khi họ quay lại.  
- **Hoạt động liên tục**: bot luôn online, không phụ thuộc vào máy cá nhân.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
1. **Telegram Bot Token** – tạo bot qua @BotFather, lấy `API Token`.  
2. **NocoDB API URL & API Key** – tạo project, bật API, lấy `Base URL` và `Authorization Header`.  
3. **Credentials trong n8n**  
   - `telegramApi` (Telegram Bot Token)  
   - `nocoDb` (NocoDB Base URL + API Key)  
   - `httpHeaderAuth` (Header `Authorization: Bearer <API_KEY>` cho các node HTTP).  
4. **Cơ sở dữ liệu NocoDB**  
   - Table **Users** (cột: `chatId`, `firstName`, `language`, `lastSeen`).  
   - Table **Dictionary** (cột: `key`, `vi`, `en`, `es`, …).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file `multilanguage-telegram-bot.json` (được export từ link gốc).  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard** và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và hướng dẫn cấu hình chi tiết:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Telegram Trigger** | `telegramTrigger` | Chọn credential `telegramApi`. Đặt **Chat Type** = `private`. |
| **chatID** | `function` | Không cần thay đổi, node này trích xuất `chatId` từ `msg` của trigger. |
| **New user?** | `function` | Kiểm tra xem `chatId` đã tồn tại trong bảng Users chưa. Không cần thay đổi. |
| **CheckUser** | `nocoDb` (getAll) | Credential `nocoDb`. **Table** = `Users`. **Filter**: `chatId = {{$json["chatId"]}}`. |
| **LoadDictionary** | `nocoDb` (getAll) | Credential `nocoDb`. **Table** = `Dictionary`. Không cần filter. |
| **Switch** | `switch` | Dựa trên `msg.command` (greeting, help, …) để định hướng luồng. Không cần thay đổi. |
| **IF** | `if` | Kiểm tra `msg.command` có phải là `start`/`help`/… không. |
| **Merge** | `merge` | Gộp dữ liệu người dùng và từ điển để tạo phản hồi. Không cần thay đổi. |
| **botmessages** | `function` | Tạo nội dung trả lời dựa trên ngôn ngữ người dùng và từ điển. Có thể tùy chỉnh mẫu câu. |
| **msg_greet** | `telegram` | Credential `telegramApi`. **Chat ID** = `{{$json["chatId"]}}`. **Message** = `{{$json["text"]}}` (được truyền từ `botmessages`). |
| **msg_welcomeback** | `telegram` | Tương tự `msg_greet`, dùng khi người dùng quay lại. |
| **msg_help** | `telegram` | Nội dung hướng dẫn sử dụng bot. |
| **msg_wrongcommand** | `telegram` | Thông báo lệnh không hợp lệ. |
| **HTTP AddUser** | `httpRequest` | **Method** = `POST`. **URL** = `{{ $credentials.nocoDb.baseUrl }}/api/v1/db/data/v1/<project>/<Users>`.<br>**Headers**: `Authorization: Bearer <API_KEY>`, `Content-Type: application/json`.<br>**Body**: JSON chứa `chatId`, `firstName`, `language`, `lastSeen`. |
| **HTTP UpdateUser** | `httpRequest` | **Method** = `PATCH`. **URL** = `{{ $credentials.nocoDb.baseUrl }}/api/v1/db/data/v1/<project>/<Users>/<recordId>`.<br>**Headers** tương tự. |
| **AddUser** | `nocoDb` (create) | Credential `nocoDb`. **Table** = `Users`. **Data**: `chatId`, `firstName`, `language`, `lastSeen`. |
| **UpdateUser** | `nocoDb` (update) | Credential `nocoDb`. **Table** = `Users`. **Record ID** = `{{$json["id"]}}`. **Data**: cập nhật `lastSeen`, `language` nếu thay đổi. |

> **Lưu ý:** Do một số thay đổi API của NocoDB (tháng 5/2022), các node `nocoDb` **getAll** vẫn hoạt động, nhưng **create** và **update** có thể cần chuyển sang node **HTTP Request** (đã có sẵn trong workflow). Nếu gặp lỗi, hãy kiểm tra URL và header theo mẫu trên.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi tin nhắn `/start` tới bot, kiểm tra phản hồi chào mừng.  
2. Kiểm tra bảng **Users** trong NocoDB – bản ghi mới phải được tạo.  
3. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  

### ✍️ Mẹo & gợi ý nâng cao
- **Ghi log chi tiết**: Thêm node `Google Sheets` hoặc `Airtable` để lưu lịch sử chat, giúp phân tích hành vi người dùng.  
- **Thông báo Slack/Telegram nhóm**: Khi có người dùng mới, gửi tin nhắn tới kênh quản trị để theo dõi.  
- **Tự động dịch bằng LLM**: Thay thế bảng Dictionary bằng OpenAI / Claude để dịch động, mở rộng ngôn ngữ không giới hạn.  
- **Báo cáo định kỳ**: Dùng node `Cron` + `HTTP Request` để gửi báo cáo số lượng người dùng, tần suất sử dụng mỗi tuần qua email.  

### 📌 Kết luận
Với workflow **Multilanguage Telegram bot**, các sếp có thể triển khai ngay một trợ lý ảo đa ngôn ngữ, tự động quản lý người dùng và trả lời nhanh chóng mà không cần viết một dòng code nào. Hãy import, cấu hình credentials, bật workflow và để bot làm việc thay bạn ngay hôm nay! 🚀