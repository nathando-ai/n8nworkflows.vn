---
title: "🚀 Tự động trích xuất dữ liệu khách hàng Odoo và xuất file Excel/JSON với n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Odoo API, cho phép truy vấn và xuất dữ liệu khách hàng theo định dạng JSON hoặc file Excel (XLSX) qua Webhook."
slug: "chuyen-doi-du-lieu-khach-hang-odoo-json-excel-n8n"
tags: [n8n, odoo, crm, automation, excel, webhook]
keywords: [n8n workflow odoo, export odoo customer excel, trích xuất dữ liệu odoo, n8n webhook crm]
---

# 🚀 Tự động trích xuất dữ liệu khách hàng Odoo và xuất file Excel/JSON với n8n

Các doanh nghiệp sử dụng Odoo CRM thường gặp khó khăn khi cần trích xuất nhanh dữ liệu khách hàng để làm báo cáo hoặc tích hợp hệ thống mà không muốn thao tác thủ công phức tạp trên giao diện quản trị. Việc xuất file Excel hay gọi API lấy dữ liệu đôi khi mất nhiều thời gian cấu hình.

Workflow n8n này do **V3 Code Studio** phát triển sẽ giải quyết triệt để bài toán trên bằng cách cung cấp một API Endpoint tự động hóa 100%. Hệ thống sẽ nhận yêu cầu qua Webhook, truy vấn trực tiếp cơ sở dữ liệu Odoo và trả về kết quả dưới dạng JSON tích hợp hoặc file Excel (.xlsx) sẵn sàng tải về chỉ trong vài giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **API theo yêu cầu:** Tạo sẵn endpoint `/api/v1/get-customers` để truy vấn dữ liệu khách hàng linh hoạt.
- **Linh hoạt định dạng:** Tự động chuyển đổi kết quả sang JSON (dùng cho tích hợp) hoặc file Excel (.xlsx) để làm báo cáo ngay lập tức.
- **Tìm kiếm thông minh:** Hỗ trợ lọc dữ liệu theo tên khách hàng với bộ lọc động (Dynamic Filter).
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn thao tác xuất file thủ công trên Odoo CRM.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n (Cloud hoặc Self-hosted).
- Tài khoản Odoo ERP và thông tin kết nối API (Odoo API credentials).
- Công cụ test API (Postman, cURL hoặc trình duyệt web).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (hoặc import file JSON mẫu từ thư viện n8n) vào giao diện Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với hệ thống Odoo của doanh nghiệp, hãy chú ý cấu hình các node sau:
- **Node `Receive Company Request1` (Webhook):** Xác định đường dẫn endpoint `/api/v1/get-customers`. Đây là nơi nhận tham số đầu vào như `name` (tên khách hàng cần tìm) và `response_format` (`json` hoặc `excel`).
- **Node `Fetch Customer` (Odoo):** 
  - Chọn hoặc tạo mới thông tin xác thực `odooApi` với URL, Database, Username và Password/API Key của Odoo.
  - Cấu hình trỏ tới bảng liên hệ `res.partner` (Contact Table) trong Odoo.
  - Tùy chỉnh danh sách trường (`fieldsList`) cần lấy trong phần Options của node (ví dụ: tên, email, số điện thoại, thành phố,...) nếu muốn lấy thêm thông tin. *(Lưu ý: Tìm kiếm theo tên có phân biệt chữ hoa/thường tùy cấu hình Odoo).*
- **Node `Check If Excel Required1` (If) & Các node xử lý file:** Phân nhánh luồng dữ liệu dựa trên tham số `response_format`. Nếu là `excel`, luồng sẽ đi qua node `Convert to Excel1` (`convertToFile`) để đóng gói thành file `.xlsx` và trả về qua node `Respond with File1`. Ngược lại, dữ liệu trả về dạng JSON qua node `Respond with JSON1`.

#### 3. Kích hoạt ⚡️
- Thực hiện test run với các URL mẫu để kiểm tra kết quả:
  - Lấy dữ liệu dạng JSON: `/api/v1/get-customers?name=Demo&response_format=json`
  - Lấy dữ liệu dạng Excel: `/api/v1/get-customers?name=Demo&response_format=excel`
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Kết nối endpoint này với Telegram hoặc Slack bot để nhân viên kinh doanh có thể tra cứu thông tin khách hàng trực tiếp từ khung chat nội bộ.
- **Lưu trữ Log:** Thêm một node Google Sheets hoặc Database ở cuối workflow để lưu lịch sử mỗi lần có yêu cầu xuất dữ liệu nhằm quản lý việc truy cập thông tin.
- **Bảo mật API:** Thêm node kiểm tra Token/API Key ngay sau Webhook để ngăn chặn các truy vấn trái phép vào hệ thống Odoo.

### 📌 Kết luận
Workflow trích xuất dữ liệu khách hàng Odoo sang JSON và Excel là một công cụ cực kỳ hữu ích giúp tự động hóa khâu báo cáo và tích hợp dữ liệu CRM. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa quy trình vận hành ngay hôm nay!