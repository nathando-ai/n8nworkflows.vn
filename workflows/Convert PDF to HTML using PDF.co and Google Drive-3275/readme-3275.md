---
title: "🚀 Chuyển PDF sang HTML tự động với PDF.co và Google Drive"
description: "Workflow n8n giúp tự động chuyển file PDF mới được tải lên Google Drive thành file HTML và lưu lại, hoàn toàn không cần code."
slug: "chuyen-pdf-sang-html-tro-vi-pdfco-giua-google-drive"
tags: [n8n, automation, no-code, google-drive, pdf, pdfco]
keywords: [n8n workflow, tự động hóa, chuyển PDF sang HTML, PDF.co, Google Drive]
---

# 🚀 Chuyển PDF sang HTML tự động với PDF.co và Google Drive

Bạn đang phải tốn thời gian và công sức để chuyển đổi hàng trăm file PDF sang HTML mỗi ngày? Workflow này sẽ giúp bạn giải quyết hoàn toàn vấn đề đó, chỉ cần một lần cấu hình và để n8n làm việc 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động chuyển đổi ngay khi file được tải lên.
- **Độ chính xác cao**: PDF.co cung cấp API chuyển đổi chất lượng, giảm lỗi so với công cụ thủ công.
- **Tích hợp liền mạch**: Lưu file HTML ngay vào thư mục Google Drive đã định sẵn.
- **Không cần code**: Chỉ cần cấu hình một vài node, workflow hoạt động 24/7.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Drive OAuth2 credentials**: Đăng ký ứng dụng Google Cloud, lấy Client ID & Client Secret, cấp quyền đọc/ghi thư mục cần dùng.
- **PDF.co API Key**: Đăng ký tại <https://pdf.co> và lấy API Key.
- **Folder ID**: ID thư mục nguồn (điều kiện file PDF) và ID thư mục đích (để lưu file HTML).
- **n8n**: Cài đặt phiên bản mới nhất (Self-hosted hoặc Cloud).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ <https://n8n.io/workflows/3275> hoặc sao chép nội dung JSON vào clipboard.
2. Mở n8n Editor → **Import** → **Import from clipboard** hoặc **Import from file**.
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| Google Drive Trigger | `Google Drive Trigger` | **Folder ID** (điều kiện file mới trong thư mục nguồn) | Chọn folder ID trong trường “Folder ID” |
| If | `If` | **Conditions**: `$json.mimeType === 'application/pdf'` | Kiểm tra file là PDF |
| HTTP Request | `HTTP Request` | <ul><li>Method: POST</li><li>URL: `https://api.pdf.co/v1/pdf/convert/to/html`</li><li>Headers: <br>`x-api-key: {{ $json.apiKey }}`<br>`Content-Type: application/json`</li><li>Body (JSON):<br>`{ "url": "https://drive.google.com/uc?export=download&id={{$json.id}}" }`</li></ul> | Sử dụng API PDF.co để chuyển đổi |
| Convert to Binary File | `Convert to Binary File` | **Binary Property**: `data` (điều chỉnh tên property nếu khác) | Chuyển response JSON thành file binary |
| Google Drive | `Google Drive` | <ul><li>Folder ID: ID thư mục đích</li><li>File Name: `{{$json.name}}.html`</li><li>Binary Property: `data`</li></ul> | Lưu file HTML vào Google Drive |
| Sticky Note | `Sticky Note` | Không cần chỉnh | Ghi chú cho workflow |

> **Lưu ý**: Trong node `HTTP Request`, bạn cần thay `{{ $json.apiKey }}` bằng API Key PDF.co. Bạn có thể lưu API Key vào **Credentials** của n8n (đặt tên `pdfcoApiKey`) và dùng `{{$credentials.pdfcoApiKey}}`.

### 3. Kích hoạt ⚡️
1. **Test run**: Chọn một file PDF trong thư mục nguồn, chạy workflow thủ công để kiểm tra.
2. Kiểm tra output: File HTML xuất hiện trong thư mục đích.
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack Notification**: Thêm node Slack để gửi tin nhắn khi file HTML được tạo thành công.
- **Logging**: Ghi log vào Google Sheets hoặc database để theo dõi lịch sử chuyển đổi.
- **Scheduled Run**: Thêm node Cron để chạy kiểm tra định kỳ (để xử lý file đã bỏ qua).
- **Email Report**: Gửi email cho người dùng khi file HTML sẵn sàng.
- **Multi-format**: Thêm các node chuyển đổi khác (PDF → PNG, PDF → DOCX) trong cùng workflow.

## 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian, giảm lỗi và tăng tính linh hoạt trong quản lý tài liệu. Hãy thử ngay, cấu hình nhanh và để n8n tự động chuyển đổi PDF sang HTML cho bạn!