---
title: "📊 Tự Động Hóa Báo Cáo Doanh Thu Tháng Từ Square Sang Email Gmail - Không Cần Code"
description: "Workflow tự động hóa lấy dữ liệu bán hàng từ Square, tổng hợp báo cáo tháng trước dưới dạng CSV và gửi tự động qua email Gmail cho bộ phận tài chính/quản lý. Giúp tiết kiệm thời gian lên đến 10 giờ/Tháng và giảm thiểu lỗi nhân sự."
slug: "tieu-dong-hoa-bao-cao-sales-square-sang-email"
tags: [n8n, automation, square-api, gmail, sales-report, no-code, finance-automation]
keywords: [tự động hóa báo cáo Square, gửi báo cáo doanh thu tháng qua email, n8n workflow sales, tự động hóa tài chính, báo cáo bán hàng tự động]
---

# 🚀 **Tự Động Hóa Báo Cáo Doanh Thu Tháng Từ Square Sang Email Gmail**

### **Giải Phóng Thời Gian Cho Bộ Phận Tài Chính & Quản Lý**
Hàng tháng, các sếp phải mất **tối thiểu 5-10 giờ** để thủ công:
- Lấy dữ liệu bán hàng từ **Square Dashboard**.
- Tổng hợp số liệu theo từng cửa hàng.
- Chuyển đổi thành báo cáo CSV.
- Gửi qua email cho bộ phận tài chính, quản lý hoặc bên thứ ba.

**Workflow này tự động hóa toàn bộ quy trình trong 1 giây!** Nó kết nối với **Square API**, lấy dữ liệu bán hàng tháng trước, tổng hợp thành báo cáo chuẩn với **Square Sales Summary**, chuyển thành file CSV và gửi tự động qua **Gmail** vào ngày đầu tháng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10 giờ/Tháng** cho bộ phận tài chính (giá trị ~500k-1M/tháng nếu tính lương nhân viên).
- **Chính xác 100%** – Dữ liệu trùng khớp với **Square Dashboard**, không sai sót như khi copy thủ công.
- **Hoạt động tự động 24/7** – Không cần nhắc nhở, báo cáo được gửi đúng giờ vào ngày đầu tháng.
- **Cá nhân hóa** – Chỉ cần thay đổi email nhận, workflow vẫn hoạt động.
- **Dễ dàng mở rộng** – Thêm logic như gửi báo cáo cho nhiều người, lưu log, hoặc kết nối với Slack/Telegram.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Square API Key** (Header Auth):
   - Đăng ký tại [Square Developer Dashboard](https://developer.squareup.com/dashboard/) và lấy **Access Token**.
   - Cấu hình trong n8n như sau:
     - **Credentials > Create New > Header Auth**
     - **Name**: `Authorization`
     - **Value**: `Bearer <your-square-access-token>`
2. **Tài Khoản Gmail** (OAuth2):
   - Cấu hình trong n8n như sau:
     - **Credentials > Create New > Gmail OAuth2**
     - Chọn email muốn gửi báo cáo.
3. **Danh sách email nhận** (cần điền trong node **Send Report**).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7090](https://n8n.io/workflows/7090) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7090) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **9 node** chính, các sếp cần chú ý cấu hình sau:

##### **A. Node "Get Dates From Last Month" (Code)**
- **Lưu ý**: Node này tính ngày tháng trước của tháng hiện tại.
  - **Cách kiểm tra**: Vào node này, chạy **Test Run** với ngày tháng hiện tại để đảm bảo logic đúng.
  - **Sửa đổi nếu cần**: Nếu muốn lấy dữ liệu từ tháng khác (ví dụ: 2 tháng trước), chỉnh sửa code trong node này:
    ```javascript
    // Ví dụ: Lấy dữ liệu từ 2 tháng trước
    const date = new Date();
    date.setMonth(date.getMonth() - 2); // Thay -2 để lấy tháng trước đó
    const startDate = date.toISOString().split('T')[0];
    const endDate = new Date(date.getFullYear(), date.getMonth() + 1, 1).toISOString().split('T')[0];
    return [{ startDate, endDate }];
    ```

##### **B. Node "Get Square Locations" (HTTP Request)**
- **Credentials**: Chọn **Square Header Auth** (đã cấu hình ở trên).
- **URL**: Để mặc định (Square API endpoint cho locations).
- **Headers**: Đảm bảo có header `Authorization: Bearer <your-token>`.

##### **C. Node "Get Sales from Square" (HTTP Request)**
- **Credentials**: Chọn **Square Header Auth** (giống node trên).
- **URL**: Cần thay đổi để lấy orders cho từng location:
  ```
  https://connect.squareup.com/v2/locations/{location-id}/transactions
  ```
  - **Lưu ý**: Node này sẽ chạy **loop** cho từng location (do node `splitOut`), nên không cần thay đổi URL trong node này.

##### **D. Node "Compile Sales Reports" (Code)**
- **Lưu ý**: Node này tổng hợp dữ liệu bán hàng thành báo cáo chuẩn với Square.
  - **Kiểm tra**: Chạy **Test Run** và mở node này để xem output. Đảm bảo số liệu trùng khớp với **Square Dashboard > Reports > Sales Summary**.
  - **Sửa đổi nếu cần**: Nếu muốn thêm cột mới (ví dụ: % tăng trưởng so với tháng trước), chỉnh sửa code trong node này.

##### **E. Node "Send Report" (Gmail)**
- **Credentials**: Chọn **Gmail OAuth2** (đã cấu hình).
- **Email To**: Điền địa chỉ email của người nhận (ví dụ: `finance@company.com`).
- **Subject**: Để mặc định hoặc thay đổi thành `"Báo Cáo Doanh Thu Tháng [Tháng/Năm]"`.
- **Body**: Nội dung email có thể chỉnh sửa để thêm thông tin như:
  ```html
  <p>Xin chào,</p>
  <p>Dưới đây là báo cáo doanh thu tháng trước của tất cả cửa hàng Square:</p>
  <p><a href="attachment://sales_report.csv">Tải báo cáo CSV</a></p>
  <p>Trân trọng,</p>
  <p>n8n Automation</p>
  ```
  - **Lưu ý**: Nếu muốn **xóa n8n attribution**, chỉnh sửa phần cuối của body email.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy workflow với **Test Run** để đảm bảo tất cả node hoạt động.
- **Bật Active**: Đặt workflow thành **Active** và chọn **Schedule Trigger** để chạy vào **ngày 1 tháng** lúc **8:00 AM**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC TỐC ĐỘNG THÊM]
1. **Gửi báo cáo cho nhiều người**:
   - Thay vì gửi email cho 1 người, sử dụng node **gmail** với danh sách email trong một file CSV hoặc database.
   - Ví dụ: Tạo một node **splitOut** trước node **gmail** để chia email nhận.

2. **Lưu log báo cáo**:
   - Thêm node **stickyNote** sau node **Send Report** để ghi lại lịch sử gửi báo cáo.
   - Cấu hình node này để lưu vào một **Google Sheet** hoặc **Notion Database**.

3. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **gmail** để thông báo khi báo cáo được gửi thành công.
   - Ví dụ:
     ```json
     {
       "operation": "postMessage",
       "text": "📊 Báo cáo doanh thu tháng trước đã được gửi thành công!",
       "channel": "#finance-alerts"
     }
     ```

4. **Thêm pagination cho dữ liệu lớn**:
   - Nếu một cửa hàng có **trên 1000 đơn hàng/tháng**, node **Get Sales from Square** sẽ bị lỗi.
   - Giải pháp: Sử dụng **Luxon** hoặc **JavaScript** trong node **Get Sales from Square** để phân trang:
     ```javascript
     const { setCredentials } = require('n8n-core');
     const { getPagination } = require('n8n-nodes-base.httpRequest');

     // Thêm logic phân trang
     const response = await $httpRequest('GET', 'https://connect.squareup.com/v2/locations/{location-id}/transactions', {
       headers: { Authorization: `Bearer ${$input.all().credentials.value}` },
       params: {
         limit: 100, // Lấy 100 đơn hàng/lần
         offset: 0   // Bắt đầu từ offset 0
       }
     });
     ```

5. **Tự động gửi báo cáo cho bên thứ ba (ví dụ: chủ nhà, đại lý)**:
   - Thay đổi email trong node **gmail** và thêm **công thức tính commission** trong node **Compile Sales Reports**.
   - Ví dụ: Nếu doanh thu > 100M, tính 5% commission và gửi cho bên thứ ba.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho bộ phận tài chính và quản lý, đồng thời **giảm thiểu lỗi** khi tổng hợp báo cáo thủ công. Với **cấu hình đơn giản** và **không cần code**, các sếp có thể:
✅ **Tiết kiệm 10 giờ/Tháng**.
✅ **Đảm bảo dữ liệu chính xác**.
✅ **Hoạt động tự động 24/7**.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình **Square API Key** + **Gmail OAuth2**.
2. **Test Run** để đảm bảo hoạt động.
3. **Bật Active** và chọn **Schedule Trigger** vào ngày 1 tháng.
4. **Mở rộng** bằng cách thêm Slack/Telegram hoặc log báo cáo.

---
:::note[CHÚ Ý CUỐI CÙNG]
- **N8n Self-hosted** là lựa chọn tốt nhất để workflow chạy ổn định 24/7.
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** (giảm tới 39%).
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
- **Nếu gặp lỗi**, hãy kiểm tra:
  - **Square API Key** có đúng không?
  - **Gmail OAuth2** có được cấp quyền đầy đủ không?
  - **Node "Compile Sales Reports"** có trả về dữ liệu đúng không?
:::