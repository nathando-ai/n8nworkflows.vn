---
title: "🏡 [Tự động hóa 100% không code] Theo dõi tuân thủ tài liệu của người thuê nhà với GPT-4o-mini, Google Drive, Sheets, email và Slack"
description: "Giải pháp tự động hóa hoàn chỉnh giúp các chủ nhà theo dõi và quản lý tài liệu của người thuê nhà một cách hiệu quả, tiết kiệm thời gian và giảm thiểu lỗi thủ công."
slug: "tu-dong-hoa-theo-doi-tuong-thu-tai-lieu-nguoi-thue-nha"
tags: [n8n, automation, no-code, google-drive, google-sheets, ai, email, slack]
keywords: [n8n workflow, tự động hóa tài liệu, quản lý tài liệu thuê nhà, AI kiểm tra tài liệu, báo cáo tuân thủ]
---

# 🏡 [Tự động hóa 100% không code] Theo dõi tuân thủ tài liệu của người thuê nhà với GPT-4o-mini, Google Drive, Sheets, email và Slack

[Các sếp chủ nhà đang gặp khó khăn khi quản lý hàng trăm tài liệu của người thuê nhà một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhận tài liệu đến kiểm tra và báo cáo tuân thủ, giảm thiểu đến 80% công việc thủ công và lỗi con người.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ 30 phút xuống còn 5 phút mỗi lần xử lý tài liệu.
- **Chính xác cao**: Sử dụng AI GPT-4o-mini để kiểm tra và phân loại tài liệu một cách chính xác.
- **Tự động hóa báo cáo**: Tạo báo cáo tuân thủ hàng tuần một cách tự động, không cần can thiệp thủ công.
- **Giảm thiểu lỗi**: Hệ thống cảnh báo và nhắc nhở tự động giúp giảm thiểu các trường hợp bỏ sót tài liệu quan trọng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive và Google Sheets để lưu trữ tài liệu và dữ liệu.
- API key từ OpenAI để sử dụng GPT-4o-mini.
- Tài khoản email (Gmail, Outlook,...) để gửi các thông báo nhắc nhở.
- Tài khoản Slack để nhận các thông báo quan trọng.
- Form hoặc hệ thống khác để người thuê nhà upload tài liệu (có thể là Google Form, Typeform, hoặc hệ thống tự xây dựng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/12688
3. Hoặc copy nội dung JSON từ link trên và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Document Upload Webhook**:
   - Cấu hình path: `/tenant-document-upload`
   - Chọn HTTP Method: `POST`
   - Cấu hình các trường dữ liệu cần thiết từ form upload tài liệu (ví dụ: tenantId, documentType, fileUrl...).

2. **Workflow Configuration**:
   - Cấu hình các tham số chung cho workflow như tên folder trên Google Drive, tên sheet trên Google Sheets, v.v.

3. **Upload to Google Drive**:
   - Chọn credentials `googleDriveOAuth2Api`.
   - Cấu hình folder ID nơi lưu trữ tài liệu.

4. **Check Document Completeness**:
   - Chọn credentials `openAiApi`.
   - Cấu hình prompt cho AI để kiểm tra tài liệu (ví dụ: "Kiểm tra xem tài liệu này có đầy đủ các mục yêu cầu không:...").

5. **Log Document Status**:
   - Chọn credentials `googleSheetsOAuth2Api`.
   - Cấu hình Spreadsheet ID và tên sheet để lưu trữ dữ liệu.

6. **Send Reminder Email**:
   - Cấu hình thông tin email gửi đi (tiêu đề, nội dung, người nhận...).

7. **Escalate to Slack**:
   - Cấu hình thông tin Slack channel và thông báo cần gửi.

8. **Weekly Schedule**:
   - Cấu hình lịch gửi báo cáo hàng tuần (ví dụ: mỗi thứ Hai lúc 8h sáng).

9. **Read Compliance Data**:
   - Chọn credentials `googleSheetsOAuth2Api`.
   - Cấu hình Spreadsheet ID và tên sheet để đọc dữ liệu.

10. **Send Compliance Report**:
    - Cấu hình thông tin email gửi báo cáo (tiêu đề, nội dung, người nhận...).

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu.
2. Kiểm tra các node quan trọng để đảm bảo dữ liệu được xử lý đúng.
3. Bật Active workflow để bắt đầu chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node Slack để nhận thông báo khi có tài liệu mới được upload.
- **Lưu log hoạt động**: Thêm node để lưu log các hoạt động quan trọng vào Google Sheets hoặc cơ sở dữ liệu.
- **Gửi báo cáo định kỳ**: Cấu hình gửi báo cáo hàng tháng hoặc theo yêu cầu.
- **Tích hợp với hệ thống CRM**: Kết nối với hệ thống CRM để quản lý thông tin người thuê nhà và lịch sử tài liệu.

### 📌 Kết luận
Workflow này giúp các sếp chủ nhà tự động hóa toàn bộ quy trình quản lý tài liệu của người thuê nhà, từ nhận tài liệu đến kiểm tra và báo cáo tuân thủ. Với việc sử dụng AI và các công cụ tự động hóa, các sếp có thể tiết kiệm thời gian, giảm thiểu lỗi và quản lý tài liệu một cách hiệu quả hơn. Hãy áp dụng ngay để nâng cao hiệu suất quản lý tài sản của bạn!