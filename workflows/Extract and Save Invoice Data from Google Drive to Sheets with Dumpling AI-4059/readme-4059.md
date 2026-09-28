---
title: "🚀 Tự động trích xuất hóa đơn từ Google Drive vào Google Sheets với Dumpling AI qua n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động theo dõi thư mục Google Drive, trích xuất dữ liệu hóa đơn thông minh bằng Dumpling AI và lưu thẳng vào Google Sheets."
slug: "trich-xuat-hoa-don-google-drive-google-sheets-dumpling-ai"
tags: [n8n, automation, no-code, google-drive, google-sheets, ai, invoice-processing]
keywords: [n8n workflow, tự động hóa hóa đơn, dumpling ai, trích xuất hóa đơn google sheets, google drive trigger]
---

# 🚀 Tự động trích xuất hóa đơn từ Google Drive vào Google Sheets với Dumpling AI

Các sếp có đang đau đầu mỗi khi cuối tháng phải ngồi nhập thủ công hàng trăm hóa đơn, chứng từ PDF vào bảng tính Excel hay Google Sheets? Việc này không chỉ tốn hàng giờ đồng hồ, dễ gây nhầm lẫn số liệu mà còn làm gián đoạn các công việc ưu tiên khác.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% này sẽ thay các sếp làm sạch toàn bộ quy trình: ngay khi có một hóa đơn mới được thả vào thư mục Google Drive, hệ thống sẽ tự động gọi AI (Dumpling AI) để đọc hiểu, trích xuất toàn bộ thông tin chi tiết (tên hàng hóa, số lượng, đơn giá, tổng tiền...) và lưu gọn gàng vào Google Sheets mà không cần một chút code thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh gõ phím mỏi tay nhập liệu hóa đơn từng dòng một.
- **Độ chính xác cực cao:** Tận dụng sức mạnh của Dumpling AI để đọc hiểu các định dạng hóa đơn phức tạp.
- **Tự động hóa hoàn toàn:** Chạy ngầm 24/7, cứ có file mới vào Drive là hệ thống tự xử lý tức thì.
- **Quản lý tài chính minh bạch:** Dữ liệu phân tách rõ ràng từng mục (line items) giúp việc tổng hợp báo cáo tài chính trở nên dễ dàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Drive Account:** Tài khoản kết nối để theo dõi thư mục hóa đơn.
- **Google Sheets Account:** Bảng tính chuẩn bị sẵn để lưu trữ dữ liệu đầu ra.
- **Dumpling AI API Key:** Tài khoản và khóa API để gọi dịch vụ trích xuất dữ liệu thông minh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ trang quản trị workflow n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Google Drive Trigger – Watch Folder for New Files:** 
  - Chọn Credentials tài khoản Google Drive của các sếp.
  - Chọn đúng thư mục (Folder ID) trên Drive nơi các sếp sẽ upload các file hóa đơn mới vào đó.
- **Download Invoice File:** 
  - Đảm bảo node này lấy đúng File ID từ trigger phía trên để tải xuống nội dung file.
- **Convert invoice File to Base64 (`extractFromFile`):** 
  - Giữ nguyên cấu hình chuyển đổi file nhị phân sang định dạng Base64 để chuẩn bị gửi sang AI.
- **Send file to Dumpling AI for Data Extraction (`httpRequest`):** 
  - Cấu hình Credentials loại Header Auth với API Key của Dumpling AI.
  - Điền đúng Endpoint URL và truyền dữ liệu Base64 kèm theo câu lệnh (prompt) hướng dẫn AI trích xuất đúng cấu trúc mong muốn.
- **Parse Dumpling AI JSON Response (`code`):** 
  - Node này dùng mã Javascript nhỏ để làm sạch và chuyển đổi chuỗi JSON trả về từ AI thành dữ liệu cấu trúc rõ ràng.
- **Split line Items from Invoice (`splitOut`):** 
  - Tách mảng dữ liệu các sản phẩm/dịch vụ trong hóa đơn thành từng dòng riêng biệt (nếu hóa đơn mua nhiều món).
- **Save Data to Google Sheet (`googleSheets`):** 
  - Chọn Credentials Google Sheets.
  - Trỏ đến Spreadsheet ID và Sheet Name cụ thể, sau đó map các trường dữ liệu từ AI vào đúng các cột tương ứng trên bảng tính.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử upload một file hóa đơn mẫu lên thư mục Google Drive để kiểm tra kết quả trả về.
- Nếu mọi thứ xanh mướt (success), các sếp hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối workflow để gửi tin nhắn thông báo tức thì: *"Vừa nhận và xử lý xong hóa đơn từ công ty ABC, tổng tiền: X VNĐ"*.
- **Xử lý file lỗi:** Thêm nhánh Error Handling để nếu AI đọc nhầm định dạng file lỗi, hệ thống sẽ chuyển file đó sang thư mục "Error_Invoices" trên Drive để kiểm tra lại.
- **Lưu trữ backup:** Kết hợp lưu trữ file hóa đơn gốc vào một thư mục "Archived" sau khi đã xử lý xong để gọn gàng không gian làm việc.

### 📌 Kết luận
Với workflow n8n kết hợp Dumpling AI này, việc quản lý và nhập liệu hóa đơn chưa bao giờ trở nên nhanh chóng và rảnh tay đến thế. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành cho đội ngũ kế toán và kinh doanh của các sếp nhé!