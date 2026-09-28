---
title: "🚀 Tự động trích xuất hóa đơn từ Google Drive vào Google Sheets với PDF.co AI Parser"
description: "Hướng dẫn xây dựng workflow n8n tự động quét hóa đơn PDF từ Google Drive, sử dụng AI của PDF.co để bóc tách dữ liệu và lưu trữ gọn gàng vào Google Sheets."
slug: "trich-xuat-hoa-don-google-drive-google-sheets-pdfco-ai"
tags: [n8n, automation, no-code, google-drive, google-sheets, ai-parser, pdfco]
keywords: [n8n workflow, tự động hóa hóa đơn, pdf.co ai parser, google drive sang google sheets, trích xuất dữ liệu pdf n8n]
---

# 🚀 Tự động trích xuất hóa đơn từ Google Drive vào Google Sheets với PDF.co AI Parser

Các sếp có đang cảm thấy mệt mỏi mỗi cuối tháng khi phải mở từng file PDF hóa đơn, thủ công copy tên nhà cung cấp, ngày tháng và tổng tiền rồi nhập vào Excel hay Google Sheets? Việc này không chỉ tốn hàng giờ đồng hồ mà còn rất dễ xảy ra sai sót nhầm lẫn số liệu.

Đừng lo, bài toán này sẽ được giải quyết triệt để 100% tự động mà không cần viết một dòng code nào với workflow n8n do chuyên gia **Robert Breen** thiết kế. Quy trình này sẽ thay các sếp "đọc hiểu" hóa đơn PDF từ Google Drive nhờ AI và tự động đồng bộ mọi thông tin quan trọng vào Google Sheets một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nhập liệu thủ công từng hóa đơn, toàn bộ quy trình diễn ra trong tích tắc.
- **Độ chính xác cao:** Ứng dụng AI mạnh mẽ từ PDF.co giúp bóc tách đúng các trường dữ liệu quan trọng như nhà cung cấp, ngày hóa đơn, hạn thanh toán và tổng tiền.
- **Chống trùng lặp thông minh:** Dữ liệu được cấu hình tính năng `Append or Update` dựa trên URL, đảm bảo không bị nhân đôi dòng khi chạy lại workflow.
- **Hoạt động liên tục 24/7:** Quản lý tài chính, công nợ tự động hóa hoàn toàn không gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt tay "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản Google Drive & Google Sheets** chứa thư mục hóa đơn mẫu.
3. **Tài khoản PDF.co** để lấy API Key sử dụng tính năng AI Invoice Parser.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 7 nodes chính được liên kết sẵn sàng: *When clicking ‘Execute workflow’, Get Parent Folder ID, Get Invoice ID's, Convert to URL, AI Invoice Parser, Set Fields,* và *Store Data in Google Sheets*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống kết nối và chạy trơn tru, các sếp cần cấu hình chính xác các thông số tại các node sau:

- **Node `Get Parent Folder ID` & `Get Invoice ID's` (Google Drive):**
  - Tạo Credentials loại **Google Drive (OAuth2)** và đăng nhập tài khoản chứa hóa đơn.
  - Tại node `Get Parent Folder ID`, cấu hình tìm kiếm tên thư mục chứa hóa đơn của các sếp (ví dụ: `n8n Invoices`).
  - Tại node `Get Invoice ID’s`, đảm bảo phần `Filter → folderId` đã được liên kết lấy ID từ node phía trước.

- **Node `AI Invoice Parser` (PDF.co API):**
  - Đăng ký tài khoản PDF.co, lấy **API Key** và tạo Credentials loại **PDF.co API** trong n8n.
  - Giữ nguyên cấu hình tham số `URL` ánh xạ với link file từ node `Convert to URL`.

- **Node `Store Data in Google Sheets` (Google Sheets):**
  - Tạo Credentials loại **Google Sheets (OAuth2)** và cấp quyền truy cập.
  - Chọn file Spreadsheet và Tab sheet tương ứng (mẫu gốc dùng Spreadsheet: `Invoice Template` và Tab: `Due`).
  - Đảm bảo các cột dữ liệu trong sheet khớp với output: `Url`, `Vendor`, `Invoice Date`, `Total`, `Due Date`.
  - Cấu hình chế độ **Append or Update** theo cột `Url` để tránh tạo bản ghi trùng lặp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm với dữ liệu mẫu và kiểm tra kết quả trong Google Sheets.
- Sau khi test thành công, bật nút **Active** để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình kế toán và vận hành, các sếp có thể mở rộng workflow này thêm các bước:
- **Tích hợp thông báo:** Gửi tin nhắn tức thì lên Slack hoặc Telegram mỗi khi có hóa đơn mới được bóc tách và lưu thành công.
- **Gửi email tự động:** Gửi thông báo nhắc nhở thanh toán tự động dựa trên trường `Due Date` (Ngày đến hạn).
- **Phân loại file:** Tự động di chuyển file PDF hóa đơn sang thư mục "Processed" trên Google Drive sau khi đã xử lý xong để tránh quét trùng lặp.

### 📌 Kết luận
Việc tự động hóa trích xuất hóa đơn không chỉ giúp giải phóng sức lao động nhân sự mà còn giúp doanh nghiệp kiểm soát tài chính, công nợ cực kỳ minh bạch và nhanh chóng. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa hiệu suất làm việc!