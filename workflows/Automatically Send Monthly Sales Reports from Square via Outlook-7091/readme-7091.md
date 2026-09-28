---
title: "📊 Tự Động Hóa Báo Cáo Doanh Thu Tháng Từ Square Sang Outlook (Không Cần Code)"
description: "Workflow này tự động lấy dữ liệu bán hàng từ Square, tổng hợp thành báo cáo CSV chuẩn với Dashboard Square, và gửi email định kỳ cho bộ phận tài chính hoặc quản lý. Giúp tiết kiệm thời gian lên đến 10 giờ/tháng và giảm sai sót trong báo cáo thủ công."
slug: "tieu-dong-hoa-bao-cao-sales-square-sang-outlook"
tags: [n8n, automation, square-api, microsoft-outlook, sales-report, no-code]
keywords: [tự động hóa báo cáo doanh thu, square api n8n, gửi báo cáo tháng từ square, workflow n8n cho doanh nghiệp, tự động hóa tài chính]
---

# 🚀 **Tự Động Hóa Báo Cáo Doanh Thu Tháng Từ Square Sang Outlook (Không Cần Code)**

### **Giải pháp hoàn hảo cho các sếp quản lý nhiều cửa hàng Square**
Hãy tưởng tượng: **Bạn không còn phải mất 2-3 tiếng mỗi tháng để thủ công tải báo cáo từ Square, tổng hợp dữ liệu, và gửi email cho bộ phận tài chính hay quản lý?** Với workflow này, **tất cả đều tự động hóa** – từ lấy dữ liệu từ API Square đến gửi báo cáo CSV chuẩn định kỳ qua Outlook.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 10-15 giờ/tháng cho việc tổng hợp báo cáo thủ công.
- **Chính xác 100%**: Dữ liệu trùng khớp với **Square Dashboard > Reports > Sales Summary**.
- **Tự động hóa hoàn toàn**: Không cần can thiệp, chạy hàng tháng tự động vào ngày 1.
- **Tích hợp Outlook**: Gửi báo cáo CSV định dạng chuyên nghiệp cho bộ phận tài chính.
- **Dễ mở rộng**: Thêm logic như phân trang (pagination) cho dữ liệu lớn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Square API Key**:
   - Đăng ký tại [Square Developer Dashboard](https://developer.squareup.com/dashboard/) và lấy **Access Token**.
   - Cấu hình **Header Auth** trong n8n với định dạng: `Bearer <your-api-key>`.
2. **Microsoft Outlook Credential**:
   - Tạo **OAuth 2.0** trong n8n để kết nối với Outlook.
3. **Email nhận báo cáo**:
   - Địa chỉ email của người quản lý hoặc bộ phận tài chính.
4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7091](https://n8n.io/workflows/7091) và import vào **n8n Editor**.
- **Hoặc copy/paste** JSON từ trang trên vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **9 node** chính, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Schedule Trigger (Định thời gian chạy)**
- **Cấu hình**: Chọn **"First day of every month at 8:00 AM"** (ngày 1 hàng tháng lúc 8h sáng).
- **Lưu ý**: Nếu muốn chạy khác, chỉnh trong **Schedule Trigger** node.

##### **🔹 Node 2 & 3: Get Square Locations & Ignore Locations w/o Sales**
- **Square API Credential**:
  - Trong **HTTP Request** node, chọn **Header Auth** và điền **Authorization** với giá trị `Bearer <your-square-access-token>`.
  - **Endpoint**: `https://connect.squareup.com/v2/locations` (mặc định).
- **Filter locations**:
  - Node **If** sẽ bỏ qua các cửa hàng không có doanh thu. **Không cần chỉnh gì** nếu muốn giữ logic mặc định.

##### **🔹 Node 4: Get Sales from Square**
- **Tham số quan trọng**:
  - **Headers**: Đảm bảo sử dụng **Square API Key** như Node 2.
  - **Query Parameters**:
    - `location_id`: Lấy từ Node 2 (tự động phân tách).
    - `start_date` & `end_date`: **Node Code "Get Dates From Last Month"** sẽ tự động tính toán (không cần chỉnh).
  - **Endpoint**: `https://connect.squareup.com/v2/locations/{location_id}/transactions`.

##### **🔹 Node 5: Compile Sales Reports (Code Node)**
- **Không chỉnh gì** nếu muốn báo cáo trùng khớp với **Square Dashboard**.
- **Nếu cần tùy chỉnh**:
  - Mở **Code Node** và chỉnh logic tính tổng doanh thu theo yêu cầu (ví dụ: thêm thuế, chiết khấu...).
  - **Lưu ý**: Đảm bảo dữ liệu ra trùng khớp với **Sales Summary** của Square.

##### **🔹 Node 6: Convert Sales Summary to CSV File**
- **Format**: CSV (mặc định).
- **Tên file**: `Square_Sales_Report_[Month_Year].csv` (ví dụ: `Square_Sales_Report_January_2024.csv`).
- **Lưu ý**: Nếu muốn đổi tên, chỉnh trong **Convert To File** node.

##### **🔹 Node 7: Send Report (Microsoft Outlook)**
- **Cấu hình Outlook**:
  - Chọn **OAuth 2.0** credential đã tạo trước.
  - **Người nhận**: Điền email của quản lý/finance team.
  - **Tiêu đề email**: Mặc định là **"Monthly Sales Report - [Month Year]"** (có thể chỉnh).
  - **Nội dung email**:
    ```markdown
    Xin chào [Tên người nhận],

    Đính kèm là báo cáo doanh thu tháng [Month] của tất cả cửa hàng Square. Dữ liệu trùng khớp với **Square Dashboard > Reports > Sales Summary**.

    Trân trọng,
    [Tên công ty]
    ```
  - **Đính kèm**: Chọn file CSV từ Node 6.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** và kiểm tra dữ liệu mẫu.
   - Kiểm tra email nhận được có đúng không.
2. **Bật Active**:
   - Chuyển trạng thái workflow sang **Active** để chạy tự động hàng tháng.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** sau Node **Send Report** để thông báo khi gửi thành công.
   - **Cách làm**:
     ```javascript
     // Thêm node Slack/Telegram sau Outlook
     // Message: "📊 Monthly Sales Report sent to [Email]!"
     ```

2. **Lưu Log Dữ liệu**:
   - Thêm **n8n-nodes-base.googleSheets** hoặc **n8n-nodes-base.s3** để lưu bản sao báo cáo vào Google Sheets hoặc AWS S3.
   - **Ưu điểm**: Dễ dàng theo dõi lịch sử và phân tích dài hạn.

3. **Tùy chỉnh Date Range**:
   - Nếu muốn lấy dữ liệu **khác tháng trước** (ví dụ: 3 tháng gần nhất), chỉnh Node **Code "Get Dates From Last Month"** bằng JavaScript:
     ```javascript
     const startDate = new Date();
     startDate.setMonth(startDate.getMonth() - 3); // 3 tháng trước
     const endDate = new Date();
     endDate.setMonth(endDate.getMonth() - 2); // 2 tháng trước
     return { start_date: startDate.toISOString().split('T')[0], end_date: endDate.toISOString().split('T')[0] };
     ```

4. **Phân trang (Pagination) cho dữ liệu lớn**:
   - Nếu một cửa hàng có **trên 1000 đơn hàng/tháng**, thêm logic pagination trong Node **Get Sales from Square**:
     ```javascript
     // Ví dụ: Lấy dữ liệu theo trang (page)
     const pageSize = 100;
     const page = 1;
     const url = `https://connect.squareup.com/v2/locations/${locationId}/transactions?page_size=${pageSize}&page=${page}`;
     ```

5. **Gửi báo cáo cho nhiều người**:
   - Thay vì chỉ gửi cho 1 email, chỉnh Node **Outlook** để gửi **CC** hoặc **BCC**:
     ```json
     "recipients": [
       { "email": "manager@example.com", "type": "to" },
       { "email": "finance@example.com", "type": "cc" }
     ]
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **tăng độ chính xác** của báo cáo, và **tích hợp hoàn hảo** với hệ thống tài chính hiện có. **Chỉ cần 10 phút cấu hình**, bạn đã có một **công cụ tự động hóa mạnh mẽ** để quản lý doanh thu hàng tháng một cách chuyên nghiệp.

👉 **Bắt đầu ngay hôm nay!**
1. **Import workflow** từ [n8n.io/workflows/7091](https://n8n.io/workflows/7091).
2. **Cấu hình Square API + Outlook**.
3. **Bật Active** và **quên đi việc tổng hợp báo cáo thủ công!**

**Nếu có vấn đề**, để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀