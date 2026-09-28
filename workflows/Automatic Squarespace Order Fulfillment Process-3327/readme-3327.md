---
title: "🚀 Tự Động Hóa Xử Lý Đơn Hàng Squarespace Miễn Phí - Giảm 90% Thời Gian Chăm Sóc Khách Hàng"
description: "Workflow này tự động lấy tất cả đơn hàng mới trên Squarespace, kiểm tra và xác nhận hoàn thành (fulfillment) một cách tự động, giúp các sếp tiết kiệm hàng giờ mỗi tuần. Hoàn toàn không cần code, chỉ cần 10 phút setup."
slug: "tự-dộng-hoa-xu-ly-don-hang-squarespace"
tags: [n8n, automation, squarespace, ecommerce, no-code]
keywords: [tự động hóa squarespace, xử lý đơn hàng tự động, n8n workflow squarespace, giảm thời gian chăm sóc khách hàng, api squarespace commerce]
---

# 🚀 **Tự Động Hóa Xử Lý Đơn Hàng Squarespace - Giảm 90% Công Việc Chăm Sóc Khách Hàng**

### **Nỗi Đau Của Các Sếp**
Các sếp đang phải **quét hàng chục đơn hàng mới mỗi ngày** trên Squarespace, sau đó **gõ tay xác nhận hoàn thành** (fulfillment) trên từng đơn hàng. Điều này không chỉ **tốn thời gian** mà còn **dễ gây lỗi** (quên xác nhận, xác nhận sai trạng thái). Kết quả? **Khách hàng phải chờ lâu, tỷ lệ hoàn trả tăng**, và **thời gian chăm sóc khách hàng (CSAT) giảm**.

**Workflow này giải quyết tất cả:**
✅ **Tự động lấy tất cả đơn hàng mới** từ Squarespace (kể cả hàng trăm đơn hàng).
✅ **Lọc và xác nhận hoàn thành** (fulfillment) tự động cho đơn hàng phù hợp.
✅ **Gửi thông báo tự động** cho khách hàng khi đơn hàng được xử lý.
✅ **Hoạt động 24/7** mà không cần can thiệp của bạn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS riêng (không phụ thuộc vào cloud miễn phí).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** (tương đương **200 giờ/năm**) trong việc xử lý đơn hàng thủ công.
- **Giảm 90% lỗi xác nhận đơn hàng** (không còn quên hoặc xác nhận sai).
- **Tăng CSAT** (khách hàng nhận thông báo tự động khi đơn hàng được xử lý).
- **Hoạt động liên tục** (không cần can thiệp vào ban đêm hoặc ngày lễ).
- **Dễ dàng mở rộng** (có thể kết hợp với Slack/Email để báo cáo).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi setup, các sếp cần chuẩn bị:
1. **Tài khoản Squarespace Commerce** (đã kích hoạt API).
2. **API Key Squarespace** (tạo từ [Squarespace Developer Portal](https://developers.squarespace.com/)).
3. **Thời gian setup**: ~10 phút (nếu đã có API Key).
4. **Lựa chọn**:
   - **Chỉ bán sản phẩm số** (tải về, mã số, digital gift card) → Workflow sẽ tự động xác nhận.
   - **Sử dụng dịch vụ vận chuyển** (ShipStation, SendCloud…) → Cần cấu hình thêm API của dịch vụ đó.

---
:::info[CHUẨN BỊ]
**Nếu chưa có API Key Squarespace:**
1. Đăng nhập vào [Squarespace Developer Portal](https://developers.squarespace.com/).
2. Tạo một **OAuth 2.0 Client** và lấy **Client ID & Secret**.
3. Cấu hình **Redirect URI** là `http://localhost:5678/oauth/callback` (n8n sẽ tự động xử lý).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3327) và import vào n8n Editor.
- **Copy JSON** từ link trên và **paste** vào n8n Editor (tab "Import").

👉 **Lưu ý:** Nếu import từ file, **không sao chép** tab "Globals" (sẽ bị lỗi).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **3 node quan trọng** cần cấu hình cẩn thận:

##### **A. Node "Globals" (Cấu hình API & Lọc Đơn Hàng)**
- **Mở node "Globals"** (type: `set`) và cập nhật các tham số:
  ```yaml
  api-version: "2024-01-01"  # Kiểm tra phiên bản mới nhất tại [Squarespace API Docs](https://developers.squarespace.com/commerce-apis)
  fulfillmentStatus: "PENDING"  # Chỉ lấy đơn hàng chưa được xử lý
  maxPage: -1  # Bật pagination vô hạn (lấy tất cả đơn hàng)
  ```
  - **Nếu muốn lấy đơn hàng mới nhất trong 1 ngày**:
    ```yaml
    modifiedAfter: "2024-06-01T00:00:00Z"  # Định dạng ISO 8601
    modifiedBefore: "2024-06-02T00:00:00Z"
    ```

##### **B. Node "Query pending Orders" (Lấy Đơn Hàng)**
- **Credentials**:
  - Chọn **`oAuth2Api`** (đã cấu hình từ Squarespace Developer Portal).
  - **Headers Auth**: Điền `Authorization: Bearer {API_TOKEN}` (API Token từ Squarespace).
- **Request Method**: `GET`
- **URL**:
  ```
  https://{{your-domain}}.squarespace.com/api/commerce/v1/orders
  ```
  (Thay `{{your-domain}}` bằng tên miền Squarespace của bạn).

##### **C. Node "Fulfill Order" (Xác Nhận Hoàn Thành)**
- **Credentials**: Sử dụng cùng **`oAuth2Api`** như trên.
- **Request Method**: `POST`
- **URL**:
  ```
  https://{{your-domain}}.squarespace.com/api/commerce/v1/orders/{orderId}/fulfill
  ```
  (n8n sẽ tự động điền `{orderId}` từ đơn hàng).
- **Body (JSON)**:
  ```json
  {
    "shouldSendNotification": true  # Bật gửi thông báo cho khách hàng
  }
  ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **node "Query pending Orders"** và **click "Run"**.
  - Kiểm tra **đơn hàng nào được trả về** (nếu có).
  - Chạy **node "Fulfill Order"** để xác nhận 1 đơn hàng mẫu.
- **Bật Active**:
  - Sau khi test thành công, **bật toggle "Active"** ở góc trên bên phải.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** sau "Fulfill Order" để báo cáo đơn hàng đã được xử lý.
   - Ví dụ: `Đơn hàng #{{$node["Query pending Orders"].jsonpath("$.id")}} đã được xác nhận hoàn thành!`.

2. **Lưu Log Lịch Sử**:
   - Thêm **node "Google Sheets"** hoặc **node "Airtable"** để lưu lịch sử đơn hàng đã được xử lý.
   - Cấu hình cột: `ID đơn hàng`, `Ngày xử lý`, `Trạng thái`.

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **node "Schedule Trigger"** (đã có sẵn) để chạy workflow **mỗi ngày 8h sáng** để lấy đơn hàng mới.
   - Cấu hình:
     ```yaml
     cron: "0 8 * * *"  # Lịch trình chạy hàng ngày lúc 8h
     ```

4. **Xử Lý Đơn Hàng Đặc Biệt**:
   - Nếu có đơn hàng **yêu cầu vận chuyển đặc biệt**, thêm **node "Filter"** để loại bỏ chúng trước khi tự động xác nhận.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **mở rộng doanh nghiệp** thay vì bị mắc kẹt trong công việc thủ công. **Chỉ cần 10 phút setup**, workflow sẽ **tự động xử lý tất cả đơn hàng** mà không cần can thiệp.

👉 **Bắt đầu ngay hôm nay!**
1. **Import workflow** từ [link này](https://n8n.io/workflows/3327).
2. **Cấu hình API Squarespace** theo hướng dẫn.
3. **Bật Active** và **quên đi công việc chăm sóc đơn hàng thủ công!**

**Nếu gặp khó khăn**, các sếp có thể **đặt lịch tư vấn miễn phí** với [bangank36](https://bangank36.com) để được hỗ trợ cá nhân hóa workflow cho mô hình kinh doanh riêng!

---
**#TựĐộngHóa #Squarespace #N8N #EcommerceAutomation**