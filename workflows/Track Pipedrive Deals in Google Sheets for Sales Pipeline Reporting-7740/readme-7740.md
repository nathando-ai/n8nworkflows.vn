---
title: "🚀 Theo dõi giao dịch Pipedrive trong Google Sheets để báo cáo đường ống bán hàng"
description: "Tự động hóa quy trình theo dõi giao dịch Pipedrive trong Google Sheets để báo cáo và phân tích đường ống bán hàng một cách hiệu quả."
slug: "theo-doi-giao-dich-pipedrive-trong-google-sheets"
tags: [n8n, automation, no-code, crm, google-sheets]
keywords: [n8n workflow, tự động hóa, crm, google sheets, báo cáo bán hàng]
---

# 🚀 Theo dõi giao dịch Pipedrive trong Google Sheets để báo cáo đường ống bán hàng

[Các sếp đang gặp khó khăn khi phải theo dõi giao dịch Pipedrive thủ công trong Google Sheets. Với workflow này, các sếp có thể tự động hóa quy trình này một cách hoàn toàn không cần code, tiết kiệm thời gian và giảm thiểu lỗi.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa quy trình theo dõi giao dịch Pipedrive trong Google Sheets.
- Tiết kiệm thời gian và giảm thiểu lỗi khi cập nhật dữ liệu.
- Phân tích và báo cáo đường ống bán hàng một cách hiệu quả.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Pipedrive với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets.
- API token từ Pipedrive.
- Thiết lập Google Sheets OAuth2 trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/7740).
2. Click vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get many deals1"**:
   - Chọn credentials "pipedriveApi".
   - (Tùy chọn) Thiết lập các bộ lọc như owner, label, created time.

2. **Node "Store in google"**:
   - Chọn credentials "googleSheetsOAuth2Api".
   - Chọn Spreadsheet và Worksheet tương ứng.
   - Đảm bảo định dạng cột trong Google Sheets phù hợp với dữ liệu từ Pipedrive.

3. **Node "Categorize stages"**:
   - Kiểm tra và điều chỉnh logic phân loại các giai đoạn giao dịch nếu cần.

4. **Node "Today's Date"**:
   - Kiểm tra định dạng ngày tháng để đảm bảo phù hợp với yêu cầu báo cáo.

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, bật "Active workflow" để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có giao dịch mới.
- Lưu log các thay đổi để theo dõi lịch sử.
- Gửi báo cáo định kỳ qua email với dữ liệu từ Google Sheets.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình theo dõi giao dịch Pipedrive trong Google Sheets một cách hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!