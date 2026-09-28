---
title: "🚀 Xây dựng Chatbot Llama riêng tư với Ollama, Groq, Slack & Google Sheets"
description: "Tự động hoá chatbot AI nội bộ, kết nối Ollama/Groq, trả lời qua Slack và lưu lịch sử vào Google Sheets chỉ trong vài phút."
slug: "xay-dung-chatbot-llama-ollama-groq-slack-google-sheets"
tags: [n8n, automation, no-code, AI, chatbot, Slack, GoogleSheets]
keywords: [n8n workflow, chatbot AI, Ollama, Groq, Slack integration, Google Sheets]
---

# 🚀 Xây dựng Chatbot Llama riêng tư với Ollama, Groq, Slack & Google Sheets

Doanh nghiệp ngày càng phụ thuộc vào AI để hỗ trợ khách hàng, nhưng **việc triển khai một chatbot nội bộ** thường gặp những rào cản:

* **Chi phí cao** khi mua dịch vụ SaaS trả phí.
* **Rủi ro bảo mật** khi dữ liệu nhạy cảm phải đi qua các máy chủ công cộng.
* **Quá trình tích hợp** phức tạp, đòi hỏi lập trình viên và thời gian dài.

**Workflow n8n** này cho phép các sếp **tự động hoá 100 %** quy trình trả lời khách hàng bằng Llama (Ollama/Groq) qua Slack, đồng thời lưu trữ toàn bộ lịch sử hội thoại vào Google Sheets – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Trả lời tự động ngay khi có tin nhắn Slack.  
- **Độ chính xác cao**: Sử dụng mô hình Llama mạnh mẽ, tùy chỉnh theo dữ liệu nội bộ.  
- **Bảo mật dữ liệu**: Tất cả thông tin chỉ lưu trên VPS và Google Sheets do sếp kiểm soát.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Thành phần | Mô tả | Ghi chú |
|------------|------|--------|
| **n8n** | Phiên bản Self‑hosted hoặc Cloud | Đảm bảo có quyền tạo webhook |
| **Ollama** | Server cài Ollama (hoặc endpoint Groq) | Cần URL và API key (nếu dùng Groq) |
| **Slack** | Workspace + Bot token | Tạo Bot, cấp quyền `chat:write`, `channels:history` |
| **Google Sheets** | Tài khoản Google, tạo bảng tính | Cấp quyền API Google Sheets, tạo Credential JSON |
| **Node.js** (nếu tự host) | Phiên bản >= 18 | Để chạy n8n |
| **API Keys** | Ollama (nếu dùng remote) / Groq API Key | Đặt trong Credential của n8n |
| **Webhook URL** | Được n8n tự sinh | Dùng làm endpoint Slack Events |
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n > Workflows > Import**.  
2. Tải file `llama-chatbot.json` (được cung cấp trong mục **Resources** của workflow gốc) hoặc **Copy/Paste** toàn bộ JSON vào ô import.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Công việc | Cấu hình cần thay đổi |
|------|-----------|-----------------------|
| **Webhook** | Nhận tin nhắn từ Slack (Event Subscriptions) | - URL: để mặc định, copy URL sau khi kích hoạt.<br>- Method: `POST` |
| **If** | Kiểm tra loại sự kiện (message, app_mention, …) | - Điều kiện: `event.type = "message"` |
| **Set** | Chuẩn hoá dữ liệu (user, text, channel) | - Đặt các trường `userId`, `text`, `channelId` |
| **Code** (JavaScript) | Gọi Ollama/Groq API, tạo prompt | - Thay `OLLAMA_URL` hoặc `GROQ_ENDPOINT`.<br>- Thêm `API_KEY` nếu dùng Groq.<br>- Tùy chỉnh `systemPrompt` nếu muốn. |
| **HTTP Request** | Gửi yêu cầu tới Ollama/Groq | - Method: `POST`.<br>- Headers: `Authorization: Bearer <API_KEY>` (nếu cần).<br>- Body: JSON chứa `model`, `messages`. |
| **Google Sheets** | Ghi lại câu hỏi & câu trả lời | - Spreadsheet ID: ID của file Google Sheet.<br>- Sheet Name: tên sheet (ví dụ `ChatLog`).<br>- Credentials: chọn Credential JSON đã tạo. |
| **Slack** | Gửi phản hồi lại kênh Slack | - Credential: Bot Token.<br>- Channel: dùng biến `{{$json["channelId"]}}`.<br>- Text: `{{$json["assistantReply"]}}`. |
| **Respond To Webhook** | Kết thúc vòng trả lời (đối với Slack) | - Đặt `Response Code: 200`. |
| **Sticky Note** | Ghi chú nội bộ | Không cần cấu hình, chỉ để hướng dẫn. |

> **⚠️ Lưu ý quan trọng:**  
> - Đảm bảo **Slack App** đã bật **Event Subscriptions** và đăng ký URL webhook của n8n.  
> - Khi sử dụng **Ollama** cài trên cùng VPS, URL thường là `http://localhost:11434/api/chat`. Nếu dùng **Groq**, URL sẽ là `https://api.groq.com/openai/v1/chat/completions`.  
> - Kiểm tra **quota** của Groq nếu dùng phiên bản miễn phí.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một tin nhắn thử vào kênh Slack đã kết nối. Kiểm tra log trong n8n → xem node `Code` và `HTTP Request` trả về nội dung hợp lý.  
2. Nếu mọi thứ ổn, bật **Active** ở góc phải của workflow.  
3. Theo dõi **Execution Log** để chắc chắn không có lỗi.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Telegram**: Dùng node `Telegram` để đồng thời trả lời trên Telegram và Slack.  
- **Lưu log chi tiết**: Thêm node `Write Binary File` để lưu toàn bộ payload vào S3 hoặc Google Cloud Storage.  
- **Báo cáo định kỳ**: Dùng node `Cron` + `Google Sheets` để tổng hợp số lượng tin nhắn, thời gian phản hồi, gửi báo cáo qua email mỗi tuần.  
- **Tùy chỉnh Prompt**: Thêm node `Set` để lấy `systemPrompt` từ một ô Google Sheet, cho phép các sếp cập nhật hướng dẫn chatbot mà không cần chỉnh workflow.  

### 📌 Kết luận
Với workflow này, các sếp có thể **triển khai nhanh một chatbot Llama nội bộ**, tích hợp liền mạch với Slack và Google Sheets, giảm chi phí, tăng bảo mật và nâng cao năng suất hỗ trợ khách hàng. Đừng chần chừ, **import ngay**, cấu hình các credential cần thiết và bật workflow để trải nghiệm sức mạnh AI tự động hoá! 🚀