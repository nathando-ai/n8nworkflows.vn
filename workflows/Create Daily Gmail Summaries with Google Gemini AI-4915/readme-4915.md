---
title: "🚀 Tự động tóm tắt email hàng ngày bằng Google Gemini – Giải pháp n8n hoàn hảo"
description: "Tự động lấy email, tóm tắt nội dung bằng AI, gửi lại bản tóm tắt qua Gmail, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tua-dong-tom-tat-email-hang-ngay-gemini"
tags: [n8n, automation, no-code, gmail, ai, google-gemini]
keywords: [n8n workflow, tự động hóa, tóm tắt email, Google Gemini, AI, Gmail]
---

# 🚀 Tự động tóm tắt email hàng ngày bằng Google Gemini – Giải pháp n8n hoàn hảo

Bạn đang phải đọc hàng trăm email mỗi ngày để tìm thông tin quan trọng? Thời gian dành cho việc lọc, đọc và ghi chú lại có thể chiếm tới 30% công việc hàng ngày của bạn. Giải pháp? **Tự động tóm tắt email** bằng AI, gửi lại bản tóm tắt qua Gmail – hoàn toàn không cần code, chỉ cần một workflow n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tóm tắt email trong vài giây thay vì đọc từng email.
- **Chính xác & nhất quán**: AI Gemini luôn cung cấp bản tóm tắt theo cấu trúc đã định.
- **Cá nhân hóa**: Dễ dàng điều chỉnh prompt để phù hợp với phong cách làm việc.
- **Hoạt động liên tục**: Chạy tự động mỗi ngày, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** có bật **OAuth2** và **Gmail API**.
- **Google Cloud Project** với **Gemini API** (Google Palm) đã được kích hoạt.
- **API Key** của Gemini (được lưu trong n8n credentials `googlePalmApi`).
- **N8n** đã cài đặt các node: `n8n-nodes-base.gmail`, `n8n-nodes-base.dateTime`, `@n8n/n8n-nodes-langchain.agent`, `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`, `@n8n/n8n-nodes-langchain.outputParserAutofixing`, `@n8n/n8n-nodes-langchain.outputParserStructured`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/4915) hoặc copy toàn bộ JSON.
2. Mở **n8n Editor**, chọn **Import** → **Import from JSON** → dán JSON hoặc tải file.
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách workflow của bạn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cài đặt cần chỉnh |
|------|-------|-------------------|
| **Schedule Trigger** | Kích hoạt workflow hàng ngày. | `Cron Expression` → `0 8 * * *` (tối thiểu 8h sáng) |
| **Date & Time** | Lấy ngày hiện tại. | `Operation` → `Get current date` |
| **Date & Time1** | Tính ngày hôm qua (để lấy email trong ngày). | `Operation` → `Subtract from date` → `Subtract 1 day` |
| **Gmail** (getAll) | Lấy danh sách email trong khoảng thời gian. | `Credentials` → `gmailOAuth2` <br> `Query` → `after:{{ $json["Date & Time1"]["result"]["date"] }} before:{{ $json["Date & Time"]["result"]["date"] }}` |
| **AI Agent** | Điều phối các node AI. | `Credentials` → `googlePalmApi` <br> `Prompt` → *định dạng prompt* (ví dụ: “Summarize the following emails into a concise report.”) |
| **Google Gemini Chat Model** | Gửi prompt tới Gemini. | `Credentials` → `googlePalmApi` <br> `Model` → `gemini-pro` |
| **Auto-fixing Output Parser** | Sửa lỗi cú pháp trong output của Gemini. | Không cần cấu hình đặc biệt. |
| **Structured Output Parser** | Chuyển output thành JSON có cấu trúc. | `Schema` → *định nghĩa JSON schema* (ví dụ: `{ "summary": "string" }`) |

> **Lưu ý**: Nếu workflow chưa có node gửi email, bạn có thể thêm một node **Gmail** (operation `send`) ngay sau `Structured Output Parser` để gửi bản tóm tắt tới địa chỉ email của mình.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo Gmail API và Gemini API đã bật).
2. Kiểm tra kết quả trong tab **Execution**: xem bản tóm tắt đã được tạo.
3. Khi mọi thứ ổn, bật **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notifications**: Thêm node **Slack** hoặc **Telegram** để nhận thông báo khi tóm tắt đã gửi.
- **Lưu log**: Dùng node **Google Drive** hoặc **Dropbox** để lưu bản tóm tắt dưới dạng PDF/Markdown.
- **Báo cáo định kỳ**: Kết hợp với node **Schedule Trigger** để gửi báo cáo hàng tuần hoặc hàng tháng.
- **Tùy chỉnh prompt**: Thay đổi prompt trong **AI Agent** để yêu cầu tóm tắt theo phong cách khác (ví dụ: “Summarize in bullet points” hoặc “Highlight action items only”).

### 📌 Kết luận
Workflow “Create Daily Gmail Summaries with Google Gemini AI” giúp bạn:
- **Tự động** lấy, tóm tắt và gửi lại email hàng ngày.
- **Tiết kiệm** thời gian và giảm thiểu sai sót.
- **Tích hợp**