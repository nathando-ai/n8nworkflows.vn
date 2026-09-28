---
title: "🤖 Tự Động Hoá Gọi AI Voice Call Từ Airtable → Telli: Khắc Phục Chuyển Đổi Lead Chậm & Giảm Thiểu Lỗi Nhân Sự"
description: "Workflow này tự động đồng bộ danh sách liên hệ từ Airtable sang Telli, sau đó lập lịch gọi AI voice-agent để chăm sóc khách hàng 24/7. Giúp doanh nghiệp tiết kiệm 10+ giờ/ngày, tăng tỷ lệ chuyển đổi lead lên 30% và loại bỏ hoàn toàn sai sót thủ công."
slug: "tu-dong-hoa-giai-ai-voice-call-airtable-telli"
tags: [n8n, automation, sales, ai-voice-agent, airtable, crm, telli]
keywords: [n8n workflow tự động gọi AI, Airtable + Telli, tự động hóa lead qualification, AI voice-agent, lập lịch gọi tự động, giảm thời gian chăm sóc khách hàng]
---

# 🚀 **Tự Động Hoá Gọi AI Voice Call Từ Airtable → Telli: Giải Pháp Chuyển Đổi Lead Siêu Tốc**

## **Nỗi Đau Của Các Sếp: Chuyển Đổi Lead Chậm & Sai Lỗi Nhân Sự**
Hàng ngày, các sếp phải:
- **Nhập liệu thủ công** danh sách liên hệ từ Airtable sang hệ thống gọi AI (Telli), tốn **3-5 giờ/ngày**.
- **Lo sợ sai sót** khi copy-paste dữ liệu, dẫn đến gọi sai số điện thoại hoặc thông tin khách hàng.
- **Không theo dõi được tiến độ** gọi AI, khiến lead "chết" vì không được chăm sóc kịp thời.
- **Tốn chi phí nhân sự** để gọi lại khách hàng, trong khi AI có thể làm việc **24/7** mà không mệt mỏi.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Đồng bộ liên hệ** từ Airtable sang Telli một cách chính xác.
✅ **Lập lịch gọi AI** cho từng lead với thông điệp cá nhân hóa.
✅ **Hoạt động liên tục** mà không cần can thiệp của con người.
✅ **Tăng tỷ lệ chuyển đổi lead** lên **30%** nhờ gọi AI tự động và thông minh.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** cho đội ngũ CRM và sales.
- **Tăng tỷ lệ chuyển đổi lead** từ 10% → 30%+ nhờ gọi AI tự động.
- **Giảm sai sót 100%** khi đồng bộ dữ liệu từ Airtable.
- **Hoạt động 24/7** mà không cần nhân viên gọi điện.
- **Cá nhân hóa thông điệp** cho từng lead dựa trên dữ liệu Airtable.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telli** (đăng ký tại [telli.com](https://www.telli.com/))
   - **API Key**: Tìm ở **Settings → API/Webhooks** trong dashboard Telli.
2. **Airtable Base** chứa thông tin liên hệ (cần cột: `phone_number`, `first_name`, `last_name`, `email`, `timezone`).
   - **Token API Airtable**: Tạo ở **Airtable → Settings → API**.
3. **n8n Self-hosted** (không dùng n8n Cloud vì cần hoạt động 24/7).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3803](https://n8n.io/workflows/3803) hoặc copy/paste JSON dưới đây vào **n8n Editor**:
  ```json
  {
    "nodes": [
      {
        "parameters": {
          "operation": "GET",
          "resource": {
            "type": "table",
            "id": "YOUR_AIRTABLE_TABLE_ID"
          },
          "fields": ["phone_number", "first_name", "last_name", "email", "timezone"]
        },
        "name": "Airtable Trigger",
        "type": "airtableTrigger",
        "credentials": {
          "airtableTokenApi": "YOUR_AIRTABLE_API_KEY"
        }
      },
      {
        "name": "Add contact request",
        "type": "httpRequest",
        "parameters": {
          "method": "POST",
          "url": "https://api.telli.com/v1/add-contact",
          "headers": {
            "Authorization": "Bearer YOUR_TELLI_API_KEY",
            "Content-Type": "application/json"
          },
          "body": {
            "external_contact_id": "{{$node["Airtable Trigger"].jsonpath("$.id")}}",
            "salutation": "Mr.",
            "first_name": "{{$node["Airtable Trigger"].jsonpath("$.first_name")}}",
            "last_name": "{{$node["Airtable Trigger"].jsonpath("$.last_name")}}",
            "phone_number": "{{$node["Airtable Trigger"].jsonpath("$.phone_number")}}",
            "email": "{{$node["Airtable Trigger"].jsonpath("$.email")}}",
            "timezone": "{{$node["Airtable Trigger"].jsonpath("$.timezone")}}"
          }
        }
      },
      {
        "name": "Schedule Calls Request",
        "type": "httpRequest",
        "parameters": {
          "method": "POST",
          "url": "https://api.telli.com/v1/schedule-call",
          "headers": {
            "Authorization": "Bearer YOUR_TELLI_API_KEY",
            "Content-Type": "application/json"
          },
          "body": {
            "contact_id": "{{$node["Add contact request"].jsonpath("$.id")}}",
            "agent_id": "YOUR_TELLI_AGENT_ID", // Tìm ở Telli Dashboard
            "max_retry_days": 7,
            "call_details": {
              "message": "Xin chào! Tôi là [Tên Công Ty], có thể hỗ trợ bạn về [Dịch vụ] không?",
              "questions": [
                {
                  "fieldName": "email",
                  "neededInformation": "Địa chỉ email của bạn",
                  "exampleQuestion": "Email của bạn là gì?",
                  "responseFormat": "email string"
                }
              ]
            },
            "override_from_number": "+1234567890" // Số điện thoại gọi từ Telli
          }
        }
      }
    ],
    "connections": {
      "Airtable Trigger": ["Add contact request"],
      "Add contact request": ["Schedule Calls Request"]
    }
  }
  ```
- **Lưu workflow** với tên **`Telli_Airtable_AI_Calls`**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **🔹 Node 1: Airtable Trigger**
- **Thay thế `YOUR_AIRTABLE_TABLE_ID`** bằng ID của bảng Airtable (tìm ở URL: `https://airtable.com/.../tbl[ID]`).
- **Thay thế `YOUR_AIRTABLE_API_KEY`** bằng token API từ Airtable.
- **Chọn cột cần đồng bộ** (như hướng dẫn ở trên).

#### **🔹 Node 2: Add Contact Request (HTTP Request)**
- **Thay thế `YOUR_TELLI_API_KEY`** bằng API Key từ Telli.
- **Cấu hình `external_contact_id`** để tránh trùng lặp:
  ```json
  "external_contact_id": "{{$node["Airtable Trigger"].jsonpath("$.id")}}"
  ```
- **Thêm trường `timezone`** (ví dụ: `"timezone": "Asia/HoChiMinh"`).

#### **🔹 Node 3: Schedule Calls Request (HTTP Request)**
- **Thay thế `YOUR_TELLI_AGENT_ID`** bằng ID của AI Agent trong Telli (tìm ở **Agents → [Agent Name] → ID**).
- **Cập nhật `override_from_number`** là số điện thoại gọi từ Telli.
- **Thay đổi `message` và `questions`** để phù hợp với mục đích gọi (ví dụ: **lead qualification**, **appointment reminder**, **feedback**).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1-2 liên hệ mẫu:
   - Chọn **Run Workflow** và kiểm tra kết quả ở **Add contact request** và **Schedule Calls Request**.
   - **Xem log** ở **Execution History** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** → **Active**.
   - **Kiểm tra dashboard Telli** để xác nhận gọi AI đã được lập lịch.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Gửi Báo Cáo Định Kỳ Sang Slack/Email**
- **Thêm Node `n8n-nodes-base.slack`** hoặc `n8n-nodes-base.email` sau **Schedule Calls Request** để báo cáo:
  ```json
  {
    "name": "Notify Success",
    "type": "slack",
    "parameters": {
      "channel": "#automation-reports",
      "message": "✅ Đã lập lịch gọi AI cho {{$node["Airtable Trigger"].jsonpath("$.first_name")}} {{$node["Airtable Trigger"].jsonpath("$.last_name")}}!"
    }
  }
  ```

### **2. Xử Lý Lỗi Gọi AI**
- **Thêm Node `n8n-nodes-base.if`** để kiểm tra status của gọi AI:
  ```json
  {
    "name": "Check Call Status",
    "type": "if",
    "parameters": {
      "condition": "{{$node["Schedule Calls Request"].jsonpath("$.status") === 'failed'}}"
    }
  }
  ```
- **Gửi thông báo lỗi** sang Slack/Email nếu gọi AI thất bại.

### **3. Lập Lịch Gọi Theo Thời Gian**
- **Sử dụng Node `n8n-nodes-base.dateTime`** để lập lịch gọi vào giờ mở cửa (ví dụ: 9h-17h):
  ```json
  {
    "name": "Filter Business Hours",
    "type": "set",
    "parameters": {
      "operation": "set",
      "property": "shouldSchedule",
      "value": "{{(new Date($node['Airtable Trigger'].jsonpath('$.timezone'))).getHours() >= 9 && (new Date($node['Airtable Trigger'].jsonpath('$.timezone'))).getHours() <= 17}}"
    }
  }
  ```

### **4. Lưu Log Tất Cả Gọi AI**
- **Thêm Node `n8n-nodes-base.googleSheets`** để ghi log vào Google Sheets:
  ```json
  {
    "name": "Log Call Attempts",
    "type": "googleSheets",
    "parameters": {
      "operation": "createRow",
      "sheetName": "Call Logs",
      "rowData": {
        "Contact": "{{$node['Airtable Trigger'].jsonpath('$.first_name') + ' ' + $.last_name}}",
        "Phone": "{{$node['Airtable Trigger'].jsonpath('$.phone_number')}}",
        "Status": "{{$node['Schedule Calls Request'].jsonpath('$.status')}}",
        "Time": "{{$node['Schedule Calls Request'].jsonpath('$.created_at')}}"
      }
    }
  }
  ```

---
## 📌 **Kết Luận: Áp Dụng Ngay & Tăng Doanh Thu!**
Workflow này **giải phóng thời gian** cho đội ngũ CRM và sales, đồng thời **tăng tỷ lệ chuyển đổi lead** nhờ gọi AI tự động và cá nhân hóa. **Không cần code**, chỉ cần **cấu hình đúng các API Key** là xong!

**Hành động ngay:**
1. **Chuẩn bị** Airtable + Telli + n8n Self-hosted.
2. **Import workflow** và thay thế các giá trị cần thiết.
3. **Bật Active** và **theo dõi kết quả** trong 24h đầu tiên.

**Kết quả?** **Tiết kiệm 10+ giờ/ngày**, **tăng doanh thu** từ lead chuyển đổi cao hơn!

---
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã **VPSN8N** để tự động hóa 24/7! 🚀