---
title: "🚀 Tạo Video & Voice Outreach Cá Nhân Hóa Tự Động với HeyGen, ElevenLabs & Perplexity"
description: "Giải pháp tự động tạo video, voice note và email cá nhân hóa cho lead mới trong Google Sheets, hoàn toàn không cần code."
slug: "tao-video-voice-personalized-heygen-elevenlabs-perplexity"
tags: [n8n, automation, no-code, lead-nurturing, multimodal-ai, ai-video, ai-voice, outreach]
keywords: [n8n workflow, tự động hóa, AI video, AI voice, outreach, lead nurturing, multimodal AI]
---

# 🚀 Tạo Video & Voice Outreach Cá Nhân Hóa Tự Động với HeyGen, ElevenLabs & Perplexity

Bạn đang gặp khó khăn khi phải tạo video, voice note và email cá nhân hóa cho từng lead mới? Việc này không chỉ tốn thời gian mà còn dễ gây sai sót khi làm thủ công. Workflow này sẽ giúp bạn **tự động** nhận dữ liệu từ Google Sheets, nghiên cứu thông tin, viết kịch bản, tạo video, chuyển văn bản thành giọng nói, lưu file, và gửi email (hoặc SMS/WhatsApp) – tất cả **không cần viết một dòng code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ làm thủ công xuống vài phút.
- **Độ chính xác cao**: Mọi dữ liệu được lấy trực tiếp từ Google Sheets, tránh lỗi nhập liệu.
- **Cá nhân hóa tối đa**: Video, voice note và email được tùy chỉnh dựa trên thông tin lead.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần giám sát.
- **Chi phí thấp**: Sử dụng các dịch vụ API với mức giá hợp lý, không cần đội ngũ phát triển.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Tài khoản Google, ID bảng tính, tên sheet.
- **Google Drive**: Tài khoản Google, thư mục lưu file.
- **Gmail**: Tài khoản Gmail, bật API và tạo OAuth 2.0 credentials.
- **Twilio** (tùy chọn): Số điện thoại, Account SID, Auth Token.
- **Perplexity**: API Key.
- **OpenAI**: API Key (đối với GPT‑5.1, GPT‑4.1‑mini).
- **OpenRouter**: API Key (đối với `openai/gpt-5.1`).
- **ElevenLabs**: API Key.
- **HeyGen**: API Key (được cung cấp khi đăng ký dịch vụ).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
- Tải file JSON từ link gốc: <https://n8n.io/workflows/11326>.
- Mở n8n Editor → `File` → `Import` → chọn file JSON.
- Hoặc copy toàn bộ JSON và dán vào `Import` → `Paste JSON`.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cài đặt cần chỉnh |
|------|-------|--------------------|
| **Google Sheets Trigger** | Gọi khi có dòng mới | Spreadsheet ID, Sheet name, Trigger type |
| **Code (JavaScript)** | Lấy dòng mới nhất | Không cần credentials |
| **Research Agent** | Sử dụng Perplexity | Chọn model `sonar-pro`, API Key |
| **Scripting Agent** | Viết kịch bản 30s | Không cần credentials |
| **OpenAI Chat Model** | Hỗ trợ nghiên cứu | API Key, Model `gpt-5.1` |
| **OpenRouter Chat Model** | Hỗ trợ nghiên cứu | API Key, Model `openai/gpt-5.1` |
| **Heygen Clone AI Creation** | Tạo video avatar | API Key, Body (JSON) với script |
| **Wait 30s** | Đợi video xử lý | Không cần chỉnh |
| **GET Result** | Kiểm tra trạng thái video | URL trả về từ HeyGen |
| **OpenAI Chat Model1** | Tạo email JSON | API Key, Model `gpt-4.1-mini` |
| **Structured Output Parser** | Phân tích JSON email | Không cần chỉnh |
| **OpenAI Chat Model2** | Xử lý thêm nếu cần | API Key, Model `gpt-4.1-mini` |
| **Convert text to speech (ElevenLabs)** | Tạo voice note | API Key, Voice ID |
| **Upload file (Google Drive)** | Lưu file audio | Google Drive credentials, thư mục |
| **Send a message (Gmail)** | Gửi email | Gmail credentials, Đính kèm video link |
| **Send an SMS/MMS/WhatsApp message (Twilio)** | Gửi link voice note (tùy chọn) | Twilio credentials, Phone number |
| **Sticky Note** | Ghi chú nội bộ | Không cần chỉnh |

> **Lưu ý**: Các node `agent` và `lmChat*` đều cần **API Key** được cấu hình trong phần `Credentials` của n8n. Đảm bảo các key này đã được bật và có quyền truy cập đầy đủ.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo Google Sheet có ít nhất một dòng dữ liệu).
2. Kiểm tra log: Đảm bảo không có lỗi và video, voice note được tạo.
3. **Bật Active**: Nhấn `Activate` để workflow tự động chạy khi có dòng mới.

## ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack**: Thêm node `Slack` để gửi link video/voice note ngay khi hoàn thành.
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại trạng thái, thời gian, link video.
- **Gửi báo cáo định kỳ**: Sử dụng node `Cron` để gửi email tổng hợp hàng ngày/tuần.
- **Tích hợp CRM**: Khi lead được chuyển sang trạng thái “Contacted”, tự động cập nhật vào HubSpot hoặc Salesforce.

## 📌 Kết luận
Workflow này giúp các sếp **tạo ra tài nguyên outreach** (video, voice note, email) một cách nhanh chóng, chính xác và cá nhân hóa. Bạn chỉ cần cấu hình một vài credentials và để n8n làm công việc nặng nề. Hãy thử ngay, và nếu muốn tùy chỉnh thêm, hãy tham khảo tutorial chi tiết tại <https://www.youtube.com/watch?v=q9AAh9zRou4> hoặc liên hệ với tác giả Automate With Marc để được hỗ trợ. Happy automating!