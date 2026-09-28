---
title: "🚀 So sánh Báo giá Nhà cung cấp bằng Grok AI & Xuất ra Google Sheets & Email"
description: "Tự động so sánh báo giá từ nhiều nhà cung cấp, tóm tắt bằng AI, lưu vào Google Sheets và gửi email ngay lập tức – giải pháp hoàn toàn không cần code."
slug: "so-sanh-bao-gia-nha-cung-cap-grok-ai-gsheet-email"
tags: [n8n, automation, no-code, vendor-management, ai-summarization]
keywords: [n8n workflow, tự động hóa, so sánh báo giá, Grok AI, Google Sheets]
---

# 🚀 So sánh Báo giá Nhà cung cấp bằng Grok AI & Xuất ra Google Sheets & Email

Bạn đang phải xử lý hàng trăm báo giá từ các nhà cung cấp, trích xuất dữ liệu, so sánh, và gửi báo cáo cho bộ phận mua hàng? Việc làm thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Workflow này giúp bạn **tự động** nhận file báo giá, **trích xuất** dữ liệu, **tóm tắt** bằng AI, **lưu trữ** vào Google Sheets và **gửi email** ngay lập tức – toàn bộ mà không cần viết một dòng code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ làm thủ công xuống chỉ vài phút.
- **Độ chính xác cao**: Trích xuất dữ liệu tự động, giảm lỗi nhập liệu.
- **Cá nhân hóa báo cáo**: AI tóm tắt nhanh, dễ đọc, dễ so sánh.
- **Hoạt động liên tục**: Lưu trữ lịch sử, dễ dàng truy xuất và phân tích sau này.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Google Sheets**: Tạo một sheet với các cột: `Vendor Name`, `Total Amount`, `Delivery Timeline`, `AI Summary`, `Status`.
- **Google API Credentials**: Tạo OAuth 2.0 client ID trong Google Cloud Console, cấp quyền `https://www.googleapis.com/auth/spreadsheets`.
- **SMTP Credentials**: Email server (Gmail, Outlook, hoặc nhà cung cấp SMTP khác) với tên người dùng, mật khẩu và port.
- **Grok API Key**: Đăng ký tại [Grok.ai](https://grok.ai) và lấy API key.
- **Webhook URL**: Được tạo khi bạn import workflow, sẽ dùng để gửi file báo giá.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/6688) hoặc copy toàn bộ JSON.
2. Mở n8n editor, chọn **Import** → **Import from file** hoặc **Paste JSON**.
3. Xác nhận và lưu.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| 1 | `Upload Quotes` | **Webhook Path**: `vendor-quote-upload` (đã được thiết lập) | Đảm bảo endpoint công khai (HTTPS). |
| 2 | `Extract File Data` | **Code**: Chèn script JavaScript để parse PDF/Excel. | Sử dụng `pdf-parse` hoặc `xlsx` nếu cần. |
| 3 | `AI Summarization` | **HTTP Request**: <br>• URL: `https://api.grok.ai/v1/chat/completions` <br>• Method: POST <br>• Headers: `Authorization: Bearer YOUR_GROK_API_KEY` <br>• Body: JSON với `model`, `messages` (đưa dữ liệu trích xuất). | Đặt `model` là `grok-1.5`. |
| 4 | `Format Summary` | **Code**: Dùng JavaScript để chuyển đổi AI response thành bảng JSON. | Định dạng theo cột Google Sheet. |
| 5 | `Log to Google Sheets` | **Credentials**: `googleApi` đã tạo. <br>• Spreadsheet ID: ID của sheet. <br>• Worksheet: `Sheet1` (hoặc tên sheet). | Chọn `append` để thêm dòng mới. |
| 6 | `Wait For Reply` | **Wait**: `Wait for 5 seconds` (hoặc tùy chỉnh). | Đảm bảo AI đã trả về. |
| 7 | `Send email` | **SMTP Credentials**: `smtp` đã tạo. <br>• To: Email nhận. <br>• Subject: “Báo giá nhà cung cấp – Tóm tắt”. <br>• Body: HTML hoặc plain text (đưa dữ liệu từ `Format Summary`). | Thêm attachment nếu cần. |

### 3. Kích hoạt ⚡️

1. **Test run**: Chọn một file mẫu, gửi qua webhook (ví dụ: `curl -F "file=@sample.pdf" https://your-n8n-domain/webhook/vendor-quote-upload`).
2. Kiểm tra logs: Đảm bảo mọi node chạy thành công, dữ liệu xuất vào Google Sheets và email được gửi.
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` để gửi thông báo khi báo giá được lưu.
- **Lưu log**: Dùng node `HTTP Request` để gửi log tới một endpoint hoặc lưu vào Cloud Storage.
- **Báo cáo định kỳ**: Thêm node `Cron` để gửi báo cáo hàng ngày/tuần tới bộ phận mua hàng.
- **Tùy chỉnh AI Prompt**: Thay đổi prompt trong node `AI Summarization` để nhấn mạnh các tiêu chí quan trọng (giá, thời gian, chất lượng).

## 📌 Kết luận

Workflow này giúp các sếp **tiết kiệm thời gian**, **giảm sai sót** và **tăng tính minh bạch** trong quy trình mua hàng. Hãy thử ngay, import, cấu hình và bật workflow – bạn sẽ thấy công việc so sánh báo giá trở nên nhanh chóng, chính xác và chuyên nghiệp hơn bao giờ hết. 🚀