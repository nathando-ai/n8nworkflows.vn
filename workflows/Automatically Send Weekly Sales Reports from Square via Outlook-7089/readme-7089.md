---
title: "📊 Tự Động Hoàn Chỉnh Báo Cáo Doanh Thu Tuần Hàng Từ Square Sang Outlook (Không Cần Code)"
description: "Workflow này tự động lấy dữ liệu doanh thu từ Square API, tổng hợp thành báo cáo tuần hàng, chuyển đổi thành file CSV và gửi email tự động qua Outlook cho bộ phận tài chính/quản lý. Giúp tiết kiệm 10+ giờ/lần so với cách thủ công."
slug: "tieu-dong-hoan-chinh-bao-cao-doanh-thu-tu-square-sang-outlook"
tags: [n8n, automation, square-api, microsoft-outlook, crm, no-code]
keywords: [n8n workflow square, tự động hóa báo cáo doanh thu, gửi báo cáo tuần hàng từ square, tự động hóa crm, n8n crm]
---

# 🚀 **Tự Động Hoàn Chỉnh Báo Cáo Doanh Thu Tuần Hàng Từ Square Sang Outlook**

### **Giải quyết vấn đề gì?**
Các sếp đang phải **tốn thời gian hàng giờ** mỗi tuần để:
- Tải xuống báo cáo doanh thu từ **Square Dashboard**.
- Chuyển đổi dữ liệu sang **Excel/CSV**.
- Gửi email cho bộ phận tài chính, quản lý hoặc đối tác bên ngoài.
- **Sai sót** khi nhập liệu thủ công (ví dụ: số liệu không khớp với Square Dashboard).

**Workflow này tự động hóa toàn bộ quy trình** chỉ trong **vài phút setup**, giúp các sếp:
✅ **Tiết kiệm 10+ giờ/lần** so với cách thủ công.
✅ **Đảm bảo dữ liệu chính xác** (khớp 100% với Square Dashboard).
✅ **Gửi báo cáo tự động** vào mỗi thứ Hai sáng (8:00 AM) qua Outlook.
✅ **Cá nhân hóa** cho từng cửa hàng/địa điểm Square.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của n8n.cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công tải báo cáo từ Square mỗi tuần.
- **Dữ liệu chính xác**: Báo cáo khớp 100% với Square Dashboard (không sai sót nhập liệu).
- **Tự động hóa hoàn chỉnh**: Gửi email định kỳ qua Outlook cho quản lý/tài chính.
- **Dễ dàng mở rộng**: Thêm logic (ví dụ: gửi báo cáo cho nhiều người nhận, thêm log, hoặc tích hợp Slack).
- **Chuẩn hóa quy trình**: Giúp bộ phận tài chính/quản lý quyết định nhanh chóng dựa trên dữ liệu chính xác.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Square API Key**:
   - Đăng ký tại [Square Developer Dashboard](https://developer.squareup.com/dashboard/).
   - Lấy **Access Token** (để cấu hình trong n8n dưới dạng **Header Auth**).
2. **Microsoft Outlook Credential**:
   - Tạo tài khoản OAuth trong n8n (để gửi email tự động).
3. **Email nhận báo cáo**:
   - Địa chỉ email của người quản lý/tài chính (cần cấu hình trong node **Microsoft Outlook**).
4. **n8n Self-hosted** (khuyến nghị) hoặc tài khoản **n8n.cloud** (miễn phí cho workflow nhỏ).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Từ file JSON**
- Tải file workflow từ [n8n.io/workflows/7089](https://n8n.io/workflows/7089).
- Trong **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.

**Cách 2: Copy/Paste JSON**
- Copy toàn bộ mã JSON từ [n8n.io/workflows/7089](https://n8n.io/workflows/7089) (ấn **Export** trên canvas).
- Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **9 node chính**, các sếp cần cấu hình kỹ các node sau:

##### **A. Node "Get Square Locations" (HTTP Request)**
- **Credentials**:
  - Chọn **Header Auth** (đã tạo trước ở phần **Yêu cầu cần thiết**).
  - **Header Key**: `Authorization`
  - **Header Value**: `Bearer <your-square-access-token>`
- **URL**: `https://connect.squareup.com/v2/locations`
- **Method**: `GET`

##### **B. Node "Get Sales from Square" (HTTP Request)**
- **Credentials**: Giống node trên (Header Auth Square).
- **URL**: `https://connect.squareup.com/v2/locations/{locationId}/transactions`
- **Query Parameters**:
  - `start_time`: Thời gian bắt đầu tuần trước (cần cấu hình trong node **"Get Dates From Last Week"**).
  - `end_time`: Thời gian kết thúc tuần trước.
  - `limit`: 100 (hoặc tăng lên nếu có nhiều đơn hàng).
- **Method**: `GET`

##### **C. Node "Compile Sales Reports" (Code)**
- **Lưu ý quan trọng**:
  - Node này **tính tổng doanh thu** cho từng cửa hàng.
  - **Không chỉnh sửa mã** nếu không hiểu JavaScript, vì nó đã được tối ưu để khớp với **Square Sales Summary Dashboard**.
  - Nếu muốn thay đổi logic, các sếp cần hiểu rõ cách tính toán của Square.

##### **D. Node "Convert Sales Summary to CSV File" (convertToFile)**
- **File Format**: Chọn **CSV**.
- **Headers**: Đảm bảo các cột (Location Name, Total Sales, etc.) khớp với dữ liệu từ Square.

##### **E. Node "Send Report" (Microsoft Outlook)**
- **Credentials**: Chọn tài khoản Outlook đã cấu hình trước.
- **Email To**: Địa chỉ email của người nhận (ví dụ: `quanly@doanhnghiep.com`).
- **Subject**: Ví dụ: **"Báo cáo Doanh Thu Tuần Hàng - Từ {start_date} Đến {end_date}"**.
- **Body**: Thể hiện nội dung email (có thể thêm logo hoặc thông tin bổ sung).
- **Attachments**: Chọn file CSV từ node **"Convert Sales Summary to CSV File"**.

##### **F. Node "Schedule Trigger" (scheduleTrigger)**
- **Cron Expression**: `0 0 8 * * 1` (chạy vào **thứ Hai lúc 8:00 AM**).
- **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh` cho Việt Nam).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra dữ liệu mẫu.
   - Kiểm tra email nhận được có đúng định dạng CSV không.
2. **Bật Active**:
   - Đảm bảo node **Schedule Trigger** hoạt động.
   - Kiểm tra log trong **n8n Dashboard** để phát hiện lỗi.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Gửi báo cáo cho nhiều người nhận**:
   - Thay vì chỉ gửi cho 1 email, các sếp có thể **split** danh sách email và gửi song song bằng node **Set** hoặc **Loop**.

2. **Thêm log để theo dõi lỗi**:
   - Sử dụng node **Sticky Note** hoặc **Set** để ghi lại thông tin debug (ví dụ: lỗi API, thời gian chạy).

3. **Tích hợp Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi báo cáo được gửi thành công.

4. **Xử lý lỗi khi Square API bị lỗi**:
   - Sử dụng node **Code** để thêm logic retry (ví dụ: nếu API trả về lỗi, workflow sẽ chạy lại sau 5 phút).

5. **Tự động lưu báo cáo vào Google Drive/OneDrive**:
   - Thêm node **Google Drive** hoặc **Microsoft OneDrive** để lưu file CSV vào cloud.

6. **Báo cáo định kỳ khác (ngày, tháng)**:
   - Thay đổi **cron expression** trong node **Schedule Trigger** để chạy theo lịch khác.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc làm thủ công báo cáo tuần hàng, đồng thời **đảm bảo dữ liệu chính xác** và **tự động hóa hoàn chỉnh**. Với chỉ **vài phút setup**, các sếp có thể:
✔ **Tiết kiệm 10+ giờ/lần**.
✔ **Giảm sai sót** khi nhập liệu.
✔ **Cung cấp dữ liệu nhanh chóng** cho quản lý/tài chính.

**Hành động ngay hôm nay**:
1. **Import workflow** từ [n8n.io/workflows/7089](https://n8n.io/workflows/7089).
2. **Cấu hình Square API** và **Outlook**.
3. **Bật Active** và để workflow làm việc cho các sếp!

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để tự động hóa 24/7! 🚀