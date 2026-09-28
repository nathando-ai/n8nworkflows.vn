---
title: "📄 **Tự Động Hóa Phân Tích & Lưu Trữ Hóa Đơn PDF vào Airtable Với LlamaParse & n8n (Không Cần Code!)**"
description: "Giải pháp tự động hóa hoàn toàn cho doanh nghiệp nhỏ và startup để phát hiện, phân tích hóa đơn PDF từ Google Drive, trích xuất dữ liệu chi tiết, và lưu trữ vào Airtable một cách tự động. Tiết kiệm thời gian lên đến 80% trong quản lý hóa đơn!"
slug: "tự-dộng-hoa-phân-tích-hoa-don-pdf-llamaparse-airtable"
tags: [n8n, automation, ai, airtable, google-drive, llama-parse, no-code, business-automation]
keywords: [n8n workflow phân tích hóa đơn, tự động hóa hóa đơn PDF, LlamaParse với n8n, lưu hóa đơn vào Airtable, tự động hóa quản lý tài chính]
---

# 🚀 **Tự Động Hóa Phân Tích Hóa Đơn PDF & Lưu Trữ Vào Airtable Với LlamaParse & n8n**

### **Nỗi Đau Của Các Sếp Trong Quản Lý Hóa Đơn**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Tải xuống** hóa đơn từ email hoặc Google Drive.
- **Đọc thủ công** từng trang PDF để trích xuất thông tin như tên khách hàng, số hóa đơn, ngày phát hành, và chi tiết hàng hóa/dịch vụ.
- **Nhập liệu** vào hệ thống quản lý (Excel, Airtable, ERP...) với nguy cơ **lỗi nhập sai** cao.
- **Tìm kiếm** hóa đơn cũ trong hàng trăm tệp PDF khi cần kiểm tra lại.

**Kết quả?** Thời gian làm việc bị "chôn vùi" trong công việc lặp lại, hiệu suất giảm, và rủi ro sai sót tăng cao.

---
### **🎯 Giải Pháp Của Workflow Này: Tự Động Hóa 100%**
Workflow này **không cần code** sẽ:
✅ **Tự động phát hiện** hóa đơn mới được upload vào Google Drive.
✅ **Phân tích nội dung** của PDF bằng **LlamaParse** (AI tiên tiến của Llama Cloud) để trích xuất:
   - Số hóa đơn, ngày phát hành, tên khách hàng, tổng tiền.
   - **Chi tiết từng dòng hàng** (sản phẩm/dịch vụ, số lượng, đơn giá, tổng).
✅ **Lưu trữ dữ liệu** vào **Airtable** với cấu trúc rõ ràng:
   - **Bảng "Invoices"** (thông tin tổng quan hóa đơn).
   - **Bảng "Line Items"** (chi tiết từng dòng hàng).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản Cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm **80% công việc thủ công** trong quản lý hóa đơn.
- **Chính xác 100%**: Tránh sai sót do nhập liệu tay (AI phân tích chính xác).
- **Dữ liệu sẵn sàng**: Tất cả thông tin hóa đơn được **cập nhật tự động** vào Airtable.
- **Tích hợp hoàn hảo**: Hoạt động liên tục, không cần can thiệp của con người.
- **Dễ dàng phân tích**: Dữ liệu trong Airtable có thể **lọc, báo cáo, và tự động hóa thêm** (ví dụ: gửi báo cáo định kỳ qua email).
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu hóa đơn và kích hoạt trigger).
2. **Tài khoản Airtable** (để lưu trữ dữ liệu hóa đơn).
3. **API Key của LlamaParse** (để phân tích PDF):
   - Đăng ký tại: [https://llama.cloud/](https://llama.cloud/)
   - Mua **gói API** phù hợp (gói free có giới hạn).
4. **API Key của OpenAI** (nếu sử dụng phiên bản gốc của workflow, nhưng **không bắt buộc** vì LlamaParse đã tích hợp sẵn).
5. **Folder Google Drive** để lưu hóa đơn (cần chia sẻ quyền cho n8n).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/2661](https://n8n.io/workflows/2661) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/2661) và dán vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **9 node chính**, nhưng các sếp chỉ cần chú ý đến **5 node quan trọng** sau:

##### **A. Cấu Hình Google Drive Trigger (Node: "Google Drive Trigger")**
- **Mục đích**: Phát hiện hóa đơn mới được upload vào folder.
- **Cách thiết lập**:
  1. Vào **Google Drive** → Tạo **1 folder mới** (ví dụ: `Hóa Đơn Auto`).
  2. Trong n8n, chọn **Google Drive Trigger**:
     - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).
     - **Folder ID**: Nhập **Folder ID** của folder bạn tạo (lấy từ liên kết Google Drive: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
     - **File Types**: Chọn `application/pdf` (chỉ phát hiện file PDF).

##### **B. Cấu Hình LlamaParse (Node: "OpenAI - Extract Line Items")**
- **Mục đích**: Gửi file PDF đến LlamaParse để phân tích.
- **Cách thiết lập**:
  1. Vào **LlamaParse Dashboard** ([https://llama.cloud/](https://llama.cloud/)) → Tạo **1 Webhook URL**.
  2. Trong n8n, chọn **HTTP Request** (node "OpenAI - Extract Line Items"):
     - **Method**: `POST`.
     - **URL**: Điền **Webhook URL** từ LlamaParse.
     - **Headers**:
       ```json
       {
         "Authorization": "Bearer YOUR_LLAMA_API_KEY",
         "Content-Type": "application/json"
       }
       ```
     - **Body**:
       ```json
       {
         "file": "{{ $node["Google Drive"].json["file"] }}",
         "webhook_url": "{{ $node["Webhook"].triggerUrl }}"
       }
       ```
       *(Lưu ý: `$node["Google Drive"].json["file"]` là đường dẫn file từ Google Drive, `$node["Webhook"].triggerUrl` là URL webhook của n8n để nhận kết quả phân tích.)*

##### **C. Cấu Hình Airtable (Node: "Create Invoice" & "Create Line Item")**
- **Mục đích**: Lưu dữ liệu hóa đơn và chi tiết dòng hàng vào Airtable.
- **Cách thiết lập**:
  1. Vào **Airtable** → Tạo **2 bảng**:
     - **Bảng "Invoices"** (cột: `Invoice Number`, `Date`, `Customer Name`, `Total Amount`, `PDF File Link`).
     - **Bảng "Line Items"** (cột: `Invoice ID` (liên kết với bảng Invoices), `Product/Service`, `Quantity`, `Unit Price`, `Total`).
  2. Trong n8n:
     - **Credentials**: Chọn `airtableTokenApi` (đã cấu hình trước).
     - **Base ID & Table Name**: Nhập **ID của Base** và tên bảng (`Invoices` và `Line Items`).
     - **Fields**:
       - **Create Invoice**:
         ```json
         {
           "Invoice Number": "{{ $json["invoice_number"] }}",
           "Date": "{{ $json["date"] }}",
           "Customer Name": "{{ $json["customer_name"] }}",
           "Total Amount": "{{ $json["total_amount"] }}",
           "PDF File Link": "{{ $node["Google Drive"].json["file"] }}"
         }
         ```
       - **Create Line Item**:
         ```json
         {
           "Invoice ID": "{{ $node["Create Invoice"].json["id"] }}",
           "Product/Service": "{{ $json["line_items"][0]["product"] }}",
           "Quantity": "{{ $json["line_items"][0]["quantity"] }}",
           "Unit Price": "{{ $json["line_items"][0]["unit_price"] }}",
           "Total": "{{ $json["line_items"][0]["total"] }}"
         }
         ```
         *(Lưu ý: Cần **lặp qua từng dòng hàng** trong `line_items` bằng node `Process Line Items` sau.)*

##### **D. Xử Lý Dữ liệu Line Items (Node: "Process Line Items")**
- **Mục đích**: Chuyển dữ liệu từ dạng JSON thành mảng để tạo nhiều dòng hàng.
- **Cách thiết lập**:
  - Trong node **Code** (tên: `Process Line Items`), sử dụng mã JavaScript sau:
    ```javascript
    // Kiểm tra nếu có dữ liệu line items
    if ($input.all().line_items && $input.all().line_items.length > 0) {
      // Tạo mảng để lưu trữ các dòng hàng
      const lineItems = $input.all().line_items.map(item => ({
        Product: item.product,
        Quantity: item.quantity,
        UnitPrice: item.unit_price,
        Total: item.total
      }));

      // Gửi dữ liệu về node tiếp theo
      return { lineItems };
    } else {
      return { lineItems: [] };
    }
    ```

##### **E. Webhook (Node: "Webhook")**
- **Mục đích**: Nhận kết quả phân tích từ LlamaParse và xử lý tiếp.
- **Cách thiết lập**:
  - **Path**: Để mặc định (`0f7f5ebb-8b66-453b-a818-20cc3647c783`).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần (n8n tự động tạo URL webhook).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Upload **1 file PDF hóa đơn** vào folder Google Drive đã cấu hình.
   - Kiểm tra **Airtable** để xem dữ liệu đã được lưu chưa.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Draft** sang **Active**.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để **báo cáo ngay khi hóa đơn mới được phân tích**.
   - Ví dụ:
     ```json
     {
       "text": `📄 Hóa đơn mới được phân tích: {{ $json["invoice_number"] }} (Tổng: {{ $json["total_amount"] }} VND)`
     }
     ```

2. **Lưu Log & Theo Dõi Lỗi**:
   - Thêm node **Google Sheets** hoặc **Airtable Logs** để ghi lại **lịch sử phân tích** và **báo cáo lỗi** (nếu LlamaParse không phân tích được).

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để **tạo báo cáo tổng hợp** hàng tháng và gửi qua email.

4. **Tự Động Hoá Thanh Toán**:
   - Kết nối với **Momo, ZaloPay, hoặc ngân hàng** để **tự động chuyển khoản** khi hóa đơn được xác nhận.

5. **Cải Thiện LlamaParse**:
   - Nếu LlamaParse không phân tích chính xác, thử **cập nhật prompt** trong HTTP Request:
     ```json
     {
       "prompt": "Extract invoice details in Vietnamese format: Invoice Number, Date, Customer Name, Line Items (Product, Quantity, Unit Price, Total).",
       "file": "{{ $node["Google Drive"].json["file"] }}"
     }
     ```

---

### **📌 Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **các quyết định chiến lược** thay vì mắc kẹt trong công việc thủ công. Với **AI + n8n + Airtable**, quản lý hóa đơn trở nên **nhanh chóng, chính xác, và tự động hóa hoàn toàn**.

**Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/2661](https://n8n.io/workflows/2661).
2. **Cấu hình Google Drive, LlamaParse, và Airtable** theo hướng dẫn trên.
3. **Upload hóa đơn đầu tiên** và xem **dữ liệu tự động xuất hiện** trong Airtable!

---
**💡 Cần hỗ trợ?** Xem video setup chi tiết tại:
[![Youtube Thumbnail](https://img.youtube.com/vi/E4I0nru-fa8/maxresdefault.jpg)](https://youtu.be/E4I0nru-fa8)

**📢 Tham gia cộng đồng 5minAI** để học thêm nhiều workflow tự động hóa khác:
👉 [https://www.skool.com/5minai](https://www.skool.com/5minai)