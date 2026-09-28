---
title: "💰 Tự Động Hoá Xử Lý File CSV Thành Hóa Đơn Bằng n8n: Lưu Trữ, Tính Toán & Gửi Email (Không Cần Code)"
description: "Workflow này tự động chuyển đổi file CSV bán hàng thành hóa đơn đã tính toán, lưu trữ trong Data Tables của n8n, phát hiện trùng lặp, và gửi thông báo email tự động - hoàn toàn không cần viết code. Giúp các sếp tiết kiệm 10+ giờ/tháng xử lý thủ công."
slug: "tieu-dong-hoa-xu-ly-csv-thanh-hoa-don-bang-n8n"
tags: [n8n, automation, invoice processing, data tables, email notifications, no-code]
keywords: [n8n workflow hóa đơn, tự động hóa CSV thành hóa đơn, lưu trữ hóa đơn trong n8n, gửi email hóa đơn tự động, giải pháp không code]
---

# 🚀 **Tự Động Hoá Xử Lý File CSV Thành Hóa Đơn Bằng n8n: Lưu Trữ + Email + Tính Toán Toàn Tự Động**

## **🔥 Nỗi Đau Của Các Sếp Khi Xử Lý Hóa Đơn Thủ Công**
Hàng ngày, các sếp phải:
- **Nhập liệu thủ công** từ file Excel/CSV sang hệ thống quản lý (tốn 30-60 phút/tuần).
- **Tính toán thủ công** tổng tiền, thuế, và hóa đơn (rất dễ sai sót).
- **Gửi email hóa đơn** cho khách hàng một cách rời rạc, mất thời gian.
- **Phải kiểm tra trùng lặp** đơn hàng để tránh sai sót trong kế toán.

**Workflow này giải quyết tất cả bằng cách:**
✅ **Tự động chuyển đổi** file CSV thành hóa đơn đã tính toán.
✅ **Lưu trữ hóa đơn** trong **Data Tables** của n8n (không cần cơ sở dữ liệu ngoài).
✅ **Phát hiện trùng lặp** đơn hàng và trả lỗi 409 (Conflict).
✅ **Gửi email hóa đơn** tự động cho khách hàng (sẵn sàng kết nối Gmail).
✅ **Hoàn toàn không cần code** – chỉ cần cấu hình vài bước.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** xử lý thủ công hóa đơn.
- **Giảm sai sót** với tính toán tự động (tổng tiền, thuế, hóa đơn).
- **Lưu trữ hóa đơn** trong Data Tables của n8n (dễ dàng truy xuất, báo cáo).
- **Gửi email hóa đơn** tự động cho khách hàng (cá nhân hóa).
- **Phát hiện trùng lặp** đơn hàng và trả lỗi 409 (không bị trùng).
- **API endpoint** để tích hợp với hệ thống bán hàng (Shopify, WooCommerce...).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần:
1. **Tài khoản n8n Self-hosted** (để lưu trữ Data Tables và chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

2. **Hai Data Tables trong n8n**:
   - **Products** (cột: `sku`, `name`, `price`, `tax_rate`).
   - **Invoices** (cột: `invoice_id`, `customer_email`, `order_date`, `subtotal`, `total_tax`, `grand_total`).

3. **API Key** (nếu sử dụng node Gmail để gửi email thực tế).

4. **File CSV mẫu** (có cấu trúc: `sku,quantity,customer_email,order_date`).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10274](https://n8n.io/workflows/10274) (hoặc copy JSON từ link trên).
- **Dán vào n8n Editor**:
  - Mở n8n Workflow Editor → **Import** → Chọn **Paste JSON**.
  - Hoặc tải file `.json` và import từ **File → Import**.

### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflow gồm **18 node**, nhưng chỉ cần chú ý đến các node sau:

#### **📌 Node 1: Webhook (Nhận File CSV)**
- **Tên node**: `Receive Sales CSV`
- **Cấu hình**:
  - **Path**: `/process-sales` (không thay đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Chọn **None** (hoặc thêm Basic Auth nếu cần).

#### **📌 Node 2: Data Tables (Products & Invoices)**
- **Tên node**: `Load Product Catalog` (Data Table - Get).
  - **Chọn Data Table**: `Products` (đã tạo trước).
  - **Operation**: `Get` (lấy dữ liệu sản phẩm để enrich).

- **Tên node**: `Insert row` (Data Table - Insert).
  - **Chọn Data Table**: `Invoices` (đã tạo trước).
  - **Cấu trúc cột**: Đảm bảo khớp với mẫu:
    ```json
    {
      "invoice_id": "{{$node["Prepare Email Notifications"].json["invoice_id"]}}",
      "customer_email": "{{$node["Prepare Email Notifications"].json["customer_email"]}}",
      "order_date": "{{$node["Prepare Email Notifications"].json["order_date"]}}",
      "subtotal": "{{$node["Calculate Invoice Totals"].json["subtotal"]}}",
      "total_tax": "{{$node["Calculate Invoice Totals"].json["total_tax"]}}",
      "grand_total": "{{$node["Calculate Invoice Totals"].json["grand_total"]}}"
    }
    ```

#### **📌 Node 3: Code (Tính Toán & Kiểm Tra)**
Workflow sử dụng **JavaScript** trong các node `code` để:
- **Parse & Validate CSV** (kiểm tra định dạng, email, số lượng).
- **Enrich with Product Data** (lấy giá sản phẩm từ Data Table `Products`).
- **Calculate Invoice Totals** (tính tổng tiền, thuế).
- **Check for Duplicates** (kiểm tra đơn hàng đã tồn tại).

**Lưu ý**:
- Các node `code` đã được cấu hình sẵn, **không cần chỉnh sửa** (nếu không biết code).
- Nếu muốn thay đổi logic, mở node `code` → **Edit** → Chỉnh sửa mã JavaScript.

#### **📌 Node 4: Email Notifications (Gửi Email)**
- **Tên node**: `Prepare Email Notifications` (Code).
  - **Output**: Sẵn sàng gửi email cho khách hàng.
- **Kết nối Gmail** (nếu muốn gửi email thực tế):
  - Thêm node **Gmail** (n8n-nodes-base.gmail).
  - Cấu hình:
    - **Credentials**: Thêm tài khoản Gmail (đã cấp quyền OAuth).
    - **Subject**: `Invoice {{invoice_id}} - Order Confirmation`.
    - **Body**: Nội dung email mẫu (đã định dạng trong node `Prepare Email Notifications`).

#### **📌 Node 5: Trả Lời API (Success/Error)**
- **Node `Return Success Response`**: Trả JSON thành công khi xử lý thành công.
- **Node `Return Duplicate Error`**: Trả lỗi 409 nếu đơn hàng trùng lặp.
- **Node `Return Validation Error`**: Trả lỗi 400 nếu CSV không hợp lệ.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test với cURL** (dùng lệnh sau để gửi file CSV mẫu):
   ```bash
   curl -X POST \
     -H "Content-Type: text/csv" \
     --data-binary $'sku,quantity,customer_email,order_date\nPROD-001,2,john@example.com,2025-01-15\nPROD-002,1,jane@example.com,2025-01-15' \
     https://<your-n8n-url>/webhook/process-sales
   ```
2. **Kiểm tra kết quả**:
   - **Data Table `Invoices`**: Xem hóa đơn đã lưu.
   - **Email**: Kiểm tra hộp thư của khách hàng (nếu kết nối Gmail).
   - **Trả lời API**: Nếu thành công, trả HTTP 200; nếu lỗi, trả 400/409.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có hóa đơn mới.
   - Ví dụ: Khi hóa đơn được tạo, gửi tin nhắn Slack:
     ```json
     "text": `New Invoice created for ${customer_email} (Total: $${grand_total})`
     ```

2. **Lưu log hoạt động**:
   - Thêm node **Set** hoặc **Code** để lưu log vào Data Table `Logs` (cột: `timestamp`, `status`, `invoice_id`).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Trigger** (n8n-nodes-base.trigger) để chạy workflow hàng ngày và gửi báo cáo tổng hợp qua email.

4. **Tích hợp với Shopify/WooCommerce**:
   - Sử dụng node **HTTP Request** để gọi API từ hệ thống bán hàng → n8n → xử lý CSV thành hóa đơn.

5. **Tự động tạo hóa đơn PDF**:
   - Kết nối với **Google Docs** hoặc **PDF Generator** để tạo hóa đơn PDF từ dữ liệu trong Data Table.
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công** trong xử lý hóa đơn, đồng thời đảm bảo:
✔ **Tính toán chính xác** (không sai sót).
✔ **Lưu trữ an toàn** trong Data Tables của n8n.
✔ **Gửi email tự động** cho khách hàng.
✔ **Phát hiện trùng lặp** và trả lỗi 409.

**Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình Data Tables.
3. **Test với cURL** và bắt đầu tự động hóa!

**🚀 Cần hỗ trợ?** Đăng ký VPS n8n với mã giảm giá **VPSN8N** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để có môi trường ổn định!