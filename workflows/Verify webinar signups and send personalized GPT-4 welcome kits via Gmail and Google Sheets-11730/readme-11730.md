---
title: "🚀 Tự động hoá đăng ký webinar & gửi Welcome Kit AI qua Gmail"
description: "Giải pháp tự động kiểm tra email đăng ký webinar, lưu dữ liệu, tạo Welcome Kit AI, gửi email, thông báo Slack, hỗ trợ tài liệu bổ sung."
slug: "tuyendung-webinar-gui-welcome-kit-ai"
tags: [n8n, automation, no-code, webinar, email, AI, google-sheets, slack, openai]
keywords: [n8n workflow, tự động hóa, webinar, email verification, welcome kit, AI]
---

# 🚀 Tự động hoá đăng ký webinar & gửi Welcome Kit AI qua Gmail

Bạn đang phải xử lý hàng trăm đăng ký webinar mỗi ngày? Mỗi lần phải kiểm tra email thủ công, gửi email chào mừng, lưu dữ liệu… Thời gian và công sức tiêu tốn rất lớn, còn sai sót dễ xảy ra.  
Workflow này sẽ **đánh giá email ngay khi người dùng đăng ký**, **đẩy dữ liệu vào Google Sheets**, **tạo Welcome Kit AI** (PDF) và **gửi email** ngay lập tức, đồng thời **thông báo Slack** cho ban tổ chức. Tất cả đều 100% không cần code, chỉ cần cấu hình một vài credential.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút thành vài giây cho mỗi đăng ký.  
- **Chính xác dữ liệu**: Email được xác thực ngay lập tức, tránh spam và sai sót.  
- **Cá nhân hóa trải nghiệm**: Welcome Kit được tạo dựa trên tên, công ty và sở thích của người đăng ký.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần giám sát.  
- **Tích hợp đa nền tảng**: Gmail, Slack, Google Sheets, Google Drive, OpenAI, VerifiEmail.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **VerifiEmail**: API key (đăng ký tại https://verifi.email).  
- **Slack**: Token bot và ID kênh thông báo.  
- **Google Sheets**: OAuth2 credentials và ID bảng tính (đặt sheet “Attendees”).  
- **Google Drive**: OAuth2 credentials và ID thư mục lưu PDF.  
- **OpenAI**: API key (đăng ký tại https://platform.openai.com).  
- **Gmail**: OAuth2 credentials (đăng ký ứng dụng Google Cloud).  
- **Webhook**: Địa chỉ URL n8n (được tạo khi import).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/11730) hoặc copy toàn bộ JSON.  
2. Mở **n8n Editor**, chọn **Import** → **JSON** → dán nội dung.  
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Mô tả | Tham số cần cấu hình |
|------|----------|-------|----------------------|
| Webhook | Webhook | Nhận dữ liệu đăng ký | `path: webinar-signup`, `httpMethod: POST` |
| VerifiEmail | VerifiEmail - Verify Email | Kiểm tra email | `verifiEmailApi` |
| If | Check Email Valid | Kiểm tra `isValid` | `conditions: isValid == true` |
| Slack | Alert - Invalid Email | Thông báo email không hợp lệ | `slackApi`, `channelId` |
| Stop and Error | Stop and Error | Dừng workflow khi email sai | - |
| Google Sheets | Store Attendee Data | Lưu dữ liệu | `googleSheetsOAuth2Api`, `operation: append`, `sheetId`, `range` |
| OpenAI | Generate Welcome Message | Tạo nội dung chào mừng | `openAiApi`, `prompt` (đưa tên, công ty, sở thích) |
| Google Drive | Create Welcome Doc | Tạo file từ text | `googleDriveOAuth2Api`, `operation: createFromText`, `folderId` |
| Google Drive | Convert to PDF | Tải file PDF | `googleDriveOAuth2Api`, `operation: download`, `fileId` |
| Gmail | Send Welcome Email | Gửi email chào mừng | `gmailOAuth2`, `to`, `subject`, `body`, `attachments` |
| Slack | Notify Organizers | Thông báo đăng ký thành công | `slackApi`, `channelId` |
| If | Check Extra Materials Requested | Kiểm tra yêu cầu tài liệu | `conditions: requestExtra == true` |
| OpenAI | Generate Extra Materials | Tạo nội dung tài liệu | `openAiApi`, `prompt` (đưa chủ đề) |
| Google Drive | Create Extra Materials PDF | Tạo PDF tài liệu | `googleDriveOAuth2Api`, `operation: createFromText`, `folderId` |
| Google Drive | Convert to PDF (Extra Materials) | Tải PDF tài liệu | `googleDriveOAuth2Api`, `operation: download`, `fileId` |
| Gmail | Send Follow-up Email | Gửi email kèm tài liệu | `gmailOAuth2`, `to`, `subject`, `body`, `attachments` |

> **Lưu ý**:  
> - Đảm bảo **OAuth2** đã được cấp quyền đầy đủ