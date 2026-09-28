---
title: "📦 **Hệ Thống Tự Động Hóa Quản Lý Kho Tài Nguyên Nguyên Vật Liệu (N8n + Google Sheets + Supabase + Email)**"
description: "Giải pháp tự động hóa 100% không code để quản lý nhập kho, phát hành nguyên vật liệu, cập nhật tồn kho thời gian thực và cảnh báo tồn kho thấp. Giúp các sếp tiết kiệm 10+ giờ/tuần, giảm sai sót và tối ưu hóa chuỗi cung ứng."
slug: "tieu-dung-quan-ly-kho-tai-nguyen-nguyen-vat-lieu-n8n"
tags: [n8n, automation, inventory-management, google-sheets, supabase, email-integration]
keywords: [tự động hóa quản lý kho, n8n workflow nguyên vật liệu, quản lý tồn kho tự động, cảnh báo tồn kho thấp, tự động hóa phát hành nguyên vật liệu]
---

# 🚀 **Tự Động Hóa Quản Lý Kho Tài Nguyên Nguyên Vật Liệu (N8n + Google Sheets + Supabase + Email)**

## **🔍 Nỗi Đau Của Các Sếp Và Giải Pháp Của N8n**
Quản lý kho nguyên vật liệu thủ công không chỉ tốn thời gian mà còn dễ gây ra những sai sót nguy hiểm:
- **Nhập liệu sai sót**: Thông tin tồn kho không đồng bộ giữa các bảng Excel và cơ sở dữ liệu.
- **Phát hành nguyên vật liệu chậm**: Quá trình xin phê duyệt thủ công kéo dài, ảnh hưởng đến sản xuất.
- **Cảnh báo tồn kho muộn**: Mất thời gian để phát hiện và đặt hàng lại nguyên vật liệu, dẫn đến gián đoạn sản xuất.
- **Không theo dõi lịch sử**: Khó tra cứu lịch sử nhập/phát hàng để phân tích và dự báo nhu cầu.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động nhập liệu** khi nhận nguyên vật liệu từ form (Google Form hoặc API).
✅ **Phê duyệt phát hành nguyên vật liệu** qua email với nút Approve/Reject.
✅ **Cập nhật tồn kho thời gian thực** trên cả Google Sheets và Supabase.
✅ **Cảnh báo tồn kho thấp** tự động qua email khi số lượng dưới ngưỡng an toàn.
✅ **Lưu trữ dữ liệu toàn diện** trên Supabase để phân tích và báo cáo.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** cho bộ phận kho và tài chính.
- **Giảm sai sót 90%** nhờ tự động hóa nhập liệu và cập nhật tồn kho.
- **Phê duyệt phát hành nguyên vật liệu chỉ trong vài giây** thay vì ngày.
- **Cảnh báo tồn kho thấp ngay lập tức**, tránh tình trạng thiếu hàng.
- **Dữ liệu đồng bộ** giữa Google Sheets và Supabase, dễ dàng phân tích.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
- **Google Sheets**:
  - Một bảng Google Sheets với các sheet sau:
    - `Raw Materials` (Nhận nguyên vật liệu).
    - `Current Stock` (Tồn kho hiện tại).
    - `Materials Issued` (Phát hành nguyên vật liệu).
  - **Credentials**: Tạo một **Service Account** trong Google Cloud và cấp quyền cho bảng Sheets (quyền `Editor`).
  - [Hướng dẫn tạo Service Account](https://developers.google.com/workspace/guides/create-credentials).

- **Supabase**:
  - Một cơ sở dữ liệu Supabase với các bảng:
    - `raw_materials` (Nhận nguyên vật liệu).
    - `current_stock` (Tồn kho hiện tại).
    - `materials_issued` (Phát hành nguyên vật liệu).
  - **Credentials**: API Key và URL của cơ sở dữ liệu Supabase.
  - [Hướng dẫn tạo Supabase](https://supabase.com/docs/guides/getting-started).

- **Gmail**:
  - Một tài khoản Gmail để gửi email cảnh báo và yêu cầu phê duyệt.
  - **Credentials**: Cấp quyền cho tài khoản này trong Google Workspace (nếu sử dụng G Suite).

#### **2. Webhook URLs**
- Các URL webhook để nhận dữ liệu từ form hoặc ứng dụng bên ngoài:
  - `https://[your-n8n-domain]/webhook/Receive-Raw-Materials-Webhook`
  - `https://[your-n8n-domain]/webhook/Receive-Issue-Request`
  - `https://[your-n8n-domain]/webhook/Get-Approvals`

#### **3. Cấu Hình Email**
- Địa chỉ email của người quản lý kho (để nhận cảnh báo tồn kho thấp).
- Địa chỉ email của người phê duyệt phát hành nguyên vật liệu.

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này có **48 node** và được chia thành **2 flow chính**:
1. **Nhận nguyên vật liệu và cập nhật tồn kho** (Flow 1).
2. **Xin phê duyệt phát hành nguyên vật liệu** (Flow 2).

**Cách import:**
- Tải file JSON từ [n8n.io/workflows/3979](https://n8n.io/workflows/3979).
- Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON.
- Hoặc copy toàn bộ JSON và dán vào **Import Workflow** → **Paste JSON**.

---
#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này phức tạp và có nhiều node cần cấu hình cẩn thận. Dưới đây là **danh sách các node quan trọng** và cách thiết lập:

##### **🔹 Flow 1: Nhận Nguyên Vật Liệu và Cập Nhật Tồn Kho**
| **Node**                          | **Lưu Ý Cần Chỉnh**                                                                 | **Tham Số Cần Điền**                          |
|-----------------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **Receive Raw Materials Webhook** | Cấu hình URL webhook trong Google Form hoặc ứng dụng bên ngoài.                   | `path`: `/Pb-raw-materials`, `httpMethod`: `POST` |
| **Append Raw Materials**          | Chọn sheet `Raw Materials` trong Google Sheets.                                    | `Spreadsheet ID`, `Sheet Name`               |
| **Lookup Existing Stock**         | Chọn sheet `Current Stock` để tra cứu tồn kho hiện tại.                          | `Spreadsheet ID`, `Sheet Name`               |
| **Update Current Stock**          | Cập nhật tồn kho khi nguyên vật liệu mới được nhận.                               | `Spreadsheet ID`, `Sheet Name`               |
| **Send Low Stock Email Alert**    | Điền email của người quản lý kho.                                               | `To`, `Subject`, `HTML Content`              |
| **New Row Current Stock**         | Thêm hàng mới vào `Current Stock` khi nguyên vật liệu mới.                       | `Spreadsheet ID`, `Sheet Name`               |
| **Current Stock Update (Supabase)** | Cập nhật bảng `current_stock` trong Supabase.                                   | `Database URL`, `API Key`, `Table Name`      |

##### **🔹 Flow 2: Xin Phê Duyệt Phát Hành Nguyên Vật Liệu**
| **Node**                          | **Lưu Ý Cần Chỉnh**                                                                 | **Tham Số Cần Điền**                          |
|-----------------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **Receive Issue Request**         | Cấu hình URL webhook trong Google Form hoặc ứng dụng bên ngoài.                   | `path`: `/raw-materials-issue`, `httpMethod`: `POST` |
| **Send Approval Request**         | Gửi email yêu cầu phê duyệt với nút Approve/Reject.                                | `To` (email người phê duyệt), `Subject`, `HTML Content` (có link Approve/Reject) |
| **Get Approvals**                 | Webhook nhận phản hồi Approve/Reject từ email.                                    | `path`: `/approve-issue`                     |
| **Update Stock After Issue**      | Cập nhật tồn kho khi nguyên vật liệu được phát hành.                              | `Spreadsheet ID`, `Sheet Name`               |
| **Send Low Stock Email Alert**    | Gửi cảnh báo tồn kho thấp sau khi phát hành.                                      | `To`, `Subject`, `HTML Content`              |
| **Create Record Issue (Supabase)** | Thêm ghi chú phát hành vào bảng `materials_issued` trong Supabase.               | `Database URL`, `API Key`, `Table Name`      |
| **Materials Issue Table Update**   | Cập nhật trạng thái phát hành trong Supabase.                                      | `Database URL`, `API Key`, `Table Name`      |

---
##### **🔹 Các Node Code (Cần Chỉnh JavaScript)**
Workflow này sử dụng **JavaScript** trong các node `Set` và `Code` để:
- **Standardize Data**: Đảm bảo dữ liệu nhập liệu nhất quán.
- **Calculate Total Price**: Tính tổng giá trị nguyên vật liệu.
- **Validate Quantity Received**: Kiểm tra số lượng nhập liệu là số dương.
- **Prepare Approval**: Kiểm tra tồn kho đủ để phê duyệt phát hành.
- **Verify Approval Data**: Kiểm tra dữ liệu phê duyệt hợp lệ.

**Lưu ý:**
- Mở node `Code` và kiểm tra lại logic nếu có thay đổi yêu cầu.
- Ví dụ: Node `Calculate Total Price` có mã:
  ```javascript
  $input.all().forEach(item => {
    item.totalPrice = item.quantityReceived * item.unitPrice;
  });
  return $input.all();
  ```

---
#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một yêu cầu mẫu đến webhook `Receive Raw Materials Webhook`.
   - Gửi một yêu cầu mẫu đến webhook `Receive Issue Request`.
   - Kiểm tra email cảnh báo tồn kho thấp (nếu tồn kho dưới ngưỡng).

2. **Bật Active**:
   - Chuyển trạng thái workflow từ `Inactive` sang `Active`.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CẢNH BÁO & TIẾP CẬN]
- **Lưu log hoạt động**: Sử dụng node **Sticky Note** để ghi lại lịch sử hoạt động của workflow.
- **Kết hợp với Slack/Telegram**: Thay vì email, gửi cảnh báo tồn kho qua Slack hoặc Telegram bằng node `Slack` hoặc `Telegram Bot`.
- **Báo cáo định kỳ**: Tạo một workflow riêng để gửi báo cáo tồn kho hàng tuần qua email.
- **Tự động đặt hàng lại**: Khi tồn kho dưới ngưỡng, tự động gửi yêu cầu đặt hàng đến nhà cung cấp.
- **Duy trì dữ liệu an toàn**: Sử dụng **Supabase** để lưu trữ dữ liệu lâu dài và dễ dàng backup.
:::

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa quản lý kho nguyên vật liệu, giúp các sếp:
✔ **Tiết kiệm thời gian** và giảm sai sót.
✔ **Quản lý tồn kho hiệu quả** với cảnh báo tự động.
✔ **Phê duyệt phát hành nhanh chóng** qua email.
✔ **Dễ dàng phân tích dữ liệu** nhờ Supabase.

**🎯 Hành động ngay:**
1. **Cài đặt n8n trên VPS** để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test với dữ liệu mẫu** trước khi chuyển sang hoạt động thực tế.

---
:::success[🚀 **BẮT ĐẦU NGÀY HÔM NAY!**]
Nếu các sếp gặp khó khăn trong quá trình cấu hình, hãy liên hệ với cộng đồng n8n hoặc đăng ký hỗ trợ từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để được tư vấn chi tiết!
:::

---
**📌 Ghi chú cuối:**
- Workflow này **không cần code** nhưng yêu cầu cấu hình cẩn thận.
- Đối với các sếp mới với n8n, hãy bắt đầu với **flow đơn giản** (như nhập liệu nguyên vật liệu) trước khi triển khai toàn bộ hệ thống.
- **Backup dữ liệu** thường xuyên để tránh mất mát.