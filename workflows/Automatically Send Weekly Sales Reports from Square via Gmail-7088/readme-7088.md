---
title: "📊 Tự Động Hóa Báo Cáo Doanh Thu Tuần Hàng Square → Email Gmail (Không Cần Code)"
description: "Workflow tự động hóa lấy dữ liệu doanh thu từ Square API, tổng hợp thành báo cáo CSV và gửi tự động hàng tuần cho bộ phận tài chính/quản lý. Giúp tiết kiệm 10+ giờ/tháng và giảm thiểu sai sót trong báo cáo thủ công."
slug: "tu-dong-hoa-bao-cao-doanh-thu-square-gmail"
tags: [n8n, automation, crm, square-api, gmail, no-code, sales-report]
keywords: [tự động hóa báo cáo square, workflow square api, gửi báo cáo doanh thu tự động, n8n workflow crm, tự động hóa tài chính]
---

# 🚀 **Tự Động Hóa Báo Cáo Doanh Thu Tuần Hàng từ Square → Email Gmail (Không Cần Code)**

### **Giải pháp cho:**
- **Các sếp quản lý cửa hàng Square** phải mất **10+ giờ/tháng** để thủ công lấy báo cáo doanh thu từ Square Dashboard và gửi cho bộ phận tài chính.
- **Bộ phận tài chính** phải chờ đợi và kiểm tra lại dữ liệu, dẫn đến **sai sót và mất thời gian**.
- **Nhân viên bán hàng** không thể theo dõi doanh thu thực tế hàng tuần do báo cáo không kịp thời.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Lấy dữ liệu doanh thu từ Square API** (không cần copy-paste).
✅ **Tổng hợp thành báo cáo CSV** (đúng với giao diện Square Dashboard).
✅ **Gửi tự động hàng tuần** (thứ 2 lúc 8h sáng) qua **Gmail** cho quản lý/tài chính.
✅ **Không cần code** – chỉ cần cấu hình API và email.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho bộ phận tài chính và quản lý.
- **Giảm thiểu sai sót** do con người (dữ liệu tự động lấy từ API chính thức).
- **Báo cáo chính xác** (đúng với giao diện Square Sales Summary).
- **Hoạt động 24/7** – không phụ thuộc vào giờ làm việc.
- **Dễ dàng mở rộng** (thêm Slack/Telegram, lưu log, báo cáo định kỳ).
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Square API Key** (Access Token):
   - Đăng ký tại [Square Developer Dashboard](https://developer.squareup.com/dashboard/).
   - Tạo **Access Token** cho ứng dụng (Scope: `locations`, `orders`).
   - **Cấu hình Header Auth** trong n8n:
     - **Tên Credential:** `Authorization`
     - **Giá trị:** `Bearer <your-square-access-token>`
     *(Ví dụ: `Bearer sq0cph-abc123-xyz456`)*

2. **Tài khoản Gmail** (để gửi báo cáo):
   - **Enable Gmail API** và tạo **OAuth2 Credential** trong n8n.
   - **Cấu hình Gmail OAuth2** trong n8n:
     - **Tên Credential:** `gmailOAuth2`
     - **Email nhận:** Điền địa chỉ email của quản lý/tài chính.

3. **n8n Self-hosted** (không dùng phiên bản miễn phí):
   - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (ổn định 24/7).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7088](https://n8n.io/workflows/7088).
- **Import vào n8n Editor**:
  - Mở **n8n Workflow Editor** → **Import** → Chọn file JSON.
  - **Hoặc copy/paste** JSON vào **Create Workflow** → **Import JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **9 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: "Get Square Locations" (HTTP Request)**
- **Credentials:** Chọn `Authorization` (đã cấu hình Square API Key).
- **Method:** `GET`
- **URL:** `https://connect.squareup.com/v2/locations`
- **Headers:**
  ```json
  {
    "Authorization": "{{$authHeader}}"
  }
  ```
  *(`$authHeader` sẽ tự động lấy từ credential Header Auth).*

##### **🔹 Node 2: "Get Sales from Square" (HTTP Request)**
- **Credentials:** Chọn `Authorization` (Square API Key).
- **Method:** `GET`
- **URL:** `https://connect.squareup.com/v2/locations/{locationId}/orders`
- **Query Parameters:**
  - `limit=1000` (để lấy tất cả đơn hàng).
  - `order_by=created_at` (sắp xếp theo thời gian).
  - **Thêm filter ngày** (xem Node 9: "Get Dates From Last Week").

##### **🔹 Node 3: "Ignore Locations w/o Sales" (If)**
- **Condition:** Kiểm tra `$.length > 0` (bỏ qua location không có đơn hàng).

##### **🔹 Node 4: "Get Dates From Last Week" (Code)**
- **Mã JavaScript:**
  ```javascript
  const startDate = new Date();
  startDate.setDate(startDate.getDate() - 7); // Ngày đầu tuần trước
  const endDate = new Date(startDate);
  endDate.setDate(endDate.getDate() + 6); // Ngày cuối tuần trước

  return {
    start_date: startDate.toISOString().split('T')[0],
    end_date: endDate.toISOString().split('T')[0]
  };
  ```
  *(Node này tự động tính ngày tuần trước để lấy dữ liệu.)*

##### **🔹 Node 5: "Compile Sales Reports" (Code)**
- **Mã JavaScript:**
  ```javascript
  // Tính tổng doanh thu theo location
  const salesByLocation = {};
  $input.all().forEach(order => {
    const locationId = order.location_id;
    const amountMoney = order.amount_money.amount;
    if (!salesByLocation[locationId]) {
      salesByLocation[locationId] = { total: 0, count: 0 };
    }
    salesByLocation[locationId].total += amountMoney;
    salesByLocation[locationId].count += 1;
  });

  return Object.values(salesByLocation).map(location => ({
    location_id: Object.keys(salesByLocation).find(key => salesByLocation[key].total === location.total),
    total_sales: location.total,
    order_count: location.count
  }));
  ```
  *(Node này tổng hợp doanh thu theo location.)*

##### **🔹 Node 6: "Convert Sales Summary to CSV File" (convertToFile)**
- **Format:** `CSV`
- **Headers:**
  ```
  Location ID,Total Sales,Order Count
  ```
- **Data:** Sử dụng kết quả từ Node 5.

##### **🔹 Node 7: "Send Report" (Gmail)**
- **Credentials:** Chọn `gmailOAuth2`.
- **To:** Điền email của quản lý/tài chính.
- **Subject:** `Báo cáo Doanh Thu Tuần ${startDate} - ${endDate}`
- **Body (HTML):**
  ```html
  <p>Xin chào,</p>
  <p>Dưới đây là báo cáo doanh thu tuần trước:</p>
  <p><a href="attachment://sales_report.csv">Tải báo cáo CSV</a></p>
  <p>Trân trọng,</p>
  <p>n8n Automation</p>
  ```
  *(Thay đổi nội dung email theo yêu cầu.)*

##### **🔹 Node 8: "Schedule Trigger" (scheduleTrigger)**
- **Cron Expression:** `0 0 8 * * 1` *(Chạy thứ 2 lúc 8h sáng).*
- **Time Zone:** Chọn theo giờ của doanh nghiệp (ví dụ: `Asia/Ho_Chi_Minh`).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **Manual Trigger** để kiểm tra workflow.
   - Kiểm tra email nhận được có đúng không.
2. **Bật Active workflow**:
   - Chuyển trạng thái từ **Draft** → **Active**.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC TỐC ĐỘNG MỞ RỘNG]
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi báo cáo được gửi.
   - Ví dụ:
     ```json
     {
       "text": `📊 Báo cáo doanh thu tuần ${startDate} - ${endDate} đã được gửi!`
     }
     ```

2. **Lưu Log vào Google Sheets**:
   - Sử dụng node **Google Sheets** để ghi lại lịch sử gửi báo cáo.
   - Cấu hình:
     - **Sheet Name:** `Sales_Reports_Log`
     - **Headers:** `Date,Location,Total Sales,Status`

3. **Gửi Báo Cáo Định Kỳ (Hàng Tháng/Nửa Tháng)**:
   - Thay đổi **Cron Expression** trong `scheduleTrigger`:
     - **Hàng tháng:** `0 0 8 1 *` *(Ngày 1 hàng tháng)*
     - **Hàng quý:** `0 0 8 1 * *` *(Ngày 1 tháng 4, 7, 10)*

4. **Thêm Pagination cho Location > 1000 Đơn Hàng**:
   - Sử dụng node **Code** để xử lý pagination:
     ```javascript
     const orders = $input.all();
     const paginatedOrders = [];
     for (let i = 0; i < orders.length; i += 1000) {
       paginatedOrders.push(orders.slice(i, i + 1000));
     }
     return paginatedOrders;
     ```
     *(Áp dụng cho Node "Get Sales from Square").*

5. **Tùy Chỉnh Thời Gian Lấy Dữ liệu**:
   - Sử dụng **Luxon** trong node **Code** để tính ngày chính xác:
     ```javascript
     const { DateTime } = require('luxon');
     const startDate = DateTime.now().minus({ weeks: 1 }).startOf('week').toISODate();
     const endDate = DateTime.now().minus({ days: 1 }).endOf('week').toISODate();
     return { start_date: startDate, end_date: endDate };
     ```
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý và bộ phận tài chính, đồng thời **giảm thiểu sai sót** trong báo cáo thủ công. **Chỉ cần 10 phút cấu hình**, bạn đã có một hệ thống tự động hóa hoàn chỉnh, hoạt động **24/7** mà không cần code.

**🚀 Hành động ngay:**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy ổn định).
2. **Import workflow** và cấu hình Square API + Gmail.
3. **Bật Active** và để nó làm việc cho bạn!

**💡 Cần hỗ trợ?**
- **Diễn đàn n8n**: [https://community.n8n.io](https://community.n8n.io)
- **TinoHost (VPS n8n)**: [https://tino.vn/vps-n8n](https://tino.vn/vps-n8n) (🎁 Mã giảm giá: **VPSN8N**)

---
**#TựĐộngHóaSquare #N8NWorkflow #SalesReportAutomation**