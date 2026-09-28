---  
title: "🚀 Phân loại tài liệu bằng Gemini và sắp xếp tự động vào Google Drive"  
description: "Tự động phân loại, đổi tên và di chuyển tài liệu từ Google Drive Inbox, ghi log vào Sheets, tạo sự kiện lịch và gửi thông báo qua Gmail – hoàn toàn không cần code."  
slug: "phan-loai-tai-lieu-gemini-google-drive"  
tags: [n8n, automation, no-code, google-drive, gemini, ai]  
keywords: [n8n workflow, tự động hóa, Gemini OCR, Google Drive, Google Sheets, Google Calendar, Gmail]  
---  

# 🚀 Phân loại tài liệu bằng Gemini và sắp xếp tự động vào Google Drive  

Bạn đang phải xử lý hàng trăm, hàng nghìn file PDF, ảnh, hay tài liệu khác trong Google Drive?  
Mỗi file cần được phân loại, đổi tên, di chuyển vào thư mục phù hợp, ghi log và thậm chí tạo lịch hẹn nếu có deadline.  
Đây là nỗi đau thực tế của nhiều doanh nghiệp, đặc biệt là các bộ phận tài chính, pháp lý, HR.  

Workflow này giải quyết toàn bộ quy trình trên bằng **Gemini 2.5 Flash OCR** và các node n8n, giúp bạn **tự động hóa 100% không cần code**.  

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)  
:::

## 🎯 Kết quả các sếp nhận được  
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ vài giờ xử lý thủ công xuống vài phút.  
- **Chính xác**: Gemini OCR nhận diện chính xác loại tài liệu và deadline.  
- **Cá nhân hóa**: Định dạng tên file chuẩn, thư mục phù hợp.  
- **Hoạt động liên tục**: Chạy tự động 24/7, ghi log và gửi thông báo kịp thời.  
:::

## 🔧 Yêu cầu cần thiết  
:::info[CHUẨN BỊ]  
- **Google Drive**: Credential có quyền đọc/ghi.  
- **Google Sheets**: Credential và ID bảng log (thành công) và bảng log lỗi.  
- **Google Calendar**: Credential và ID lịch.  
- **Gmail**: Credential và địa chỉ email nhận thông báo.  
- **Gemini API Key**: Credential “Query Auth” (parameter name: `key`).  
- **Folder IDs**:  
  - Inbox folder ID (được lấy trong node “Get inbox files”).  
  - Folder IDs cho từng loại tài liệu (được cấu hình trong node “Generate filename”).  
- **Spreadsheet ID**: Đã tạo sẵn bảng log (cột: File ID, Tên file, Loại, Thời gian, Deadline, Ghi chú).  
- **Calendar ID**: Đã tạo sẵn lịch (để ghi nhận deadline).  
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥  
- Tải file JSON từ <https://n8n.io/workflows/15866> hoặc copy nội dung JSON vào **n8n Editor** → **Import**.  
- Kiểm tra lại tên workflow: **Classify documents with Gemini and organize them in Google Drive**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
| Node | Tên node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| **Get inbox files** | `Get inbox files` | `resource: fileFolder`, `folderId` (Inbox folder ID) | Chỉ lấy file, không folder. |
| **Loop through files** | `Loop through files` | `batchSize: 10` (hoặc tùy nhu cầu) | Đảm bảo không vượt quá quota. |
| **Download file** | `Download file` | `fileId` (được truyền từ loop) | Credential Google Drive. |
| **Check file type** | `Check file type` | `Switch` conditions: `mimeType` = `application/pdf` hoặc `image/*` | Xử lý file PDF/ảnh. |
| **Convert to Base64** | `Convert to Base64` | Code: `return [{ json: { base64: Buffer.from(item.binary.data, 'binary').toString('base64') } }]` | Đảm bảo `binary.data` có dữ liệu. |
| **Gemini OCR classification** | `Gemini OCR classification` | `URL: https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent` <br> `Method: POST` <br> `Body: { contents: [{ mimeType: 'image/png', data: $json.base64 }] }` <br> `Auth: Query Auth (key)` | Thay `mimeType` tùy file. |
| **Parse AI response** | `Parse AI response` | Code: `return [{ json: { type: $json.responses[0].candidates[0].content.parts[0].text, confidence: $json.responses[0].candidates[0].content.parts[0].confidence } }]` | Kiểm tra `confidence` > 0.6. |
| **Classification check** | `Classification check` | `If` condition: `{{$json.confidence}} > 0.6` | Nếu không đủ, chuyển sang node “Handle unsupported format”. |
| **Generate filename** | `Generate filename` | Code: `return [{ json: { newName: $json.type + '_' + $now + '.' + $json.extension } }]` | Tùy chỉnh pattern. |
| **Rename file** | `Rename file` | `fileId`, `newName` (từ node “Generate filename”) | Credential Google Drive. |
| **Move to folder** | `Move to folder` | `fileId`, `folderId` (định danh folder theo loại) | Đảm bảo folder tồn tại. |
| **Log to spreadsheet** | `Log to spreadsheet` | `Spreadsheet ID`, `Sheet Name`, `Row Data` (File ID, Tên, Loại, Thời gian, Deadline) | Credential Google Sheets. |
| **Has deadline?** | `Has deadline?` | `If` condition: `{{$json.deadline}} != ''` | Nếu có, tiếp tục. |
| **Add to calendar** | `Add to calendar` | `Calendar ID`, `Event Title`, `Start Time`, `End Time` | Credential Google Calendar. |
| **Send deadline alert** | `Send deadline alert` | `To`, `Subject`, `Body` (đưa thông tin deadline) | Credential Gmail. |
| **Send error notification** | `Send error notification` | `To`, `Subject`, `Body` (đưa lỗi) | Credential Gmail. |
| **Log error to sheet** | `Log error to sheet` | `Spreadsheet ID`, `Sheet Name`, `Row Data` (File ID, Lỗi, Thời gian) | Credential Google Sheets. |
| **Handle unsupported format** | `Handle unsupported format` | Code: `return [{ json: { error: 'Unsupported file format' } }]` | Gửi email lỗi. |
| **Done - no deadline** | `Done - no deadline` | `NoOp` | Chỉ để kết thúc luồng. |
| **When clicking 'Execute workflow'** | `When clicking 'Execute workflow'` | `Manual Trigger` | Để chạy thủ công. |

### 3. Kích hoạt ⚡️  
- **Test run**: Chọn một file mẫu trong Inbox, chạy workflow thủ công, kiểm tra log và thư mục đích.  
- **Bật Active**: Khi đã ổn định, bật **Active** cho workflow.  

## ✍️ Mẹo & gợi ý nâng cao  
- **Gửi báo cáo định kỳ**: Thêm node “Cron” để chạy hàng ngày, ghi log tổng hợp vào Google Sheets.  
- **Slack/Telegram notification**: Thêm node “Slack” hoặc “Telegram” để nhận thông báo ngay khi có deadline.  
- **Lưu log chi tiết**: Sử dụng node “Code” để ghi log vào CloudWatch hoặc Firebase.  
- **Tăng độ tin cậy**: Sử dụng “Retry” node cho HTTP Request (Gemini) với 3 lần thử.  

## 📌 Kết luận  
Workflow này giúp các sếp tiết kiệm thời gian, giảm sai sót và tăng tính minh bạch trong quản lý tài liệu.  
Hãy thử triển khai ngay, tùy chỉnh prompt Gemini, pattern tên file và các folder ID phù hợp với doanh nghiệp của mình.  

Chúc các sếp thành công và tiết kiệm thời gian!