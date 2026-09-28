---
title: "🚀 Thu thập Lead tự động với AI Gemini 2.0 Flash & Google Sheets"
description: "Workflow n8n tự động thu thập thông tin khách hàng tiềm năng qua chatbot, xử lý bằng Gemini AI và lưu vào Google Sheets, giảm 90% công việc thủ công."
slug: "thu-thap-lead-tu-dong-gemini-google-sheets"
tags: [n8n, automation, no-code, lead-generation, chatbot, google-sheets]
keywords: [n8n workflow, tự động hóa lead, Gemini AI, Google Sheets, chatbot]
---

# 🚀 Thu thập Lead tự động với AI Gemini 2.0 Flash & Google Sheets

Bạn có bao giờ phải **đánh mất hàng chục lead** chỉ vì nhân viên không kịp nhập dữ liệu, hoặc vì chatbot trả lời không đồng nhất?  
Việc **thu thập, phân loại và lưu trữ** thông tin khách hàng tiềm năng bằng tay khiến doanh nghiệp tốn thời gian, dễ sai sót và mất cơ hội bán hàng.  

**Workflow này** sẽ giải quyết toàn bộ vấn đề trên:  
- Nhận tin nhắn từ website, app hoặc bất kỳ nền tảng chat nào qua **Webhook**.  
- **AI Gemini 2.0 Flash** phân tích ngữ cảnh, trả lời nhanh gọn, đồng thời trích xuất các trường thông tin quan trọng.  
- Dữ liệu được **lưu tự động vào Google Sheets** để bạn và đội ngũ sales có thể truy cập ngay lập tức.  
- Toàn bộ quy trình chạy **100% không cần viết code** – chỉ cần cấu hình một lần và để nó hoạt động 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn nhập liệu thủ công, lead được ghi lại ngay khi khách hàng tương tác.  
- **Độ chính xác cao**: AI trích xuất thông tin dựa trên ngữ cảnh, giảm lỗi nhập sai.  
- **Cá nhân hoá**: Trả lời khách hàng ngay lập tức, tăng tỷ lệ chuyển đổi.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc của nhân viên.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** với quyền **Google Sheets API** (OAuth2) – dùng credential `googleSheetsOAuth2Api`.  
- **API Key Google Palm (Gemini)** – tạo credential `googlePalmApi`.  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud).  
- **Google Sheet** đã tạo sẵn với các cột:  
  1. Full Name  
  2. Company Name  
  3. Email Address  
  4. Phone Number (tùy chọn)  
  5. Project Intent/Needs  
  6. Project Timeline  
  7. Budget Range  
  8. Preferred Communication Channel  
  9. How they heard about the company  
- URL webhook sẽ được cung cấp cho widget chat trên website/app.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Editor.  
2. Nhấn **Import** → **Upload JSON** và chọn file JSON của workflow (hoặc copy/paste nội dung JSON).  
3. Sau khi import, workflow sẽ xuất hiện với 6 node đã được nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **Webhook** | - **Path**: `4777b330-6bf9-460e-aaf0-52d6263d17d7` (không thay đổi nếu muốn giữ URL hiện tại) <br> - **HTTP Method**: `POST` | URL cuối cùng sẽ là `https://<your-n8n-domain>/webhook/4777b330-6bf9-460e-aaf0-52d6263d17d7` |
| **Respond to Webhook** | Không cần thay đổi, chỉ đảm bảo trả về **JSON** được cấu trúc bởi node phía sau. | |
| **AI Agent** | - **Agent Name**: tùy đặt (ví dụ: `LeadCaptureAgent`) <br> - **Tools**: thêm **Google Gemini Chat Model** và **Simple Memory** làm tool. | Agent sẽ điều phối việc gọi AI và quản lý ngữ cảnh. |
| **Google Gemini Chat Model** | - **Credential**: chọn `googlePalmApi` <br> - **Model**: `gemini-1.0-flash` (hoặc phiên bản mới nhất) <br> - **Prompt**: Đặt prompt để trích xuất các trường lead (Full Name, Email, …). | Prompt mẫu: <br>```\nExtract the following fields from the user's message and return a JSON object with keys: fullName, companyName, email, phone, intent, timeline, budget, channel, source.\n``` |
| **Simple Memory** | - **Window Size**: `5` (giữ 5 tin nhắn gần nhất) | Giúp AI nhớ ngữ cảnh trong một buổi chat. |
| **Google Sheets** | - **Credential**: chọn `googleSheetsOAuth2Api` <br> - **Spreadsheet ID**: ID của Google Sheet đã tạo <br> - **Sheet Name**: tên sheet (ví dụ: `Leads`) <br> - **Operation**: `Append` <br> - **Columns Mapping**: ánh xạ các trường JSON từ AI sang cột Google Sheet. | Đảm bảo quyền **Editor** cho tài khoản Google đã tạo credential. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Dùng công cụ Postman hoặc curl để gửi POST request tới webhook với payload mẫu:  
   ```json\n{\n  \"message\": \"Xin chào, tôi là Nguyễn Văn A từ Công ty XYZ, email: a@example.com, muốn biết về giải pháp marketing, ngân sách 10-20 triệu, thời gian triển khai 2 tháng.\"\n}\n```  
2. Kiểm tra phản hồi từ node **Respond to Webhook** – phải nhận được JSON chứa câu trả lời AI và trạng thái `success`.  
3. Kiểm tra Google Sheet – một dòng mới phải được thêm với đầy đủ thông tin.  
4. Khi mọi thứ ổn, bật **Active** cho workflow (nút toggle ở góc trên bên phải).  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` để gửi thông báo ngay khi có lead mới.  
- **Lưu log chi tiết**: Dùng node `Write Binary File` hoặc `Google Drive` để lưu toàn bộ hội thoại dưới dạng JSON cho mục đích audit.  
- **Báo cáo định kỳ**: Thêm node `Cron` + `Google Sheets` để tổng hợp số lượng lead mỗi ngày/tuần và gửi email báo cáo tự động.  
- **Phân loại lead**: Sử dụng thêm một node `IF` dựa trên `budget` hoặc `timeline` để tự động gắn nhãn “Hot”, “Warm”, “Cold”.  

### 📌 Kết luận
Với workflow **Conversational Lead Capture with Gemini 2.0 Flash AI and Google Sheets**, các sếp có thể biến mọi cuộc trò chuyện thành nguồn lead chất lượng, giảm thiểu công việc nhập liệu và tăng tốc độ phản hồi khách hàng. Hãy **import ngay**, cấu hình các credential cần thiết và để n8n làm việc thay bạn 24/7! 🚀