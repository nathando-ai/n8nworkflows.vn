---
title: "🚀 Tự động trích xuất và cấu trúc tài liệu tiếng Thái vào Google Sheets với Typhoon OCR và Llama 3.1"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc file PDF tiếng Thái, dùng Typhoon OCR và Llama 3.1 trích xuất dữ liệu thông minh và lưu trực tiếp vào Google Sheets."
slug: "trich-xuat-tai-lieu-tieng-thai-typhoon-ocr-google-sheets"
tags: [n8n, automation, ai, ocr, google-sheets, llama3, typhoon-ocr]
keywords: [n8n workflow, ocr tiếng thái, typhoon ocr, llama 3.1 openrouter, n8n google sheets, tự động hóa tài liệu]
---

# 🚀 Tự động trích xuất và cấu trúc tài liệu tiếng Thái vào Google Sheets với Typhoon OCR và Llama 3.1

Việc xử lý và số hóa các tài liệu tiếng Thái (như hóa đơn, hợp đồng, báo cáo) thủ công thường chiếm rất nhiều thời gian, dễ xảy ra sai sót do rào cản ngôn ngữ và tính chất phức tạp của ký tự tiếng Thái. Các công cụ OCR thông thường đôi khi gặp khó khăn trong việc bóc tách chính xác ngữ cảnh.

Giải pháp? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: từ việc đọc file PDF tiếng Thái trên server, trích xuất văn bản thô bằng **Typhoon OCR**, chuyển đổi thành dữ liệu JSON có cấu trúc bằng **Llama 3.1 (thông qua OpenRouter)**, và cuối cùng tự động lưu trữ gọn gàng vào **Google Sheets**. Giải pháp 100% không cần code thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Vì workflow này sử dụng tính năng thực thi lệnh hệ thống (`executeCommand`) để chạy Typhoon OCR, các sếp **bắt buộc phải cài đặt n8n trên VPS riêng (Self-hosted)** để workflow chạy ổn định 24/7.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Thay vì gõ tay từng trường dữ liệu tiếng Thái, hệ thống tự động bóc tách từ PDF sang Google Sheets trong vài giây.
- **Độ chính xác cao với AI**: Kết hợp giữa Typhoon OCR chuyên dụng cho tiếng Thái và mô hình ngôn ngữ lớn Llama 3.1 giúp hiểu sâu ngữ cảnh tài liệu.
- **Dữ liệu có cấu trúc chuẩn chỉnh**: Chuyển văn bản thô thành dữ liệu dạng bảng (JSON/Google Sheets) cực kỳ sạch sẽ và sẵn sàng để phân tích.
- **Tối ưu vận hành**: Tiết kiệm hàng chục giờ nhập liệu thủ công mỗi tuần cho đội ngũ vận hành và kế toán.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n Self-hosted**: Có quyền truy cập terminal/server để cấu hình công cụ OCR (Typhoon OCR).
- **Tài khoản OpenRouter**: Lấy API Key để sử dụng mô hình `scb10x/llama3.1-typhoon2-70b-instruct`.
- **Google Sheets API / OAuth2**: Tài khoản Google đã được cấu hình credentials để n8n có thể ghi dữ liệu vào bảng tính.
- **Thư mục chứa file**: Một thư mục `doc` trên server n8n để chứa các file PDF tiếng Thái đầu vào.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng Copy/Paste JSON trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Load PDFs from doc Folder (`readWriteFile`)**: Cấu hình đường dẫn trỏ chính xác đến thư mục `doc` trên server của các sếp để hệ thống quét các file PDF tiếng Thái cần xử lý.
- **Extract Text with Typhoon OCR (`executeCommand`)**: Node này chạy lệnh hệ thống để thực thi Typhoon OCR trên file PDF. Đảm bảo server n8n đã cài đặt sẵn môi trường và thư viện cần thiết cho Typhoon OCR.
- **OpenRouter Chat Model (`lmChatOpenRouter`)**: 
  - Chọn credentials `openRouterApi`.
  - Tại ô Model, đảm bảo chọn đúng mã mô hình: `scb10x/llama3.1-typhoon2-70b-instruct`.
- **Structure Text to JSON with LLM (`chainLlm`)**: Viết Prompt hướng dẫn AI trích xuất các trường thông tin cụ thể từ văn bản OCR tiếng Thái (ví dụ: Tên công ty, Mã số thuế, Tổng tiền, Ngày tháng...) thành định dạng JSON.
- **Parse JSON to Sheet Format (`code`)**: Viết đoạn code JavaScript ngắn để làm sạch và định dạng lại mảng JSON cho khớp với các cột trên Google Sheets.
- **Save to Google Sheet (`googleSheets`)**: 
  - Chọn credentials `googleSheetsOAuth2Api`.
  - Chọn Operation: `Append`.
  - Điền Spreadsheet ID và chọn đúng Sheet Name/Range tương ứng.

#### 3. Kích hoạt ⚡️
- Đặt file PDF mẫu vào thư mục `doc`.
- Nhấn **Test workflow** để kiểm tra dữ liệu chảy qua từng node có chính xác không.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack Bot**: Thêm node thông báo qua Telegram hoặc Slack mỗi khi xử lý xong một file PDF tiếng Thái để kịp thời nắm bắt tình hình.
- **Tự động hóa qua Webhook**: Thay vì dùng `Manual Trigger` và quét thư mục định kỳ, có thể kết hợp Webhook để nhận file PDF từ Google Drive hoặc Email khách hàng gửi đến.
- **Lưu trữ file backup**: Thêm bước di chuyển file PDF sang thư mục `processed` sau khi đã xử lý xong để tránh xử lý trùng lặp.

### 📌 Kết luận
Ứng dụng AI và OCR chuyên biệt vào xử lý tài liệu tiếng Thái chưa bao giờ dễ dàng đến thế với n8n. Hãy thiết lập ngay workflow này để giải phóng sức lao động và tối ưu hóa quy trình xử lý tài liệu đa ngôn ngữ cho doanh nghiệp của các sếp!