---
title: "🚀 Tự Động Hóa Quản Lý Kho Hàng & Tạo Đơn Hàng Mua (PO) với Airtable + Email Tự Động – Giảm Thiểu Thiếu Hàng & Tránh Trùng Lặp"
description: "Workflow này tự động kiểm tra hàng tồn kho thấp vào mỗi đêm, tính toán lượng đặt hàng động, loại bỏ đơn hàng trùng lặp và gửi email tự động đến nhà cung cấp. Giúp doanh nghiệp giảm thiểu thiếu hàng, tối ưu hóa quy trình mua hàng và tiết kiệm thời gian quản lý."
slug: "tieu-dong-hoa-quan-ly-kho-hang-voi-airtable"
tags: [n8n, automation, airtable, sendinblue, inventory-management, no-code]
keywords: [n8n workflow quản lý kho, tự động hóa đơn hàng mua, airtable tự động hóa, email tự động nhà cung cấp, quản lý tồn kho không code]
---

# 🚀 **Tự Động Hóa Quản Lý Kho Hàng & Tạo Đơn Hàng Mua (PO) với Airtable + Email Tự Động**

### **Nỗi Đau Của Các Sếp**
Quản lý kho hàng thủ công không chỉ tốn thời gian mà còn dễ gây ra những vấn đề như:
- **Thiếu hàng đột xuất** vì không theo dõi kịp thời lượng tồn kho.
- **Đơn hàng trùng lặp** khi nhiều nhân viên tạo PO cho cùng một sản phẩm.
- **Nhà cung cấp không được thông báo kịp thời**, dẫn đến chậm trễ trong quá trình mua hàng.
- **Sự cố nhân sự** (nhân viên nghỉ, thay đổi) làm gián đoạn quy trình mua hàng.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa **tất cả các bước** từ kiểm tra tồn kho thấp đến gửi email PO cho nhà cung cấp, **không cần viết một dòng code nào**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Giảm thiểu thiếu hàng** với việc tự động phát hiện sản phẩm có tồn kho thấp và tạo đơn hàng mua (PO) kịp thời.
✅ **Tránh trùng lặp đơn hàng** bằng cách kiểm tra và loại bỏ các PO đã tồn tại trước khi tạo mới.
✅ **Tiết kiệm thời gian** (tối thiểu **5-10 giờ/tuần**) vì không cần phải theo dõi thủ công tồn kho và gửi email PO.
✅ **Cá nhân hóa thông báo** với email chi tiết về sản phẩm, lượng đặt hàng và nhà cung cấp.
✅ **Hoạt động liên tục** (24/7) ngay cả khi nhân viên nghỉ hoặc thay đổi.

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airtable** với:
   - **Token API** (để kết nối với n8n).
   - **Bảng dữ liệu** có các trường sau:
     - `Products` (tên sản phẩm, số lượng tồn kho, ngưỡng cảnh báo).
     - `Suppliers` (tên nhà cung cấp, email, số điện thoại).
     - `Purchase Orders (PO)` (trạng thái: *Pending*, *Sent*, *Completed*).
2. **Tài khoản SendInBlue (Brevo)** để gửi email tự động.
3. **Thời gian chạy**: Workflow sẽ chạy **mỗi đêm 12h00** (giá trị mặc định).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5815) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 phần chính**:
#### **Phần 1: Tạo Đơn Hàng Mua (PO) Tự Động**
| Node | Yêu Cầu Cấu Hình |
|------|------------------|
| **Run Every Midnight** | Đặt lịch chạy **0 0 12 * * *** (mỗi đêm 12h00). |
| **Get Products with Low Stock** | Chọn **Airtable Base** và **Table Name** là `Products`. Thiết lập điều kiện tìm kiếm (ví dụ: `stock < reorder_threshold`). |
| **Get Supplier Details** | Chọn **Airtable Base** và **Table Name** là `Suppliers`. Kết nối với trường `product_id` từ bước trước. |
| **Calculate Dynamic Re-order Quantity** | Sử dụng **JavaScript** trong node Code để tính toán:
   ```javascript
   const dailySales = 5; // Giả sử trung bình bán 5 sản phẩm/ngày
   const leadTime = 3;   // Thời gian giao hàng từ nhà cung cấp (ngày)
   const safetyMargin = 0.2; // Hệ số an toàn 20%
   const reorderQuantity = (dailySales * leadTime) * (1 + safetyMargin);
   return { reorderQuantity };
   ``` |
| **Remove Duplicate Product Orders** | Node Code này sẽ **lọc bỏ** các sản phẩm đã có PO trong trạng thái *Pending* hoặc *Sent*. |
| **Create Purchase Records** | Chọn **Airtable Base** và **Table Name** là `Purchase Orders`. Đảm bảo các trường như `product_name`, `supplier_email`, `quantity`, `status` được điền chính xác. |

#### **Phần 2: Gửi Email PO & Cập Nhật Trạng Thái**
| Node | Yêu Cầu Cấu Hình |
|------|------------------|
| **Get Purchase Orders which are Pending** | Chọn **Airtable Base** và **Table Name** là `Purchase Orders`. Lọc theo `status = "Pending"`. |
| **Group Products with Suppliers** | Node Code này sẽ **nhóm sản phẩm** theo nhà cung cấp để gửi email duy nhất cho mỗi nhà cung cấp. |
| **Send PO to Suppliers via Email** | Chọn **SendInBlue Credentials** và cấu hình:
   - **From Email**: Địa chỉ email của doanh nghiệp.
   - **Template**: Sử dụng **HTML Email Template** với nội dung như:
     ```html
     <h2>Purchase Order for {{productName}}</h2>
     <p>Quantity: {{quantity}}</p>
     <p>Total: {{quantity * price}}</p>
     ```
   - **To Email**: Địa chỉ email của nhà cung cấp (được lấy từ Airtable). |
| **Update PO Status to "Sent"** | Chọn **Airtable Base** và **Table Name** là `Purchase Orders`. Cập nhật trường `status` thành `"Sent"` cho các PO đã gửi. |

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Tạo **1 sản phẩm có tồn kho thấp** trong Airtable.
   - Chạy **Manual Trigger** trong n8n Editor để kiểm tra workflow.
   - Kiểm tra **email** và **Airtable** xem PO có được tạo và gửi không.
2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow thành **"Active"**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có PO mới được tạo.
   - Ví dụ: `"New PO created for {{productName}}! Supplier: {{supplierName}}"`.
2. **Lưu Log Lịch Sử**:
   - Sử dụng **Airtable** hoặc **Google Sheets** để lưu lịch sử PO, giúp theo dõi dễ dàng.
3. **Tự Động Gửi Báo Cáo Định Kỳ**:
   - Thêm node **SendInBlue** hoặc **Email** để gửi báo cáo hàng tuần về tình trạng kho hàng.
4. **Cập Nhật Ngưỡng Cảnh Báo**:
   - Sử dụng **Airtable Automation** hoặc **n8n** để tự động điều chỉnh ngưỡng cảnh báo tồn kho dựa trên mùa vụ.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc quản lý kho hàng thủ công, **giảm thiểu rủi ro thiếu hàng** và **tối ưu hóa quy trình mua hàng**. Với **không cần viết code**, các sếp có thể **áp dụng ngay** và bắt đầu tự động hóa ngay từ hôm nay!

👉 **Bắt đầu ngay**: Import workflow, cấu hình và **chỉnh sửa các node quan trọng** như hướng dẫn trên. Nếu có vấn đề, hãy để lại bình luận dưới đây!

---
**#TựĐộngHóa #Airtable #n8n #QuảnLýKho #POAutomation**