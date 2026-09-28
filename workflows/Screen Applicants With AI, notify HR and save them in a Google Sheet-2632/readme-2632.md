---
title: "🚀 Tự động Xử Lý Hồ Sơ Tuyển Dụng Với AI – Gửi Thông Báo HR & Lưu Trữ Google Sheet"
description: "Giải pháp tự động nhận hồ sơ, phân tích CV bằng AI, gửi email thông báo cho HR và lưu danh sách ứng viên vào Google Sheet – hoàn toàn không cần code."
slug: "tuyendung-giua-ai-gmail-google-sheets"
tags: [n8n, automation, no-code, HR, AI]
keywords: [n8n workflow, tự động hóa, AI, screen applicants, google sheets, gmail]
---

# 🚀 Tự động Xử Lý Hồ Sơ Tuyển Dụng Với AI – Gửi Thông Báo HR & Lưu Trữ Google Sheet

Bạn đang phải mất hàng giờ để lọc, đánh giá và lưu trữ hồ sơ ứng viên? Mỗi lần nhận được CV mới, bạn phải gửi email xác nhận, thông báo cho bộ phận HR, rồi nhập dữ liệu vào bảng tính – công việc lặp đi lặp lại, dễ sai sót và tốn thời gian.  
Workflow **Screen Applicants With AI, notify HR and save them in a Google Sheet** giúp bạn:

- Nhận hồ sơ ngay khi ứng viên gửi form.
- Phân tích CV bằng AI (Google Gemini) và đánh giá điểm số.
- Gửi email xác nhận tới ứng viên và thông báo tới HR.
- Lưu danh sách ứng viên vào Google Sheet một cách tự động.

Tất cả chỉ với **1 workflow** – không cần viết code, chỉ cần cấu hình một vài credential.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ lên chỉ vài phút.
- **Độ chính xác cao**: AI phân tích CV giảm sai sót so với đánh giá thủ công.
- **Tự động liên tục**: Không cần can thiệp thủ công, workflow chạy 24/7.
- **Dễ dàng mở rộng**: Thêm Slack, Telegram, báo cáo định kỳ chỉ vài dòng cấu hình.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ / Credential | Mô tả | Cách lấy |
|-----------------------|-------|----------|
| **Google Gemini (Palm API)** | API key cho mô hình Gemini | Tạo project trên Google Cloud, bật Gemini API, lấy API key |
| **Gmail OAuth2** | Đăng nhập Gmail để gửi email | Tạo OAuth2 client trên Google Cloud, cấp quyền Gmail API |
| **Google Sheets OAuth2** | Truy cập Google Sheets | Tạo OAuth2 client, cấp quyền Sheets API |
| **Form Trigger** | Form để nhận hồ sơ | Sử dụng n8n form hoặc Google Form (đảm bảo file CV được upload) |
| **Google Cloud APIs** | Sheets, Gmail, Gemini | Bật trong Google Cloud Console |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/2632) hoặc copy toàn bộ JSON.  
2. Mở n8n Editor → **Import** → **Import from file** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên | Credential | Tham số cần cấu hình | Ghi chú |
|------|-----|------------|----------------------|---------|
| 1 | **Application Form** | - | - | Đảm bảo form có trường `name`, `email`, `cv` (file PDF). |
| 2 | **Convert Binary to Json** | - | `operation: pdf` | Chuyển CV PDF sang JSON để AI đọc. |
| 3 | **Using AI Analysis & Rating** | - | Prompt: “Analyze the CV and give a score 1-10.” | Có thể tùy chỉnh prompt trong node. |
| 4 | **Google Gemini Chat Model** | `googlePalmApi` | `model: gemini-pro` | Đặt API key trong credential. |
| 5 | **Confirmation of CV Submission** | `gmailOAuth2` | `to: {{ $json.email }}`, `subject: Confirmation`, `body: ...` | Gửi email xác nhận tới ứng viên. |
| 6 | **Inform HR New CV Received** | `gmailOAuth2` | `to: hr@example.com`, `subject: New CV`, `body: ...` | Thông báo HR. |
| 7 | **Candidate Lists** | `googleSheetsOAuth2Api` | `operation: append`, `sheetId`, `range: Sheet1!A1` | Thêm dữ liệu vào Google Sheet. |

> **Lưu ý**:  
> - Mỗi node cần được **đặt Credential** đúng (đăng nhập Google, Gmail, Gemini).  
> - Kiểm tra **định dạng dữ liệu** (JSON) trước khi gửi tới AI.  
> - Nếu CV không phải PDF, thay đổi `operation` trong node `Convert Binary to Json`.  
> - Đảm bảo **định dạng email** trong Gmail node (đặt `to`, `subject`, `body` đúng).  

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** với dữ liệu mẫu (đăng form). Kiểm tra log, xác nhận email, dữ liệu trong Google Sheet.  
2. Khi mọi thứ ổn, bật **Active** (đánh dấu workflow là “Active”).  
3. Workflow sẽ tự động chạy mỗi khi có submission mới.

## ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack notification**: Thêm node Slack → gửi tin nhắn khi CV được nhận.  
- **Lưu log**: Sử dụng node “Write Binary File” để lưu PDF đã phân tích vào Google Drive.  
- **Báo cáo định kỳ**: Thêm node “Cron” → “Google Sheets” → “Email” để gửi báo cáo hàng ngày.  
- **Tùy chỉnh prompt**: Thêm biến `{{ $json.name }}` vào prompt để AI cá nhân hóa đánh giá.  
- **Sử dụng Google Drive**: Lưu CV đã upload vào Drive và lưu link trong Sheet.

## 📌 Kết luận
Workflow này giúp bạn **đơn giản hóa toàn bộ quy trình tuyển dụng**: từ nhận hồ sơ, phân tích AI, gửi email, tới lưu trữ dữ liệu – tất cả tự động, không cần code.  
Hãy thử ngay, áp dụng vào quy trình tuyển dụng của công ty bạn và cảm nhận sự khác biệt!