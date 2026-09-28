---
title: "💰 Tự Động Gửi Nhắc Nhở Thanh Toán Hóa Đơn Xero Qua Email Outlook - Giảm 90% Thời Gian Theo Dõi"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp theo dõi hóa đơn Xero, gửi nhắc nhở thanh toán tự động qua Outlook cho khách hàng, và ghi lịch sử nhắc nhở trong Xero. Giúp tiết kiệm 5-10 giờ/tháng và giảm tỷ lệ hóa đơn trễ trả."
slug: "tieu-dong-nhac-nho-thanh-toan-xero-outlook"
tags: [n8n, automation, xero, microsoft-outlook, invoice-processing, no-code]
keywords: [tự động hóa hóa đơn xero, nhắc nhở thanh toán tự động, n8n workflow xero outlook, giảm hóa đơn trễ trả, tự động hóa doanh thu]
---

# 🚀 **Tự Động Gửi Nhắc Nhở Thanh Toán Hóa Đơn Xero Qua Email Outlook - Giải Pháp 100% Không Code**

### **Nỗi Đau Của Các Sếp Với Hóa Đơn Trễ Trả**
Hóa đơn trễ trả không chỉ gây mất doanh thu mà còn làm mất uy tín với khách hàng. Thông thường, các sếp phải:
- **Theo dõi thủ công** hàng ngày trên Xero để kiểm tra hóa đơn đã đến hạn.
- **Gửi email nhắc nhở** một cách rời rạc, dễ quên hoặc không đồng bộ.
- **Ghi chép lịch sử** nhắc nhở vào file Excel hoặc ghi nhớ trên giấy, dẫn đến mất mát dữ liệu.
- **Tốn thời gian** từ 5-10 giờ/tháng chỉ để theo dõi và nhắc nhở, thay vì tập trung vào chiến lược kinh doanh.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động hóa 100%** việc theo dõi và nhắc nhở hóa đơn trong vòng 7 ngày.
✅ **Gửi email cá nhân hóa** qua Outlook với nội dung chuyên nghiệp, không quên khách hàng.
✅ **Ghi lịch sử nhắc nhở** vào Xero để dễ theo dõi và báo cáo.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tháng** chỉ để theo dõi hóa đơn và gửi nhắc nhở.
- **Giảm tỷ lệ hóa đơn trễ trả** từ 30% xuống dưới 5% (dựa trên dữ liệu thực tế của các doanh nghiệp áp dụng).
- **Cải thiện trải nghiệm khách hàng** với email nhắc nhở chuyên nghiệp và lịch sử ghi chép rõ ràng.
- **Hoạt động tự động** mà không cần can thiệp, giảm thiểu lỗi người dùng.
- **Dễ dàng mở rộng** với các tính năng như nhắc nhở theo mức độ ưu tiên, gửi qua Slack, hoặc thêm liên kết thanh toán trực tuyến.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Xero** với quyền API (miễn phí cho tất cả người dùng Xero).
2. **Tài khoản Microsoft Outlook** (hoặc Office 365) để gửi email.
3. **Email của khách hàng** đã được cấu hình trong Xero Contacts.
4. **n8n instance** (self-hosted hoặc dùng dịch vụ n8n.cloud) với các credential sau đã cấu hình:
   - **Xero OAuth2** (để lấy dữ liệu hóa đơn).
   - **Microsoft Outlook OAuth2** (để gửi email).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor/) và chọn **Import Workflow**.
2. Chọn file JSON đã tải từ [link gốc](https://n8n.io/workflows/12648) hoặc copy/paste JSON vào ô **Import Workflow**.
3. Nhấn **Import** và workflow sẽ xuất hiện trên canvas.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **7 node chính**, các sếp cần chú ý cấu hình các node sau:

##### **A. Daily Invoice Check Trigger (n8n-nodes-base.scheduleTrigger)**
- **Cấu hình:**
  - Thời gian chạy mặc định là **12:00 PM hàng ngày**.
  - **Lưu ý:** Các sếp có thể điều chỉnh thời gian này để phù hợp với lịch làm việc của doanh nghiệp (ví dụ: 9h sáng hoặc 3h chiều).
  - **Không cần thay đổi** nếu muốn giữ nguyên lịch chạy mặc định.

##### **B. Fetch All Xero Invoices (n8n-nodes-base.xero)**
- **Cấu hình:**
  - Chọn **Operation: getAll** (lấy tất cả hóa đơn).
  - **Credentials:** Chọn credential Xero OAuth2 đã cấu hình trước đó.
  - **Không cần thay đổi** các tham số khác, workflow sẽ tự động lấy dữ liệu.

##### **C. Filter Out Paid Invoices (n8n-nodes-base.if)**
- **Cấu hình:**
  - Điều kiện mặc định là **`$.status === "PAID"`** (loại bỏ hóa đơn đã thanh toán).
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi logic lọc (ví dụ: loại bỏ hóa đơn đã hủy).

##### **D. Filter Invoices Due Soon (n8n-nodes-base.if)**
- **Cấu hình:**
  - Điều kiện mặc định là **`$.dueDate <= new Date().setDate(new Date().getDate() + 7)`** (lọc hóa đơn đến hạn trong 7 ngày).
  - **Lưu ý:** Nếu muốn thay đổi thời gian nhắc nhở (ví dụ: 14 ngày), các sếp cần chỉnh sửa **node Calculate Days Until Due** (xem phần sau).

##### **E. Calculate Days Until Due (n8n-nodes-base.code)**
- **Cấu hình:**
  - Mã JavaScript mặc định:
    ```javascript
    $input.all().map((invoice) => {
      const dueDate = new Date(invoice.dueDate);
      const today = new Date();
      const diffDays = Math.ceil((dueDate - today) / (1000 * 60 * 60 * 24));
      return {
        ...invoice,
        diffDays: diffDays
      };
    });
    ```
  - **Lưu ý:**
    - Thay đổi `diffDays <= 7` thành `diffDays <= 14` (hoặc số ngày khác) để thay đổi ngưỡng nhắc nhở.
    - Ví dụ: Nếu muốn nhắc nhở **14 ngày trước hạn**, thay `7` thành `14`.

##### **F. Log Reminder in Xero History (n8n-nodes-base.httpRequest)**
- **Cấu hình:**
  - **Method:** POST
  - **URL:** `https://api.xero.com/api.xro/2.0/Invoices/{invoiceId}/HistoryEntries`
  - **Headers:**
    - `Authorization: Bearer {Xero_OAuth_Token}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "type": "REMINDER_SENT",
      "description": "Automated reminder sent via n8n",
      "date": "$jsonDateTime_iso"
    }
    ```
  - **Lưu ý:**
    - Thay `{invoiceId}` bằng `$node["Fetch All Xero Invoices"].json[].id` (hoặc biến tương ứng trong workflow).
    - **Không cần chỉnh sửa** nếu đã cấu hình credential Xero OAuth2 đúng.

##### **G. Send a message1 (n8n-nodes-base.microsoftOutlook)**
- **Cấu hình:**
  - **Credentials:** Chọn credential Microsoft Outlook OAuth2 đã cấu hình.
  - **Email Template:**
    - **Subject:** `Nhắc nhở thanh toán hóa đơn #$$.invoiceNumber`
    - **Body (HTML):**
      ```html
      <p>Xin chào <strong>$$.contactDetails.firstName</strong>,</p>
      <p>Hóa đơn <strong>#$$.invoiceNumber</strong> với tổng số tiền <strong>$$.amountDue</strong> sẽ đến hạn vào ngày <strong>$$.dueDate</strong>.</p>
      <p>Vui lòng thanh toán sớm nhất có thể để tránh phí trễ.</p>
      <p>Trân trọng,</p>
      <p>Đội ngũ [Tên Công Ty]</p>
      ```
  - **Lưu ý:**
    - Thay thế `$$.contactDetails.firstName` bằng tên khách hàng từ Xero.
    - Thay thế `$$.amountDue` bằng số tiền còn phải trả (đơn vị tiền tệ).
    - **Không cần chỉnh sửa** các biến khác nếu đã cấu hình credential Outlook đúng.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run Dữ Liệu Mẫu:**
   - Chọn **Execute Workflow** và chọn **Test Execution** để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra email nhắc nhở đã được gửi đến Outlook và lịch sử đã được ghi vào Xero.

2. **Bật Active Workflow:**
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.
   - Workflow sẽ tự động chạy hàng ngày theo lịch đã thiết lập.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thay Đổi Thời Gian Nhắc Nhở:**
   - Mở node **Calculate Days Until Due** và thay đổi `diffDays <= 7` thành `diffDays <= 14` (hoặc số ngày khác) để nhắc nhở sớm hơn hoặc muộn hơn.

2. **Nhắc Nhở Escalating (Tăng Cường):**
   - Thêm **node IF** mới sau **Filter Invoices Due Soon** để phân loại hóa đơn:
     - **Hóa đơn đến hạn trong 3 ngày:** Gửi email nhắc nhở cấp thiết.
     - **Hóa đơn đến hạn trong 7 ngày:** Gửi email nhắc nhở thông thường.
   - **Cách làm:**
     - Thêm node IF mới và cấu hình điều kiện:
       ```javascript
       // Ví dụ: Nhắc nhở cấp thiết nếu diffDays <= 3
       if ($.diffDays <= 3) {
         // Gửi email nhắc nhở cấp thiết
       }
       ```

3. **Thêm Liên Kết Thanh Toán Trực Tuyến:**
   - Sửa email template để bao gồm liên kết thanh toán (nếu khách hàng có thể thanh toán trực tuyến):
     ```html
     <p>Vui lòng thanh toán qua liên kết dưới đây: <a href="$$.paymentLink">Thanh toán ngay</a></p>
     ```
   - **Lưu ý:** Các sếp cần cung cấp `$$.paymentLink` từ Xero hoặc hệ thống thanh toán khác.

4. **Gửi Báo Cáo Định Kỳ:**
   - Thêm node **Google Sheets** hoặc **Slack** để gửi báo cáo tổng hợp hóa đơn đã nhắc nhở hàng tháng.
   - **Cách làm:**
     - Thêm node **Google Sheets** và cấu hình để ghi dữ liệu hóa đơn đã nhắc nhở vào sheet mới.
     - Thêm node **Slack** để thông báo khi có hóa đơn lớn cần theo dõi.

5. **Phân Loại Khách Hàng:**
   - Sử dụng **node IF** để phân loại khách hàng theo tag (ví dụ: khách hàng VIP, khách hàng thường).
   - **Cách làm:**
     - Kiểm tra `$$.contactDetails.tags` và gửi email nhắc nhở khác nhau cho từng nhóm.

---

### 📌 **Kết Luận**
Workflow **Tự Động Gửi Nhắc Nhở Thanh Toán Hóa Đơn Xero Qua Outlook** là giải pháp hoàn hảo để các sếp:
✔ **Tiết kiệm thời gian** và tập trung vào chiến lược kinh doanh.
✔ **Giảm tỷ lệ hóa đơn trễ trả** và cải thiện doanh thu.
✔ **Cải thiện trải nghiệm khách hàng** với email nhắc nhở chuyên nghiệp.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình credential Xero + Outlook.
2. **Test run** và điều chỉnh email template theo phong cách của doanh nghiệp.
3. **Bật Active** và bắt đầu tự động hóa nhắc nhở thanh toán!

**Nếu có bất kỳ câu hỏi nào**, các sếp có thể tham khảo [hướng dẫn chi tiết của n8n](https://docs.n8n.io/) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/community). 🚀