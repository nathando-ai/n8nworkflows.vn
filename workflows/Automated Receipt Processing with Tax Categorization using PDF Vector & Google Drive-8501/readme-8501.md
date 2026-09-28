---
title: "🚀 Tự Động Xử Lý Hóa Đơn & Phân Loại Thuế Tự Động Với PDF Vector + Google Drive (Không Cần Code)"
description: "Workflow tự động hóa xử lý hóa đơn, trích xuất thông tin chi tiết, phân loại thuế và lưu trữ dữ liệu vào Google Sheets chỉ trong vài phút - giải pháp hoàn hảo cho doanh nghiệp cần quản lý chi phí và tối ưu hóa khai thuế."
slug: "tu-dong-xu-ly-hoa-don-phan-loai-thue"
tags: [n8n, automation, invoice-processing, ai-summarization, pdf-vector, google-drive, google-sheets]
keywords: [tự động hóa hóa đơn, phân loại thuế tự động, trích xuất dữ liệu PDF, n8n workflow, quản lý chi phí doanh nghiệp, OCR hóa đơn]
---

# 🚀 **Tự Động Xử Lý Hóa Đơn & Phân Loại Thuế Tự Động Với PDF Vector + Google Drive**

### **Giải pháp hoàn hảo cho các sếp quản lý chi phí, kế toán và nhân viên hành chính**
Hóa đơn, hóa đơn, hóa đơn... Một ngày làm việc của các sếp thường bắt đầu và kết thúc với việc **quét, nhập liệu, phân loại và tính toán thuế** cho hàng chục hóa đơn. Thời gian và công sức bỏ ra để xử lý thủ công không chỉ làm giảm hiệu suất mà còn dễ gây sai sót trong phân loại thuế, ảnh hưởng trực tiếp đến lợi nhuận cuối cùng của doanh nghiệp.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Trích xuất dữ liệu** từ hóa đơn PDF, ảnh hoặc file Word (ngay cả khi chất lượng kém)
✅ **Phân loại thuế tự động** (đơn hàng, du lịch, thiết bị, ăn uống...)
✅ **Tính toán phần trăm khấu trừ** (ví dụ: 50% cho hóa đơn ăn uống)
✅ **Lưu trữ dữ liệu** vào Google Sheets (sẵn sàng sync với QuickBooks hoặc phần mềm kế toán khác)
✅ **Hoạt động 24/7** mà không cần can thiệp của con người

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tuần** cho bộ phận kế toán và hành chính.
- **Giảm sai sót 90%** trong việc phân loại thuế và trích xuất dữ liệu.
- **Tối ưu hóa khai thuế** với phân loại thuế chính xác và phần trăm khấu trừ tự động.
- **Hoạt động liên tục** (không cần phải làm thủ công vào cuối tháng).
- **Dữ liệu sẵn sàng** để phân tích chi phí và báo cáo cho ban lãnh đạo.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu hóa đơn và trích xuất dữ liệu).
2. **Tài khoản Google Sheets** (để lưu trữ dữ liệu chi phí đã phân loại).
3. **API Key của PDF Vector** (miễn phí, đăng ký tại [pdfvector.com](https://pdfvector.com/)).
4. **Folder Google Drive** chứa hóa đơn (PDF, ảnh hoặc file Word) cần xử lý.
5. **Google Sheets** đã tạo sẵn với các cột: `Merchant`, `Date`, `Items`, `Subtotal`, `Tax Amount`, `Tax Category`, `Deductible Percentage`, `Total`.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow này bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/8501](https://n8n.io/workflows/8501) và import vào n8n Editor.
- **Copy/paste JSON** từ trang trên vào n8n Editor (đường dẫn: `https://n8n.io/workflows/8501` → nút "Copy JSON").

:::note[LƯU Ý]
- Nếu các sếp **self-hosted n8n**, đảm bảo đã cài đặt **node PDF Vector** từ [n8n.io/nodes/n8n-nodes-pdfvector](https://n8n.io/nodes/n8n-nodes-pdfvector).
- Nếu dùng **n8n Cloud**, node PDF Vector đã sẵn sàng.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Google Drive**
1. **Node "Google Drive - Get Receipt"**:
   - **Credentials**: Chọn tài khoản Google Drive đã kết nối.
   - **Folder ID**: Điền ID của folder chứa hóa đơn (có thể lấy từ URL của folder trên Google Drive).
   - **File ID**: Để trống để lấy tất cả file trong folder (hoặc điền ID file cụ thể nếu muốn xử lý file riêng lẻ).

#### **B. Cấu hình PDF Vector**
1. **Node "PDF Vector - Extract Receipt"**:
   - **API Key**: Điền API Key từ tài khoản PDF Vector.
   - **Prompt**: Đã sẵn sàng, không cần chỉnh sửa (nếu muốn tối ưu, các sếp có thể điều chỉnh prompt để phù hợp với loại hóa đơn của doanh nghiệp).

2. **Node "PDF Vector - Tax Categorization"**:
   - **API Key**: Điền cùng API Key như trên.
   - **Prompt**: Đã tối ưu hóa để phân loại thuế, nhưng các sếp có thể chỉnh sửa để thêm/loại bỏ các danh mục thuế cụ thể (ví dụ: thêm "Xe cộ" hoặc "Dịch vụ internet").

#### **C. Cấu hình Google Sheets**
1. **Node "Save to Expense Sheet"**:
   - **Credentials**: Chọn tài khoản Google Sheets đã kết nối.
   - **Sheet Name**: Điền tên sheet muốn lưu dữ liệu (ví dụ: "Expense_Tracker").
   - **Range**: Điền `A1` (nếu muốn ghi từ ô A1) hoặc `Sheet1!A1` (nếu sheet có tên khác).

#### **D. Node "Process Expense Data" (Code)**
- **Mã JavaScript**: Các sếp có thể chỉnh sửa để:
  - **Tính toán tổng chi phí** theo danh mục thuế.
  - **Lọc hóa đơn không phù hợp** (ví dụ: loại bỏ hóa đơn cá nhân).
  - **Thêm cột mới** như `Tax_Deductible_Amount` (tính từ `Total * Deductible Percentage`).

:::note[MẪU MÃ CODE]
```javascript
// Ví dụ: Tính toán phần trăm khấu trừ cho hóa đơn ăn uống
if (node.input.data[0].TaxCategory === "Meals") {
  node.input.data[0].TaxDeductibleAmount = node.input.data[0].Total * 0.5;
} else {
  node.input.data[0].TaxDeductibleAmount = node.input.data[0].Total;
}
return node.input.data;
```
:::

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Manual Trigger** và nhấn "Execute Workflow" để kiểm tra với 1-2 hóa đơn mẫu.
   - Kiểm tra kết quả trong Google Sheets để đảm bảo dữ liệu trích xuất và phân loại chính xác.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active** và đặt **Interval** (ví dụ: kiểm tra folder Google Drive **mỗi giờ**).

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Kết hợp với Slack/Telegram để báo cáo**
- Thêm node **Slack/Telegram** sau "Save to Expense Sheet" để gửi thông báo khi có hóa đơn mới được xử lý.
- **Mẫu thông báo**:
  ```
  📄 Hóa đơn mới được xử lý:
  - **Người bán**: [Merchant Name]
  - **Ngày**: [Date]
  - **Tổng chi phí**: [Total]
  - **Danh mục thuế**: [Tax Category]
  - **Phần trăm khấu trừ**: [Deductible Percentage]%
  ```

### **2. Lưu log hoạt động**
- Thêm node **Google Sheets (Append)** để lưu log hoạt động (thời gian xử lý, file ID, trạng thái thành công/thất bại).

### **3. Tích hợp với QuickBooks**
- Sau khi dữ liệu được lưu vào Google Sheets, các sếp có thể sử dụng **n8n QuickBooks node** để tự động sync vào phần mềm kế toán.

### **4. Tối ưu hóa prompt cho PDF Vector**
- Nếu hóa đơn của doanh nghiệp có **cấu trúc đặc biệt**, các sếp có thể chỉnh sửa prompt để:
  - **Trích xuất thông tin cụ thể** (ví dụ: chỉ lấy mã số thuế của người bán).
  - **Loại bỏ dữ liệu không cần thiết** (ví dụ: bỏ qua phần "Điều khoản thanh toán").

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa hoàn toàn quy trình xử lý hóa đơn và phân loại thuế**, tiết kiệm thời gian và giảm sai sót. Với **PDF Vector** và **Google Drive**, các sếp không cần viết một dòng code nào cả, chỉ cần cấu hình và chạy 24/7.

**Hành động ngay hôm nay:**
1. **Đăng ký API Key PDF Vector** (miễn phí) tại [pdfvector.com](https://pdfvector.com/).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để nó làm việc cho doanh nghiệp!

👉 **Nếu cần hỗ trợ**, các sếp có thể tham gia **community n8n** hoặc liên hệ với PDF Vector qua [support@pdfvector.com](mailto:support@pdfvector.com).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::