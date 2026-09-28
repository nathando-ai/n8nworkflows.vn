---
title: "🚀 Tự động chuyển đổi và phân tích hội thảo, podcast bằng ElevenLabs & Google Gemini AI"
description: "Hướng dẫn chi tiết cách dùng workflow n8n để tự động chuyển đổi audio/video thành văn bản, phân tích nội dung, lưu trữ vào Google Docs, gửi email báo cáo – hoàn toàn không cần code."
slug: "transcribe-analyze-meetings-podcasts-elevenlabs-google-gemini"
tags: [n8n, automation, no-code, speech-to-text, transcription, AI, google, elevenlabs, gemini]
keywords: [n8n workflow, tự động hóa, speech to text, transcription, AI analysis, google docs, google sheets, gmail, elevenlabs, google gemini]
---

# 🚀 Tự động chuyển đổi và phân tích hội thảo, podcast bằng ElevenLabs & Google Gemini AI

Bạn đang phải mất hàng giờ để lắng nghe, ghi chép và phân tích các cuộc họp hoặc podcast? Workflow này sẽ giúp bạn:

- **Chuyển đổi** audio/video thành văn bản chính xác (đến 99 ngôn ngữ) chỉ trong vài phút.
- **Phân tích** nội dung bằng AI, tóm tắt, trích xuất điểm chính và đề xuất hành động.
- **Lưu trữ** bản ghi và báo cáo vào Google Docs, Google Sheets.
- **Gửi** email báo cáo tự động tới những người liên quan.

Và tất cả đều **không cần viết code** – chỉ cần cấu hình một vài credential và chạy workflow.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ hàng giờ lắng nghe xuống vài phút.
- **Độ chính xác cao**: Hỗ trợ 99 ngôn ngữ, giảm sai sót so với ghi chép thủ công.
- **Tự động hóa liên tục**: Chạy 24/7, không cần can thiệp.
- **Cá nhân hóa**: Gửi email báo cáo tùy chỉnh, lưu trữ vào Google Docs phù hợp với quy trình làm việc.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ / Credential | Mô tả | Cách lấy |
|-----------------------|-------|----------|
| **Google Sheets** | Để lưu trữ URL audio/video và cập nhật kết quả | Tạo tài khoản Google, bật Sheets API, tạo OAuth2 credential trong n8n |
| **Google Docs** | Tạo và cập nhật tài liệu báo cáo | Tạo OAuth2 credential trong n8n |
| **Google Gemini (Palm)** | Phân tích nội dung | Tạo API key từ Google Cloud, bật Gemini API |
| **ElevenLabs** | Speech‑to‑Text (và Text‑to‑Speech nếu cần) | Đăng ký tại <https://try.elevenlabs.io> và lấy API key |
| **Gmail** | Gửi email báo cáo | Tạo OAuth2 credential trong n8n |
| **HTTP Header Auth** | Đặt header `xi-api-key` cho ElevenLabs | Tạo credential trong n8n |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ <https://n8n.io/workflows/8755> hoặc sao chép toàn bộ JSON.
2. Trong n8n Editor, chọn **Import** → **Import from Clipboard** hoặc **Import from File**.
3. Dán JSON hoặc chọn file, rồi nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Cần cấu hình gì | Mẹo |
|------|----------|-----------------|-----|
| `When clicking ‘Execute workflow’` | `manualTrigger` | Không cần cấu hình | Dùng để chạy thủ công |
| `Loop Over Items` | `splitInBatches` | `Batch Size` (đặt 1 nếu chỉ xử lý một URL) | Giúp xử lý từng URL một |
| `Get audio urls` | `googleSheets` (read) | Sheet ID, Range (ví dụ: `Sheet1!A2:A`) | Đảm bảo cột `Audio URL` có dữ liệu |
| `Speech-to-Text` | `httpRequest` | Header `xi-api-key` = API key ElevenLabs | Đặt trong phần **Authentication** |
| `Update row` | `googleSheets` (update) | Sheet ID, Range, Row ID (được lấy từ `Get audio urls`) | Cập nhật cột `Transcript` và `Analysis` |
| `Transcript Analysis` | `googleGemini` | Prompt mẫu: “Analyze the following transcript and summarize key points.” | Đặt `Input` là `{{ $json["Transcript"] }}` |
| `Markdown` | `markdown` | Nội dung Markdown (được tạo từ `Transcript Analysis`) | Dùng để format email |
| `Add Transcript to Doc` | `googleDocs` (update) | Document ID, Range | Thêm transcript vào tài liệu |
| `Create Doc` | `googleDocs` (create) | Tên tài liệu | Tạo mới khi chưa có |
| `Send email` | `gmail` | To, Subject, Body (Markdown) | Đặt `To` = YOUR_EMAIL_ADDRESS |
| `Call 'ElevenLabs Text-to-Speech'` | `executeWorkflow` | Sub‑workflow ID (nếu có) | Dùng nếu muốn chuyển văn bản thành audio |
| `When Executed by Another Workflow` | `executeWorkflowTrigger` | Trigger ID | Dùng khi workflow được gọi từ workflow khác |
| `Execute workflow trigger` | `executeWorkflowTrigger` | Trigger ID | Dùng khi workflow được gọi từ workflow khác |

#### Cấu hình chi tiết từng node
1. **Get audio urls**  
   - **Sheet ID**: ID