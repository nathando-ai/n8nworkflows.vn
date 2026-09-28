---
title: "🚀 Tự động hoá đăng ký newsletter: Kiểm tra email, gửi email chào mừng & ghi log Google Sheets"
description: "Giải pháp hoàn chỉnh giúp doanh nghiệp tự động nhận đăng ký newsletter, xác thực email, gửi email chào mừng và lưu trữ toàn bộ dữ liệu vào Google Sheets – không cần viết code."
slug: "tuyendung-newsletter-kiem-tra-email-gmail-google-sheets"
tags: [n8n, automation, no-code, email, google-sheets, verifi-email]
keywords: [n8n workflow, tự động hóa, newsletter signup, email verification, google sheets, gmail]
---

# 🚀 Tự động hoá đăng ký newsletter: Kiểm tra email, gửi email chào mừng & ghi log Google Sheets

Bạn đang phải xử lý hàng trăm, hàng nghìn đăng ký newsletter mỗi ngày? Việc nhập dữ liệu thủ công, kiểm tra email, gửi email chào mừng và lưu trữ mọi thông tin lại làm bạn mệt mỏi và dễ mắc lỗi. Workflow n8n dưới đây giúp bạn:

- Nhận dữ liệu đăng ký qua webhook
- Kiểm tra tính đầy đủ của dữ liệu
- Xác thực email (định dạng, domain, MX, disposable, score)
- Gửi email chào mừng nếu hợp lệ
- Ghi log các trường hợp không hợp lệ và toàn bộ dữ liệu vào Google Sheets
- Hoàn toàn không cần viết code

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng nghìn đăng ký trong vài giây.
- **Chính xác**: Kiểm tra email trước khi gửi, giảm spam và lỗi gửi.
- **Cá nhân hóa**: Email chào mừng được tạo động, chèn tên, link xác nhận, unsubscribe.
- **Hoạt động liên tục**: Ghi log vào Google Sheets, dễ dàng phân tích và báo cáo.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Google Sheets OAuth2**: Đăng ký và cấp quyền truy cập tới Google Sheets.
- **Gmail OAuth2**: Đăng ký và cấp quyền gửi email qua Gmail.
- **Verifi Email API**: Đăng ký tại <https://verifi.email> và lấy API key.
- **Google Sheets**: Tạo 3 sheet trong một file Google Sheets:
  - `Invalid_Submissions`
  - `Invalid_Emails`
  - `Master_Log`
- **Sheet ID**: Thay `YOUR_SHEET_ID` trong các node Google Sheets bằng ID file Google Sheets của bạn.
- **Webhook URL**: Khi workflow được publish, n8n sẽ cung cấp URL webhook (`https://<your-n8n-domain>/webhook/newsletter-signup`).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ <https://n8n.io/workflows/10138> hoặc copy toàn bộ JSON.
2. Mở n8n Editor → **Import** → **Import from JSON** → dán JSON → **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| Webhook | `Webhook - Newsletter Signup` | `path: newsletter-signup` <br> `httpMethod: POST` | Đảm bảo URL đúng khi gửi POST từ website |
| Google Sheets (Log Incomplete) | `Log Incomplete Submissions` | `sheetId: YOUR_SHEET_ID` <br> `sheetName: Invalid_Submissions` | |
| Verifi Email | `Verifi Email` | `apiKey: YOUR_VERIFI_API_KEY` | |
| Google Sheets (Log Invalid) | `Log Invalid Emails` | `sheetId: YOUR_SHEET_ID` <br> `sheetName: Invalid_Emails` | |
| Google Sheets (Master Log) | `Log to Master Sheet` | `sheetId: YOUR_SHEET_ID` <br> `sheetName: Master_Log` | |
| Gmail | `Send Welcome Email` | `from: Your Brand Team <your@email.com>` | Đảm bảo email gửi đi đúng tên và địa chỉ |
| Code nodes | `Generate Welcome Email HTML`, `Prepare Invalid Email Message`, `Format Master Log Entry` | Kiểm tra biến `{{$json["name"]}}`, `{{$json["email"]}}` và các trường dữ liệu khác | Đảm bảo các biến được truyền đúng từ node trước |

> **Tip**: Mỗi node `if` cần kiểm tra điều kiện đúng (`{{ $json["email"] !== "" && $json["name"] !== "" }}`) và chuyển sang nhánh tương ứng.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn **Execute Workflow** với dữ liệu mẫu (định dạng JSON dưới đây) để kiểm tra luồng.
2. **Bật Active**: Khi mọi thứ hoạt động đúng, chuyển workflow sang trạng thái **Active**.
3. **Kiểm tra logs**: Mở Google Sheets để xem dữ liệu đã ghi log.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram Notification**: Thêm node Slack/Telegram để nhận thông báo khi có đăng ký mới hoặc lỗi.
- **Scheduled Report**: Sử dụng node `Cron` + `Google Sheets` để gửi báo cáo hàng ngày về số lượng đăng ký, email hợp lệ, lỗi.
- **Retry & Error Handling**: Bật `Retry` cho node `Verifi Email` và `Gmail` để tự động thử lại khi API bị lỗi tạm thời.
- **Webhook Security**: Thêm header `X-API-Key` và kiểm tra trong node `Code` để bảo vệ webhook khỏi spam.

## 📌 Kết luận

Workflow này giúp các sếp chuyển từ quy trình thủ công sang tự động hoàn toàn, giảm thiểu sai sót, tăng tính chuyên nghiệp và cung cấp dữ liệu chi tiết cho phân tích. Hãy triển khai ngay, tùy chỉnh theo nhu cầu và tận hưởng lợi ích của tự động hoá 100% không cần code!

---