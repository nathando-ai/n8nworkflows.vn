---
title: "🚀 Tự Động Hóa Đóng Giao Dịch Lạnh HubSpot Với Gmail Feedback & Thông Báo Slack (N8N)"
description: "Workflow tự động hóa đóng các giao dịch lạnh (21+ ngày không tương tác) trên HubSpot, gửi email yêu cầu phản hồi qua Gmail và thông báo Slack cho team. Giúp tiết kiệm thời gian, tối ưu hóa pipeline bán hàng và cải thiện chất lượng dữ liệu."
slug: "tu-dong-hoa-dong-giao-dich-hubspot-voi-gmail-feedback"
tags: [n8n, automation, hubspot, gmail, slack, sales-funnel, no-code]
keywords: [n8n workflow hubspot, tự động hóa bán hàng, đóng giao dịch lạnh, email tự động, slack notification, sales automation]
---

# 🚀 **Tự Động Hóa Đóng Giao Dịch Lạnh HubSpot Với Gmail Feedback & Thông Báo Slack**

### **Giải pháp cho các sếp bán hàng: Xóa bỏ công việc thủ công, tối ưu pipeline và cải thiện chất lượng dữ liệu**
Bạn đã bao giờ phải mất nhiều giờ mỗi tuần để kiểm tra và đóng các giao dịch lạnh (cold deals) trên HubSpot? Hay phải nhắc nhở khách hàng qua email một cách thủ công để lấy phản hồi? **Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài phút cài đặt!**

Với **n8n**, bạn có thể:
✅ **Tự động đóng** các giao dịch không tương tác trong **21+ ngày** thành trạng thái *Closed Lost* trên HubSpot.
✅ **Gửi email tự động** qua Gmail để lấy phản hồi từ khách hàng, với nội dung cá nhân hóa (tên, thông tin giao dịch).
✅ **Thông báo ngay lập tức** cho team qua Slack khi một giao dịch được đóng, giúp mọi người cập nhật tình hình pipeline một cách nhanh chóng.
✅ **Tiết kiệm thời gian** lên đến **10+ giờ/tuần** (tính cho team bán hàng có 10+ giao dịch lạnh mỗi tuần).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và độ tin cậy cao.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho n8n)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải thủ công kiểm tra và đóng giao dịch lạnh hàng tuần.
- **Chính xác cao**: Dựa trên logic tự động (21+ ngày không tương tác) thay vì phụ thuộc vào con người.
- **Cá nhân hóa email**: Gửi email phản hồi với tên khách hàng và thông tin giao dịch, tăng tỷ lệ phản hồi.
- **Team đồng bộ**: Thông báo Slack ngay khi một giao dịch được đóng, giúp team bán hàng cập nhật kịp thời.
- **Dữ liệu sạch**: Loại bỏ giao dịch lạnh khỏi pipeline, giúp tập trung vào khách hàng tiềm năng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản HubSpot** (có **App Token** để kết nối API).
✔ **Tài khoản Gmail** (đã cấp quyền OAuth 2.0 cho n8n).
✔ **Tài khoản Slack** (có **OAuth Token** để gửi thông báo).
✔ **Thời gian định kỳ** (workflow chạy hàng ngày/ngày thứ 2 để kiểm tra giao dịch).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần kiến thức code**: Workflow đã được cấu hình sẵn, chỉ cần import và cấu hình credentials.
- **Test trước khi chạy live**: Đảm bảo email và Slack notification không bị spam.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON của workflow từ [n8n.io/workflows/9096](https://n8n.io/workflows/9096) hoặc copy toàn bộ JSON dưới đây.

**Bước 2:** Mở **n8n Editor** và chọn **Import Workflow** (hoặc paste JSON vào ô Import).

```json
{
  "nodes": [
    {
      "parameters": {
        "functionCode": "return $input.all();"
      },
      "name": "Extract Deal Fields",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": {
        "x": 300,
        "y": 200
      }
    },
    {
      "name": "Schedule Trigger",
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1,
      "position": {
        "x": 100,
        "y": 100
      },
      "credentials": {}
    },
    {
      "name": "Get HubSpot Deals",
      "type": "n8n-nodes-base.hubspot",
      "typeVersion": 1,
      "position": {
        "x": 100,
        "y": 300
      },
      "credentials": {
        "hubspotAppToken": ""
      },
      "operation": "getAll",
      "resource": "deal"
    },
    {
      "name": "Filter Cold Leads (21+ days)",
      "type": "n8n-nodes-base.filter",
      "typeVersion": 1,
      "position": {
        "x": 300,
        "y": 400
      },
      "conditions": [
        {
          "propertyName": "hs_lastmodifieddate",
          "operator": "lessThan",
          "values": [
            "21 days ago"
          ]
        }
      ]
    },
    {
      "name": "Update Deal to Closed Lost",
      "type": "n8n-nodes-base.hubspot",
      "typeVersion": 1,
      "position": {
        "x": 500,
        "y": 400
      },
      "credentials": {
        "hubspotAppToken": ""
      },
      "operation": "update",
      "resource": "deal",
      "propertyName": "dealstage",
      "propertyValue": "Closed Lost"
    },
    {
      "name": "Fetch Deal Associations",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": {
        "x": 500,
        "y": 600
      },
      "method": "GET",
      "url": "https://api.hubapi.com/crm/v3/objects/contacts?dealId={{$node["Get HubSpot Deals"].json[\"dealId\"]}}"
    },
    {
      "parameters": {
        "functionCode": "return $input.all();"
      },
      "name": "Extract Contact IDs",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": {
        "x": 700,
        "y": 600
      }
    },
    {
      "name": "Get Contact Details",
      "type": "n8n-nodes-base.hubspot",
      "typeVersion": 1,
      "position": {
        "x": 700,
        "y": 800
      },
      "credentials": {
        "hubspotAppToken": ""
      },
      "operation": "get"
    },
    {
      "parameters": {
        "functionCode": "return $input.all();"
      },
      "name": "Extract Contact Email",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": {
        "x": 900,
        "y": 800
      }
    },
    {
      "name": "Send Gmail Feedback Request",
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 1,
      "position": {
        "x": 900,
        "y": 1000
      },
      "credentials": {
        "gmailOAuth2": ""
      },
      "subject": "Feedback for your recent interaction with {{$node[\"Get HubSpot Deals\"].json[\"dealname\"]}}",
      "to": "{{$node[\"Extract Contact Email\"].json[\"email\"]}}",
      "html": "<p>Hi {{$node[\"Get Contact Details\"].json[\"firstname\"]}},</p><p>Thank you for your interest in {{$node[\"Get HubSpot Deals\"].json[\"dealname\"]}}. We noticed it has been some time since our last interaction. Could you please share your feedback?</p>"
    },
    {
      "name": "Send Slack Notification",
      "type": "n8n-nodes-base.slack",
      "typeVersion": 1,
      "position": {
        "x": 1100,
        "y": 1000
      },
      "credentials": {
        "slackOAuth2Api": ""
      },
      "message": "🚨 Deal **{{$node[\"Get HubSpot Deals\"].json[\"dealname\"]}}** has been marked as **Closed Lost** in HubSpot. Feedback requested via email."
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "Get HubSpot Deals",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get HubSpot Deals": {
      "main": [
        [
          {
            "node": "Extract Deal Fields",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Filter Cold Leads (21+ days)",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Extract Deal Fields": {
      "main": []
    },
    "Filter Cold Leads (21+ days)": {
      "main": [
        [
          {
            "node": "Update Deal to Closed Lost",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Update Deal to Closed Lost": {
      "main": [
        [
          {
            "node": "Fetch Deal Associations",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Fetch Deal Associations": {
      "main": [
        [
          {
            "node": "Extract Contact IDs",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Extract Contact IDs": {
      "main": [
        [
          {
            "node": "Get Contact Details",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get Contact Details": {
      "main": [
        [
          {
            "node": "Extract Contact Email",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Extract Contact Email": {
      "main": [
        [
          {
            "node": "Send Gmail Feedback Request",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Send Gmail Feedback Request": {
      "main": [
        [
          {
            "node": "Send Slack Notification",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

**Bước 3:** Chọn **Active** để bật workflow.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Credentials**
- **HubSpot**:
  - Đăng nhập vào [HubSpot Developer](https://developers.hubspot.com/) và tạo **App Token**.
  - Trong n8n, đi đến **Credentials** > **Add New** > Chọn **HubSpot** và nhập token.
- **Gmail**:
  - Cấp quyền OAuth 2.0 cho n8n từ [Google Cloud Console](https://console.cloud.google.com/).
  - Thêm credentials trong n8n (**Credentials** > **Add New** > **Gmail OAuth 2.0**).
- **Slack**:
  - Tạo **OAuth Token** từ [Slack API](https://api.slack.com/apps).
  - Thêm vào n8n (**Credentials** > **Add New** > **Slack OAuth 2.0 API**).

##### **B. Cấu hình Schedule Trigger**
- Đi đến node **Schedule Trigger** và chọn **Daily** (hoặc **Weekly** nếu muốn chạy ít hơn).
- Thời gian khuyến nghị: **Sáng sớm (7h-8h)** để email và Slack notification không bị spam.

##### **C. Cấu hình Filter Cold Leads**
- Node **Filter Cold Leads (21+ days)** đã được cấu hình sẵn với logic:
  ```javascript
  "conditions": [
    {
      "propertyName": "hs_lastmodifieddate",
      "operator": "lessThan",
      "values": ["21 days ago"]
    }
  ]
  ```
- **Không cần chỉnh** nếu muốn giữ mặc định (21 ngày). Nếu muốn thay đổi, chỉnh tại node **Filter**.

##### **D. Cấu hình Email & Slack**
- **Email**:
  - Nội dung email đã được cá nhân hóa với `{{$node["Get Contact Details"].json["firstname"]}}` và `{{$node["Get HubSpot Deals"].json["dealname"]}}`.
  - **Không cần chỉnh** nếu muốn giữ nguyên. Nếu muốn thay đổi, mở node **Send Gmail Feedback Request** và sửa `subject` và `html`.
- **Slack**:
  - Thông báo sẽ gửi đến **#general** (hoặc channel khác nếu cấu hình).
  - Mở node **Send Slack Notification** và chỉnh `message` nếu muốn thay đổi nội dung.

---

#### **3. Kích hoạt ⚡️**
**Bước 1:** Chạy **Test Run** với một giao dịch mẫu để kiểm tra:
- Email có được gửi không?
- Slack notification có hiển thị không?
- Giao dịch có được đóng thành *Closed Lost* không?

**Bước 2:** Sau khi test thành công, bật **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Logs cho Dữ liệu**:
   - Thêm node **Sticky Note** sau **Update Deal to Closed Lost** để ghi lại lịch sử các giao dịch được đóng.
   - **Cách làm**: Thêm node `n8n-nodes-base.stickyNote` và