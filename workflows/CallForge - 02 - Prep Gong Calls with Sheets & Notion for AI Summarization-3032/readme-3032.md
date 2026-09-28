---
title: "🚀 CallForge - Tự động chuẩn bị cuộc gọi Gong với Sheets & Notion cho AI Summarization"
description: "Workflow n8n tự động lấy dữ liệu cuộc gọi Gong, enrich bằng Google Sheets & Notion, rồi chuẩn bị transcript cho AI tóm tắt – giảm 90% thời gian xử lý thủ công."
slug: "callforge-tu-dong-chuan-bi-cuoc-goi-gong-voi-sheets-notion"
tags: [n8n, automation, no-code, sales, AI, gong, notion, google-sheets]
keywords: [n8n workflow, tự động hóa, Gong, Notion, Google Sheets, AI summarization]
---

# 🚀 CallForge - Tự động chuẩn bị cuộc gọi Gong với Sheets & Notion cho AI Summarization

Các sếp thường phải **đối mặt với hàng chục, hàng trăm bản ghi âm cuộc gọi Gong** mỗi tuần. Việc tải transcript, so sánh với danh sách đối thủ, kiểm tra lỗi phát âm hay nhập sai dữ liệu – tất cả đều tốn thời gian và dễ gây sai sót.  
**CallForge** giải quyết toàn bộ quy trình này **100 % không cần viết code**: tự động lấy cuộc gọi từ Gong, kéo dữ liệu tích hợp từ Google Sheets, danh sách đối thủ từ Notion, chuẩn hoá transcript và chuyển ngay cho workflow AI tóm tắt. Kết quả? Tiết kiệm thời gian, tăng độ chính xác và chuẩn bị dữ liệu cho mọi bộ phận (sales, product, marketing) trong tích tắc.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm 80‑90 % thời gian** so với việc xử lý thủ công từng bản ghi.  
- **Độ chính xác cao**: loại bỏ trùng lặp, chuẩn hoá dữ liệu trước khi đưa vào AI.  
- **Enrich dữ liệu** bằng thông tin từ Sheets & Notion → AI nhận ngữ cảnh đầy đủ, giảm lỗi “mis‑pronunciation”.  
- **Hoạt động liên tục** 24/7, không cần can thiệp sau khi đã cấu hình.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Gong** + API key (`gongApi`).  
- **Google Workspace**: quyền truy cập Google Sheets, tạo OAuth2 credential (`googleSheetsOAuth2Api`).  
- **Notion**: API token (`notionApi`) và 2 database (một cho *Competitors*, một cho *Previous Phone Calls*).  
- **OpenAI** (hoặc LLM tương đương) để tóm tắt transcript – được cấu hình trong workflow “Transcript Processor”.  
- **n8n** (phiên bản ≥ 1.0) đã cài đặt và có quyền chạy các workflow con.  
:::

## 🚀 Cách import & Lên đồ

### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ trang gốc hoặc liên kết chia sẻ).  
2. Mở n8n → **Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào **Editor → Import from Clipboard**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và hướng dẫn cấu hình chi tiết:

| Node | Loại | Cấu hình cần làm |
|------|------|-------------------|
| **When clicking ‘Test workflow’** | `manualTrigger` | Không cần cấu hình – dùng để test nhanh. |
| **Gong** | `gong` | - Chọn **Credentials → gongApi**.<br>- Đặt **Operation**: `listCalls` (hoặc tùy nhu cầu).<br>- Lưu ý: chọn **Date Range** để chỉ lấy các cuộc gọi mới. |
| **Get Integrations** | `googleSheets` | - Credentials: **googleSheetsOAuth2Api**.<br>- **Spreadsheet ID**: ID của sheet chứa danh sách tích hợp.<br>- **Range**: ví dụ `Integrations!A2:B`.<br>- Đánh dấu **Return All Rows**. |
| **Comma Separate Integrations** | `set` | - Tạo trường mới `integrationsCsv` = `{{$json["values"].join(", ")}}`. |
| **Comma separate competitors** | `set` | - Tương tự, tạo `competitorsCsv` từ dữ liệu Notion (sẽ được merge sau). |
| **Get list of Competitors** | `notion` | - Credentials: **notionApi**.<br>- **Resource**: `database`.<br>- **Database ID**: ID database “Competitors”. |
| **Get Previous Phone Calls** | `notion` | - Credentials: **notionApi**.<br>- **Operation**: `getAll`.<br>- **Resource**: `databasePage`.<br>- **Database ID**: database “Previous Phone Calls”. |
| **Isolate Only Call IDs** | `set` | - Tạo mảng `callIds` chỉ chứa trường `id` của mỗi cuộc gọi (định dạng `{{$json["id"]}}`). |
| **Only Process New Calls** | `compareDatasets` | - **First Dataset**: `callIds` (từ Gong).<br>- **Second Dataset**: `processedIds` (từ Notion).<br>- **Mode**: `exclude` → chỉ giữ những ID chưa xuất hiện. |
| **Loop Over Calls** | `splitInBatches` | - **Batch Size**: 1 (để xử lý từng cuộc gọi một). |
| **Process All Call Transcripts** | `executeWorkflow` | - Chọn workflow con **“Transcript Processor”** (được cung cấp trong repo).<br>- Truyền **callId** và **rawTranscript** vào workflow con. |
| **Receive all Transcripts** | `noOp` | - Dùng làm “đầu ra” tổng hợp, không cần cấu hình. |
| **Merge 3 objects into one** | `merge` | - Merge dữ liệu từ Gong, Integrations CSV, Competitors CSV thành một object duy nhất. |
| **Aggregate Call Data** / **Call Aggregator** / **Integration Aggregator** | `aggregate` | - Đặt **Mode**: `Append` để gom lại các object thành mảng. |
| **Split Out Call Data and Competitors** | `splitOut` | - Tách mảng thành 2 phần: dữ liệu cuộc gọi & danh sách đối thủ. |
| **Reduce down to 1 object** | `aggregate` | - **Mode**: `First` hoặc `Merge` tùy mục đích, tạo object cuối cùng để truyền vào AI. |
| **Execute Workflow Trigger** | `executeWorkflowTrigger` | - Đánh dấu workflow con “Call Processor” (AI) để nhận dữ liệu đã chuẩn hoá. |

> **Lưu ý:**  
> - Đảm bảo **All Credentials** đã được tạo trong n8n → **Credentials** trước khi import.  
> - Kiểm tra **field mapping** trong các node `set` và `merge` để dữ liệu truyền đúng tên trường mà workflow AI mong đợi (ví dụ: `transcript`, `integrations`, `competitors`).  
> - Nếu muốn giới hạn thời gian lấy cuộc gọi, chỉnh **Date Filter** trong node Gong.

### 3. Kích hoạt ⚡️
1. **Test chạy**: Nhấn nút **Execute Workflow** → kiểm tra log ở mỗi node, đặc biệt node **Only Process New Calls** để chắc chắn không có bản ghi trùng.  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Đặt **Trigger** (nếu muốn tự động chạy định kỳ) bằng cách thêm node **Cron** hoặc **Webhook** tùy nhu cầu.

## ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau node `Receive all Transcripts` để gửi thông báo “Cuộc gọi X đã được tóm tắt”.  
- **Lưu log chi tiết**: Dùng node `Google Sheets` hoặc `Airtable` để ghi lại `callId`, `status`, `summary` cho báo cáo hàng tuần.  
- **Báo cáo định kỳ**: Kết hợp `Cron` + `Google Docs` để tự động tạo bản tóm tắt tổng hợp mọi cuộc gọi trong tháng và gửi email cho đội ngũ.  
- **Mở rộng AI**: Thay OpenAI bằng `Claude` hoặc `Gemini` nếu muốn so sánh chất lượng tóm tắt.  

## 📌 Kết luận
Với **CallForge**, các sếp có thể biến một quy trình tốn công sức thành một chuỗi tự động hoá liền mạch, luôn cung cấp dữ liệu sạch, đầy đủ ngữ cảnh cho AI và giảm thiểu lỗi con người. Hãy **import ngay**, cấu hình các credential, và bật workflow – để đội ngũ sales và product luôn nhận được thông tin chính xác, kịp thời và sẵn sàng hành động! 🚀