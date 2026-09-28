---
title: "💰 Tự Động Hóa Tạo & Gửi Hóa Đơn PDF + Email Từ Airtable (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn tạo hóa đơn PDF chuyên nghiệp từ dữ liệu Airtable, gửi email tự động với đính kèm, và cập nhật trạng thái 'Đã gửi' - tiết kiệm thời gian lên đến 80% cho bộ phận tài chính."
slug: "tieu-dong-hoa-tao-hoa-don-airtable-email"
tags: [n8n, automation, airtable, pdf-generator, email-automation, invoice-management]
keywords: [tự động hóa hóa đơn, n8n workflow airtable, tạo hóa đơn pdf tự động, gửi email hóa đơn tự động, quản lý hóa đơn không code]
---

# 🚀 **Tự Động Hóa Tạo & Gửi Hóa Đơn PDF Từ Airtable (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, bộ phận tài chính phải:
- **Tìm kiếm và tổng hợp** dữ liệu khách hàng, mặt hàng, và chi tiết hóa đơn từ Airtable.
- **Tạo hóa đơn** từ đầu bằng Excel/Canva hoặc sử dụng các công cụ có phí.
- **Gửi email** với hóa đơn đính kèm, đồng thời cập nhật trạng thái "Đã gửi" thủ công.
- **Lo lắng** về sai sót trong quá trình nhập liệu hoặc mất thời gian cho công việc lặp lại.

**Workflow này giải quyết tất cả!** Với **Airtable + n8n + CustomJS PDF Toolkit**, các sếp có thể:
✅ **Tạo hóa đơn PDF chuyên nghiệp** chỉ bằng một cú nhấp chuột.
✅ **Gửi email tự động** với hóa đơn đính kèm đến khách hàng.
✅ **Cập nhật trạng thái** "Đã gửi" trong Airtable để tránh trùng lặp.
✅ **Tiết kiệm thời gian** lên đến **80%** cho công việc quản lý hóa đơn hàng tháng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ nhanh, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tạo hóa đơn thủ công mỗi tháng.
- **Chính xác 100%**: Dữ liệu tự động lấy từ Airtable, tránh sai sót nhập liệu.
- **Hóa đơn chuyên nghiệp**: PDF được thiết kế đẹp mắt với logo, thông tin công ty, và chi tiết chi tiết.
- **Gửi email tự động**: Khách hàng nhận hóa đơn ngay lập tức qua email.
- **Quản lý dễ dàng**: Trạng thái "Đã gửi" được cập nhật tự động, không bị quên.
- **Mở rộng dễ dàng**: Kết hợp với Slack/Telegram để thông báo hoặc lưu log cho báo cáo.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Airtable** (đã tạo bảng `Invoices`, `Clients`, và `Invoice Items` theo mẫu [đây](https://airtable.com/apphyDa3uYAq0VOMW/shrSe39NZYrqm4gtE)).
2. **API Key Airtable**:
   - Mở Airtable → Cài đặt → **API Key** (để sử dụng trong n8n).
3. **Tài khoản Email SMTP** (để gửi email tự động):
   - Dịch vụ như **Gmail (SMTP), SendGrid, hoặc Mailgun**.
   - Cấu hình **SMTP Host, Port, Username, Password, và Security Protocol** (TLS/SSL).
4. **CustomJS PDF Toolkit** (đã cài đặt node `@custom-js/n8n-nodes-pdf-toolkit` trong n8n).
5. **Thông tin công ty** (để điền vào hóa đơn):
   - Tên công ty, địa chỉ, số điện thoại, email, và logo (nếu có).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow** từ [n8n.io/workflows/9772](https://n8n.io/workflows/9772) (chọn **Download JSON**).
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
- **Hoặc** copy/paste JSON từ file vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **11 node**, các sếp cần chú ý cấu hình **các node sau**:

##### **A. Cấu Hình Airtable**
1. **Node "Get Ready Invoices"**:
   - **Table**: Chọn bảng `Invoices` trong Airtable.
   - **Filter**: Lọc theo trường `Status = "Ready"` (để lấy hóa đơn chưa gửi).
   - **Fields**: Chọn các trường cần lấy (ví dụ: `Invoice ID`, `Client`, `Amount`, `Due Date`).

2. **Node "Get Clients"**:
   - **Table**: Chọn bảng `Clients`.
   - **Fields**: Lấy thông tin khách hàng (ví dụ: `Name`, `Email`, `Phone`).

3. **Node "Get Invoice Items"**:
   - **Table**: Chọn bảng `Invoice Items`.
   - **Filter**: Lấy theo `Invoice ID` (sẽ được nối với hóa đơn trong quá trình aggregate).

4. **Node "Update record"**:
   - **Table**: Bảng `Invoices`.
   - **Field to Update**: `Status` → Đặt giá trị `"Sent"` (để hóa đơn không bị reload lần sau).

##### **B. Cấu Hình CustomJS PDF Generator**
1. **Node "Set Company Details"**:
   - Điền thông tin công ty vào các trường:
     - `companyName`, `address`, `phone`, `email`, `logoUrl` (nếu có).
   - **Lưu ý**: Nếu không có logo, để trống `logoUrl`.

2. **Node "Map Fields"**:
   - **Mapping từ Airtable sang PDF**:
     - `invoiceNumber` → `Invoice ID` (trong Airtable).
     - `clientName` → `Client.Name`.
     - `clientEmail` → `Client.Email`.
     - `items` → `Invoice Items` (sẽ được aggregate sau).
     - `dueDate` → `Due Date`.
     - `totalAmount` → `Amount`.

3. **Node "Generate Invoice"**:
   - **Template**: Chọn mẫu PDF đã thiết kế (nếu có nhiều mẫu, chọn mặc định).
   - **Credentials**: Đảm bảo đã chọn `customJsApi` (đã cấu hình trong n8n).

##### **C. Cấu Hình Email**
1. **Node "Send Email With Attachment"**:
   - **SMTP Credentials**: Chọn `smtp` (đã cấu hình trước).
   - **From Email**: Điền email gửi (ví dụ: `billing@congty.com`).
   - **To Email**: Lấy từ trường `Client.Email` trong Airtable.
   - **Subject**: Ví dụ: `"Hóa đơn #{{$node["Get Ready Invoices"].json["$"].invoiceNumber}} - {{$node["Get Ready Invoices"].json["$"].clientName}}"`.
   - **Body**: Nội dung email (có thể thêm thông báo như: *"Xin chào [Tên Khách Hàng], đây là hóa đơn của bạn. Vui lòng thanh toán trước ngày [Due Date]."*).
   - **Attachment**: Chọn file PDF được tạo bởi `Generate Invoice`.

##### **D. Node "Aggregate" & "Loop Over Items"**
- **Aggregate** sẽ kết hợp dữ liệu từ `Get Ready Invoices`, `Get Clients`, và `Get Invoice Items` thành một danh sách hóa đơn hoàn chỉnh.
- **Loop Over Items** sẽ xử lý từng hóa đơn một (do số lượng mặt hàng không nhất thiết bằng số lượng hóa đơn).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** để chạy thử với một hóa đơn mẫu.
   - Kiểm tra:
     - Hóa đơn PDF có được tạo không?
     - Email có được gửi không?
     - Trạng thái trong Airtable có được cập nhật thành `"Sent"` không?

2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Thêm node `slackSend` hoặc `telegramSend` sau `Send Email` để thông báo khi hóa đơn được gửi thành công.
   - Ví dụ: *"Hóa đơn #{{$node["Get Ready Invoices"].json["$"].invoiceNumber}} đã được gửi cho {{$node["Get Ready Invoices"].json["$"].clientName}}!"*

2. **Lưu Log Cho Báo Cáo**:
   - Thêm node `stickyNote` để ghi lại lịch sử gửi hóa đơn (ví dụ: ngày gửi, khách hàng, trạng thái).
   - Có thể kết nối với **Google Sheets** để tự động tạo báo cáo tháng.

3. **Tự Động Chạy Hàng Tháng**:
   - Sử dụng **n8n Trigger** (ví dụ: `cronTrigger`) để chạy workflow tự động vào ngày cuối tháng.
   - Cấu hình trong `cronTrigger`:
     - `Schedule`: `0 0 1 1 *` (ngày 1 hàng tháng, lúc 00:00).

4. **Tùy Chỉnh Mẫu PDF**:
   - Nếu muốn thay đổi thiết kế hóa đơn, chỉnh sửa template trong **CustomJS PDF Toolkit**.
   - Các sếp có thể tải template mẫu từ [đây](https://www.beta.customjs.space/images/integration/n8n/InvoiceGeneratorWorkflow.png) và điều chỉnh.

5. **Xử Lý Lỗi**:
   - Nếu email không gửi được, kiểm tra:
     - SMTP có đúng không? (Kiểm tra port, TLS/SSL).
     - Email `From` có hợp lệ không?
     - Khách hàng có tồn tại trong Airtable không?

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại quản lý hóa đơn, đồng thời **tăng cường chuyên nghiệp** với hóa đơn PDF đẹp mắt và gửi email tự động. **Chỉ cần một cú nhấp chuột**, hóa đơn đã sẵn sàng được gửi!

**Hành động ngay hôm nay**:
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Airtable, SMTP, và thông tin công ty**.
3. **Test run** và **bật Active** để bắt đầu tự động hóa!

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để có môi trường ổn định 24/7! 🚀