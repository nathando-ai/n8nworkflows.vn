---
title: "🚀 Tự Động Hoàn Thành Cuộc Hẹn Google Calendar Từ Trello - Không Cần Code!"
description: "Workflow này tự động tạo cuộc họp Google Calendar từ thẻ Trello, thêm liên kết cuộc họp vào thẻ và gửi thông báo cho người tham gia - tiết kiệm 100% thời gian quản lý lịch!"
slug: "tự-dộng-hoàn-thành-cuộc-họp-google-calendar-tu-trello"
tags: [n8n, automation, trello, google-calendar, no-code, ai-ops]
keywords: [n8n workflow trello calendar, tự động hóa cuộc họp google, quản lý lịch từ trello, tự động tạo cuộc họp google calendar, tiết kiệm thời gian quản lý lịch]
---

# 🚀 **Tự Động Tạo Cuộc Hẹn Google Calendar Từ Trello - Không Cần Code!**

### **💡 Giải quyết vấn đề gì?**
Các sếp thường phải làm thủ công:
- **Tạo cuộc họp Google Calendar** cho từng yêu cầu từ Trello
- **Tìm email người tham gia** và thêm họ vào cuộc họp
- **Chuyển thẻ Trello** sang trạng thái đã xử lý
- **Quên gửi thông báo** cho người tham gia

Kết quả? **Tốn thời gian, dễ lỡ, và không chuyên nghiệp**. Workflow này **tự động hóa toàn bộ quy trình** chỉ với một thẻ Trello!

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30-50% thời gian** quản lý lịch và cuộc họp hàng ngày
- **Không bao giờ quên** gửi thông báo cho người tham gia
- **Cuộc họp được tự động tạo** với thông tin từ thẻ Trello (tiêu đề, mô tả, thời gian dự kiến)
- **Liên kết cuộc họp được thêm tự động** vào thẻ Trello để theo dõi
- **Hoạt động 24/7** mà không cần can thiệp thủ công
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản Trello** và **API Key Trello** (tạo tại [Trello Developer Portal](https://trello.com/app-key))
2. **Tài khoản Google Calendar** và **API Key Google Calendar** (tạo tại [Google Cloud Console](https://console.cloud.google.com/))
3. **Trello Board** có **List** để lưu thẻ cuộc họp (ví dụ: "Cuộc họp cần tạo")
4. **Email của người tham gia** (có thể lấy từ thẻ Trello hoặc nhập thủ công)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4081](https://n8n.io/workflows/4081) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
  ```json
  {
    "nodes": [
      {
        "parameters": {
          "method": "GET",
          "url": "https://api.trello.com/1/members/me/lists?key={{$trelloApiKey}}&token={{$trelloToken}}"
        },
        "name": "Get List ID",
        "type": "n8n-nodes-base.httpRequest"
      },
      {
        "parameters": {
          "options": {
            "boardId": "{{$boardId}}",
            "listName": "{{$listName}}"
          }
        },
        "name": "Trigger Move Card in Trello",
        "type": "n8n-nodes-base.trelloTrigger"
      },
      {
        "parameters": {
          "resource": "card",
          "operation": "moveCard",
          "action": "{{$action}}"
        },
        "name": "Filter Action",
        "type": "n8n-nodes-base.filter"
      },
      {
        "parameters": {
          "id": "{{$cardId}}"
        },
        "name": "Trello: Get Card Info",
        "type": "n8n-nodes-base.trello"
      },
      {
        "parameters": {
          "code": "return JSON.parse($input.json['email']).map(email => email.trim()).filter(email => email.length > 0);"
        },
        "name": "Get Email",
        "type": "n8n-nodes-base.code"
      },
      {
        "parameters": {
          "code": "return $input.json.map(email => ({ email }));"
        },
        "name": "Separates Emails",
        "type": "n8n-nodes-base.code"
      },
      {
        "parameters": {
          "id": "{{$cardId}}",
          "name": "{{$cardName}}",
          "desc": "{{$cardDescription}}",
          "action": "addText",
          "text": "Liên kết cuộc họp: {{$meetingLink}}"
        },
        "name": "Trello: Add Meeting Link",
        "type": "n8n-nodes-base.trello"
      },
      {
        "parameters": {
          "method": "GET",
          "url": "https://admin.googleapis.com/admin/directory/v1/customSecuritySettings/organization/calendarSettings?key={{$googleApiKey}}"
        },
        "name": "Get Organization ID",
        "type": "n8n-nodes-base.httpRequest"
      },
      {
        "parameters": {
          "summary": "{{$cardName}}",
          "description": "{{$cardDescription}}",
          "start": "{{$startTime}}",
          "end": "{{$endTime}}",
          "attendees": "{{$emails}}"
        },
        "name": "Calendar: Create Meeting",
        "type": "n8n-nodes-base.googleCalendar"
      }
    ],
    "connections": {
      "httpRequest1": {
        "main": ["trelloTrigger1"]
      },
      "trelloTrigger1": {
        "main": ["filter1"]
      },
      "filter1": {
        "main": ["trello1"]
      },
      "trello1": {
        "main": ["code1"]
      },
      "code1": {
        "main": ["code2"]
      },
      "code2": {
        "main": ["trello2"]
      },
      "trello2": {
        "main": ["httpRequest2"]
      },
      "httpRequest2": {
        "main": ["googleCalendar1"]
      }
    }
  }
  ```
- **Nhấn "Import"** và bắt đầu cấu hình!

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Các node **quan trọng nhất** cần cấu hình cẩn thận:

##### **🔹 Node `Get List ID` (HTTP Request)**
- **URL**: `https://api.trello.com/1/members/me/lists?key={{$trelloApiKey}}&token={{$trelloToken}}`
- **Tham số cần điền**:
  - `$trelloApiKey`: API Key Trello (tạo tại [Trello Developer](https://trello.com/app-key))
  - `$trelloToken`: Token Trello (tạo tại [Trello Developer](https://trello.com/app-key))

##### **🔹 Node `Trigger Move Card in Trello` (Trello Trigger)**
- **Cấu hình**:
  - **Board ID**: ID của Board Trello (tìm tại URL: `https://trello.com/b/[BOARD_ID]/...`)
  - **List Name**: Tên của List chứa thẻ cuộc họp (ví dụ: "Cuộc họp cần tạo")
  - **Action**: Chọn **"moveCard"** khi thẻ được chuyển sang List khác

##### **🔹 Node `Trello: Get Card Info` (Trello)**
- **ID**: `$cardId` (lấy từ thẻ Trello)
- **Tham số cần extra**:
  - `$cardName`: Tên cuộc họp (ví dụ: "Hội nghị chiến lược tháng 6")
  - `$cardDescription`: Mô tả cuộc họp (ví dụ: "Thảo luận về dự án X")
  - `$startTime` & `$endTime`: Thời gian cuộc họp (định dạng ISO, ví dụ: `"2024-06-15T09:00:00+07:00"`)

##### **🔹 Node `Get Email` & `Separates Emails` (Code)**
- **Cấu hình**:
  - Nếu email **được lưu trong mô tả thẻ Trello**, cấu hình như sau:
    ```javascript
    // Node "Get Email":
    return JSON.parse($input.json['description']).emails;
    ```
  - Nếu email **nhập thủ công**, điền vào `$emails` dưới dạng mảng:
    ```json
    ["email1@example.com", "email2@example.com"]
    ```

##### **🔹 Node `Calendar: Create Meeting` (Google Calendar)**
- **Tham số cần điền**:
  - **Summary**: `$cardName` (tên cuộc họp)
  - **Description**: `$cardDescription` (mô tả cuộc họp)
  - **Start/End Time**: `$startTime` & `$endTime` (định dạng ISO)
  - **Attendees**: `$emails` (mảng email người tham gia)

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một thẻ Trello mẫu:
   - Chuyển thẻ từ List "Cuộc họp cần tạo" sang List khác (ví dụ: "Đã xử lý").
   - Kiểm tra **Google Calendar** và **thẻ Trello** có được cập nhật không.
2. **Bật Active workflow** khi test thành công!

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi thông báo Slack/Telegram** khi cuộc họp được tạo thành công:
  ```javascript
  // Thêm node "Slack" hoặc "Telegram Bot" sau node "Calendar: Create Meeting"
  {
    "parameters": {
      "text": `Cuộc họp "${$cardName}" đã được tạo thành công!\nLiên kết: {{$meetingLink}}`
    },
    "name": "Notify Slack",
    "type": "n8n-nodes-base.slack"
  }
  ```
- **Lưu log cuộc họp** vào Google Sheets:
  ```javascript
  // Thêm node "Google Sheets" sau node "Calendar: Create Meeting"
  {
    "parameters": {
      "sheetName": "Cuộc họp",
      "row": [
        { "title": "$cardName" },
        { "description": "$cardDescription" },
        { "startTime": "$startTime" },
        { "endTime": "$endTime" },
        { "meetingLink": "$meetingLink" }
      ]
    },
    "name": "Log to Google Sheets",
    "type": "n8n-nodes-base.googleSheets"
  }
  ```
- **Tự động gửi email thông báo** cho người tham gia:
  ```javascript
  // Thêm node "Email" (ví dụ: SendGrid hoặc Gmail)
  {
    "parameters": {
      "to": "{{$emails}}",
      "subject": `Bạn đã được mời tham gia cuộc họp: {{$cardName}}`,
      "html": `<p>Xin chào,</p><p>Bạn đã được mời tham gia cuộc họp:</p><p><strong>{{$cardName}}</strong></p><p>Thời gian: {{$startTime}} - {{$endTime}}</p><p>Liên kết: <a href="{{$meetingLink}}">{{$meetingLink}}</a></p>`
    },
    "name": "Send Email Notification",
    "type": "n8n-nodes-base.email"
  }
  ```
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc quản lý cuộc họp thủ công. **Chỉ cần một thẻ Trello**, hệ thống sẽ tự động:
✅ Tạo cuộc họp Google Calendar
✅ Thêm liên kết vào thẻ Trello
✅ Gửi thông báo cho người tham gia

**🚀 Hãy áp dụng ngay và tự động hóa quy trình của mình!**
Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với **Prompt and Paste** tại [n8n.io](https://n8n.io/workflows/4081).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::