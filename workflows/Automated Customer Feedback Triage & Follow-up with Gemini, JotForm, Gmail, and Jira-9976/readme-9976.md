---
title: "🚀 Tự Động Phân Loại Phản Hồi Khách Hàng & Theo Dõi Với Gemini, JotForm, Gmail và Jira"
description: "Workflow n8n tự động thu thập phản hồi từ JotForm, phân tích cảm xúc bằng Gemini, tạo ticket Jira và gửi email trả lời nhanh chóng, giảm 80% thời gian xử lý."
slug: "tu-dong-phan-loai-phan-hoi-khach-hang-gemini-jotform-gmail-jira"
tags: [n8n, automation, no-code, jira, gmail, jotform, gemini, AI]
keywords: [n8n workflow, tự động hóa, feedback, jira, gmail, gemini, AI]
---

# 🚀 Tự Động Phân Loại Phản Hồi Khách Hàng & Theo Dõi Với Gemini, JotForm, Gmail và Jira

Doanh nghiệp thường phải đối mặt với **hàng trăm email phản hồi** mỗi ngày. Việc **đọc, phân loại, tạo ticket và trả lời** thủ công không chỉ tốn thời gian mà còn dễ gây sai sót, làm mất cơ hội cải thiện dịch vụ.  
Workflow **Automated Customer Feedback Triage & Follow-up** giải quyết toàn bộ quy trình này **100% không cần code**: từ việc thu thập phản hồi qua JotForm, phân tích cảm xúc bằng Google Gemini, tạo ticket Jira tự động, đến việc gửi email trả lời và hỏi thêm thông tin khi cần.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm 80% thời gian** xử lý phản hồi so với cách thủ công.  
- **Độ chính xác cao** trong phân loại cảm xúc nhờ AI Gemini.  
- **Tự động tạo ticket Jira** ngay khi phản hồi tiêu cực, giảm thời gian phản hồi.  
- **Gửi email trả lời nhanh** và thu thập thêm thông tin khi cần, nâng cao trải nghiệm khách hàng.  
- **Hoạt động liên tục 24/7** mà không cần giám sát.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản JotForm** (đăng ký tại: https://www.jotform.com/?partner=zainurrehman) và tạo form thu thập feedback.  
- **API Key Google Gemini** (bạn cần bật Gemini API trong Google Cloud).  
- **Tài khoản Gmail** (được cấu hình làm OAuth2 trong n8n).  
- **Tài khoản Jira Software** (cần Project Key và API token).  
- **n8n** (cài đặt trên VPS hoặc dịch vụ cloud).  
- **Node “@n8n/n8n-nodes-langchain”** đã được cài đặt (có trong Marketplace).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ link gốc: https://n8n.io/workflows/9976).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON hoặc **Paste JSON** vào ô.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|---------|--------------------|
| **JotForm Trigger** | Lắng nghe form mới | Chọn **Credential** JotForm, nhập **Form ID** của form feedback. |
| **AI Agent** | Điều phối luồng AI | Chọn **Model** = “Google Gemini Chat Model”, thiết lập **System Prompt**: “Phân loại feedback thành Positive, Negative, Neutral”. |
| **Google Gemini Chat Model** | Xử lý ngôn ngữ | Điền **API Key** Gemini, thiết lập **Temperature** (0.2 – 0.5). |
| **Gmail Trigger** | Nhận email trả lời từ khách | Kết nối **Credential** Gmail, chọn **Mailbox** (Inbox) và **Label** (nếu có). |
| **Simple Memory** | Lưu trữ ngữ cảnh hội thoại | Để mặc định, hoặc tùy chỉnh **Window Size** = 5. |
| **Reply to a message in Gmail** | Trả lời email tự động | Chọn **Credential** Gmail, thiết lập **Subject** và **Body** (sử dụng biến `{{ $json["response"] }}`). |
| **AI Agent (Chat)** | Đặt câu hỏi bổ sung khi feedback tiêu cực | Prompt: “Hãy hỏi khách hàng chi tiết hơn về vấn đề gặp phải”. |
| **Send a message in Gmail** | Gửi email hỏi thêm thông tin | Cấu hình **To**, **Subject**, **Body** (sử dụng biến từ AI Agent). |
| **Edit Fields** (Set) | Chuẩn bị dữ liệu cho Jira | Đặt các trường: `summary`, `description`, `projectKey`, `issueType`. |
| **Create an issue in Jira Software** | Tạo ticket Jira | Chọn **Credential** Jira, nhập **Project Key**, **Issue Type** (Bug/Task). |
| **Structured Output Parser** | Chuyển kết quả Gemini thành JSON | Định nghĩa schema: `{ "sentiment": "string", "reason": "string" }`. |

> **Lưu ý:** Mỗi node sử dụng **Credential** phải được tạo trước trong **n8n → Credentials**. Đảm bảo quyền truy cập API (Jira, Gmail, Gemini) đã được cấp.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một mẫu feedback qua JotForm → Kiểm tra log trong n8n để xác nhận các node chạy đúng.  
2. Kiểm tra email trả lời và ticket Jira được tạo.  
3. Khi mọi thứ ổn, bật **Active** (nút toggle ở góc trên bên phải) để workflow chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node Slack để thông báo ngay khi ticket mới được tạo.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để lưu lịch sử feedback, giúp phân tích xu hướng.  
- **Báo cáo định kỳ**: Sử dụng node Cron + Gmail để gửi báo cáo tổng hợp feedback hàng tuần.  
- **Tối ưu Prompt**: Thêm các ví dụ trong System Prompt của Gemini để cải thiện độ chính xác phân loại.  

### 📌 Kết luận
Với workflow **Automated Customer Feedback Triage & Follow-up**, các sếp có thể **tự động hoá toàn bộ quy trình phản hồi khách hàng** chỉ trong vài phút thiết lập, giảm tải công việc thủ công, nâng cao độ hài lòng và phản hồi nhanh chóng. Hãy triển khai ngay hôm nay để trải nghiệm hiệu quả thực sự!