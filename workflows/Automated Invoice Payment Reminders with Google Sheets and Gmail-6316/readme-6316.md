---
title: "💰 **Tự Động Gửi Nhắc Nhở Thanh Toán Hóa Đơn Với Google Sheets & Gmail (N8N)** – Giảm Thiểu Trễ Thanh Toán & Tiết Kiệm Thời Gian"
description: "Workflow tự động hóa gửi nhắc nhở thanh toán hóa đơn hàng ngày, giúp doanh nghiệp tránh tình trạng trễ thu, tiết kiệm thời gian và cải thiện lưu chuyển tiền tệ. Hoạt động 24/7 mà không cần code!"
slug: "tieu-dong-hoa-nhac-nho-thanh-toan-hoa-don"
tags: [n8n, automation, invoice, google-sheets, gmail, no-code, business-automation]
keywords: [tự động hóa hóa đơn n8n, nhắc nhở thanh toán tự động, google sheets + gmail n8n, giảm trễ thu hóa đơn, workflow n8n cho doanh nghiệp]
---

# 🚀 **Tự Động Gửi Nhắc Nhở Thanh Toán Hóa Đơn – Giải Pháp Không Cần Code Cho Doanh Nghiệp**

### **Nỗi Đau Của Doanh Nghiệp Khi Quản Lý Hóa Đơn Thhand Công**
Hóa đơn chưa được thanh toán kịp thời là "đại địch" của nhiều doanh nghiệp, đặc biệt là các **freelancer, SMBs, và công ty dịch vụ**. Việc theo dõi ngày hết hạn, gửi nhắc nhở thủ công không chỉ **tiêu tốn thời gian** mà còn dễ gây **lỗi sót** hoặc **trễ thu**. Kết quả?
- **Lưu chuyển tiền tệ chậm**: Tiền "đóng băng" trong hóa đơn chưa thu.
- **Thời gian bị "cướp":** Nhân viên phải dành giờ làm việc cho việc nhắc nhở thay vì phát triển kinh doanh.
- **Mối quan hệ khách hàng bị ảnh hưởng**: Nhắc nhở muộn hoặc không chuyên nghiệp làm giảm uy tín.
- **Stress không cần thiết**: Lo lắng về việc khách hàng quên hoặc cố tình trễ thanh toán.

**Giải pháp?** Một **workflow tự động hóa hoàn toàn** với **n8n**, kết hợp **Google Sheets** (để lưu trữ dữ liệu hóa đơn) và **Gmail** (để gửi email nhắc nhở). Hệ thống sẽ **kiểm tra hàng ngày**, **lọc hóa đơn cần nhắc nhở**, và **gửi email cá nhân hóa** tự động – **không cần can thiệp của con người**.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm thời gian**: Không phải mất giờ để nhắc nhở thủ công.
✅ **Chính xác 100%**: Không bỏ sót hóa đơn nào, kể cả những hóa đơn đã quá hạn.
✅ **Cá nhân hóa email**: Gửi nhắc nhở khác nhau cho hóa đơn **sắp hết hạn** và **đã quá hạn**.
✅ **Hoạt động liên tục**: Kiểm tra và gửi nhắc nhở **mỗi ngày** (cấu hình được).
✅ **Cải thiện lưu chuyển tiền tệ**: Giảm thời gian chờ thu, tăng khả năng thu tiền kịp thời.
✅ **Dễ dàng mở rộng**: Thêm logic nhắc nhở, thay đổi nội dung email mà không cần code.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n** (self-hosted hoặc dùng dịch vụ cloud).
2. **Google Sheets** chứa dữ liệu hóa đơn với **các cột bắt buộc**:
   - `InvoiceID` (Mã hóa đơn)
   - `ClientName` (Tên khách hàng)
   - `ClientEmail` (Email khách hàng)
   - `Amount` (Số tiền)
   - `DueDate` (Ngày hết hạn – **định dạng `YYYY-MM-DD`**)
   - `Status` (Trạng thái: `Pending` hoặc `Paid`)
3. **Tài khoản Gmail** (để gửi email nhắc nhở).
4. **API Key OAuth2** cho:
   - **Google Sheets** (để đọc dữ liệu).
   - **Gmail** (để gửi email).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- Mở **n8n Editor** và tạo **workflow mới**.
- Nhấp vào **`...` (More Options)** → Chọn **`Import from JSON`**.
- Dán **JSON dưới đây** vào và nhấn **`Import`**:
```json
{
  "nodes": {
    "1": {
      "parameters": {
        "functionCode": "const today = new Date();\nconst remindBeforeDays = 3; // Nhắc nhở trước 3 ngày\nconst remindAfterDays = 7; // Nhắc nhở sau 7 ngày\n\nconst invoicesToRemind = [];\n\n$json.map(invoice => {\n  const dueDate = new Date(invoice.DueDate);\n  const timeDiff = today.getTime() - dueDate.getTime();\n  const daysDiff = timeDiff / (1000 * 3600 * 24);\n\n  // Kiểm tra nếu hóa đơn chưa thanh toán và trong khoảng nhắc nhở\n  if (invoice.Status === 'Pending' && \n      (daysDiff <= remindBeforeDays || daysDiff >= -remindAfterDays)) {\n\n    // Tạo subject và body tùy thuộc vào trạng thái\n    let subject, body;\n    if (daysDiff <= remindBeforeDays) {\n      subject = `📌 Nhắc Nhở: Hóa Đơn ${invoice.InvoiceID} Sắp Hết Hạn (${Math.ceil(daysDiff)} ngày)`;\n      body = `\n      <p><strong>Xin chào ${invoice.ClientName},</strong></p>\n      <p>Hóa đơn <strong>${invoice.InvoiceID}</strong> (${invoice.Amount} VND) sẽ hết hạn vào ngày <strong>${invoice.DueDate}</strong>.</strong></p>\n      <p>Vui lòng thanh toán kịp thời để tránh phí chậm trễ.</p>\n      <p>Cảm ơn!</p>\n      <p><strong>Chú ý:</strong> Hóa đơn sẽ được nhắc nhở lại nếu chưa thanh toán.</p>\n      `;\n    } else {\n      subject = `⚠️ Hóa Đơn ${invoice.InvoiceID} Đã Quá Hạn (${Math.ceil(-daysDiff)} ngày)`;\n      body = `\n      <p><strong>Xin chào ${invoice.ClientName},</strong></p>\n      <p>Hóa đơn <strong>${invoice.InvoiceID}</strong> (${invoice.Amount} VND) đã quá hạn từ ngày <strong>${invoice.DueDate}</strong>.</strong></p>\n      <p>Vui lòng thanh toán ngay để tránh ảnh hưởng đến dịch vụ.</p>\n      <p>Cảm ơn!</p>\n      `;\n    }\n\n    invoicesToRemind.push({\n      ...invoice,\n      subject,\n      body\n    });\n  }\n  return invoicesToRemind;\n})"
      },
      "name": "3. Filter & Prepare Reminders",
      "type": "function"
    },
    "2": {
      "parameters": {
        "credentials": {
          "googleSheetsOAuth2Api": ""
        },
        "sheetId": "YOUR_GOOGLE_SHEET_ID",
        "range": "Invoices!A:F"
      },
      "name": "2. Read Invoice Data (Google Sheets)",
      "type": "googleSheets"
    },
    "3": {
      "parameters": {},
      "name": "4. If Invoices to Remind?",
      "type": "if"
    },
    "4": {
      "parameters": {
        "credentials": {
          "gmailOAuth2": ""
        },
        "from": "YOUR_SENDER_EMAIL@example.com",
        "subject": "{{$json.subject}}",
        "html": "{{$json.body}}",
        "to": "{{$json.ClientEmail}}"
      },
      "name": "5. Send Invoice Reminder (Gmail)",
      "type": "gmail"
    },
    "5": {
      "parameters": {
        "interval": "24",
        "value": "hours",
        "timezone": "Asia/Ho_Chi_Minh"
      },
      "name": "1. Daily Schedule Trigger",
      "type": "scheduleTrigger"
    }
  },
  "connections": {
    "main": [
      {
        "node": "5",
        "connection": "main",
        "port": "output",
        "type": "direct",
        "id": "c1"
      },
      {
        "node": "2",
        "connection": "main",
        "port": "output",
        "type": "direct",
        "id": "c2"
      },
      {
        "node": "3",
        "connection": "main",
        "port": "output",
        "type": "direct",
        "id": "c3"
      },
      {
        "node": "3",
        "connection": "main",
        "port": "output",
        "type": "direct",
        "id": "c4",
        "nodeType": "if",
        "subNode": "false"
      },
      {
        "node": "3",
        "connection": "main",
        "port": "output",
        "type": "direct",
        "id": "c5",
        "nodeType": "if",
        "subNode": "true"
      },
      {
        "node": "4",
        "connection": "main",
        "port": "output",
        "type": "direct",
        "id": "c6"
      }
    ]
  }
}
```
> **Lưu ý:** Thay thế `YOUR_GOOGLE_SHEET_ID` và `YOUR_SENDER_EMAIL@example.com` bằng thông tin thực tế của các sếp.

---

### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
#### **Node 1: Daily Schedule Trigger**
- **Cấu hình thời gian**: Thay đổi `timezone` và `interval` để workflow chạy vào **lúc phù hợp** (ví dụ: **8h sáng hàng ngày**).
- **Ví dụ**:
  ```json
  "timezone": "Asia/Ho_Chi_Minh", // Thay đổi theo múi giờ của doanh nghiệp
  "interval": "24",
  "value": "hours"
  ```

#### **Node 2: Read Invoice Data (Google Sheets)**
- **Thiết lập OAuth2**:
  - Đăng nhập vào n8n → **Credentials** → Tạo mới **Google Sheets OAuth2**.
  - Chọn **Google Sheets API** và cấp quyền.
- **Thay đổi Sheet ID**:
  - Mở Google Sheets → URL sẽ có dạng: `https://docs.google.com/spreadsheets/d/[SHEET_ID]/edit`.
  - Copy `SHEET_ID` và thay thế vào `sheetId`.
- **Kiểm tra cột dữ liệu**:
  - **Bắt buộc**: `InvoiceID`, `ClientEmail`, `DueDate` (định dạng `YYYY-MM-DD`), `Status`.
  - **Ví dụ**:
    ```json
    "range": "Invoices!A:F" // Đảm bảo bao gồm tất cả cột cần thiết
    ```

#### **Node 3: Filter & Prepare Reminders (Function)**
- **Cấu hình ngày nhắc nhở**:
  - Thay đổi `remindBeforeDays` (nhắc nhở trước bao nhiêu ngày) và `remindAfterDays` (nhắc nhở sau bao nhiêu ngày quá hạn).
  - **Ví dụ**:
    ```javascript
    const remindBeforeDays = 3; // Nhắc nhở trước 3 ngày
    const remindAfterDays = 7; // Nhắc nhở sau 7 ngày quá hạn
    ```
- **Tùy chỉnh nội dung email**:
  - Thay đổi `subject` và `body` trong code để phù hợp với brand của doanh nghiệp.

#### **Node 4: If Invoices to Remind?**
- **Node này kiểm tra** nếu có hóa đơn cần nhắc nhở.
- **Không cần chỉnh sửa**, chỉ cần đảm bảo **Node 3** trả về dữ liệu đúng.

#### **Node 5: Send Invoice Reminder (Gmail)**
- **Thiết lập OAuth2**:
  - Tạo **Gmail OAuth2** trong n8n (đăng nhập Gmail → cấp quyền cho n8n).
- **Thay đổi email gửi**:
  - Đặt `from` là email chính thức của doanh nghiệp.
  - **Ví dụ**:
    ```json
    "from": "biz@example.com"
    ```

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Nhấn **`Test`** để chạy workflow với dữ liệu mẫu.
   - Kiểm tra **Execution History** để xác nhận email được gửi đúng.
2. **Bật Active**:
   - Nhấn **`Active`** để workflow chạy tự động hàng ngày.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để thông báo khi có hóa đơn quá hạn.
   - **Cách làm**:
     - Thêm **node Slack** sau **Node 5** và cấu hình để gửi tin nhắn khi có hóa đơn quá hạn.

2. **Lưu Log Lịch Sử**:
   - Thêm **node StickyNote** hoặc **Google Sheets** để ghi lại lịch sử nhắc nhở.
   - **Ưu điểm**: Theo dõi được khách hàng đã nhận nhắc nhở bao nhiêu lần.

3. **Gửi Email Của Nhiều Người**:
   - Sử dụng **node Gmail** với **multiple recipients** (nhiều email cùng lúc).
   - **Cách làm**:
     ```json
     "to": "{{$json.ClientEmail}}"
     ```
     (Nếu muốn gửi cho nhiều người, sử dụng **node Function** để split email.)

4. **Tự Động Chuyển Hóa Đơn Quá Hạn Sang Trạng Thái "Overdue"**:
   - Thêm **node Google Sheets** sau **Node 5** để cập nhật trạng thái hóa đơn trong sheet.
   - **Ví dụ**:
     ```javascript
     // Trong Function Node, thêm logic cập nhật status
     if (daysDiff > remindAfterDays) {
       updateSheetRow(invoice.Invoice