---
title: "🚀 Tự Động Kiểm Tra Trạng Thái Nhiều Website & Cảnh Báo Khi Ngắt Kết Nối (Downtime Alerts)"
description: "Workflow tự động hóa 100% không code để theo dõi trạng thái hoạt động của nhiều URL, ghi log vào Google Sheets và gửi cảnh báo email khi website ngắt kết nối. Giúp các sếp tiết kiệm thời gian và đảm bảo uptime cao cho hệ thống."
slug: "tieu-dong-kiem-tra-website-downtime-alerts"
tags: [n8n, automation, website-monitoring, downtime-alerts, google-sheets, gmail]
keywords: [tự động hóa n8n, kiểm tra uptime website, cảnh báo downtime, tự động hóa email, google sheets n8n]
---

# 🚀 **Tự Động Kiểm Tra Trạng Thái Website & Cảnh Báo Khi Ngắt Kết Nối (Downtime Alerts)**

### **🔍 Nỗi Đau Của Các Sếp**
Các sếp thường phải mất thời gian thủ công kiểm tra website hàng ngày để đảm bảo uptime cao, đặc biệt khi quản lý nhiều trang web. Nếu một website ngắt kết nối (downtime), việc phát hiện muộn có thể gây mất doanh thu và ảnh hưởng đến uy tín. **Workflow này tự động hóa toàn bộ quy trình**, giúp các sếp:
- **Kiểm tra trạng thái** của nhiều URL một lúc.
- **Ghi log** kết quả vào Google Sheets.
- **Cảnh báo ngay** qua email khi phát hiện downtime.
- **Tiết kiệm thời gian** và giảm thiểu rủi ro.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần viết code, chỉ cần nhập danh sách URL.
- **Báo cáo chi tiết**: Ghi log trạng thái website vào Google Sheets với thời gian thực.
- **Cảnh báo tức thời**: Nhận email khi website ngắt kết nối.
- **Hoạt động liên tục**: Duy trì uptime cao với kiểm tra định kỳ (ví dụ: hàng giờ).
- **Dễ mở rộng**: Thêm/loại URL hoặc thay đổi lịch kiểm tra một cách đơn giản.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets và Gmail OAuth2).
2. **Danh sách URL** cần kiểm tra (các sếp nhập vào node **"URLs"**).
3. **Thời gian kiểm tra định kỳ** (ví dụ: hàng giờ, hàng ngày).
4. **Email nhận cảnh báo** (được cấu hình trong node **Gmail**).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở [n8n Editor](https://n8n.io/editor).
2. Nhấn **"Import"** và chọn file JSON (hoặc copy/paste JSON vào ô **"Import Workflow"**).
3. Chọn **"Import"** để tải workflow vào hệ thống.

---
#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **12 node** chính, các sếp cần chú ý cấu hình các node sau:

##### **A. Node "URLs" (n8n-nodes-base.set)**
- **Mục đích**: Nhập danh sách URL cần kiểm tra.
- **Cách làm**:
  - Nhấn **"Add Item"** và nhập URL (ví dụ: `https://example.com`).
  - Lặp lại cho tất cả URL cần theo dõi.
  - Lưu ý: **Không bỏ trống** danh sách này, workflow sẽ không hoạt động nếu không có URL.

##### **B. Node "Schedule Trigger" (n8n-nodes-base.scheduleTrigger)**
- **Mục đích**: Xác định lịch kiểm tra (ví dụ: hàng giờ, hàng ngày).
- **Cách làm**:
  - Chọn **"Cron"** và nhập biểu thức thời gian (ví dụ: `0 * * * *` để kiểm tra hàng giờ).
  - Hoặc chọn **"Manual Trigger"** nếu muốn kiểm tra theo yêu cầu.

##### **C. Node "Bucle URLs" (n8n-nodes-base.splitInBatches)**
- **Mục đích**: Chia danh sách URL thành batch để kiểm tra từng URL một.
- **Cách làm**:
  - Thiết lập **"Batch Size"** (ví dụ: 5 URL/lần) để tránh quá tải hệ thống.
  - **Không cần chỉnh sửa** các tham số khác.

##### **D. Node "Request" (n8n-nodes-base.httpRequest)**
- **Mục đích**: Gửi yêu cầu HTTP để kiểm tra trạng thái URL.
- **Cách làm**:
  - **Method**: Chọn **"GET"**.
  - **URL**: Sử dụng biến `{{$node["URLs"].json[0].url}}` để lấy URL từ danh sách.
  - **Headers**: Thêm `Accept: */*` để đảm bảo yêu cầu được xử lý.
  - **Lưu ý**: Node này sẽ trả về **status code** (ví dụ: 200 = hoạt động, 404/500 = ngắt kết nối).

##### **E. Node "Code" (n8n-nodes-base.code)**
- **Mục đích**: Xử lý logic kiểm tra trạng thái (ví dụ: phân loại URL thành "Success" hoặc "Error").
- **Cách làm**:
  - Mở node **"Code"** và thay thế code mặc định bằng:
    ```javascript
    // Kiểm tra status code
    if (json.statusCode >= 200 && json.statusCode < 400) {
      return { json: { status: "Success", url: $input.all()[0].json.url } };
    } else {
      return { json: { status: "Error", url: $input.all()[0].json.url } };
    }
    ```
  - **Lưu ý**: Code này phân loại URL thành **"Success"** (trạng thái tốt) hoặc **"Error"** (ngắt kết nối).

##### **F. Node "Success" & "Error" (n8n-nodes-base.googleSheets)**
- **Mục đích**: Ghi log kết quả vào Google Sheets.
- **Cách làm**:
  1. **Cấu hình OAuth2**:
     - Đăng nhập vào [Google Cloud Console](https://console.cloud.google.com/) và tạo **OAuth 2.0 Client ID**.
     - Trở lại n8n và thêm **credentials** cho Google Sheets (tên: `googleSheetsOAuth2Api`).
  2. **Chọn Sheet**:
     - Chọn **Google Sheet** cần ghi log (tạo mới nếu chưa có).
     - Chọn **tab** (ví dụ: "Monitoring Logs").
     - **Operation**: Chọn **"Append"** để thêm dữ liệu mới.
  3. **Cấu hình cột**:
     - Điền tên cột (ví dụ: `Timestamp`, `URL`, `Status`).
     - **Lưu ý**: Các cột này sẽ tự động được điền từ node **"Code"**.

##### **G. Node "Send a message" (n8n-nodes-base.gmail)**
- **Mục đích**: Gửi email cảnh báo khi phát hiện downtime.
- **Cách làm**:
  1. **Cấu hình OAuth2**:
     - Đăng nhập vào [Google OAuth Consent Screen](https://console.cloud.google.com/apis/credentials) và tạo **OAuth 2.0 Client ID**.
     - Trở lại n8n và thêm **credentials** cho Gmail (tên: `gmailOAuth2`).
  2. **Thiết lập email**:
     - **To**: Nhập email nhận cảnh báo (ví dụ: `sếp@example.com`).
     - **Subject**: `🚨 Cảnh báo: Website ${url} đang ngắt kết nối`.
     - **Body**: Sử dụng template:
       ```plaintext
       Website **{{$node["Error"].json[0].url}}** đang ngắt kết nối (Status: **{{$node["Error"].json[0].status}}**).
       Thời gian phát hiện: **{{$node["Error"].json[0].timestamp}}**.
       ```
  3. **Lưu ý**: Email này sẽ được gửi **chỉ khi** node **"Error"** có dữ liệu.

##### **H. Node "Total" (n8n-nodes-base.summarize)**
- **Mục đích**: Tóm tắt kết quả (ví dụ: số URL hoạt động vs. ngắt kết nối).
- **Cách làm**:
  - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.
  - **Lưu ý**: Node này không ảnh hưởng đến quá trình cảnh báo nhưng hữu ích cho báo cáo.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** để kiểm tra với dữ liệu mẫu.
   - Kiểm tra Google Sheets và email để xác nhận workflow hoạt động.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **"Inactive"** sang **"Active"**.
   - **Lưu ý**: Nếu sử dụng **Schedule Trigger**, workflow sẽ chạy tự động theo lịch đã thiết lập.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Webhook hoặc MCP**:
   - Các sếp có thể thay thế **Manual Trigger** bằng **Webhook** để kích hoạt workflow từ bên ngoài (ví dụ: qua API hoặc ứng dụng khác).
   - **Cách làm**:
     - Thêm node **Webhook** và cấu hình URL nhận request.
     - Kết nối node này với node **"Bucle URLs"**.

2. **Lưu Log Chi Tiết**:
   - Thêm node **Sticky Note** để ghi chú thêm thông tin (ví dụ: lý do downtime, người xử lý).
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.stickyNote` và cấu hình nội dung ghi chú.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **Schedule Trigger** để gửi báo cáo tổng hợp hàng tuần qua email.
   - **Cách làm**:
     - Thêm một **Schedule Trigger** mới với biểu thức `0 0 0 * * 0` (tối thứ 7).
     - Kết nối với node **Gmail** để gửi báo cáo tổng hợp từ Google Sheets.

4. **Kết Hợp Slack/Telegram**:
   - Thay vì email, các sếp có thể gửi cảnh báo qua **Slack** hoặc **Telegram**.
   - **Cách làm**:
     - Thêm node **Slack** hoặc **Telegram** và cấu hình webhook.
     - Kết nối node này với node **"Error"** để gửi thông báo tức thời.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa việc kiểm tra uptime website, giảm thiểu downtime và tiết kiệm thời gian. **Chỉ cần nhập danh sách URL và cấu hình email**, workflow sẽ tự động:
✅ Kiểm tra trạng thái website.
✅ Ghi log vào Google Sheets.
✅ Gửi cảnh báo email khi phát hiện downtime.

**Hãy áp dụng ngay để đảm bảo uptime cao cho hệ thống của các sếp!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/5298)** (n8n Community) | **📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**