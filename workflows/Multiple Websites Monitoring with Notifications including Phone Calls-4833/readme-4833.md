---
title: "🚨 **Tự Động Hóa Theo Dõi Trạng Thái Website + Thông Báo Ngay Lập Tức (Gồm Gọi Điện, Email, Slack, Telegram)**"
description: "Workflow tự động theo dõi 100+ website 24/7, phát hiện downtime, ghi log chi tiết vào Google Sheets và thông báo ngay lập tức qua **gọi điện tự động, email, Slack, Telegram** – Giúp các sếp giảm thiểu mất mát doanh thu do downtime."
slug: "tieu-doi-website-voi-thong-bao-ngay-lap-tuc"
tags: [n8n, automation, website-monitoring, downtime-alert, no-code, devops]
keywords: [n8n workflow theo dõi website, tự động hóa downtime, thông báo gọi điện tự động, Slack Telegram email alert, Google Sheets logging]
---

# 🚨 **Tự Động Hóa Theo Dõi Website + Thông Báo Ngay Lập Tức (Gọi Điện + Email + Slack + Telegram)**

## **Nỗi Đau Của Các Sếp Khi Theo Dõi Website Thủ Công**
Các sếp đã bao giờ **lo lắng website của mình bị down** nhưng không biết cách phát hiện kịp thời? Hay **mất hàng chục triệu đồng** mỗi giờ do downtime không được xử lý ngay? Với cách làm thủ công:
- Phải **check website một cách thủ công** (tốn thời gian, dễ quên).
- **Không có thông báo tức thời** khi website down (gián tiếp gây mất doanh thu).
- **Không ghi log** để phân tích nguyên nhân sau này.
- **Không có cách thông báo đa kênh** (gọi điện, email, Slack, Telegram) để đảm bảo ai đó **ngay lập tức** xử lý.

**Workflow này giải quyết tất cả!** Nó sẽ:
✅ **Theo dõi 100+ website** một cách tự động, **24/7**.
✅ **Phát hiện downtime ngay lập tức** và **ghi log chi tiết** vào Google Sheets.
✅ **Thông báo ngay lập tức** qua:
   - **Gọi điện tự động** (sử dụng API gọi điện như Vapi).
   - **Email** (Gmail).
   - **Slack/Telegram** (để team biết ngay).
✅ **Cập nhật trạng thái uptime/downtime** tự động sau khi website hồi phục.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần check website thủ công hàng ngày.
- **Giảm thiểu mất mát**: Phát hiện downtime **ngay lập tức**, giảm thiểu ảnh hưởng đến doanh thu.
- **Ghi log chi tiết**: Dữ liệu downtime được lưu vào **Google Sheets**, giúp phân tích nguyên nhân sau này.
- **Thông báo đa kênh**: **Gọi điện, email, Slack, Telegram** đảm bảo **ai đó sẽ biết ngay** và xử lý.
- **Hồi phục tự động**: Khi website trở lại hoạt động, workflow sẽ **cập nhật trạng thái** và thông báo.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu danh sách website và log downtime).
   - **Sheet mẫu**: [Tải mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1_VVpkIvpYQigw5q0KmPXUAC2aV2rk1nRQLQZ7YK2KwY/edit?usp=sharing)
     - **Sheet 1**: Danh sách website cần theo dõi (cột `Domain`).
     - **Sheet 2**: Log downtime (cột `Timestamp`, `Duration`, `Status`).
2. **API Key gọi điện tự động** (ví dụ: [Vapi](https://vapi.vn/)).
   - **Cài đặt Vapi**:
     - Tạo **assistant** mới với **First message**:
       ```
       Hello {{name}}, I'm Website Monitoring Assistant. This is a system alert. The {{web_domain}} is currently down. Please take immediate action to investigate and resolve the issue. Thank you.
       ```
3. **Tài khoản Gmail** (để gửi email thông báo).
4. **Webhook/Token Slack & Telegram** (để gửi thông báo).
5. **n8n Self-hosted** (để workflow chạy 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor.

#### **Cách import từ file JSON:**
1. Tải workflow từ [n8n.io/workflows/4833](https://n8n.io/workflows/4833).
2. Nhấn **Export** (tại góc trên bên phải).
3. Trong n8n Editor, nhấn **Import** và chọn file JSON vừa tải.

#### **Cách copy/paste JSON:**
1. Mở n8n Editor.
2. Nhấn **Import** → **Paste JSON**.
3. Dán JSON từ [tại đây](https://n8n.io/workflows/4833) (hoặc file JSON đã tải).

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "Website URLs" (Google Sheets)**
- **Mục đích**: Lấy danh sách website cần theo dõi từ **Sheet 1**.
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: `Sheet 1` (danh sách website).
  - **Range**: `A2:B` (giả sử cột `A` là tên domain, `B` là tên website).

#### **🔹 Node "Check website status" (HTTP Request)**
- **Mục đích**: Kiểm tra trạng thái của mỗi website.
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: `https://{{$node["Website URLs"].json()["domain"]}}` (động态 lấy domain từ Google Sheets).
  - **Response Format**: `json`.

#### **🔹 Node "Notify over Phone Call" (HTTP Request)**
- **Mục đích**: Gọi điện tự động khi website down.
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.vapi.vn/v1/calls` (hoặc API gọi điện khác).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_VAPI_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "to": "+84123456789", // Số điện thoại người nhận
      "from": "+84987654321", // Số điện thoại gọi từ
      "text": "Website {{web_domain}} đang down. Vui lòng kiểm tra ngay!"
    }
    ```

#### **🔹 Node "Email Notification" (Gmail)**
- **Mục đích**: Gửi email thông báo khi website down/up.
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2`.
  - **To**: Email của người nhận.
  - **Subject**:
    - Nếu website **down**: `"ALERT: Website {{web_domain}} đang down!"`
    - Nếu website **up**: `"Website {{web_domain}} đã hồi phục!"`
  - **Body**:
    ```
    Website {{web_domain}} đang trong trạng thái: {{status}}.
    Thời gian bắt đầu downtime: {{timestamp}}.
    ```

#### **🔹 Node "Slack/Telegram Notification"**
- **Mục đích**: Gửi thông báo đến Slack/Telegram.
- **Cấu hình**:
  - **Slack**:
    - **Credentials**: `slackOAuth2Api`.
    - **Channel**: `#website-alerts`.
    - **Message**: `Website {{web_domain}} đang down!`.
  - **Telegram**:
    - **Credentials**: `telegramApi`.
    - **Chat ID**: ID của chat Telegram.
    - **Message**: `Website {{web_domain}} đang down!`.

#### **🔹 Node "Update Uptime and Total Downtime" (Google Sheets)**
- **Mục đích**: Cập nhật trạng thái uptime/downtime vào **Sheet 2**.
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Sheet Name**: `Sheet 2`.
  - **Range**: `A2:F` (cột ghi log downtime).
  - **Operation**: `update`.

#### **🔹 Node "Find Existing Record" (Code)**
- **Mục đích**: Kiểm tra xem website đã có log downtime trước đó chưa.
- **Code mẫu** (nếu cần chỉnh sửa):
  ```javascript
  // Kiểm tra xem website đã có log downtime trước đó
  const existingRecord = $input.all().find(item => item.domain === $node["Website URLs"].json()["domain"]);
  return existingRecord ? { json: { exists: true, record: existingRecord } } : { json: { exists: false } };
  ```

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Run Once** và kiểm tra các node hoạt động như thế nào.
2. **Bật Active**:
   - Sau khi kiểm tra xong, **bật Active** để workflow chạy tự động theo lịch trình.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Thêm Log Chi Tiết Hơn**
- **Thêm cột `Notes`** vào Google Sheets để ghi chú nguyên nhân downtime.
- **Sử dụng node `stickyNote`** để lưu ý các sự kiện đặc biệt.

### **2. Thêm Báo Cáo Định Kỳ**
- **Sử dụng node `scheduleTrigger`** để gửi **báo cáo tuần/month** về downtime qua email/Slack.
- **Tạo một workflow phụ** để tổng hợp dữ liệu từ Google Sheets và gửi báo cáo.

### **3. Kết Hợp với Monitoring Tools**
- **Nếu đã dùng tools như UptimeRobot, Pingdom**, có thể **tích hợp API** của chúng vào workflow để lấy dữ liệu trạng thái website.

### **4. Thêm AI Chatbot Trả Lời**
- **Sử dụng node `n8n-nodes-base.llm`** (nếu có) để tạo **chatbot tự động** trả lời khi website down:
  ```
  "Xin lỗi quý khách! Website đang bị down. Chúng tôi đang xử lý ngay lập tức. Vui lòng quay lại sau."
  ```

---

## 📌 **Kết Luận**
Workflow này **giải quyết hoàn toàn** vấn đề downtime website một cách **tự động hóa 100% không cần code**. Các sếp sẽ:
✔ **Không bao giờ bỏ lỡ downtime** nhờ thông báo **ngay lập tức** qua **gọi điện, email, Slack, Telegram**.
✔ **Ghi log chi tiết** để phân tích và cải thiện.
✔ **Tiết kiệm thời gian** và **giảm thiểu mất mát doanh thu**.

**Hãy áp dụng ngay để bảo vệ website của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản tại n8n.io](https://n8n.io/workflows/4833)**
**📌 [Mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1_VVpkIvpYQigw5q0KmPXUAC2aV2rk1nRQLQZ7YK2KwY/edit?usp=sharing)**