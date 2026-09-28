---
title: "🚀 Hướng dẫn sử dụng Workflow chuẩn n8n: Load Data into Spreadsheet or Database"
description: "Khám phá mẫu workflow nền tảng (Building Block) giúp bạn giả lập dữ liệu CRM và chuẩn bị sẵn sàng để đẩy vào Google Sheets, Airtable hoặc Database trong n8n."
slug: "load-data-into-spreadsheet-or-database-n8n-workflow"
tags: [n8n, automation, no-code, data-pipeline, crm, building-blocks]
keywords: [n8n workflow, load data into spreadsheet, crm contacts mock data, n8n building blocks, tự động hóa dữ liệu]
---

# 🚀 Tối ưu hóa quy trình nạp dữ liệu với Workflow mẫu: Load Data into Spreadsheet or Database

Các sếp có bao giờ cảm thấy đau đầu khi xây dựng một luồng tự động hóa nhưng chưa có dữ liệu mẫu (mock data) để test, hoặc luân chuyển dữ liệu từ một nguồn giả lập sang các bảng tính (Google Sheets, Airtable) hay database mà không biết bắt đầu từ đâu? Việc nhập liệu thủ công hoặc thiết kế luồng từ con số không thường tốn rất nhiều thời gian và dễ phát sinh lỗi cấu trúc dữ liệu.

Đừng lo lắng! Bài viết này sẽ hướng dẫn các sếp cách sử dụng workflow mẫu **"Load data into spreadsheet or database"** do Max Tkacz (Design @ n8n) thiết kế. Đây là một Building Block cực kỳ hữu ích giúp các sếp hiểu rõ cấu trúc truyền dữ liệu mẫu (đặc biệt là danh sách liên hệ CRM) để dễ dàng tích hợp vào bất kỳ cơ sở dữ liệu hay trang tính nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian thiết kế:** Cung cấp sẵn tập dữ liệu giả lập (Mock data) chuẩn xác cho các liên hệ CRM, không mất công tự tạo dữ liệu test.
- **Dễ dàng mở rộng:** Khung workflow dạng "Building Block" cho phép thay thế node chờ bằng các node kết nối Google Sheets, Airtable, PostgreSQL hoặc MySQL chỉ trong vài nốt nhạc.
- **Kiểm soát cấu trúc dữ liệu:** Giúp các sếp định hình rõ ràng các trường dữ liệu (fields) cần thiết trước khi đẩy lên hệ thống đích.
- **Thử nghiệm an toàn:** Cho phép chạy thủ công (Manual Trigger) để kiểm tra kết quả trả về của từng node mà không làm ảnh hưởng đến dữ liệu thật trên production.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một phiên bản n8n đang hoạt động (Cloud hoặc Self-hosted).
- Workflow mẫu từ kho lưu trữ chính thức của n8n (Workflow ID: 980).
- *(Tùy chọn)* Tài khoản Google Sheets, Airtable hoặc Database (PostgreSQL/MySQL) nếu các sếp muốn thay thế node "Replace me" để lưu dữ liệu thật.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp có thể truy cập trang chủ n8n workflows, tìm kiếm ID **980** hoặc sao chép mã JSON của workflow.
- Tại giao diện n8n Editor của mình, chọn **Add workflow** -> **Import from JSON** và dán mã nguồn vào để bắt đầu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes cơ bản hoạt động tuần tự như sau:

- **On clicking 'execute' (`manualTrigger`):** Node kích hoạt thủ công. Các sếp chỉ cần nhấn nút **Execute workflow** để bắt đầu chạy thử nghiệm quá trình sinh dữ liệu.
- **Set (`set`):** Node dùng để định nghĩa hoặc thiết lập các biến môi trường, tham số cấu hình ban đầu trước khi tạo dữ liệu. Các sếp có thể bổ sung các trường thông tin chung (như ngày tháng, mã lô dữ liệu) tại đây nếu cần.
- **Mock data (CRM Contacts) (`function`):** Node chứa đoạn mã JavaScript tạo ra danh sách liên hệ CRM giả lập (bao gồm tên, email, số điện thoại, công ty...). Các sếp có thể click vào node này để xem cấu trúc dữ liệu hoặc tùy chỉnh lại danh sách các trường thông tin cho phù hợp với nhu cầu thực tế của doanh nghiệp mình.
- **Replace me (`noOp`):** Đây là **điểm dừng giữ chỗ (No Operation)**. Các sếp **bắt buộc phải xóa hoặc thay thế** node này bằng các node tích hợp thực tế như:
  - *Google Sheets* (để append row vào bảng tính).
  - *Airtable* (để tạo record mới).
  - *PostgreSQL / MySQL* (để insert dữ liệu vào database).

#### 3. Kích hoạt ⚡️
- Sau khi đã thay thế node `Replace me` bằng node kết nối kho lưu trữ dữ liệu thực tế và điền Credentials đầy đủ, hãy bấm **Execute Workflow** để kiểm tra log dữ liệu đầu ra.
- Nếu dữ liệu được đẩy thành công vào Spreadsheet hoặc Database, các sếp có thể cấu hình thêm Trigger tự động (ví dụ: Schedule Trigger chạy định kỳ hàng ngày) thay vì dùng nút bấm thủ công.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo:** Thêm node Slack hoặc Telegram ở cuối luồng để nhận thông báo ngay lập tức mỗi khi dữ liệu được đồng bộ thành công vào database.
- **Xử lý lỗi (Error Handling):** Thêm nhánh **Error Trigger** để bắt lỗi trong quá trình ghi dữ liệu vào database, tránh việc luồng bị dừng đột ngột mà không rõ nguyên nhân.
- **Lọc dữ liệu trùng lặp:** Trước khi đẩy vào spreadsheet, hãy thêm một node **If** hoặc **Code** để kiểm tra xem email liên hệ đã tồn tại trong hệ thống hay chưa, giúp làm sạch dữ liệu (data cleaning).

### 📌 Kết luận
Workflow **Load data into spreadsheet or database** là một bước đệm hoàn hảo giúp các sếp làm chủ cách xử lý dữ liệu dạng danh sách (list/arrays) và đẩy chúng lên các hệ thống lưu trữ bên ngoài trong n8n. Hãy áp dụng ngay cấu trúc này để tự động hóa việc đồng bộ dữ liệu CRM cho doanh nghiệp của mình nhé!