---
title: "🚀 Tự động xử lý tài liệu tài chính từ Google Drive với AI, Notion, Gmail, Slack và Google Sheets"
description: "Giải pháp tự động 100% xử lý, phân loại, routing và phê duyệt tài liệu tài chính, giảm thời gian thủ công và tăng độ chính xác."
slug: "tuyendung-xu-ly-tai-lieu-tai-chinh"
tags: [n8n, automation, no-code, AI, finance]
keywords: [n8n workflow, tự động hóa tài chính, AI summarization, document extraction, workflow automation]
---

# 🚀 Tự động xử lý tài liệu tài chính

Bạn đang phải mất hàng giờ mỗi ngày để quét, phân loại, trích xuất dữ liệu và phê duyệt các tài liệu tài chính?  
Workflow này sẽ **đánh bại** những nỗi đau đó bằng cách tự động:

- **Tải** tài liệu từ Google Drive (định kỳ hoặc thủ công qua webhook).  
- **Chia** PDF thành từng trang, **OCR** trích xuất văn bản.  
- **AI** phân loại tài liệu (hoá đơn, bảng lương, hợp đồng, PO…) và trích xuất dữ liệu chính (số tiền, nhà cung cấp, ngày, số hoá đơn) kèm điểm confidence.  
- **Routing** theo phòng ban, **đánh giá** giá trị cao để gửi lên CFO, **đánh dấu** cần review khi confidence thấp.  
- **Tự động** tạo task phê duyệt trong Notion, gửi email Gmail, cảnh báo Slack và ghi log vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ → vài phút.  
- **Độ chính xác**: AI + OCR giảm lỗi nhập liệu.  
- **Tự động hóa 24/7**: Không cần can thiệp thủ công.  
- **Audit trail**: Mọi hành động được ghi lại trong Google Sheets.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ | Credential | Mô tả |
|---------|------------|-------|
| **Google Drive** | `googleDriveOAuth2Api` | Truy cập folder chứa scan. |
| **Google Sheets** | `googleSheetsOAuth2Api` | Sheet ghi log. |
| **HTML to PDF Split** | `htmlcsstopdfApi` | API key cho dịch vụ split PDF. |
| **OpenAI** | `openaiApiKey` | Được dùng trong node `AI: Extract & Classify`. |
| **Notion** | `notionOAuth2` | Database ID cho task phê duyệt. |
| **Gmail** | `gmailOAuth2` | Email CFO. |
| **Slack** | `slackOAuth2` | Workspace & channel. |
| **Webhook** | - | Đường dẫn `manual-trigger-scan`. |
:::

> **Lưu ý**: Nếu chưa có tài khoản, hãy tạo tài khoản và cấp quyền cần thiết trước khi import workflow.

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn file JSON (được tải từ link gốc hoặc copy nội dung JSON).  
3. Nhấn **Import**.  
4. Kiểm tra lại các node và các tham số.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tham số cần cấu hình | Ghi chú |
|------|----------------------|---------|
| **Trigger: Daily Schedule1** | `cron` (ví dụ: `0 0 * * *`) | Lên lịch lấy scan hàng ngày. |
| **Trigger: Webhook Scan1** | `path: manual-trigger-scan`, `method: POST` | Để trigger thủ công. |
| **Fetch Bulk Scan from Drive1** | `folderId` | ID folder chứa scan. |
| **Split PDF into Pages1** | `operation: splitPdf`, `resource: pdfManipulation` | Đảm bảo API key hợp lệ. |
| **Extract from File** | `operation: pdf` | Trích xuất văn bản từ từng trang. |
| **AI: Extract & Classify** | `openaiApiKey`, `model`, `prompt` | Cập nhật prompt phù hợp với loại tài liệu. |
| **Route by Department1** | `switch` | Định nghĩa điều kiện routing (ví dụ: `department == 'Finance'`). |
| **Escalate High Value?1** | `if` | Kiểm tra `amount > 1000000`. |
| **Escalate to CFO (Gmail)1** | `to`, `subject`, `body` | Email CFO. |
| **Notion: Create Approval Task** | `databaseId`, `properties` | Tạo page trong database phê duyệt. |
| **Slack: Alert Team** | `channel`, `message` | Cảnh báo khi cần review. |
| **Log to Audit Sheet** | `spreadsheetId`, `range` | Ghi log. |
| **IF: Quality Check Required?** | `if` | Kiểm tra `confidence < 0.8`. |
| **Verify File Integrity1** | `code` | Kiểm tra checksum (có thể tùy chỉnh). |

> **Tip**: Mỗi node `code` (Verify File Integrity, AI: Extract & Classify) có thể được mở rộng bằng JavaScript tùy theo quy trình của doanh nghiệp.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo các node trả về dữ liệu đúng).  
2. Kiểm tra log trong Google Sheets và Notion.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  

### ✍️ Mẹo & gợi ý nâng cao
- **Slack + Telegram**: Thêm node `Telegram` để gửi cảnh báo tới nhóm chat.  
- **Lưu log chi tiết**: Sử dụng node `Code` để ghi log vào file hoặc dịch vụ lưu trữ (S3, GCS).  
- **Báo cáo định kỳ**: Thêm node `ScheduleTrigger` để gửi báo cáo tổng hợp hàng tuần qua Gmail hoặc Notion.  
- **Tự động cập nhật database Notion**: Khi task được phê duyệt, dùng node `Notion` để cập nhật trạng thái.  
- **Tăng độ an toàn**: Sử dụng `n8n` version 1.0+ với `n8n-pro` để bảo mật credentials và giới hạn quyền truy cập.

### 📌 Kết luận
Workflow này đã được thiết kế để **đơn giản, mạnh mẽ và linh hoạt**. Bạn chỉ cần cấu hình một vài credential và một số tham số, sau đó workflow sẽ tự động:

- Tải tài liệu, trích xuất dữ liệu, phân loại, routing, phê duyệt, cảnh báo và ghi log.  
- Giảm thiểu sai sót, tăng tốc độ xử lý và cung cấp audit trail đầy đủ.

Hãy **đặt workflow lên VPS của mình ngay hôm nay** và trải nghiệm tự động hóa tài chính 100% không cần code!