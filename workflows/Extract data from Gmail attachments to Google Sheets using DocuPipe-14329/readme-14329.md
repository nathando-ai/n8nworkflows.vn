---
title: "🚀 Tự động trích xuất dữ liệu từ tệp đính kèm Gmail vào Google Sheets bằng DocuPipe"
description: "Giải pháp tự động 100% không cần code: nhận email, trích xuất dữ liệu AI từ tệp đính kèm, lưu vào Google Sheets và sao lưu lên Google Drive."
slug: "tac-dong-trich-xuat-du-lieu-gmail-attachment-google-sheets-docupipe"
tags: [n8n, automation, no-code, gmail, google-sheets, docupipe]
keywords: [n8n workflow, tự động hóa, docupipe, gmail attachments, google sheets]
---

# 🚀 Tự động trích xuất dữ liệu từ tệp đính kèm Gmail vào Google Sheets bằng DocuPipe

Bạn đang nhận hàng nghìn email chứa hóa đơn, hợp đồng, phiếu thu… và phải trích xuất dữ liệu thủ công?  
Workflow này sẽ **đánh dấu** email, **tải lên** DocuPipe để AI trích xuất, **sao lưu** tệp lên Google Drive, rồi **đưa dữ liệu** vào Google Sheets – hoàn toàn tự động, không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút sang vài giây.  
- **Chính xác**: AI DocuPipe giảm sai sót so với nhập tay.  
- **Cá nhân hóa**: Thêm metadata (tên file, thời gian) ngay trong sheet.  
- **Hoạt động liên tục**: 24/7, không cần giám sát.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Mô tả | Lưu ý |
|---------|-------|-------|
| **Gmail** | Tài khoản Gmail có quyền truy cập API | Tạo label “DocuPipe - Processing” (hoặc tùy chỉnh) |
| **DocuPipe** | Tài khoản DocuPipe + API key | Đăng ký tại [docupipe.ai](https://docupipe.ai) |
| **Google Drive** | Tài khoản Google Drive | Folder backup (được chọn trong node) |
| **Google Sheets** | Tài khoản Google Sheets | Sheet header phải khớp với schema DocuPipe |
| **n8n Community Node** | `n8n-nodes-docupipe` | Cài đặt qua Settings → Community Nodes |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/14329>  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Xác nhận import, workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên trong workflow | Tham số cần cấu hình | Ghi chú |
|------|--------------------|----------------------|---------|
| **New Email with Attachment** | `gmailTrigger` | `gmailOAuth2` | Đăng ký OAuth2 cho Gmail. |
| **Label as Processing** | `gmail` | `gmailOAuth2` | `operation: addLabels`, `resource: message`, `labels: DocuPipe - Processing`. |
| **Upload Attachment & Extract Data** | `docuPipe` | `docuPipeApi` | `operation: uploadAndExtract`, `resource: extraction`, chọn **Schema** trong DocuPipe. |
| **Save Attachment to Drive** | `googleDrive` | `googleDriveOAuth2Api` | `operation: upload`, chọn **Folder** backup. |
| **Extraction Complete** | `docuPipeTrigger` | `docuPipeApi` | Webhook tự động, không cần chỉnh. |
| **Get Extracted Data** | `docuPipe` | `docuPipeApi` | `operation: getResult`, `resource: extraction`. |
| **Process Extraction Result** | `code` | - | Dùng JavaScript để flatten dữ liệu, thêm metadata. |
| **Add Metadata** | `set` | - | Thêm `DocumentName`, `ProcessedAt`. |
| **Append Row to Spreadsheet** | `googleSheets` | `googleSheetsOAuth2Api` | `operation: appendRow`, chọn **Spreadsheet** và **Sheet**. |

#### Cấu hình chi tiết

- **gmailOAuth2**: Tạo trong Credentials → Gmail → OAuth2.  
- **docuPipeApi**: Tạo trong Credentials → DocuPipe → API Key.  
- **googleDriveOAuth2Api**: Tạo trong Credentials → Google Drive → OAuth2.  
- **googleSheetsOAuth2Api**: Tạo trong Credentials → Google Sheets → OAuth2.  

> **Tip**: Đảm bảo quyền truy cập đầy đủ (read/write) cho từng dịch vụ.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với một email mẫu có attachment. Kiểm tra log, xem dữ liệu đã được trích xuất và ghi vào Google Sheets chưa.  
2. **Bật Active**: Sau khi xác nhận, chuyển workflow sang trạng thái **Active**.  
3. **Theo dõi**: Kiểm tra log định kỳ, đảm bảo không có lỗi “Missing credentials” hoặc “Invalid schema”.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram notification**: Thêm node `slack` hoặc `telegram` sau `Append Row` để thông báo khi dữ liệu được ghi vào sheet.  
- **Lưu log vào Google Sheets**: Sử dụng node `googleSheets` để ghi log lỗi, thời gian xử lý.  
- **Định kỳ backup**: Dùng node `cron` để chạy một workflow khác sao lưu toàn bộ sheet vào Google Drive.  
- **Tùy chỉnh schema**: Tạo nhiều schema trong DocuPipe (ví dụ: Hóa đơn, Hợp đồng) và dùng node `switch` để chọn schema phù hợp dựa vào tên file.  

## 📌 Kết luận

Workflow “Tự động trích xuất dữ liệu từ tệp đính kèm Gmail vào Google Sheets bằng DocuPipe” giúp các sếp tiết kiệm thời gian, giảm sai sót và tăng tính liên tục trong quản lý dữ liệu tài liệu.  
Hãy **đăng ký** tài khoản DocuPipe, **cài đặt** các credentials, **import** workflow và **bật** nó ngay hôm nay để trải nghiệm tự động hóa 100% không cần code!