---
title: "🚀 Xây dựng Chatbot SEO thông minh với GPT‑4o‑mini & Google Sheets"
description: "Tự động hoá chatbot SEO trả lời câu hỏi dựa trên dữ liệu Google Sheets, không cần viết code, chạy 24/7 trên n8n."
slug: "xay-dung-chatbot-seo-gpt4o-mini-google-sheets"
tags: [n8n, automation, no-code, AI, chatbot, SEO]
keywords: [n8n workflow, tự động hóa, chatbot SEO, GPT-4o-mini, Google Sheets, RAG]
---

# 🚀 Xây dựng Chatbot SEO thông minh với GPT‑4o‑mini & Google Sheets

Doanh nghiệp ngày càng phụ thuộc vào nội dung SEO để thu hút khách hàng, nhưng việc trả lời nhanh các câu hỏi “tôi muốn biết …” từ khách hàng vẫn còn tốn thời gian và phải tra cứu thủ công trong hàng chục, hàng trăm dòng dữ liệu.  
**Workflow này** sẽ biến Google Sheets chứa danh sách từ khóa, mô tả, URL… thành một chatbot AI dựa trên GPT‑4o‑mini, cho phép các sếp trả lời khách hàng ngay lập tức, chính xác và luôn cập nhật mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Trả lời khách hàng trong vài giây thay vì phút‑giờ.  
- **Độ chính xác cao**: Dữ liệu nguồn luôn là Google Sheets được cập nhật liên tục.  
- **Cá nhân hoá**: Chatbot có thể nhớ ngữ cảnh ngắn nhờ Memory Buffer.  
- **Hoạt động 24/7**: Không cần nhân viên trực, giảm chi phí vận hành.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Google** với quyền truy cập Google Sheets chứa dữ liệu SEO.  
- **API Key OpenAI** (cấp quyền `Chat Completion` cho model `gpt-4o-mini`).  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud).  
- **Credentials** trong n8n:  
  - `Google Sheets OAuth2` (hoặc Service Account).  
  - `OpenAI API` (đặt tên `OpenAI API`).  
- **Webhook URL** (n8n sẽ tạo tự động, dùng để tích hợp vào website hoặc Slack/Telegram).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Click **Import** → **From File** → Chọn file JSON (được tải về từ phần “Download JSON” ở cuối README).  
   *Hoặc* copy toàn bộ JSON và dán vào **Import → Paste JSON**.  
3. Nhấn **Import**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần thay đổi |
|------|---------|-----------------------|
| **Webhook (Chat Trigger)** | Nhận request từ người dùng (web, Slack, Telegram…) | - `HTTP Method`: `POST` <br> - `Path`: tùy chọn (ví dụ: `/seo-chat`) |
| **Google Sheets** | Đọc dữ liệu SEO từ sheet | - **Credentials**: chọn Google Sheets OAuth2 <br> - **Spreadsheet ID**: ID của file Google Sheets <br> - **Sheet Name**: tên sheet chứa dữ liệu (ví dụ: `Keywords`) |
| **Set (Cấu hình LLM)** | Đặt tham số cho GPT‑4o‑mini | - `model`: `gpt-4o-mini` <br> - `temperature`: `0.2` (độ sáng tạo thấp để trả lời chính xác) |
| **LM Chat OpenAI** | Gọi API OpenAI | - **Credentials**: chọn `OpenAI API` <br> - `Prompt`: để trống (sẽ được tạo bởi node Agent) |
| **Agent (LangChain RAG)** | Kết hợp Retrieval‑Augmented Generation | - `Retriever`: chọn `Google Sheets` (đọc dữ liệu) <br> - `Prompt Template`: “Bạn là trợ lý SEO, trả lời câu hỏi dựa trên dữ liệu sau… {context}” |
| **Memory Buffer Window** | Giữ ngữ cảnh hội thoại ngắn | - `Window Size`: `5` (lưu 5 tin nhắn gần nhất) |
| **Code** (tùy chọn) | Xử lý dữ liệu trước/ sau khi trả lời | - Thêm script nếu muốn lọc, định dạng lại câu trả lời. |
| **Sticky Note** | Ghi chú hướng dẫn nội bộ | - Không cần cấu hình, chỉ để mô tả luồng. |

> **⚠️ Lưu ý:** Đảm bảo **Google Sheets** có cột `question` và `answer` (hoặc `keyword`, `description`) để Agent có thể truy vấn đúng. Nếu cấu trúc khác, chỉnh lại **Prompt Template** trong node Agent cho phù hợp.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một payload JSON mẫu tới webhook, ví dụ:  
   ```json
   { "message": "Tôi muốn biết cách tối ưu từ khóa “điện thoại giá rẻ”" }
   ```  
   Kiểm tra log ở node **Agent** và **LM Chat OpenAI** để chắc chắn dữ liệu được truy xuất đúng.  
2. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  
3. Đặt **Cron** hoặc **Trigger** nếu muốn chatbot hoạt động tự động theo lịch (ví dụ: gửi báo cáo SEO hàng ngày).

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node **LM Chat OpenAI** để trả lời trực tiếp trong kênh nhóm.  
- **Lưu log**: Dùng node **Google Drive** hoặc **Postgres** để ghi lại toàn bộ câu hỏi & câu trả lời, phục vụ phân tích hiệu suất.  
- **Báo cáo định kỳ**: Kết hợp **Cron** + **Google Sheets** để xuất danh sách câu hỏi phổ biến mỗi tuần, giúp SEO team tối ưu nội dung.  
- **Tối ưu Prompt**: Thêm các hướng dẫn chi tiết trong Prompt Template (ví dụ: “Luôn trả lời bằng tiếng Việt, không đưa ra thông tin ngoài dữ liệu”) để tăng độ chính xác.  

### 📌 Kết luận
Với workflow này, các sếp có thể biến một bảng Google Sheets đơn giản thành một **Chatbot SEO thông minh**, trả lời khách hàng nhanh chóng, giảm tải nhân sự và nâng cao trải nghiệm người dùng. Hãy import ngay, cấu hình các credentials, bật chạy và cảm nhận sức mạnh của tự động hoá AI không code! 🚀