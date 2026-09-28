---
title: "🚀 Tự Động Tạo Lịch Trình Du Lịch Từ Email Với Llama AI"
description: "Giải pháp tự động nhận yêu cầu lịch trình du lịch qua email, dùng Llama AI tạo itinerary chi tiết và gửi lại ngay lập tức – không cần viết code."
slug: "tu-dong-hoa-lich-trinh-du-lich-voi-llama-ai"
tags: [n8n, automation, no-code, AI, travel, email]
keywords: [n8n workflow, tự động hóa, Llama AI, itinerary, email automation]
---

# 🚀 Tự Động Tạo Lịch Trình Du Lịch Từ Email Với Llama AI

Bạn đã từng mất hàng giờ để đọc email yêu cầu chuyến đi, tra cứu thông tin địa điểm, lên lịch trình và gửi lại cho khách?  
Công việc này không chỉ tốn thời gian mà còn dễ gây sai sót, khiến khách hàng phải chờ đợi.  
**Workflow này** sẽ tự động hoá toàn bộ quy trình: nhận email, dùng Llama 3.2 tạo itinerary chi tiết, và gửi lại kết quả – **100 % không cần code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút xuống còn vài giây cho mỗi yêu cầu.  
- **Độ chính xác cao**: Llama AI xử lý thông tin, giảm thiểu lỗi con người.  
- **Cá nhân hoá**: Tự động chèn tên khách, sở thích, ngân sách vào itinerary.  
- **Hoạt động liên tục**: Không cần giám sát, workflow chạy 24/7.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (hoặc bất kỳ dịch vụ email nào hỗ trợ IMAP/SMTP).  
- **App password** cho Gmail (để kết nối IMAP & SMTP).  
- **API Ollama** đã cài đặt và chạy trên máy chủ (cung cấp model `llama3.2-16000:latest`).  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **Credentials** trong n8n:
  - `imap` – thông tin IMAP của email.
  - `smtp` – thông tin SMTP của email.
  - `ollamaApi` – URL và token (nếu có) để gọi Ollama.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Tải file JSON của workflow (được cung cấp ở phần cuối) hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard**.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hướng dẫn cấu hình | Ghi chú |
|------|-------------------|---------|
| **Ollama Model** (`lmOllama`) | - Chọn **Credentials → ollamaApi**.<br>- Model: `llama3.2-16000:latest`. | Đảm bảo Ollama server đang chạy và có model này. |
| **Trigger From Mail (IMAP)** | - Credentials → **imap**.<br>- **Host**: `imap.gmail.com`<br>- **Port**: `993`<br>- **Secure**: `true`<br>- **User**: `your-email@gmail.com`<br>- **Password**: *App password*. | Node này sẽ “lắng nghe” hộp thư đến, chỉ xử lý email chưa đọc có tiêu đề chứa từ khóa **Travel Request** (có thể tùy chỉnh trong node). |
| **Basic LLM** (`chainLlm`) | - **LLM**: chọn node **Ollama Model** làm nguồn.<br>- **Prompt**: <br>```text\nBạn là trợ lý du lịch. Dựa trên nội dung email dưới đây, tạo một itinerary chi tiết (ngày, địa điểm, hoạt động, thời gian, chi phí ước tính). Định dạng markdown.\nEmail:\n{{ $json["body"] }}\n``` | Prompt có thể tùy chỉnh để đáp ứng phong cách viết của công ty. |
| **Email Field Setup** (`set`) | - Thêm các trường cần thiết cho email gửi: <br>```\n{\n  "to": "{{$json[\"from\"]}}",\n  "subject": "Your Travel Itinerary 🎒",\n  "html": "{{$node[\"Basic LLM\"].json[\"response\"]}}"\n}\n``` | Đảm bảo trường **to** lấy địa chỉ người gửi ban đầu. |
| **Sending Email** (`emailSend`) | - Credentials → **smtp**.<br>- **User**: `your-email@gmail.com`<br>- **Password**: *App password*<br>- **Host**: `smtp.gmail.com`<br>- **Port**: `465`<br>- **SSL/TLS**: `true` | Node này sẽ gửi itinerary đã tạo về lại người yêu cầu. |

> **⚠️ Lưu ý:** Sau khi cấu hình xong, bật **Execute Workflow** để kiểm tra kết nối từng node (IMAP, SMTP, Ollama). Nếu có lỗi, kiểm tra lại **App password**, **cổng** và **địa chỉ server**.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một email mẫu tới hộp thư đã cấu hình, tiêu đề “Travel Request – Vietnam”.  
2. Kiểm tra log trong n8n → **Execution** để xác nhận:
   - Email được đọc thành công.  
   - Prompt gửi tới Ollama và nhận phản hồi.  
   - Email trả lời được gửi đi.  
3. Khi mọi thứ ổn, **bật chế độ Active** (toggle ở góc trên bên phải) để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để nhận thông báo khi itinerary đã gửi.  
- **Lưu log vào Google Sheet**: Dùng node **Google Sheets** để ghi lại ngày, khách, địa điểm, thời gian tạo.  
- **Bổ sung dữ liệu thời tiết**: Kết nối API thời tiết (OpenWeather) trong prompt để đưa dự báo vào itinerary.  
- **Định dạng PDF**: Sử dụng node **HTML to PDF** rồi gửi file đính kèm thay vì markdown.  

### 📌 Kết luận
Với workflow **Automatic Travel Itinerary Generation via Email with Llama AI**, các sếp có thể biến việc tạo lịch trình du lịch thành một quy trình tự động, nhanh chóng và không lỗi.  
Hãy triển khai ngay trên n8n, tùy chỉnh prompt cho phù hợp với phong cách công ty, và để Llama AI lo phần còn lại – khách hàng sẽ nhận được itinerary chuyên nghiệp trong tích tắc! 🚀