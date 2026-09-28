---
title: "🚀 Tự Động Vô Hiệu Hóa Sản Phẩm Magento 2 Không Bán Sau 1 Năm Với Gmail Xác Nhận (N8n)"
description: "Giải pháp tự động hóa hoàn toàn không cần code để tự động phát hiện và vô hiệu hóa sản phẩm Magento 2 không bán trong 12 tháng, giảm thiểu rác thải catalog và tối ưu hóa trải nghiệm mua sắm. Kết hợp phân tích đơn hàng, xác nhận quản lý và báo cáo tự động."
slug: "tự-dộng-vô-hiệu-hoá-sản-phẩm-magento-2-không-bán-sau-1-năm"
tags: [n8n, Magento 2, automation, ecommerce, inventory-management]
keywords: [tự động hóa Magento 2, vô hiệu hóa sản phẩm không bán, n8n workflow, quản lý kho hàng, tự động hóa bán hàng]
---

# 🚀 **Tự Động Vô Hiệu Hóa Sản phẩm Magento 2 Không Bán Sau 1 Năm Với Gmail Xác Nhận**

## **Nỗi Đau Của Các Sếp: Sản Phẩm "Lên Cây" Chiếm Chỗ Trong Catalog**
Hàng năm, các cửa hàng Magento 2 phải đối mặt với **sản phẩm "lên cây"** – những mặt hàng không bán được trong thời gian dài, nhưng vẫn chiếm chỗ trong catalog, làm giảm hiệu quả SEO, tăng chi phí quản lý và làm mất uy tín với khách hàng. Thường thì các sếp phải:
- **Làm thủ công:** Tải danh sách sản phẩm, kiểm tra đơn hàng, vô hiệu hóa từng sản phẩm một – mất **từ 5-10 giờ/lần**.
- **Rủi ro cao:** Có thể vô hiệu hóa sản phẩm nhầm hoặc bỏ sót, gây mất doanh thu hoặc phản hồi tiêu cực từ khách hàng.
- **Không báo cáo:** Không biết được số lượng sản phẩm bị vô hiệu hóa, không có dữ liệu để tối ưu hóa chiến lược sản phẩm.

**Giải pháp này tự động hóa toàn bộ quy trình** – từ phân tích đơn hàng đến vô hiệu hóa sản phẩm, **với sự xác nhận cuối cùng từ quản lý qua Gmail**, giúp các sếp **tiết kiệm thời gian, giảm sai sót và có báo cáo chi tiết**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo tính ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Tự động hóa quy trình vô hiệu hóa sản phẩm trong **vài phút/năm** thay vì **5-10 giờ/lần**.
✅ **Chính xác 100%:** Không bỏ sót sản phẩm nào và tránh vô hiệu hóa nhầm.
✅ **Xác nhận quản lý:** Quản lý có thể **xem và xác nhận** danh sách sản phẩm trước khi vô hiệu hóa.
✅ **Báo cáo chi tiết:** Nhận email tổng kết số lượng sản phẩm vô hiệu hóa, lý do và thời gian thực hiện.
✅ **Tối ưu hóa catalog:** Loại bỏ sản phẩm không bán, **cải thiện SEO và trải nghiệm khách hàng**.
✅ **Hoạt động liên tục:** Workflow chạy tự động **mỗi năm** (hoặc theo lịch đặt sẵn).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
📌 **Tài khoản Magento 2 API:**
- **API Key** và **Secret Key** từ Magento Admin (`Stores > Configuration > Advanced > Web Services > REST`).
- **Endpoint API** của Magento (thường là `https://tên-domain.com/rest`).

📌 **Tài khoản Gmail:**
- **Tài khoản quản lý** (cần có quyền gửi và nhận email trong hệ thống).
- **Mã OAuth 2.0** của Gmail (cài đặt trong [Google Cloud Console](https://console.cloud.google.com/)).

📌 **Thiết lập n8n:**
- **Self-hosted n8n** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
- **Node `httpRequest`** được cấu hình với **header `Authorization: Bearer {API_KEY}`** cho Magento.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/6501](https://n8n.io/workflows/6501) (chọn **Download JSON**).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6501) và paste vào **Import Workflow** trong n8n.

#### **Phương pháp 2: Copy/Paste JSON**
- Mở **n8n Editor**, nhấn **Import** > **Paste JSON** và dán toàn bộ mã từ [n8n.io/workflows/6501](https://n8n.io/workflows/6501).

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node "Schedule Trigger" (Đặt lịch chạy)**
- **Thiết lập lịch chạy:** Cần đặt **một lần/năm** (ví dụ: **ngày 1 tháng 1**).
  - Trong **n8n**, mở node này > **Edit** > **Schedule** > Chọn **Cron Expression**:
    ```
    0 0 1 1 *  # Chạy vào ngày 1 tháng 1 hàng năm
    ```
  - **Lưu ý:** Nếu muốn chạy **mỗi tháng**, thay bằng:
    ```
    0 0 1 * *  # Chạy vào ngày 1 của mỗi tháng
    ```

#### **🔹 Node "Fetch Orders since 1 year ago" (Lấy đơn hàng trong 1 năm qua)**
- **Endpoint API Magento:**
  - Cấu hình **URL:** `https://tên-domain.com/rest/V1/orders?searchCriteria[pageSize]=1000`
  - **Headers:**
    ```
    Authorization: Bearer {API_KEY}
    Content-Type: application/json
    ```
  - **Lưu ý:** Nếu Magento có **pagination**, cần thêm tham số `searchCriteria[page]=2` để lấy trang tiếp theo.

#### **🔹 Node "Calculate date an year ago (ISO)" (Tính ngày 1 năm trước)**
- **Code trong node:**
  ```javascript
  const oneYearAgo = new Date();
  oneYearAgo.setFullYear(oneYearAgo.getFullYear() - 1);
  oneYearAgo.setHours(0, 0, 0, 0);
  return { date: oneYearAgo.toISOString() };
  ```
  - **Không cần chỉnh sửa**, nhưng các sếp nên **kiểm tra ngày tháng** để đảm bảo logic đúng.

#### **🔹 Node "Extract Sold SKUs from orders" (Trích xuất SKU đã bán)**
- **Code trong node:**
  ```javascript
  const soldSkus = [];
  $input.all().forEach(order => {
    if (order.items && order.items.length > 0) {
      order.items.forEach(item => {
        if (!soldSkus.includes(item.sku)) {
          soldSkus.push(item.sku);
        }
      });
    }
  });
  return { soldSkus };
  ```
  - **Không cần chỉnh sửa**, nhưng các sếp nên **test với 1-2 đơn hàng** để đảm bảo SKU được trích xuất chính xác.

#### **🔹 Node "Get All Product Skus" (Lấy tất cả SKU sản phẩm)**
- **Endpoint API Magento:**
  - **URL:** `https://tên-domain.com/rest/V1/products?searchCriteria[pageSize]=1000`
  - **Headers:** Giống như node lấy đơn hàng.
  - **Lưu ý:** Nếu có **pagination**, cần thêm logic để lấy tất cả trang.

#### **🔹 Node "Filter products NOT sold in last year" (Lọc sản phẩm không bán trong 1 năm)**
- **Code trong node:**
  ```javascript
  const unsoldSkus = $input.all().filter(product => {
    return !$input.previousOutput.data.soldSkus.includes(product.sku);
  });
  return { unsoldSkus };
  ```
  - **Không cần chỉnh sửa**, nhưng các sếp nên **kiểm tra danh sách** để đảm bảo logic lọc chính xác.

#### **🔹 Node "Gmail User for Approval" (Gửi email xác nhận)**
- **Cấu hình Gmail:**
  - **Tài khoản:** Chọn tài khoản quản lý.
  - **Email nội dung:**
    ```html
    <p>Xin chào,</p>
    <p>Danh sách sản phẩm không bán trong 1 năm qua:</p>
    <ul>
      $input.all().forEach(item => {
        $output.push(`<li>${item.sku} - ${item.name}</li>`);
      });
    </ul>
    <p>Vui lòng xác nhận vô hiệu hóa các sản phẩm này.</p>
    <p>Trân trọng,</p>
    <p>Hệ thống tự động</p>
    ```
  - **Lưu ý:** Các sếp nên **test gửi email** trước để đảm bảo nội dung hiển thị đúng.

#### **🔹 Node "Disable Products" (Vô hiệu hóa sản phẩm)**
- **Endpoint API Magento:**
  - **URL:** `https://tên-domain.com/rest/V1/products/{sku}/status`
  - **Method:** `PUT`
  - **Body (JSON):**
    ```json
    {
      "status": "disabled"
    }
    ```
  - **Headers:** Giống như các node khác.
  - **Lưu ý:** Nếu Magento có **các trường bắt buộc khác**, cần thêm vào body.

#### **🔹 Node "Built Reporting Email" & "Build Decision Email" (Xây dựng email báo cáo)**
- **Code trong node:**
  ```javascript
  // Built Reporting Email
  const reportEmail = {
    subject: "Báo cáo sản phẩm vô hiệu hóa tự động",
    html: `
      <h2>Báo cáo sản phẩm vô hiệu hóa</h2>
      <p>Ngày thực hiện: ${new Date().toLocaleDateString()}</p>
      <p>Số lượng sản phẩm vô hiệu hóa: ${$input.all().length}</p>
      <ul>
        $input.all().forEach(item => {
          $output.push(`<li>${item.sku} - ${item.name}</li>`);
        });
      </ul>
    `
  };
  return reportEmail;
  ```
  - **Không cần chỉnh sửa**, nhưng các sếp nên **kiểm tra email** sau khi chạy để đảm bảo nội dung chính xác.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với dữ liệu mẫu:**
   - Chọn **Run Workflow** và chọn **Test Execution**.
   - **Kiểm tra các node quan trọng:**
     - `Fetch Orders` (đã lấy được đơn hàng không?).
     - `Extract Sold SKUs` (đã trích xuất SKU đúng không?).
     - `Filter Unsold Products` (danh sách sản phẩm không bán có chính xác không?).
     - `Gmail Approval` (email có gửi được không?).

2. **Bật Active Workflow:**
   - Sau khi test thành công, **bật Active** để workflow chạy tự động theo lịch đặt sẵn.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với Slack/Telegram để Báo Lỗi**
- Thêm **node `slack` hoặc `telegram`** sau node `Gmail Approval` để **báo lỗi** nếu email không được xác nhận.
- **Cấu hình:**
  - **Webhook URL** từ Slack/Telegram.
  - **Nội dung thông báo:**
    ```json
    {
      "text": "⚠️ Email xác nhận vô hiệu hóa sản phẩm không bán đã gửi nhưng chưa được trả lời!"
    }
    ```

### **2. Lưu Log Tất Cả Các Thao Tác**
- Thêm **node `stickyNote`** để lưu **log chi tiết** của workflow (ngày chạy, số lượng sản phẩm vô hiệu hóa, SKU, lý do).
- **Cách sử dụng:**
  - Trong node `stickyNote`, chọn **Create New Sticky Note**.
  - **Nội dung:**
    ```json
    {
      "workflow": "Disable Unsold Products",
      "date": "$input.currentDate",
      "products_disabled": $input.all().length,
      "skus": $input.all().map(item => item.sku)
    }
    ```

### **3. Gửi Báo Cáo Định Kỳ (Hàng Tháng)**
- **Sử dụng node `scheduleTrigger`** để chạy **mỗi tháng** và gửi **báo cáo tổng hợp** về số lượng sản phẩm vô hiệu hóa.
- **Cấu hình:**
  - **Cron Expression:** `0 0 1 * *` (ngày 1 của mỗi tháng).
  - **Email nội dung:**
    ```html
    <h2>Báo cáo sản phẩm vô hiệu hóa (Tháng ${currentMonth})</h2>
    <p>Tổng số sản phẩm vô hiệu hóa trong năm: ${totalDisabled}</p>
    <p>Số lượng mới vô hiệu hóa: ${newDisabled}</p>
    <table>
      <tr><th>SKU</th><th>Tên Sản Phẩm</th><th>Ngày Vô Hiệu Hóa</th></tr>
      $input.all().forEach(item => {
        $output.push(`<tr><td>${item.sku}</td><td>${item.name}</td><td>${item.disabledDate}</td></tr>`);
      });
    </table>
    ```

### **4. Tích Hợp Với Google Sheets để Theo Dõi**
- Thêm **node `googleSheets`** để **lưu tất cả dữ liệu vô hiệu hóa** vào một bảng Google Sheets.
- **Cấu hình:**
  - **Sheet Name:** `Magento_Unsold_Products`.
  - **Headers:** `SKU, Product Name, Disabled Date, Reason`.
  - **Data:**
    ```json
    {
      "SKU": $input.item.sku,
      "Product Name": $input.item.name,
      "Disabled Date": "$input.currentDate",
      "Reason": "Không bán trong 1 năm"
    }
    ```

---

## 📌 **K