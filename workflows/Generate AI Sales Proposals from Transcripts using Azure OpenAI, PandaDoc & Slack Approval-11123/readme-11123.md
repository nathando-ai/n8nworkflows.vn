---
title: "🚀 Tự động tạo đề xuất bán hàng từ bản ghi hội thoại với Azure OpenAI, PandaDoc & Slack"
description: "Chuyển nhanh các cuộc gọi bán hàng và biểu mẫu intake thành đề xuất gửi ngay, giảm thời gian chuẩn bị, tăng tỷ lệ chốt giao dịch."
slug: "tua-dong-tao-de-xuat-ban-hang-tu-bang-ghi-hoi-thoai"
tags: [n8n, automation, no-code, CRM, AI, Sales]
keywords: [n8n workflow, tự động hóa, AI, PandaDoc, Slack, Fireflies, Azure OpenAI, Sales Proposal]
---

# 🚀 Tự động tạo đề xuất bán hàng từ bản ghi hội thoại với Azure OpenAI, PandaDoc & Slack

Bạn đang mất hàng giờ để viết đề xuất bán hàng, chờ phản hồi từ khách hàng, và phải liên tục nhắc nhở họ ký hợp đồng?  
Workflow này sẽ **đưa toàn bộ quy trình từ ghi âm cuộc gọi → tạo đề xuất → phê duyệt → gửi → theo dõi** vào một chuỗi tự động 100% không cần code.  

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ viết đề xuất xuống < 30 phút.  
- **Chính xác & nhất quán**: Đề xuất được tạo theo mẫu chuẩn, không sai sót.  
- **Tự động phê duyệt**: Slack approval loop giảm thời gian chờ 50%.  
- **Theo dõi hiệu quả**: Audit trail của PandaDoc giúp nhận biết khi nào khách ký.  
- **Tập trung vào bán hàng**: Nhân viên bán hàng không còn lo lắng về giấy tờ.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ | API Key / Credential | Mô tả |
|---------|----------------------|-------|
| **Azure OpenAI** | `azureOpenAiApi` | Key + endpoint, chọn mô hình `gpt-4o-mini` hoặc tương đương. |
| **PandaDoc** | `pandaDocApiKey` | Key, ID mẫu (Template ID), ID folder (Folder ID). |
| **Slack** | `slackApi` | Bot token, ID kênh phê duyệt. |
| **Fireflies.ai** | `firefliesApi` | API key, ID cuộc gọi (Transcript ID). |
| **Airtable** | `airtableTokenApi` | API key, Base ID, Table name (để upsert contact). |
| **Google Sheets** (tùy chọn) | `googleSheetsApi` | Key, ID sheet. |
| **Webhook** (tùy chọn) | `webhookUrl` | URL nhận dữ liệu từ biểu mẫu. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ <https://n8n.io/workflows/11123> hoặc copy toàn bộ JSON.  
2. Mở n8n Editor → **Import** → **Import from JSON** → dán JSON.  
3. Lưu lại workflow với tên “Generate AI Sales Proposals”.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| **On form submission** | `formTrigger` | URL webhook, field mapping (goals, budget, timeline). | Đảm bảo biểu mẫu gửi dữ liệu đúng định dạng. |
| **Basic LLM Chain** | `chainLlm` | Prompt template (problem → solution → scope → budget → timeline → next steps). | Sử dụng `Structured Output Parser` để lấy JSON. |
| **Azure OpenAI Chat Model** | `lmChatAzureOpenAi` | `azureOpenAiApi`, model `gpt-4o-mini`. | Kiểm tra quota, latency. |
| **Structured Output Parser** | `outputParserStructured` | Định nghĩa schema JSON. | Đảm bảo output đúng cấu trúc để dùng trong PandaDoc. |
| **Create Document** | `httpRequest` (Create) | Method POST, URL `https://api.pandadoc.com/public/v1/documents`, body: template ID + data. | Sử dụng token `pandaDocApiKey`. |
| **If** | `if` | Kiểm tra `document.status` (draft/sent). | Định hướng flow. |
| **Send Document** | `httpRequest` (Send) | Method POST, URL `https://api.pandadoc.com/public/v1/documents/{id}/send`. | Gửi tới email khách. |
| **Wait** | `wait` | Thời gian chờ (ví dụ 48h). | Để kiểm tra ký. |
| **Set Initial Variables** | `set` | Khởi tạo `contactStage`, `proposalId`, `transcriptId`. | Dùng cho Airtable. |
| **Update Variables** | `set` | Cập nhật `status` sau phê duyệt. | |
| **Update Contact** | `airtable` (upsert) | `airtableTokenApi`, Base ID, Table. | Cập nhật stage “Proposal Sent”. |
| **Get a list of transcripts** | `fireflies` | `firefliesApi`, operation `getTranscriptsList`. | Lấy transcript ID. |
| **Get a transcript** | `fireflies` | `firefliesApi`, operation `getTranscript`. | Lấy nội dung hội thoại. |
| **If1** | `if` | Kiểm tra `transcript.status` (completed). | |
| **Get Audit Trail** | `httpRequest` | URL `https://api.pandadoc.com/public/v1/documents/{id}/audit`. | Kiểm tra ký. |
| **Update Contact1/2** | `airtable` | Cập nhật stage “Signed” hoặc “Reminder Sent”. | |
| **Wait1** | `wait` | Thời gian chờ trước reminder. | |
| **Send a message and wait for response** | `slack` | `slackApi`, operation `sendAndWait`. | Phê duyệt. |
| **Send Reminder1** | `httpRequest` | URL `https://api.pandadoc.com/public/v1/documents/{id}/send`. | Gửi reminder. |
| **Get Recepient ID** | `httpRequest` | Slack API `users.info`. | Lấy ID người nhận. |
| **Send a message** | `slack` | `slackApi`, operation `send`. | Gửi thông báo. |
| **Send a message1** | `slack` | `slackApi`, operation `send`. | Gửi thông báo cuối. |

> **Tip**: Đối với mỗi node HTTP Request, hãy bật **Authentication** → **Bearer Token** và nhập `pandaDocApiKey`.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (điền form, chọn transcript). Kiểm tra log từng node.  
2. **Bật Active**: Trên giao diện n8n, chuyển trạng thái sang **Active**.  
3. **Giám sát**: Kiểm tra Dashboard → **Workflow Activity** để đảm bảo không có lỗi.

## ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp HubSpot**: Thay Airtable bằng HubSpot CRM để tự động cập nhật deal stage.  
- **Email follow‑up**: Thêm node `emailSend` sau khi gửi reminder để nhắc khách ký.  
- **Lưu log vào Google Sheets**: Dùng node `googleSheets` để ghi lại thời gian gửi, phản hồi Slack, trạng thái ký.  
- **Slack Bot Custom Commands**: Tạo slash command `/approve-proposal` để phê duyệt nhanh hơn.  
- **Sử dụng Zapier**: Khi PandaDoc gửi webhook “signed”, trigger Zapier để cập nhật hệ thống ERP.

## 📌 Kết luận
Workflow “Generate AI Sales Proposals from Transcripts using Azure OpenAI, PandaDoc & Slack” là công cụ **đột phá** giúp các doanh nghiệp chuyển đổi quy trình bán hàng từ thủ công sang tự động, giảm thời gian chuẩn bị, tăng tính chính xác và giảm thiểu công việc theo dõi.  
Hãy **cài đặt ngay** và trải nghiệm sự khác biệt trong quy trình bán hàng của bạn!  

> **Tác giả**: Sparsh From Automation Jinn (Founder @ Automation Jinn) – <https://www.automationjinn.com>  
> **Link gốc workflow**: <https://n8n.io/workflows/11123>