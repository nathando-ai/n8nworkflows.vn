---
title: "📄 Tự Động Hóa Phân Tích & Trích Xuất Dữ Liệu Hóa Đơn PDF → Excel Bằng Nanonets OCR (Không Code)"
description: "Workflow tự động hóa nhận file PDF hóa đơn, trích xuất dữ liệu chi tiết (số hóa đơn, ngày, tổng tiền, chi tiết hàng hóa) bằng công nghệ OCR của Nanonets, sau đó xuất ra file Excel sẵn sàng phân tích. Giúp doanh nghiệp tiết kiệm 80% thời gian xử lý hóa đơn thủ công."
slug: "tieu-dong-hoa-phan-tich-hoa-don-pdf-den-excel"
tags: [n8n, automation, invoice processing, OCR, Nanonets, Excel, no-code]
keywords: [tự động hóa hóa đơn PDF, trích xuất dữ liệu hóa đơn, Nanonets OCR, export Excel từ PDF, workflow n8n không code, tự động hóa tài chính doanh nghiệp]
---

# 🚀 **Tự Động Hóa Phân Tích Hóa Đơn PDF → Excel: Từ Thủ Công Sang Tự Động 100%**

### **Nỗi Đau Của Các Sếp: "Tôi phải mất 2-3 tiếng mỗi tuần để nhập liệu hóa đơn từ PDF vào Excel!"**
Hóa đơn PDF từ nhà cung cấp, đơn hàng từ khách hàng, hoặc giấy tờ pháp lý từ cơ quan thuế... đều là những tệp cần phải **quét, trích xuất, và nhập liệu thủ công** vào bảng Excel. Đây là công việc **mòn mỏi, dễ sai sót**, và **tốn thời gian** mà không mang lại giá trị thực sự cho doanh nghiệp.

**Workflow này giải quyết:**
✅ **Tự động nhận file PDF** từ form hoặc webhook (không cần cài đặt phần mềm).
✅ **Trích xuất dữ liệu chi tiết** (số hóa đơn, ngày, tổng tiền, chi tiết hàng hóa, số lượng, đơn vị, giá) bằng **Nanonets OCR** (chính xác hơn 95%).
✅ **Xuất ra file Excel** sẵn sàng phân tích, tổng hợp, hoặc kết nối với phần mềm kế toán.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** so với nhập liệu thủ công (tính toán: 20 giờ/tháng → chỉ 4 giờ/tháng).
- **Giảm sai sót** (OCR Nanonets có độ chính xác cao, giảm thiểu lỗi nhập liệu).
- **Dữ liệu sẵn sàng phân tích** (Excel có định dạng chuẩn, dễ kết nối với Power BI, Google Sheets, hoặc phần mềm kế toán).
- **Hoạt động tự động** (không cần phải nhớ nhắc nhở, hoạt động liên tục).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Nanonets** (đăng ký tại [nanonets.com](https://nanonets.com/)) và **API Key**.
2. **Workflow ID** của Nanonets (mỗi workflow OCR sẽ có ID riêng).
3. **Credentials trong n8n**:
   - Thêm **HTTP Basic Auth** cho Nanonets (tên: `Nanonets Credentials`, API Key từ tài khoản Nanonets).
   - Thêm **Webhook URL** (nếu sử dụng phương thức nhận file qua webhook).

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng cách:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/6194) (ấn "Export" trên trang workflow gốc).
- **Copy JSON** và dán vào **n8n Editor** (trang `Workflow` → `Import`).

:::note[**Lưu ý**]
- Nếu import từ file JSON, **không cần chỉnh sửa** phần `Webhook Path` (n8n sẽ tự động sinh URL).
- Nếu copy/paste, **đảm bảo giữ nguyên cấu trúc JSON** để tránh lỗi.
:::

### **2. Các Bước Cấu Hình Bắt Buộc 📌**

#### **A. Cấu Hình Credentials cho Nanonets**
1. Trong **n8n Credentials Manager** (đường dẫn: `Settings` → `Credentials`):
   - Tạo **một credential mới** với loại **HTTP Basic Auth**.
   - **Tên credential**: `Nanonets Credentials` (hoặc tên tùy ý).
   - **Username**: `API Key` từ tài khoản Nanonets (tìm ở `API Keys` trong tài khoản).
   - **Password**: **Không cần điền** (n8n sẽ tự động sử dụng API Key).

2. **Áp dụng credential** cho các node `HTTP Request` trong workflow:
   - Mở node `HTTP Request` và `HTTP Request2`.
   - Trong tab `Credentials`, chọn `Nanonets Credentials`.

#### **B. Điền Workflow ID của Nanonets**
1. **Tạo một Workflow OCR mới** trên Nanonets:
   - Đăng nhập [nanonets.com](https://nanonets.com/).
   - Tạo **Workflow mới** với loại **Document Processing**.
   - Chọn **template "Invoice"** (hoặc tạo từ đầu với các field cần trích xuất).
   - Sau khi tạo xong, **copy Workflow ID** (tìm ở URL hoặc tab `Settings` của workflow).

2. **Áp dụng Workflow ID vào node `HTTP Request`**:
   - Mở node `HTTP Request` (node đầu tiên sau Webhook).
   - Trong tab `Request Configuration`:
     - **Method**: `POST`.
     - **URL**: `https://api.nanonets.com/v2/OCR/Process`.
     - **Headers**:
       ```
       Content-Type: application/json
       Authorization: Basic [API Key của bạn]
       ```
     - **Body (JSON)**:
       ```json
       {
         "workflow_id": "[Workflow ID của bạn]",
         "file": "{{ $json.file }}"
       }
       ```
       (Thay `{{ $json.file }}` bằng biến file từ Webhook).

   - Mở node `HTTP Request2` (node tiếp theo):
     - **URL**: `https://api.nanonets.com/v2/OCR/Results`.
     - **Headers**:
       ```
       Authorization: Basic [API Key của bạn]
       ```
     - **Body (JSON)**:
       ```json
       {
         "workflow_id": "{{ $json.workflow_id }}"
       }
       ```

#### **C. Cấu Hình Node `Convert to File`**
- Node này chuyển kết quả JSON thành file Excel.
- **Không cần chỉnh sửa** (n8n sẽ tự động định dạng ra file `.xls`).

#### **D. Cấu Hình Node `Code` (Xử Lý Dữ Liệu)**
- Node `Code` và `Code1` sử dụng **JavaScript** để xử lý dữ liệu từ Nanonets.
- **Không cần chỉnh sửa** (n8n đã cấu hình sẵn logic trích xuất dữ liệu).

#### **E. Cấu Hình Webhook (Nếu Sử Dụng)**
- Nếu muốn nhận file qua **webhook** (thay vì form):
  - Node `Webhook` đã được cấu hình sẵn với `path: "1a03d800-3e91-4284-9323-0609c0974f18"`.
  - **Không cần chỉnh sửa** (n8n sẽ tự động sinh URL webhook).
  - **URL webhook** sẽ có dạng: `https://[tên-domain-n8n]/webhook/1a03d800-3e91-4284-9323-0609c0974f18`.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với File Mẫu**:
   - Tải một file PDF hóa đơn mẫu lên.
   - Gửi file qua **Webhook** (hoặc form nếu sử dụng phương thức này).
   - Kiểm tra kết quả trong node `Convert to File` (file Excel sẽ được tạo).

2. **Bật Active Workflow**:
   - Đảm bảo tất cả node đều **đỏ (active)**.
   - Bật `Active` ở góc trên bên phải.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối với Slack/Telegram để Báo Lỗi**
- Thêm node `Slack` hoặc `Telegram Bot` sau node `HTTP Request2` để **báo lỗi** nếu OCR không thành công.
- Ví dụ:
  ```json
  {
    "operation": "sendMessage",
    "text": "Lỗi khi trích xuất hóa đơn: {{ $json.error }}"
  }
  ```

### **2. Lưu Log Lịch Sử Trích Xuất**
- Thêm node `Google Sheets` hoặc `Airtable` để **lưu lịch sử** các file đã xử lý (tên file, ngày giờ, trạng thái).

### **3. Tự Động Gửi Excel qua Email**
- Sử dụng node `Send Email` (Gmail/SMTP) để **gửi file Excel** cho bộ phận kế toán hàng ngày.

### **4. Cập Nhật Workflow Nanonets**
- Nếu cần **thêm/bỏ field** trong hóa đơn, cập nhật **Workflow ID** trên Nanonets và **re-run** workflow.

---
## 📌 **Kết Luận: Từ Thủ Công Sang Tự Động Trong Vài Phút**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc mòn mỏi nhập liệu hóa đơn, đồng thời **tăng độ chính xác** và **tạo ra dữ liệu sẵn sàng phân tích**. **Chỉ cần 5 phút để cấu hình**, sau đó **hoạt động tự động 24/7**.

**Bắt đầu ngay!**
1. **Import workflow** từ [đây](https://n8n.io/workflows/6194).
2. **Cấu hình credentials** và **Workflow ID** của Nanonets.
3. **Test với file mẫu** và **bật active**.

**🎁 Đăng ký VPS TinoHost để self-host n8n ổn định 24/7:**
👉 [Đăng ký VPS N8N](https://tino.vn/vps-n8n?affid=388) (💰 **Giảm 39%** với mã **VPSN8N**).

---
**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/). 🚀