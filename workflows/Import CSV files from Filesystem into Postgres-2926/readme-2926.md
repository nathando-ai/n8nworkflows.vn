---
title: "🚀 Tự động hóa Import file CSV từ Filesystem vào cơ sở dữ liệu PostgreSQL bằng n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n để tự động đọc file CSV từ thư mục hệ thống, chuyển đổi dữ liệu và đồng bộ thẳng vào PostgreSQL một cách mượt mà, không cần viết code."
slug: "import-csv-files-tu-filesystem-vao-postgres-bang-n8n"
tags: [n8n, automation, no-code, postgresql, csv, database, workflow]
keywords: [n8n workflow, import csv vào postgres, tự động hóa dữ liệu, read binary file, spreadsheet file n8n, postgresql automation]
---

# 🚀 Tự động hóa Import file CSV từ Filesystem vào PostgreSQL với n8n

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi phải nhận các file CSV dữ liệu lớn từ đối tác hoặc hệ thống cũ, rồi lại lọ mọ mở DBeaver hay pgAdmin để viết câu lệnh `COPY` hoặc `INSERT` thủ công vào PostgreSQL chưa? Việc này không chỉ tốn thời gian, dễ gây sai sót lệch định dạng cột mà còn cực kỳ nhàm chán nếu phải làm lặp đi lặp lại hàng tuần, hàng tháng.

Giải pháp ở đây là gì? Hãy để **n8n** gánh thay các sếp! Với workflow tự động hóa này, toàn bộ quy trình đọc file CSV từ thư mục hệ thống (Filesystem), chuyển đổi thành định dạng bảng và đẩy thẳng vào cơ sở dữ liệu PostgreSQL sẽ được xử lý gọn trong một nốt nhạc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các file dữ liệu lớn mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Loại bỏ hoàn toàn các thao tác thủ công khi đưa dữ liệu từ file vào database.
- **Tốc độ xử lý ấn tượng:** Đọc file dung lượng lớn từ ổ cứng server và nạp vào PostgreSQL siêu tốc.
- **Độ chính xác cao:** Tránh được các lỗi đánh máy, lỗi cú pháp SQL hoặc lệch kiểu dữ liệu thường gặp.
- **Linh hoạt mở rộng:** Dễ dàng kết hợp thêm các bước thông báo (gửi Telegram/Slack) sau khi import thành công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt n8n (ưu tiên Self-hosted để n8n có quyền truy cập vào Filesystem của máy chủ).
- **Cơ sở dữ liệu PostgreSQL:** Thông tin kết nối (Host, Port, Database, User, Password).
- **File CSV:** Chuẩn bị sẵn file CSV cần import nằm trong thư mục mà tiến trình n8n có thể đọc được.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ chính thức của n8n (Workflow ID: `2926`) hoặc copy đoạn mã JSON tương ứng và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes cơ bản nhưng cực kỳ mạnh mẽ. Các sếp cần cấu hình chính xác từng node sau đây:

- **On clicking 'execute' (Manual Trigger):**
  - Đây là điểm khởi đầu dạng thủ công. Các sếp có thể thay thế bằng node *Schedule Trigger* (chạy định kỳ hàng ngày/hàng tuần) hoặc *Webhook* nếu muốn kích hoạt tự động từ hệ thống ngoài.
- **Read From File (Read Binary File):**
  - Node này chịu trách nhiệm đọc file từ ổ cứng. 
  - **Cấu hình:** Điền chính xác đường dẫn tuyệt đối tới file CSV trên server của các sếp (Ví dụ: `/data/uploads/customers.csv`). Đảm bảo user chạy n8n có quyền đọc file tại thư mục này.
- **Convert To Spreadsheet (Spreadsheet File):**
  - Node này giúp chuyển đổi tệp nhị phân (binary) của file CSV thành các items dữ liệu dạng JSON mà n8n có thể hiểu được.
  - **Cấu hình:** Giữ nguyên các thiết lập mặc định (chọn định dạng CSV) hoặc tùy chỉnh dấu phân tách (Delimiter) nếu file CSV sử dụng dấu chấm phẩy (`;`) thay vì dấu phẩy (`,`).
- **Postgres (PostgreSQL Node):**
  - Node cuối cùng chịu trách nhiệm ghi dữ liệu vào database của các sếp.
  - **Cấu hình:** 
    - Chọn **Credentials** kết nối PostgreSQL của các sếp.
    - Chọn **Operation**: `Insert` (hoặc `Upsert` nếu cần cập nhật dữ liệu trùng khóa chính).
    - Chọn **Table**: Tên bảng trong database nhận dữ liệu.
    - Ánh xạ (Map) các trường dữ liệu từ node trước (`Convert To Spreadsheet`) vào các cột tương ứng trong bảng PostgreSQL.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với một file CSV nhỏ.
- Kiểm tra lại kết quả trên database xem dữ liệu đã vào đúng chuẩn chưa.
- Sau khi test ngon lành, hãy gạt công tắc sang **Active** để hệ thống sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động xóa/di chuyển file:** Sau khi import thành công, các sếp có thể thêm node **Execute Command** hoặc node quản lý file để di chuyển file CSV đó vào thư mục `archive/` nhằm tránh việc import trùng lặp ở lần chạy sau.
- **Nhận thông báo qua Telegram/Slack:** Thêm một node nhắn tin ở cuối workflow để thông báo kết quả: *"Đã import thành công 1,500 dòng từ file orders.csv vào lúc 08:00 AM!"*.
- **Xử lý file hàng loạt:** Kết hợp node *List Files* để n8n tự động quét cả một thư mục chứa hàng loạt file CSV và xử lý tuần tự từng file một.

### 📌 Kết luận
Việc đưa dữ liệu từ file CSV lên PostgreSQL nay đã trở nên đơn giản hơn bao giờ hết nhờ workflow n8n này. Hãy áp dụng ngay vào hệ thống của các sếp để tiết kiệm hàng giờ đồng hồ mỗi tuần cho những công việc giá trị hơn!