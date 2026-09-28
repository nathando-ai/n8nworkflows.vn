---
title: "🚀 Tự động tóm tắt tin tức từ RSS bằng AI Gemini và lưu vào Google Sheets"
description: "Workflow n8n tự động hóa việc lấy tin tức từ RSS, tóm tắt bằng AI Gemini và lưu vào Google Sheets, giúp tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-tom-tat-tin-tuc-rss-voi-gemini-va-google-sheets"
tags: [n8n, automation, no-code, AI, Google Sheets]
keywords: [n8n workflow, tự động hóa, tóm tắt tin tức, AI Gemini, Google Sheets]
---

# 🚀 Tự động tóm tắt tin tức từ RSS bằng AI Gemini và lưu vào Google Sheets

[Các sếp] có bao giờ phải mất hàng giờ để đọc và tóm tắt tin tức từ nhiều nguồn RSS khác nhau? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài phút, giúp tiết kiệm thời gian quý giá và tập trung vào những việc quan trọng hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lấy và tóm tắt tin tức từ nhiều nguồn RSS trong vài phút.
- **Chính xác và hiệu quả**: Sử dụng AI Gemini để tóm tắt nội dung một cách chính xác và súc tích.
- **Quản lý thông tin hiệu quả**: Lưu trữ và quản lý tin tức tóm tắt trong Google Sheets một cách dễ dàng.
- **Hoạt động liên tục**: Workflow có thể được lập lịch để chạy tự động theo thời gian.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API Key từ Google Gemini.
- Danh sách các nguồn RSS cần theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/8024](https://n8n.io/workflows/8024) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc, copy toàn bộ nội dung JSON từ trang web và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Get RSS Feed List"**: Cấu hình thông tin Google Sheets chứa danh sách các nguồn RSS.
  - Chọn credentials "googleSheetsOAuth2Api".
  - Điền thông tin Sheet ID và tên Sheet chứa danh sách nguồn RSS.

- **Node "Read RSS"**: Không cần cấu hình thêm, node này sẽ đọc dữ liệu từ các nguồn RSS đã được cấu hình.

- **Node "Loop Over Rss Elements"**: Không cần cấu hình thêm, node này sẽ lặp qua từng phần tử tin tức từ các nguồn RSS.

- **Node "Get Row for URL is in Sheets"**: Cấu hình thông tin Google Sheets để kiểm tra xem tin tức đã tồn tại hay chưa.
  - Chọn credentials "googleSheetsOAuth2Api".
  - Điền thông tin Sheet ID và tên Sheet chứa dữ liệu tin tức.

- **Node "Convert HTML to Markdown"**: Không cần cấu hình thêm, node này sẽ chuyển đổi nội dung HTML thành Markdown.

- **Node "Append Aummary to Google Sheets"**: Cấu hình thông tin Google Sheets để lưu trữ tin tức tóm tắt.
  - Chọn credentials "googleSheetsOAuth2Api".
  - Điền thông tin Sheet ID và tên Sheet chứa dữ liệu tin tức tóm tắt.

- **Node "Combine Rss with source name"**: Không cần cấu hình thêm, node này sẽ kết hợp thông tin tin tức với tên nguồn.

- **Node "Check If Article Exists"**: Không cần cấu hình thêm, node này sẽ kiểm tra xem tin tức đã tồn tại trong Google Sheets hay chưa.

- **Node "Summarize Content"**: Cấu hình thông tin cho AI Gemini để tóm tắt nội dung tin tức.
  - Chọn credentials "googlePalmApi".
  - Điền thông tin Prompt cho AI Gemini (ví dụ: "Summarize the following article in 3 sentences:").

- **Node "Format Output"**: Không cần cấu hình thêm, node này sẽ định dạng đầu ra của tin tức tóm tắt.

- **Node "Schedule Trigger"**: Cấu hình thời gian chạy tự động cho workflow.
  - Chọn "Schedule" và đặt thời gian chạy (ví dụ: hàng ngày lúc 8:00 AM).

- **Node "Filter Last X Days"**: Cấu hình số ngày để lọc tin tức mới nhất.
  - Điền số ngày cần lọc (ví dụ: 7 ngày).

- **Node "Settings"**: Cấu hình các thiết lập chung cho workflow.
  - Điền thông tin các thiết lập cần thiết (ví dụ: số lượng tin tức tối đa để xử lý).

- **Node "End of worfklow"**: Không cần cấu hình thêm, node này đánh dấu kết thúc của workflow.

- **Node "Get Webpage HTML Content"**: Không cần cấu hình thêm, node này sẽ lấy nội dung HTML của trang web.

- **Node "Extract Body Content in HTML"**: Không cần cấu hình thêm, node này sẽ trích xuất nội dung chính từ HTML.

- **Node "Google Gemini Chat Model1"**: Cấu hình thông tin cho AI Gemini để tóm tắt nội dung tin tức.
  - Chọn credentials "googlePalmApi".
  - Điền thông tin Prompt cho AI Gemini (ví dụ: "Summarize the following article in 3 sentences:").

- **Node "Append Aummary to Google Sheets1"**: Cấu hình thông tin Google Sheets để lưu trữ tin tức tóm tắt.
  - Chọn credentials "googleSheetsOAuth2Api".
  - Điền thông tin Sheet ID và tên Sheet chứa dữ liệu tin tức tóm tắt.

- **Node "Clear sheet"**: Cấu hình thông tin Google Sheets để xóa dữ liệu cũ.
  - Chọn credentials "googleSheetsOAuth2Api".
  - Điền thông tin Sheet ID và tên Sheet cần xóa dữ liệu.

- **Node "Loop Over RSS Feed"**: Không cần cấu hình thêm, node này sẽ lặp qua từng nguồn RSS.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn vào nút "Execute workflow" để kiểm tra workflow chạy đúng hay không.
2. Nếu workflow chạy thành công, nhấn vào nút "Activate" để kích hoạt workflow và chạy tự động theo lịch trình đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể cấu hình workflow để gửi tin tức tóm tắt qua Slack hoặc Telegram để nhận thông báo ngay lập tức.
- **Lưu log hoạt động**: Các sếp có thể cấu hình workflow để lưu log hoạt động vào Google Sheets để theo dõi quá trình xử lý tin tức.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo định kỳ qua email hoặc Slack để cập nhật tình hình tin tức mới nhất.
- **Tích hợp với các công cụ khác**: Các sếp có thể tích hợp workflow với các công cụ khác như Notion, Trello để quản lý thông tin một cách hiệu quả hơn.

### 📌 Kết luận
Workflow "Summarize RSS News with Gemini AI and Store in Google Sheets" giúp các sếp tự động hóa việc lấy tin tức từ RSS, tóm tắt bằng AI Gemini và lưu vào Google Sheets, tiết kiệm thời gian và nâng cao hiệu quả làm việc. Các sếp chỉ cần cấu hình một lần và workflow sẽ chạy tự động theo lịch trình đã đặt, giúp các sếp tập trung vào những việc quan trọng hơn.