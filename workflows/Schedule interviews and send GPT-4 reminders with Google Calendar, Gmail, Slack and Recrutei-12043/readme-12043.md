---
title: "🚀 Tự Động Lên Lịch Phỏng Vấn & Gửi Nhắc Nhở GPT‑4 với Google Calendar, Gmail, Slack & Recrutei"
description: "Workflow n8n tự động tạo lịch phỏng vấn, sinh link Google Meet, soạn email nhắc nhở bằng GPT‑4 và gửi tới ứng viên 24h trước, đồng thời cập nhật trạng thái trên Recrutei."
slug: "tu-dong-len-lich-phong-van-gpt4-google-calendar-gmail-slack-recrutei"
tags: [n8n, automation, no-code, google-calendar, gmail, slack, openai, recrutei]
keywords: [n8n workflow, tự động hóa, lịch phỏng vấn, email tự động, GPT‑4, Recrutei]
---

# 🚀 Tự Động Lên Lịch Phỏng Vấn & Gửi Nhắc Nhở GPT‑4

Bạn đã từng phải **đánh đồng** công việc nhập liệu thủ công: tạo lịch Google Calendar, sao chép link Meet, viết email nhắc nhở, rồi lại cập nhật trạng thái ứng viên trên ATS?  
Mọi việc này không chỉ tốn thời gian mà còn dễ gây lỗi, làm giảm trải nghiệm của ứng viên và làm chậm quy trình tuyển dụng.

**Workflow này** giải quyết toàn bộ chuỗi công việc trên **100 % không cần code**: nhận dữ liệu phỏng vấn qua webhook, tạo sự kiện Google Calendar (có link Meet), dùng GPT‑4 soạn email nhắc nhở chuyên nghiệp, gửi tự động qua Gmail, và cập nhật trạng thái ứng viên trên Recrutei. Các sếp sẽ có một quy trình “đóng gói” hoàn chỉnh, chạy liên tục 24/7.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Tự động tạo lịch, soạn email và cập nhật ATS trong vòng vài giây.  
- **Độ chính xác cao**: Không còn lỗi sai ngày giờ, link Meet hay nội dung email.  
- **Trải nghiệm ứng viên chuyên nghiệp**: Email nhắc nhở được cá nhân hoá, ngôn ngữ tự nhiên nhờ GPT‑4.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào người dùng cuối.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Google** (Google Calendar & Gmail) – kết nối OAuth2 trong n8n.  
- **API Key OpenAI** (GPT‑4.1‑mini) – để node `@n8n/n8n-nodes-langchain.openAi` hoạt động.  
- **Token Recrutei** – sẽ được đặt trong header `Authorization: Bearer <TOKEN>` của các node `httpRequest`.  
- **Workspace Slack** và **Bot token** – để gửi tin nhắn “Request for candidate approval”.  
- **Webhook URL** – sẽ được cung cấp cho ATS Recrutei để truyền dữ liệu phỏng vấn.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Truy cập **n8n > Workflows > Import**.  
2. Tải file JSON của workflow (được đính kèm trong mục “Resources” của bài viết) hoặc **Copy/Paste** toàn bộ JSON vào ô import.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và cách cấu hình chúng:

| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Webhook** | Nhận dữ liệu phỏng vấn từ Recrutei ATS. | - `Path`: **interview-calendar-meet** (đã có). <br> - Lưu URL (ví dụ: `https://your-n8n.com/webhook/interview-calendar-meet`) và dán vào Recrutei > Settings > Webhooks. |
| **Formatting the start date/time** (Set) | Chuyển đổi ngày/giờ sang định dạng ISO cho Google Calendar. | - Đảm bảo trường `startDate` và `startTime` từ webhook được ghép thành `startDateTimeISO`. |
| **Create the interview and invites the candidate** (Google Calendar) | Tạo sự kiện Google Calendar + link Meet. | - **Credentials**: `googleCalendarOAuth2Api` (kết nối tài khoản Google). <br> - **Conference data**: chọn `hangoutsMeet`. <br> - Điền `summary`, `description`, `start`, `end`, `attendees` (email ứng viên). |
| **Creates the e‑mail content** (OpenAI) | Soạn email nhắc nhở bằng GPT‑4. | - **Credentials**: `openAiApi`. <br> - **Model**: `gpt-4.1-mini`. <br> - **Prompt**: <br>```text\nYou are a recruitment assistant. Write a polite reminder email in English for a technical interview. Include candidate name, vacancy title, date, time, and Google Meet link.\n``` |
| **Separates the text** (Set) | Tách tiêu đề, nội dung email thành các trường riêng để Gmail dùng. | - Kiểm tra output của OpenAI, đặt `subject` và `body`. |
| **Wait until 1 day before the interview** (Wait) | Dừng workflow cho tới 24h trước sự kiện. | - Kiểu **Wait Until** → `{{ $json["startDateTimeISO"] | dateSubtract(1, "day") }}`. |
| **Send the message to the candidate** (Gmail) | Gửi email nhắc nhở. | - **Credentials**: `gmailOAuth2`. <br> - **To**: email ứng viên. <br> - **Subject** & **Body** lấy từ node “Separates the text”. |
| **Adding observation in candidate** (HTTP Request) | Ghi chú “Reminder sent” vào ATS Recrutei. | - **Method**: `POST`. <br> - **URL**: `https://api.recrutei.com/v1/candidates/{{candidateId}}/observations`. <br> - **Headers**: `Authorization: Bearer <YOUR_RECRUTEI_TOKEN>`. <br> - **Body**: `{ "note": "Reminder email sent" }`. |
| **Wait** (Wait) | Đợi cho đến khi phỏng vấn kết thúc (tùy chọn). | - Có thể để **5 phút** hoặc **0** nếu không cần. |
| **If** (If) | Kiểm tra kết quả phỏng vấn (được trả về từ ATS). | - Điều kiện: `{{ $json["status"] === "passed" }}` (hoặc tùy bạn). |
| **Adding observation in candidate1** (HTTP Request) | Ghi chú “Interview passed/failed”. | - Tương tự node trên, thay nội dung `note`. |
| **Getting the vacancy** (HTTP Request) | Lấy thông tin vacancy để xác định `pipe_stage_id` cuối cùng. | - **GET** `https://api.recrutei.com/v1/vacancies/{{vacancyId}}`. |
| **Selecting pipe stage id** (Set) | Trích xuất `lastStageId` từ response của node “Getting the vacancy”. |
| **Moving candidate to last stage** (HTTP Request) | Đưa ứng viên vào stage cuối cùng của pipeline. | - **PATCH** `https://api.recrutei.com/v1/candidates/{{candidateId}}/stage`. <br> - Body: `{ "stageId": "{{ $json["lastStageId"] }}" }`. |
| **Reproval e‑mail** (Gmail) | Gửi email từ chối (nếu không đạt). | - Cấu hình giống node Gmail trên, thay `subject`/`body` phù hợp. |
| **Request for candidate aproval** (Slack) | Gửi tin nhắn Slack để yêu cầu phê duyệt cuối cùng. | - **Credentials**: `slackApi`. <br> - **Operation**: `sendAndWait`. <br> - Nội dung: “Candidate {{name}} đã hoàn thành phỏng vấn. Approve? (Yes/No)”. |
| **Reproving candidate** (HTTP Request) | Gửi yêu cầu cập nhật trạng thái “reproved” qua API Recrutei. | - **POST** `https://api.recrutei.com/v1/candidates/{{candidateId}}/reprove`. |

> **Lưu ý:**  
> - Tất cả các node `httpRequest` cần **đặt Header** `Authorization: Bearer <YOUR_RECRUTEI_TOKEN>` và `Content-Type: application/json`.  
> - Kiểm tra lại **định dạng ngày‑giờ** ở node “Formatting the start date/time” để tránh lỗi múi giờ.  
> - Nếu muốn thay đổi thời gian nhắc nhở, chỉnh node **Wait until 1 day before** (ví dụ: 12h trước: `dateSubtract(12, "hour")`).  

### 3. Kích hoạt ⚡️
1. **Test run**: Dùng công cụ “Execute Workflow” với payload mẫu (định dạng JSON từ Recrutei).  
2. Kiểm tra:  
   - Sự kiện Google Calendar được tạo và có link Meet.  
   - Email nhắc nhở được gửi và nội dung đúng.  
   - Các observation được ghi vào Recrutei.  
   - Tin nhắn Slack xuất hiện và phản hồi đúng.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow chạy tự động.

## ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack + Google Chat**: Thêm node Google Chat để gửi reminder tới kênh nội bộ.  
- **Lưu log vào Google Sheet**: Dùng node Google Sheets để ghi lại thời gian gửi, trạng thái phản hồi, giúp báo cáo hàng tuần.  
- **Đa ngôn ngữ**: Thêm biến `language` vào payload, rồi trong prompt OpenAI chèn `Write the email in {{language}}`.  
- **Tự động tạo Zoom**: Thay `hangoutsMeet` bằng API Zoom nếu công ty dùng Zoom.  
- **Retry & Alert**: Dùng node “Error Trigger” + Slack để nhận thông báo khi bất kỳ node nào thất bại.

## 📌 Kết luận
Với workflow này, các sếp sẽ **loại bỏ hoàn toàn công đoạn thủ công** trong việc lên lịch phỏng vấn và nhắc nhở ứng viên, đồng thời **đảm bảo tính nhất quán** và **cá nhân hoá** nhờ GPT‑4. Hãy triển khai ngay, kết nối các tài khoản cần thiết, và để n8n làm việc thay bạn – tiết kiệm thời gian, nâng cao chất lượng tuyển dụng! 🚀