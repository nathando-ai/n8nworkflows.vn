---
title: "📊 Tự Động Hóa Báo Cáo Tổng Kết Doanh Thu Square: Tiết Kiệm 100% Thời Gian Lấy Dữ Liệu"
description: "Workflow này tự động lấy báo cáo tổng kết doanh thu từ Square API, đồng bộ hóa dữ liệu chính xác theo Dashboard Square, và chuẩn bị sẵn cho báo cáo tự động hàng ngày. Giúp các sếp tiết kiệm thời gian, giảm thiểu sai sót và tích hợp dễ dàng với Google Sheets, Slack, email hay phần mềm kế toán."
slug: "tieu-dong-hoa-bao-cao-doanh-thu-square"
tags: [n8n, automation, crm, square-api, reporting]
keywords: [tự động hóa square, báo cáo doanh thu tự động, n8n workflow square, api square, báo cáo hàng ngày]
---

# 🚀 **Tự Động Hóa Báo Cáo Doanh Thu Square: Lấy Dữ Liệu Tự Động, Báo Cáo Chỉ Với Một Click**

### **Nỗi Đau Của Các Sếp**
Lấy báo cáo doanh thu từ Square thủ công hàng ngày không chỉ tốn thời gian mà còn dễ gây sai sót, đặc biệt khi phải xử lý nhiều cửa hàng hoặc dữ liệu lớn. Các sếp phải:
- **Lặp đi lặp lại** mỗi ngày để lấy dữ liệu từ Square Dashboard.
- **Lo lắng về tính chính xác** khi nhập liệu thủ công.
- **Không tích hợp** được với các công cụ phân tích, email tự động hay phần mềm kế toán.
- **Phải điều chỉnh thủ công** khi muốn lấy báo cáo cho nhiều ngày hoặc thời gian khác nhau.

Workflow này **giải quyết tất cả** bằng cách tự động lấy báo cáo doanh thu từ Square API, tính toán tổng hợp và chuẩn bị sẵn cho các ứng dụng khác như **Google Sheets, Slack, email tự động hay tích hợp với QuickBooks/Xero**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần lấy báo cáo thủ công hàng ngày.
- **Dữ liệu chính xác**: Tính toán tự động, trùng khớp với Dashboard Square.
- **Tích hợp linh hoạt**: Sử dụng làm sub-workflow cho Google Sheets, email, Slack hay phần mềm kế toán.
- **Hoạt động liên tục**: Chạy tự động hàng ngày hoặc theo lịch trình tùy chỉnh.
- **Dễ dàng mở rộng**: Thêm logic tính toán, báo cáo định kỳ hoặc phân tích dữ liệu sâu hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Square API Key**:
   - Đăng ký tại [Square Developer Dashboard](https://developer.squareup.com/) để lấy **Access Token**.
   - Tham khảo hướng dẫn [Square API Authentication](https://developer.squareup.com/docs/connect/overview/authentication).
2. **Credentials trong n8n**:
   - Tạo **Header Auth** trong n8n với tên **"Authorization"** và giá trị là `Bearer <your-square-access-token>`.
   - Hướng dẫn chi tiết ở phần **Cách cấu hình credentials** dưới đây.
3. **Thời gian múi giờ**:
   - Workflow mặc định lấy dữ liệu theo **múi giờ Toronto (-05:00)**. Nếu ở múi giờ khác (ví dụ: Việt Nam +07:00), cần điều chỉnh tham số `start_at` và `end_at` trong node **Get Sales from Square**.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6358](https://n8n.io/workflows/6358) và import vào n8n Editor.
- **Hoặc copy/paste** JSON từ file vào **Import Workflow** trong n8n Dashboard.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần chú ý cấu hình như sau:

##### **A. Node "Get Square Locations" (HTTP Request)**
- **Credentials**: Chọn **Header Auth** đã tạo trước đó (tên: "Authorization").
- **Method**: `GET`
- **URL**: `https://connect.squareup.com/v2/locations`
- **Headers**:
  - `Authorization`: `Bearer <your-square-access-token>`
  - `Square-Version`: `2023-06-01` (hoặc phiên bản mới nhất).

##### **B. Node "Get Sales from Square" (HTTP Request)**
- **Credentials**: Chọn **Header Auth** cùng với node trên.
- **Method**: `GET`
- **URL**: `https://connect.squareup.com/v2/locations/{location-id}/transactions/search`
  - Tham số `{location-id}` sẽ được lấy từ node **Turn Locations Into List**.
- **Query Parameters**:
  - `start_at`: `2024-01-01T00:00:00-05:00` (điều chỉnh theo múi giờ của bạn).
  - `end_at`: `2024-01-01T23:59:59-05:00`.
  - `limit`: `1000` (để lấy tất cả đơn hàng trong ngày).
  - `order`: `created_at DESC`.
- **Headers**:
  - `Authorization`: `Bearer <your-square-access-token>`
  - `Square-Version`: `2023-06-01`.

##### **C. Node "Compile Sales Reports" (Code)**
- **Mã JavaScript mặc định** đã tính toán tổng doanh thu, số đơn hàng và giá trị trung bình.
- **Lưu ý**:
  - Các sếp **không cần chỉnh sửa** mã này trừ khi muốn thêm logic tính toán riêng.
  - Kết quả sẽ trả về một đối tượng JSON với cấu trúc:
    ```json
    {
      "location_id": "123456789",
      "total_sales": 1500000,
      "total_orders": 120,
      "avg_order_value": 12500,
      "date": "2024-01-01"
    }
    ```

##### **D. Node "When Executed by Another Workflow" (ExecuteWorkflowTrigger)**
- **Chức năng**: Workflow này **không chạy độc lập**, mà phải được gọi từ một workflow chính.
- **Cách sử dụng**:
  - Trong workflow chính, thêm node **Execute Workflow** và chọn workflow này.
  - **Điền tham số `report_date`** theo định dạng `YYYY-MM-DD` (ví dụ: `2024-01-01`).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy workflow với một ngày mẫu (ví dụ: `2024-01-01`) để kiểm tra kết quả.
   - Kiểm tra dữ liệu trả về có trùng khớp với Dashboard Square không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Với Google Sheets**:
   - Sau node **Compile Sales Reports**, thêm node **Google Sheets** để ghi dữ liệu vào bảng tính.
   - Cấu hình để tạo một sheet mới hàng ngày hoặc ghi vào sheet đã tồn tại.

2. **Gửi Báo Cáo Đến Slack/Email**:
   - Thêm node **Slack** hoặc **Email** để thông báo kết quả báo cáo.
   - Ví dụ: Gửi báo cáo hàng ngày cho team quản lý.

3. **Lưu Log Dữ Liệu**:
   - Sử dụng node **Database** (MySQL/PostgreSQL) để lưu lịch sử báo cáo.
   - Có thể kết hợp với **n8n Database Node** để quản lý dữ liệu dài hạn.

4. **Tính Toán Chi Tiết Hơn**:
   - Trong node **Code**, các sếp có thể thêm logic tính toán như:
     - Tính tỷ lệ tăng trưởng so với ngày trước.
     - Phân loại doanh thu theo sản phẩm.
     - Tính toán lợi nhuận sau chi phí.

5. **Chạy Theo Lịch Trình**:
   - Sử dụng node **Schedule** trong workflow chính để chạy báo cáo hàng ngày, hàng tuần hoặc hàng tháng.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lấy báo cáo thủ công, đồng thời **tăng cường tính chính xác và tự động hóa** cho quá trình phân tích doanh thu. Bằng cách tích hợp với **Google Sheets, Slack, email hay phần mềm kế toán**, các sếp có thể:
- **Tự động hóa báo cáo hàng ngày** mà không cần can thiệp.
- **Dễ dàng phân tích dữ liệu** qua nhiều thời kỳ.
- **Tích hợp với hệ thống kế toán** để giảm thiểu sai sót trong nhập liệu.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình Square API.
3. **Test run** với một ngày mẫu.
4. **Tích hợp với công cụ của bạn** (Google Sheets, Slack, email...).

👉 **[Tải workflow ngay](https://n8n.io/workflows/6358)** và bắt đầu tự động hóa báo cáo doanh thu Square của mình!