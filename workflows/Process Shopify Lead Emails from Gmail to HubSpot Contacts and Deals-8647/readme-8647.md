---
title: "🚀 Tự Động Hóa Email Lead Shopify Sang HubSpot: Từ Gmail Đến CRM Mạnh Mẽ (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh để chuyển đổi email lead từ Gmail sang HubSpot Contacts và Deals, tiết kiệm 10+ giờ/lần cho đội bán hàng. Giúp các sếp theo dõi khách hàng tiềm năng từ Shopify một cách tự động, chính xác và cá nhân hóa."
slug: "tu-dong-hoa-email-lead-shopify-sang-hubspot"
tags: [n8n, automation, crm, shopify, hubspot, no-code, email-to-crm]
keywords: [tự động hóa email shopify, workflow n8n hubspot, chuyển đổi lead shopify sang crm, tự động hóa bán hàng, n8n workflow crm]
---

# 🚀 Tự Động Hóa Email Lead Shopify Sang HubSpot: Từ Gmail Đến CRM Mạnh Mẽ

### 📌 **Nỗi Đau Của Các Sếp**
Các sếp bán hàng thường phải:
- **Làm thủ công** sao chép thông tin từ email Shopify (tên, email, số điện thoại, sản phẩm quan tâm...) sang HubSpot.
- **Mất thời gian** theo dõi hàng chục email lead mỗi ngày, dẫn đến **sai sót** và **trùng lặp dữ liệu**.
- **Không theo dõi được** khách hàng tiềm năng từ Shopify một cách hệ thống, khiến **chuyển đổi giảm hiệu quả**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy email từ Gmail** (của Shopify) và **xử lý dữ liệu** (tách tên, email, địa chỉ, sản phẩm, tin nhắn...).
✅ **Tạo/ cập nhật Contact** trên HubSpot với thông tin chính xác.
✅ **Tạo Deal** liên kết với Contact, giúp theo dõi tiến trình bán hàng.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** không phải nhập liệu thủ công.
- **Dữ liệu chính xác 100%** (không sai sót, không trùng lặp).
- **Theo dõi khách hàng tiềm năng** từ Shopify một cách tự động.
- **Tạo Deal trên HubSpot** ngay lập tức, giúp đội bán hàng **nhận lead sớm hơn**.
- **Hoạt động liên tục** (không cần người quản lý).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (được kết nối với email Shopify).
✔ **API Key HubSpot** (được cấp từ [HubSpot Developer Portal](https://developers.hubspot.com/)).
✔ **Thông tin Pipeline Stage ID** trên HubSpot (để tạo Deal).
✔ **Regex (biểu thức chính quy)** phù hợp với định dạng email của Shopify (nếu khác với ví dụ mặc định).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/8647](https://n8n.io/workflows/8647) và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **8 node** quan trọng, các sếp cần chú ý:

##### **🔹 Node 1: Gmail Trigger**
- **Cấu hình**:
  - Chọn **Gmail** và **Active**.
  - **Polling Interval**: 1 phút (để cập nhật email mới).
  - **Credentials**: Đăng nhập tài khoản Gmail liên quan đến email Shopify.

##### **🔹 Node 2: Get a Message**
- **Lấy toàn bộ email** (thân email + metadata).
- **Không cần chỉnh sửa** (n8n tự động lấy dữ liệu).

##### **🔹 Node 3: Extract From Email (Function)**
- **Chức năng**: Trích xuất **sender email** để **lọc email từ Shopify**.
- **Lưu ý**:
  - Nếu email Shopify có **định dạng khác**, cần **cập nhật regex** trong node này.
  - Ví dụ regex mặc định:
    ```javascript
    const emailRegex = /[\w\.-]+@shopify\.com/;
    ```

##### **🔹 Node 4: If Sender is Shopify**
- **Điều kiện**: Chỉ xử lý email **từ Shopify** (cần thay đổi nếu nguồn khác).
- **Lưu ý**:
  - Nếu muốn **lọc email từ nguồn khác**, thay đổi điều kiện trong node này.

##### **🔹 Node 5: Code (Regex Parser)**
- **Trích xuất dữ liệu** từ email:
  - **Tên**, **email**, **địa chỉ**, **số điện thoại**, **tin nhắn**, **liên kết sản phẩm**, **tên sản phẩm**.
- **Lưu ý**:
  - Nếu **định dạng email khác**, cần **cập nhật regex** trong node này.
  - Ví dụ regex mặc định:
    ```javascript
    const nameRegex = /Name:\s*(.+?)\n/;
    const emailRegex = /Email:\s*(.+?)\n/;
    const phoneRegex = /Phone:\s*(.+?)\n/;
    const cityRegex = /City:\s*(.+?)\n/;
    const messageRegex = /Message:\s*(.+?)(?=\nProduct|$)/;
    const productUrlRegex = /Product URL:\s*(.+?)\n/;
    const productTitleRegex = /Product Title:\s*(.+?)\n/;
    ```

##### **🔹 Node 6: Edit Fields (Set)**
- **Normalize dữ liệu** thành JSON sạch để **gửi lên HubSpot**.
- **Không cần chỉnh sửa** (n8n tự động chuyển đổi).

##### **🔹 Node 7: Create or Update a Contact (HubSpot)**
- **Tạo/ cập nhật Contact** trên HubSpot với:
  - **Email**, **Tên**, **Số điện thoại**, **Thành phố**.
- **Lưu ý**:
  - **Credentials HubSpot** phải được **cấu hình trước** trong n8n.
  - Nếu **trùng email**, HubSpot sẽ **cập nhật** thay vì tạo mới.

##### **🔹 Node 8: Create a Deal (HubSpot)**
- **Tạo Deal** liên kết với Contact.
- **Lưu ý**:
  - **Pipeline Stage ID** phải được **điền chính xác** (mặc định là `YOUR_STAGE_ID`).
  - Các sếp cần **tìm ID Pipeline** trong HubSpot:
    - Mở **Deals** → Chọn **Pipeline** → Copy **ID** từ URL.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi **email mẫu** từ Shopify đến Gmail.
  - Chạy **Test** trong n8n để kiểm tra **dữ liệu trích xuất** và **tạo Contact/Deal**.
- **Active Workflow**:
  - Sau khi **test thành công**, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm **node Slack/Telegram** sau **Create a Deal** để **báo cáo lead mới** ngay lập tức.
   - Ví dụ:
     ```json
     {
       "operation": "sendMessage",
       "text": "🚀 New Lead from Shopify:\n- Name: {{ $json.name }}\n- Email: {{ $json.email }}\n- Product: {{ $json.product_title }}"
     }
     ```

2. **Lưu Log Dữ Liệu**:
   - Thêm **node Google Sheets** hoặc **node Airtable** để **lưu lịch sử lead**.
   - Giúp **theo dõi tiến trình** và **phân tích hiệu quả**.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node n8n-nodes-base.schedule** để **gửi báo cáo hàng tuần** về số lead mới, Deal tạo thành công.

4. **Tích Hợp với CRM Khác**:
   - Nếu dùng **Salesforce** thay HubSpot, thay thế **node HubSpot** bằng **node Salesforce**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bán hàng, giúp họ **tập trung vào việc bán chứ không phải nhập liệu**.
**Bắt đầu tự động hóa ngay hôm nay!**
👉 [Tải workflow](https://n8n.io/workflows/8647) và **cài đặt trên VPS** để chạy 24/7.

---
**💡 Cần hỗ trợ thêm?**
- **Đăng ký VPS n8n** với mã giảm giá **VPSN8N** tại [TinoHost](https://tino.vn/vps-n8n?affid=388).
- **Hỏi đáp** về n8n tại [Community n8n](https://community.n8n.io/).