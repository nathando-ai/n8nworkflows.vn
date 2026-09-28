---
title: "🚀 Tự động tạo hóa đơn PDF chuyên nghiệp từ Google Sheets bằng n8n và DocuPotion"
description: "Hướng dẫn xây dựng workflow n8n tự động phát hiện trạng thái Active trên Google Sheets, tổng hợp chi tiết, tạo file PDF qua DocuPotion và lưu trữ trực tiếp vào Google Drive."
slug: "tu-dong-tao-hoa-don-pdf-google-sheets-docu_potion-n8n"
tags: [n8n, automation, google-sheets, google-drive, docupotion, invoice]
keywords: [n8n workflow, tạo hóa đơn tự động, google sheets pdf, docu_potion n8n, tự động hóa kế toán]
---

# 🚀 Tự động hóa tạo hóa đơn PDF từ Google Sheets với DocuPotion và Google Drive

Các sếp làm freelancer, chủ doanh nghiệp nhỏ hay đội ngũ kế toán có bao giờ cảm thấy mệt mỏi khi cứ phải thủ công copy dữ liệu từ Google Sheets sang file PDF để gửi cho khách? Việc này không chỉ tốn hàng giờ đồng hồ mỗi tuần mà còn rất dễ nhầm lẫn thông tin, số lượng hay đơn giá.

Workflow n8n này chính là "vũ khí" tự động hóa 100% giúp các sếp giải quyết triệt để nỗi đau đó. Chỉ cần đổi trạng thái thành `Active` trên Google Sheets, hệ thống sẽ tự động gom nhặt dữ liệu, sinh ra chiếc hóa đơn PDF đẹp mắt, lưu vào Google Drive và cập nhật ngược lại link tải vào bảng tính. Quá chuyên nghiệp và nhanh chóng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần thao tác thủ công, tiết kiệm hàng chục giờ làm việc mỗi tháng.
- **Chính xác tuyệt đối:** Lấy đúng dữ liệu khách hàng và danh sách sản phẩm/dịch vụ (line items) từ Google Sheets.
- **Chuyên nghiệp:** Tạo file PDF chuẩn chỉnh thông qua template của DocuPotion.
- **Đồng bộ mượt mà:** Tự động lưu file lên Google Drive và điền link `pdf_url` kèm cập nhật trạng thái `Sent` ngay trong bảng tính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Google Account** (Để kết nối Google Sheets và Google Drive).
- **Tài khoản DocuPotion** (Dịch vụ tạo template tài liệu chuyên nghiệp).
- **Cài đặt Community Node:** `n8n-nodes-docupotion`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n (`15259`) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Invoice Status Updated to Active (`googleSheetsTrigger`):** 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Thay thế **Document ID** của template mẫu bằng Google Sheet quản lý hóa đơn thực tế của doanh nghiệp.
  - Sheet của các sếp cần chuẩn bị 2 tab chính:
    1. `invoices`: Các cột gồm `invoice_number`, `invoice_date`, `due_date`, `status`, `customer_name`, `customer_email`, `customer_company`, `customer_address`, `pdf_url`.
    2. `line items`: Các cột gồm `invoice_number`, `description`, `quantity`, `unit_price`.

- **Filter for Updated Invoice (`filter`):**
  - Thiết lập điều kiện lọc: Chỉ cho phép các dòng có `status` bằng `Active` đi tiếp.

- **Loop Over Invoices (`splitInBatches`):**
  - Giúp xử lý từng hóa đơn một cách tuần tự, tránh quá tải khi có nhiều hóa đơn cùng kích hoạt.

- **Get Invoice Items (`googleSheets`):**
  - Lấy tất cả các dòng sản phẩm/dịch vụ (line items) khớp với số hóa đơn (`invoice_number`). Nhớ trỏ đúng Document ID.

- **Create JSON Object From Items (`aggregate`):**
  - Gom nhóm các dòng sản phẩm thành một mảng JSON duy nhất để truyền vào template PDF.

- **Generate PDF (`n8n-nodes-docupotion.docupotion`):**
  - Cài đặt community node DocuPotion (`Settings → Community Nodes → DocuPotion`).
  - Tạo mẫu hóa đơn template bên trong DocuPotion và dán **Template ID** vào node này.

- **Upload to Google Drive (`googleDrive`):**
  - Mặc định file PDF sẽ được lưu ở thư mục gốc (Root) của Drive với tên `Invoice-{invoice_number}.pdf`. Các sếp có thể đổi sang thư mục con (Folder) tùy ý trong cấu hình node.

- **Add Link to Google Sheet (`googleSheets` - Update):**
  - Cập nhật lại dòng tương ứng trong Google Sheet: Điền link file vào cột `pdf_url` và đổi trạng thái thành `Sent`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách đổi một dòng trạng thái trong Google Sheets sang `Active`.
- Kiểm tra kết quả trả về ở Google Drive, Google Sheets và bật nút **Active** để hệ thống chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp gửi Email:** Nối thêm node Gmail hoặc SendGrid ngay sau khi upload xong để tự động gửi hóa đơn PDF tới email (`customer_email`) của khách hàng.
- **Thông báo nội bộ:** Gắn thêm node Telegram hoặc Slack để bắn thông báo về nhóm kế toán mỗi khi có hóa đơn mới được tạo thành công.
- **Lưu log lỗi:** Sử dụng Error Trigger để bắt sự cố nếu tài khoản DocuPotion hết hạn hoặc thiếu dữ liệu đầu vào.

### 📌 Kết luận
Workflow tự động hóa tạo hóa đơn PDF với Google Sheets và DocuPotion là giải pháp tuyệt vời giúp tối ưu hóa quy trình tài chính - kế toán cho các cá nhân và doanh nghiệp nhỏ. Hãy "lên đồ" ngay hôm nay để tiết kiệm thời gian và nâng tầm chuyên nghiệp cho doanh nghiệp của các sếp!