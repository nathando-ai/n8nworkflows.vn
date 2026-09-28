---
title: "🚀 Tự Động Hóa Đồng Bộ Khách Hàng Magento 2 → Google Contacts & Sheets (Không Trùng Lặp) - Giảm 90% Công Việc Thủ Công"
description: "Workflow tự động hóa đồng bộ hóa khách hàng mới từ Magento 2 sang Google Contacts và Google Sheets hàng ngày, loại bỏ trùng lặp và tiết kiệm 90% thời gian quản lý CRM. Phù hợp cho các sếp eCommerce cần quản lý khách hàng hiệu quả mà không cần code."
slug: "tuy-dong-hoa-dong-bo-khach-hang-magento-2-google-contacts-sheets"
tags: [n8n, automation, magento-2, google-contacts, google-sheets, crm, no-code]
keywords: [tự động hóa magento 2, đồng bộ khách hàng google contacts, loại bỏ trùng lặp google sheets, workflow n8n magento, tự động hóa crm ecommerce]
---

# 🚀 Đồng Bộ Khách Hàng Magento 2 → Google Contacts & Sheets (Không Trùng Lặp) - Giải Pháp Tự Động Hóa CRM 24/7

### 🔥 **Nỗi Đau Của Các Sếp ECommerce**
Quản lý khách hàng thủ công trên Magento 2 và Google Contacts là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**. Các sếp thường phải:
- **Lấy dữ liệu khách hàng** từ Magento hàng ngày và nhập vào Google Contacts.
- **Loại bỏ trùng lặp** giữa khách hàng cũ và mới bằng cách so sánh thủ công.
- **Lưu lịch sử đồng bộ** vào Google Sheets để theo dõi.
- **Tốn ít nhất 2-3 giờ/ngày** cho công việc này.

**Kết quả?** Dữ liệu không đồng bộ, khách hàng bị mất, và CRM không được tối ưu.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 90% thời gian** quản lý khách hàng (từ 3h/ngày xuống còn 10 phút).
✅ **Loại bỏ hoàn toàn trùng lặp** khách hàng giữa Magento và Google Contacts.
✅ **Lưu lịch sử đồng bộ** tự động vào Google Sheets với thời gian và số lượng khách hàng mới.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.
✅ **Cập nhật dữ liệu chính xác** hàng ngày, không lo mất khách hàng.

---
### 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản Magento 2** (API Key và URL API của Magento).
📌 **Tài khoản Google Workspace** (Google Contacts và Google Sheets).
📌 **API Key của Google** (tạo từ [Google Cloud Console](https://console.cloud.google.com/)).
📌 **Google Sheet** đã tạo sẵn với các cột: `Email`, `Name`, `Date Synced`, `Status`.
📌 **Google Contacts** (để đồng bộ hóa thông tin khách hàng).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1️⃣ **Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/6783) hoặc copy toàn bộ JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Workflow sẽ hiển thị với 8 nodes chính.

#### 2️⃣ **Cấu Hình Cần Thiết (BẮT BUỘC Chỉnh)**
##### **A. Schedule Trigger (Động cơ chạy hàng ngày)**
- **Cấu hình:**
  - **Cron:** `0 0 * * *` (chạy hàng ngày lúc 00:00).
  - **Time Zone:** Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý:** Đảm bảo server n8n **không bị ngắt kết nối** (nên self-hosted).

##### **B. GET PREVIOUS DATE (Lấy ngày trước để so sánh)**
- **Code Node:**
  ```javascript
  $input.all()[0].json.date = new Date($input.all()[0].json.date).setDate($input.all()[0].json.date.getDate() - 1);
  return [{ json: { date: $input.all()[0].json.date } }];
  ```
- **Lưu ý:** Node này **không cần chỉnh sửa** nếu đã import từ file JSON.

##### **C. Get New Customers (Lấy khách hàng mới từ Magento)**
- **HTTP Request Node:**
  - **Method:** `GET`
  - **URL:** `https://[your-magento-url]/rest/V1/customers?searchCriteria[filterGroups][0][filters][0][field]=created_at&searchCriteria[filterGroups][0][filters][0][value]=${previousDate}&searchCriteria[filterGroups][0][filters][0][conditionType]=gt`
  - **Headers:**
    ```
    Authorization: Bearer [YOUR_MAGENTO_API_KEY]
    Content-Type: application/json
    ```
  - **Lưu ý:** Thay `[your-magento-url]` và `[YOUR_MAGENTO_API_KEY]` bằng thông tin thực tế.

##### **D. Get Existing Emails (Lấy danh sách email đã tồn tại trong Google Sheets)**
- **Google Sheets Node:**
  - **Sheet Name:** Đặt tên sheet đã tạo trước (ví dụ: `Khách Hàng Magento`).
  - **Range:** `Sheet1!A2:B` (cột Email và Name).
  - **Lưu ý:** Đảm bảo cột `Email` ở vị trí A và `Name` ở B.

##### **E. Compare Datasets (So Sánh và loại bỏ trùng lặp)**
- **Compare Datasets Node:**
  - **Left Dataset:** Dữ liệu từ Magento (khách hàng mới).
  - **Right Dataset:** Dữ liệu từ Google Sheets (khách hàng cũ).
  - **Key Field:** `email` (để so sánh).
  - **Lưu ý:** Node này sẽ **tự động loại bỏ** khách hàng đã tồn tại.

##### **F. Create Google Contact (Tạo liên hệ mới trong Google Contacts)**
- **Google Contacts Node:**
  - **Email:** `$json.email`
  - **First Name:** `$json.firstname`
  - **Last Name:** `$json.lastname`
  - **Phone Numbers:** (Nếu có) `$json.telephone`
  - **Lưu ý:** Đảm bảo **API Key Google** đã được cấu hình trong n8n.

##### **G. Log Synced Email (Ghi log vào Google Sheets)**
- **Google Sheets Node:**
  - **Sheet Name:** `Lịch Sử Đồng Bộ`.
  - **Range:** `Sheet1!A1` (để ghi dữ liệu mới).
  - **Cột cần ghi:** `Email`, `Name`, `Date Synced`, `Status`.
  - **Lưu ý:** Cấu trúc cột phải khớp với sheet đã tạo.

---
#### 3️⃣ **Kích Hoạt ⚡️**
- **Bước 1:** Chạy **Test Run** với dữ liệu mẫu (nếu có).
- **Bước 2:** Đánh dấu workflow thành **Active**.
- **Bước 3:** Kiểm tra **Google Contacts** và **Google Sheets** để xác nhận đồng bộ.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
💡 **Kết Nối Slack/Telegram:**
- Thêm node **Slack/Telegram** sau node `Log Synced Email` để thông báo khi đồng bộ thành công.
- **Cấu hình:**
  ```json
  {
    "type": "slackWebhook",
    "options": {
      "url": "YOUR_SLACK_WEBHOOK_URL",
      "payload": {
        "text": "🚀 Đồng bộ khách hàng mới thành công! Số lượng: {{ $node["Log Synced Email"].json.length }}"
      }
    }
  }
  ```

💡 **Lưu Log Chi Tiết:**
- Thêm node **Google Drive** để lưu log chi tiết của workflow (ví dụ: file CSV hàng ngày).

💡 **Báo Cáo Định Kỳ:**
- Sử dụng node **Google Sheets** để tạo báo cáo tổng hợp hàng tuần/month với số lượng khách hàng mới.

💡 **Xử Lý Khách Hàng Trùng Lặp:**
- Nếu có trường hợp khách hàng trùng lặp do cập nhật thông tin, thêm node **Google Contacts Update** để cập nhật thông tin mới.

---
### 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn công việc quản lý khách hàng thủ công**, giúp các sếp tập trung vào chiến lược kinh doanh thay vì công việc lặp lại. **Tự động hóa đồng bộ hóa hàng ngày** giữa Magento 2 và Google Contacts không chỉ tiết kiệm thời gian mà còn **giảm thiểu sai sót** và **tối ưu hóa CRM**.

**Hành động ngay:**
1. **Self-host n8n** trên VPS để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và theo dõi kết quả!

👉 **Đăng ký VPS TinoHost (Mã giảm giá: VPSN8N)** để tự động hóa hoàn toàn:
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)

---