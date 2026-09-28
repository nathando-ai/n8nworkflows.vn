---
title: "🚀 Hướng dẫn Import file CSV vào MySQL tự động cực nhanh với n8n"
description: "Giải pháp tự động hóa giúp các sếp đọc file CSV từ máy chủ, xử lý và đổ dữ liệu vào database MySQL chỉ trong một nốt nhạc mà không cần viết code."
slug: "import-csv-vao-mysql-tu-dong-bang-n8n"
tags: [n8n, automation, no-code, mysql, csv-import, database]
keywords: [n8n workflow, import csv mysql, tu dong hoa du lieu, n8n mysql, doc file csv n8n]
---

# 🚀 Tự động Import file CSV vào MySQL cực kỳ nhanh chóng với n8n

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi phải nhập thủ công hàng ngàn dòng dữ liệu từ file CSV vào database MySQL? Việc copy-paste hoặc viết các script Python phức tạp vừa tốn thời gian, vừa dễ xảy ra sai sót dữ liệu. 

Đừng lo lắng nữa! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ gọn nhẹ nhưng mạnh mẽ, giúp tự động đọc file CSV, chuyển đổi định dạng và insert toàn bộ dữ liệu vào MySQL chỉ bằng một cú click chuột hoặc thiết lập chạy tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các file dữ liệu lớn không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Không cần code script hay thao tác thủ công qua phpMyAdmin/DBeaver.
- **Xử lý dữ liệu lớn chính xác:** Tự động map cấu trúc cột từ CSV sang các trường tương ứng trong bảng MySQL.
- **Linh hoạt kích hoạt:** Có thể chạy thủ công khi cần hoặc kết hợp với Schedule/Webhook để chạy tự động theo lịch trình.
- **Dễ dàng mở rộng:** Dễ dàng áp dụng cho các tệp dữ liệu khách hàng, sản phẩm, đơn hàng định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đã được cài đặt và hoạt động.
- File CSV cần import được lưu sẵn trên hệ thống (hoặc đường dẫn thư mục mà n8n có quyền truy cập).
- Thông tin kết nối cơ sở dữ liệu MySQL (Host, Port, Database, Username, Password).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ cấu trúc JSON của workflow **Import CSV into MySQL** (tác giả: Eduard) và paste trực tiếp vào không gian làm việc của n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 4 nodes chính, các sếp cần cấu hình chính xác các điểm sau:

- **Node `On clicking 'execute'` (manualTrigger):** 
  - Đây là điểm khởi đầu thủ công. Các sếp có thể giữ nguyên hoặc thay thế bằng node `Schedule Trigger` nếu muốn tự động hóa chạy định kỳ hàng ngày/hàng tuần.
- **Node `Read From File` (readBinaryFile):** 
  - Tại đây, các sếp cần cấu hình đường dẫn tuyệt đối đến file CSV trên server (ví dụ: `/data/uploads/customers.csv`). Đảm bảo container n8n có quyền đọc thư mục này (nếu chạy qua Docker, hãy nhớ mount thư mục volume).
- **Node `Convert To Spreadsheet` (spreadsheetFile):** 
  - Node này sẽ đóng vai trò đọc file nhị phân vừa lấy được và chuyển đổi thành dạng dữ liệu bảng (JSON items) mà n8n có thể hiểu và thao tác. Giữ nguyên các thiết lập mặc định nếu file CSV sử dụng định dạng chuẩn (phân cách bằng dấu phẩy `,`).
- **Node `Insert into MySQL` (mySql):** 
  - **Credentials:** Tạo hoặc chọn kết nối MySQL với thông tin chính xác (Host, Database, User, Password).
  - **Operation:** Chọn `Insert`.
  - **Table:** Điền tên bảng (Table Name) trong database MySQL nơi các sếp muốn đổ dữ liệu vào.
  - **Mapping:** Đảm bảo các cột dữ liệu từ file CSV khớp với tên các cột (Columns) trong bảng MySQL của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Execute Workflow"** để test thử lần đầu với file mẫu.
- Kiểm tra lại database MySQL xem dữ liệu đã được nạp thành công hay chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc **Active** ở góc trên bên phải để sẵn sàng vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch:** Thay thế node kích hoạt thủ công bằng `Schedule Trigger` để n8n tự động quét và import file CSV mới vào mỗi khung giờ cố định.
- **Nhận thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để n8n gửi tin nhắn báo cáo kết quả (ví dụ: *"Đã import thành công 1,500 dòng dữ liệu vào bảng MySQL!"*) ngay sau khi hoàn tất.
- **Xử lý file qua Email/Webhook:** Thay vì đọc file từ local server, các sếp có thể cấu hình để n8n tự động bắt file CSV đính kèm từ Email đến hoặc qua Webhook từ hệ thống khác.

### 📌 Kết luận
Việc tích hợp dữ liệu từ CSV vào MySQL chưa bao giờ đơn giản và nhanh chóng đến thế với n8n. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình xử lý dữ liệu của các sếp và loại bỏ hoàn toàn các thao tác thủ công nhàm chán!