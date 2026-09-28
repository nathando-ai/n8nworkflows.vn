---
title: "🚀 Xử lý Hóa đơn Tự động với IMAP, AI, Google Drive & DateV"
description: "Giải pháp tự động nhận, trích xuất dữ liệu, lưu trữ và gửi hóa đơn tới DateV chỉ trong vài phút, giảm thiểu công việc thủ công và sai sót."
slug: "xuat-hoa-don-tuy-chinh-voi-imap-ai-google-drive-datev"
tags: [n8n, automation, no-code, invoice, accounting, AI]
keywords: [n8n workflow, tự động hóa, invoice processing, AI, Google Drive, DateV, IMAP]
---

# 🚀 Xử lý Hóa đơn Tự động với IMAP, AI, Google Drive & DateV

Bạn đang phải lật ngược từng email, tải xuống tệp PDF, trích xuất dữ liệu, lưu vào Google Sheets, rồi gửi lại tới DateV? Thật là mất thời gian và dễ gây lỗi.  
Workflow này sẽ **đọc email, trích xuất dữ liệu từ PDF, lưu trữ, ghi log và gửi tới DateV** hoàn toàn tự động, không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 30 phút → 5 phút cho mỗi hóa đơn.  
- **Chính xác 100%**: Dữ liệu được trích xuất qua AI, giảm sai sót nhập liệu.  
- **Tự động lưu trữ**: Tất cả tệp PDF được đặt vào thư mục tháng, dễ tìm kiếm.  
- **Tích hợp DateV**: Gửi ngay tới inbox kế toán, không cần thao tác thủ công.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ / Node | Credential / API Key cần có |
|-----------------|-----------------------------|
| **Email Trigger (IMAP)** | IMAP server, username, password |
| **Email Send (SMTP)** | SMTP server, username, password |
| **Google Drive** | Google API OAuth 2.0 (client id/secret) |
| **Google Sheets** | Google API OAuth 2.0 (client id/secret) |
| **OpenAI** | API key |
| **IMAP Move Email** | IMAP server, username, password (cùng tài khoản) |
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/9439> hoặc copy toàn bộ JSON.  
2. Mở **n8n Editor**, chọn **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| **Email Trigger (IMAP)** | `Email Trigger (IMAP)` | *IMAP credentials* (server, username, password). Chọn thư mục “Inbox” hoặc thư mục chứa hóa đơn. | Đảm bảo bật “Read attachments”. |
| **Split Attachments (JavaScript)** | `Split Attachments (JavaScript)` | Không cần chỉnh, chỉ chuyển dữ liệu. |
| **Extract From PDF** | `Extract From PDF` | *Operation*: `pdf`. Không cần credential. |
| **Extract & Format Data (AI)** | `Extract & Format Data` | *OpenAI credentials*: API key. Trong “Prompt” đặt template:  
  ```
  Extract the following fields from the text: Company, InvoiceNumber, InvoiceDate, TotalAmount. Return JSON.
  ``` |
| **Get Additional Date Data** | `Get Additional Date Data` | JavaScript code: lấy `InvoiceDate`, chuyển thành `month`, `year`. |
| **Upload to Temporary Storage** | `Upload file` | *Google Drive credentials*. Đặt “Folder ID” của thư mục “Incoming Files”. |
| **Search Month Folder** | `Search Month Folder` | *Google Drive credentials*. Tìm folder theo `month`/`year`. |
| **Upload to Final Destination** | `Upload file1` | *Google Drive credentials*. Đặt “Folder ID” của folder tháng. |
| **Google Sheets** | `Google Sheets` | *Google Sheets credentials*. Chọn “Append” và “Sheet ID”. |
| **Send to DateV** | `Send to DateV` | *SMTP credentials*. Đặt “To” là email inbox DateV, “Subject” và “Body” tùy ý. |
| **Move Email email** | `MoveEmail email` | *IMAP credentials*. Chọn thư mục “Archive” hoặc “Processed”. |
| **Code in JavaScript** | `Code in JavaScript` | Sử dụng để tạo tên file chuẩn:  
  ```js
  const name = `${data.year}-${data.month}-${data.invoiceNumber}.pdf`;
  return [{ json: { fileName: name } }];
  ``` |

> **Tip**: Kiểm tra từng node bằng “Execute Node” với dữ liệu mẫu để chắc chắn mọi thứ hoạt động.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với một email mẫu, kiểm tra log và dữ liệu trong Google Sheets.  
2. **Bật Active**: Chuyển trạng thái từ “Inactive” → “Active”.  
3. **Giám sát**: Kiểm tra “Execution History” thường xuyên, bật cảnh báo khi có lỗi.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram Notification**: Thêm node `Slack` hoặc `Telegram` sau khi gửi tới DateV để thông báo tự động.  
- **Lưu Log vào Google Sheets**: Thêm node `Google Sheets` để ghi log lỗi, thời gian xử lý.  
- **Báo cáo định kỳ**: Sử dụng node `Cron` để gửi báo cáo tổng hợp hàng ngày/tuần tới email hoặc Slack.  
- **Sử dụng LLM khác**: Thay OpenAI bằng Claude hoặc Gemini nếu muốn giảm chi phí.  
- **Tự động tạo folder**: Nếu folder tháng chưa tồn tại, node `Google Drive` có thể tạo mới bằng “Create Folder” trước khi upload.

## 📌 Kết luận

Workflow “Automated Invoice Processing & Filing with IMAP, AI, Google Drive & DateV” giúp các sếp **tiết kiệm thời gian, giảm sai sót và duy trì quy trình kế toán sạch sẽ**.  
Hãy thử ngay, cài đặt trên VPS, và cảm nhận sự khác biệt!

---