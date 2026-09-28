---
title: "🚀 Xuất dữ liệu công ty từ Odoo qua API Endpoint với lựa chọn JSON và Excel trong n8n"
description: "Hướng dẫn xây dựng API endpoint tự động truy vấn và xuất dữ liệu công ty từ Odoo dưới dạng JSON hoặc file Excel (.xlsx) cực kỳ nhanh chóng bằng n8n."
slug: "xuat-du-lieu-cong-ty-odoo-api-json-excel-n8n"
tags: [n8n, automation, odoo, api, crm, excel, no-code]
keywords: [n8n workflow, odoo api, xuat du lieu odoo, n8n webhook, odoo to excel, tich hop odoo n8n]
---

# 🚀 Xuất dữ liệu công ty từ Odoo qua API Endpoint với lựa chọn JSON và Excel

Các sếp đang đau đầu vì mỗi lần cần lấy dữ liệu công ty từ hệ thống Odoo CRM lại phải thao tác thủ công xuất báo cáo, hoặc tốn hàng tuần để lập trình viên viết API riêng biệt cho từng nhu cầu (JSON cho hệ thống tích hợp, Excel cho sếp lớn xem báo cáo)? 

Giải pháp đây rồi! Workflow n8n này sẽ giúp các sếp tạo ra một **API Endpoint linh hoạt 100% không cần code**, tự động nhận yêu cầu, truy vấn dữ liệu từ Odoo và trả về kết quả dưới dạng **JSON** hoặc **file Excel (.xlsx)** ngay lập tức dựa theo tham số truyền vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo API Endpoint tức thì:** Cung cấp sẵn đường dẫn API để query dữ liệu công ty từ Odoo mà không cần đụng đến code backend phức tạp.
- **Linh hoạt định dạng trả về:** Hỗ trợ cả 2 định dạng phổ biến là **JSON** (cho các ứng dụng tích hợp, webhook) và **Excel (.xlsx)** (cho báo cáo kinh doanh trực quan).
- **Tìm kiếm thông minh:** Hỗ trợ lọc dữ liệu theo tên công ty bằng bộ lọc động (Dynamic Filter) cực kỳ tiện lợi.
- **Tiết kiệm thời gian tối đa:** Thay vì mất hàng giờ thao tác thủ công trên Odoo, mọi thứ được xử lý tự động trong vòng tích tắc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Odoo Account:** Tài khoản truy cập Odoo CRM/ERP và thông tin kết nối API (URL, Database, Username, API Key).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình, hoặc import thông qua file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để API hoạt động trơn tru với hệ thống Odoo của các sếp, hãy chú ý cấu hình các node sau:

- **Receive Company Request (Webhook):** Node này đóng vai trò nhận request từ bên ngoài. Các sếp hãy lưu ý đường dẫn endpoint mặc định: `/api/v1/get-companies`.
- **Fetch Companies from Odoo (Odoo Node):** 
  - Chọn hoặc tạo mới **Credentials** kết nối tới tài khoản Odoo của các sếp (`odooApi`).
  - Cấu hình trỏ tới bảng quản lý công ty `res.company`.
  - *Lưu ý quan trọng:* Tính năng tìm kiếm theo tên có phân biệt chữ hoa/thường (case-sensitive) tùy thuộc vào cấu hình của Odoo. Các sếp có thể tùy chỉnh thêm các trường dữ liệu muốn lấy (như mã số thuế VAT, địa chỉ, số điện thoại...) trong phần `fieldsList`.
- **Check If Excel Required (If Node) & Convert to Excel (Convert To File):** Xử lý logic rẽ nhánh tự động. Nếu tham số `response_format=excel`, hệ thống sẽ tự động đóng gói dữ liệu thành file `.xlsx` và trả về qua node **Respond with File**, ngược lại sẽ trả về dữ liệu dạng JSON qua node **Respond with JSON**.

#### 3. Cách Test API ⚡️
Sau khi kích hoạt workflow (Active), các sếp có thể test trực tiếp trên trình duyệt hoặc Postman với cấu trúc URL như sau:
- Lấy dữ liệu dạng JSON: 
  `https://domain-n8n. của-sếp/api/v1/get-companies?name=Tech&response_format=json`
- Tải file Excel trực tiếp: 
  `https://domain-n8n.của-sếp/api/v1/get-companies?name=Tech&response_format=excel`

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình kinh doanh, các sếp có thể mở rộng workflow này bằng cách:
1. **Ghi Log vào Google Sheets / Airtable:** Mỗi khi có một bên gọi API truy vấn dữ liệu, lưu lại lịch sử (Ai gọi, thời điểm nào, từ khóa gì) để dễ dàng kiểm soát.
2. **Tích hợp Thông báo Telegram/Slack:** Bắn một tin nhắn thông báo về nhóm chat nội bộ mỗi khi có đối tác hoặc hệ thống khác tải báo cáo Excel từ Odoo.
3. **Bảo mật API Endpoint:** Thêm một Header Auth (Bearer Token) ở node Webhook đầu vào để đảm bảo chỉ những hệ thống được cấp phép mới có quyền gọi API lấy dữ liệu công ty.

### 📌 Kết luận
Với workflow n8n này, việc trích xuất và tích hợp dữ liệu từ Odoo chưa bao giờ dễ dàng đến thế. Hãy "lên đồ" ngay hôm nay để tự động hóa toàn bộ hệ thống báo cáo và đồng bộ dữ liệu của doanh nghiệp các sếp nhé!