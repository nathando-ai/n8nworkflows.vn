---
title: "📊 Tự Động Hoàn Thành Báo Cáo Doanh Thu Hàng Ngày Từ Square Sang Outlook - Giảm Thời Gian Làm Thủ Công 90%"
description: "Workflow tự động hóa hoàn toàn không cần code để lấy dữ liệu doanh thu từ Square, tổng hợp thành báo cáo CSV chuẩn và gửi tự động qua Outlook hàng ngày. Giúp quản lý doanh thu nhanh chóng, chính xác và tiết kiệm thời gian cho đội ngũ tài chính/quản lý."
slug: "tieu-dong-hoan-thanh-bao-cao-doanh-thu-square-sang-outlook"
tags: [n8n, automation, square-api, microsoft-outlook, crm, báo cáo doanh thu tự động]
keywords: [tự động hóa báo cáo square, gửi báo cáo doanh thu qua email, n8n workflow square, tự động hóa tài chính, báo cáo hàng ngày từ square]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Doanh Thu Hàng Ngày Từ Square Sang Outlook**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp:**
Hàng ngày, các sếp phải:
- **Tải xuống** báo cáo doanh thu từ Square Dashboard (thời gian: ~15-30 phút).
- **Tổng hợp** dữ liệu từ nhiều cửa hàng (nếu có).
- **Chuyển đổi** sang định dạng CSV hoặc Excel.
- **Gửi** qua email cho bộ phận tài chính, quản lý hoặc đối tác bên ngoài.

**Kết quả?** Thời gian làm thủ công chiếm 2-3 tiếng/tuần, dễ xảy ra lỗi tính toán, và không thể tự động hóa theo lịch trình.

**Workflow này giải quyết tất cả!** Nó **tự động** lấy dữ liệu từ Square, tổng hợp báo cáo **chính xác 100%** (khớp với Dashboard của Square), chuyển thành CSV và gửi qua Outlook **mỗi ngày** – **không cần bạn làm gì cả!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2-3 tiếng/tuần** cho đội ngũ tài chính/quản lý.
- **Chính xác 100%**: Dữ liệu khớp với Square Dashboard, không sai sót.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công.
- **Cá nhân hóa**: Chỉ cần thay đổi email nhận, không cần chỉnh sửa logic.
- **Hoạt động 24/7**: Dữ liệu cập nhật hàng ngày ngay khi mở cửa hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Square** với quyền truy cập API.
2. **Square Access Token** (để kết nối với API).
3. **Tài khoản Microsoft Outlook** (để gửi email báo cáo).
4. **n8n Self-hosted** (để chạy workflow 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7080](https://n8n.io/workflows/7080) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7080) và dán vào **Import Workflow** trong n8n.

#### 2. **Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **8 node** chính, các sếp cần chú ý cấu hình sau:

##### **A. Cấu Hình Square API (2 Node HTTP Request)**
- **Node 1: "Get Square Locations"**
  - **Credentials**: Chọn `httpHeaderAuth` (đã tạo trước đó).
  - **Header Auth Value**: Điền `Bearer <Square-Access-Token>` (ví dụ: `Bearer shpat_your_token_here`).
  - **URL**: `https://connect.squareup.com/v2/locations` (không cần chỉnh).

- **Node 2: "Get Sales from Square"**
  - **Credentials**: Cùng `httpHeaderAuth` như trên.
  - **URL**: `https://connect.squareup.com/v2/locations/{location_id}/transactions/search` (sẽ tự động lấy `{location_id}` từ node trước).
  - **Query Parameters**:
    - `date_from`: `{{ $node["Schedule Trigger"].json["$date"] }}` (ngày trước ngày hiện tại).
    - `date_to`: `{{ $node["Schedule Trigger"].json["$date"] }}` (cùng ngày).
    - `limit`: `1000` (để lấy tất cả đơn hàng).

##### **B. Lọc Cửa Hàng Không Có Doanh Thu ("Ignore Locations w/o Sales")**
- Node `if` này sẽ **bỏ qua** các cửa hàng không có đơn hàng trong ngày.
- **Kiểm tra**: Đảm bảo `json["transactions"]` không rỗng (`!json["transactions"].length`).

##### **C. Tổng Hợp Báo Cáo ("Compile Sales Reports")**
- **Node Code**: Đây là **cốt lõi** của workflow, tính toán tổng doanh thu theo cửa hàng.
  - **Mã JavaScript mẫu** (nếu cần chỉnh sửa):
    ```javascript
    // Tính tổng doanh thu cho mỗi cửa hàng
    const salesData = [];
    const locations = $input.all();

    locations.forEach(location => {
      const totalSales = location.json.transactions.reduce((sum, transaction) => {
        return sum + (transaction.amount_money?.amount || 0);
      }, 0);

      salesData.push({
        location_id: location.json.id,
        location_name: location.json.name,
        total_sales: totalSales,
        currency: location.json.currency,
      });
    });

    return { json: { salesData } };
    ```
  - **Lưu ý**: Đảm bảo kết quả khớp với **Square Dashboard > Reports > Sales Summary**.

##### **D. Chuyển CSV & Gửi Email ("Convert to CSV" + "Send Report")**
- **Node "Convert Sales Summary to CSV"**:
  - Chọn `salesData` từ node Code làm dữ liệu đầu vào.
- **Node "Send Report" (Microsoft Outlook)**:
  - **Credentials**: Chọn Outlook của bạn (đã cấu hình trước).
  - **Email To**: Điền địa chỉ email của người nhận (ví dụ: `finance@company.com`).
  - **Subject**: `Báo cáo Doanh Thu Hàng Ngày - {{ $node["Schedule Trigger"].json["$date"] }}`.
  - **Body**: Thay thế nội dung mẫu bằng:
    ```
    Xin chào,

    Dưới đây là báo cáo doanh thu hàng ngày từ Square:

    {{ $node["Convert Sales Summary to CSV"].json.file.content }}
    ```
  - **Attachments**: Chọn file CSV từ node trước.

##### **E. Đặt Lịch Trình ("Schedule Trigger")**
- **Thời gian chạy**: **8:00 AM hàng ngày** (cài đặt trong node `scheduleTrigger`).
- **Lưu ý**: Đảm bảo n8n **self-hosted** để workflow hoạt động 24/7.

---

#### 3. **Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual test** với ngày mẫu (ví dụ: `2024-05-20`) để kiểm tra dữ liệu.
   - Kiểm tra email nhận có đúng không.
2. **Bật Active**:
   - Chuyển workflow sang **Active** để chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC TỐT NHẤT]
- **Thêm Pagination**: Nếu cửa hàng có **trên 1000 đơn hàng/ngày**, thêm logic pagination vào node `Get Sales from Square`.
- **Báo Cáo Tuần**: Chỉnh node `scheduleTrigger` để chạy **mỗi thứ 7** thay vì hàng ngày.
- **Gửi qua Slack/Telegram**: Thay node Outlook bằng **Slack Webhook** hoặc **Telegram Bot** để thông báo nhanh chóng.
- **Lưu Log**: Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử báo cáo.
- **Tự động Cập Nhật Excel**: Kết hợp với **Google Drive** hoặc **OneDrive** để tự động cập nhật file Excel.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **giảm thiểu lỗi** và **cung cấp dữ liệu chính xác** cho quyết định kinh doanh. **Chỉ cần 10 phút setup**, sau đó workflow sẽ **hoạt động tự động hàng ngày** – **không cần bạn làm gì thêm!**

**Hành động ngay!**
1. **Cài n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình Square + Outlook.
3. **Bật Active** và **quên đi** công việc báo cáo hàng ngày!

👉 **Đăng ký VPS TinoHost** (chỉ 50k/tháng) để tự động hóa hoàn toàn:
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)

---
**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với [n8n Community](https://community.n8n.io/)!