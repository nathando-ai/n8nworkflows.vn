---
title: "📊 **Tự Động Hóa Báo Cáo Doanh Thu Hàng Ngày từ Square qua Gmail (Không Cần Code!)**"
description: "Workflow tự động kết nối API Square để tạo báo cáo tổng hợp doanh thu hàng ngày cho tất cả cửa hàng, chuyển đổi thành file CSV và gửi email tự động cho ban quản lý. Giúp tiết kiệm thời gian, giảm thiểu sai sót và nâng cao hiệu quả quản lý tài chính."
slug: "tieu-dong-hoa-bao-cao-doanh-thu-square-qua-gmail"
tags: [n8n, automation, square-api, gmail, crm, no-code]
keywords: [tự động hóa square, báo cáo doanh thu hàng ngày, n8n workflow, gửi email tự động từ square, api square, tự động hóa quản lý cửa hàng]
---

# 🚀 **Tự Động Hóa Báo Cáo Doanh Thu Hàng Ngày từ Square qua Gmail**

### **Giải quyết vấn đề gì?**
Các sếp quản lý cửa hàng hay doanh nghiệp sử dụng **Square** thường phải mất **giờ đồng hồ** mỗi ngày để:
- Tải xuống báo cáo doanh thu từ **Square Dashboard**.
- Chuyển đổi dữ liệu thành file Excel/CSV.
- Gửi email cho ban quản lý, kế toán hoặc đối tác bên ngoài.

**Workflow này tự động hóa toàn bộ quá trình** chỉ trong **vài phút setup**, giúp các sếp:
✅ **Tiết kiệm 5-10 giờ/tháng** cho công việc thủ công.
✅ **Đảm bảo dữ liệu chính xác** (không sai sót như khi copy-paste).
✅ **Cá nhân hóa báo cáo** cho từng cửa hàng.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Báo cáo doanh thu tự động** cho từng cửa hàng, sắp xếp theo định dạng **CSV** (tương tự Square Dashboard).
- **Gửi email tự động** đến ban quản lý, kế toán hoặc đối tác (ví dụ: chủ nhà, đại lý).
- **Tối ưu hóa quyết định kinh doanh** bằng dữ liệu thời gian thực.
- **Kết nối với QuickBooks/Excel** dễ dàng để nhập sổ sách.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần:
1. **Tài khoản Square** và **Square Access Token** (để kết nối API).
2. **Tài khoản Gmail** (để gửi báo cáo tự động).
3. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).
4. **VPS 2GB+ RAM** (để workflow chạy ổn định 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6460](https://n8n.io/workflows/6460).
- Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6460) và dán vào **"Import from JSON"** trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **8 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Schedule Trigger (Đặt lịch chạy)**
- **Thời gian chạy mặc định:** 8:00 AM hàng ngày (lấy dữ liệu **hôm trước**).
- **Lưu ý:**
  - Đổi thời gian thành **4:00 AM** (nếu muốn lấy dữ liệu **hôm trước** sớm hơn).
  - Chọn **"Every day"** và cấu hình ngày tháng theo ý muốn.

##### **🔹 Node 2 & 4: Get Square Locations & Get Sales from Square (HTTP Request)**
- **Sử dụng credential `httpHeaderAuth`** (đã tạo trước ở bước **Chuẩn bị**).
- **Cấu hình tham số:**
  - **URL:**
    - **Get Square Locations:** `https://connect.squareup.com/v2/locations`
    - **Get Sales from Square:** `https://connect.squareup.com/v2/locations/{location-id}/transactions`
  - **Headers:**
    - `Authorization: Bearer <your-square-access-token>`
    - `Content-Type: application/json`
  - **Query Parameters (cho node Get Sales):**
    - `start_date`: `YYYY-MM-DD` (ngày trước ngày chạy workflow).
    - `end_date`: `YYYY-MM-DD` (ngày trước ngày chạy workflow).
    - `limit`: `1000` (mặc định, có thể tăng nếu có nhiều đơn hàng).

##### **🔹 Node 3: Ignore Locations w/o Sales (If)**
- **Điều kiện:** Bỏ qua các cửa hàng **không có doanh thu** (trống hoặc `null`).
- **Cấu hình:**
  - Chọn **"If"** → **"No sales data"** → **"Skip"**.

##### **🔹 Node 5: Compile Sales Reports (Code)**
- **Mục đích:** Tính tổng doanh thu, số đơn hàng, và các chỉ số khác.
- **Lưu ý:**
  - **Không chỉnh sửa mã** nếu muốn kết quả **tương tự Square Dashboard**.
  - Nếu cần **cá nhân hóa**, các sếp có thể mở node này và sửa logic (ví dụ: thêm cột mới).

##### **🔹 Node 6: Convert Sales Summary to CSV File**
- **Chọn format:** `CSV`.
- **Tên file:** `Square_Sales_Report_YYYY-MM-DD.csv`.
- **Lưu ý:**
  - File sẽ được tạo trong **temporary storage** của n8n.

##### **🔹 Node 7: Send Report (Gmail)**
- **Sử dụng credential `gmailOAuth2`** (đã tạo trước).
- **Cấu hình email:**
  - **Người nhận:** Điền email của ban quản lý/ké toán (ví dụ: `keetoan@doanhnghiep.com`).
  - **Tiêu đề email:** `Báo cáo Doanh Thu Hôm Qua - [Tên Cửa Hàng]`.
  - **Nội dung email:**
    ```html
    <p>Xin chào,</p>
    <p>Dưới đây là báo cáo doanh thu hôm qua cho tất cả cửa hàng:</p>
    <p><a href="[LINK_DOWNLOAD_CSV]">Tải báo cáo CSV</a></p>
    <p>Trân trọng,</p>
    <p>Hệ thống tự động hóa Square</p>
    ```
  - **Lưu ý:**
    - Thay thế `[LINK_DOWNLOAD_CSV]` bằng liên kết **tạm thời** từ n8n (có thể sử dụng **Google Drive** hoặc **Dropbox** để chia sẻ file lâu dài).

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC TỐI ƯU NÂNG CAO]
1. **Thêm Slack/Telegram Notification:**
   - Sử dụng **node Slack** hoặc **Telegram Bot** để thông báo khi báo cáo được gửi thành công.
   - Ví dụ: `"Báo cáo doanh thu đã được gửi cho [email]!"`.

2. **Lưu log vào Google Sheets:**
   - Sử dụng **node Google Sheets** để ghi lại lịch sử báo cáo (ngày, tổng doanh thu, số đơn hàng).

3. **Tự động gửi báo cáo định kỳ cho nhiều người:**
   - Sử dụng **node Split** để chia danh sách email và gửi từng người một.

4. **Tích hợp với QuickBooks:**
   - Sử dụng **node QuickBooks** để nhập dữ liệu tự động vào sổ sách.

5. **Thêm pagination cho nhiều đơn hàng:**
   - Nếu một cửa hàng có **trên 1000 đơn hàng**, cần thêm **pagination** trong API request.
   - Sử dụng **node Loop** để lấy dữ liệu theo trang.
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **đảm bảo dữ liệu chính xác** và **tự động hóa hoàn toàn**. Bằng cách chỉ **cấu hình 1 lần**, các sếp sẽ nhận được **báo cáo doanh thu hàng ngày** được gửi tự động vào email mỗi sáng.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho công việc quản lý!**
Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với **n8n Community** tại [n8n.io/community](https://n8n.io/community).

---
**🔹 [Xem workflow gốc](https://n8n.io/workflows/6460) | 🔹 [Tải file JSON](https://n8n.io/workflows/6460/download)**