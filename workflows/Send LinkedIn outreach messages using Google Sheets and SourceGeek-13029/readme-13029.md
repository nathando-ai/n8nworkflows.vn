---
title: "🚀 Tự Động Hóa Gửi Tin Nhắn LinkedIn từ Google Sheets với SourceGeek"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n để tự động gửi tin nhắn kết nối (Outreach) trên LinkedIn hàng loạt từ dữ liệu Google Sheets, sử dụng SourceGeek để đảm bảo an toàn tài khoản."
slug: "tu-dong-gui-tin-nhan-linkedin-google-sheets-sourcegeek"
tags: [n8n, automation, linkedin, lead-nurturing, sourcegeek, google-sheets]
keywords: [n8n workflow linkedin, tự động hóa outreach, sourcegeek n8n, gửi tin nhắn linkedin hàng loạt, lead nurturing n8n]
---

# 🚀 Tự Động Hóa Gửi Tin Nhắn LinkedIn từ Google Sheets với SourceGeek

Trong lĩnh vực Sales và Marketing, việc kết nối và gửi tin nhắn (Outreach) cho các ứng viên tiềm năng hoặc khách hàng mục tiêu trên LinkedIn là một phần không thể thiếu. Tuy nhiên, làm việc này thủ công là cực kỳ tốn thời gian, dễ gây sai sót và quan trọng nhất là **rủi ro bị LinkedIn hạn chế tài khoản (Shadowban)** do thao tác quá nhanh hoặc lặp lại.

Workflow này được thiết kế để giải quyết triệt để nỗi đau đó. Bằng cách kết hợp **Google Sheets** (làm cơ sở dữ liệu), **SourceGeek** (công cụ chuyên dụng để tương tác LinkedIn an toàn) và **n8n** (động cơ tự động hóa), các sếp có thể tự động hóa toàn bộ quy trình gửi tin nhắn đầu tiên (1st message) một cách có kiểm soát, chính xác và an toàn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần gửi tin nhắn theo lịch hoặc hàng loạt, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian khổng lồ:** Tự động hóa quy trình gửi tin nhắn, các sếp chỉ cần tập trung vào việc chuẩn bị nội dung và danh sách mục tiêu.
- **An toàn tài khoản LinkedIn:** Sử dụng SourceGeek giúp mô phỏng hành vi người dùng và kiểm soát tốc độ gửi, giảm thiểu rủi ro bị khóa tài khoản so với các script tự viết.
- **Dữ liệu minh bạch & Theo dõi được:** Mỗi tin nhắn được gửi sẽ tự động cập nhật timestamp (thời gian gửi) ngay trên Google Sheets, giúp dễ dàng thống kê và quản lý pipeline.
- **Linh hoạt & Dễ mở rộng:** Có thể dễ dàng thêm các bước chờ (Wait) hoặc logic phức tạp hơn trong n8n để tối ưu chiến dịch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Cloud hoặc Self-hosted.
2. **Tài khoản Google:** Để kết nối Google Sheets (OAuth2).
3. **Tài khoản SourceGeek:** Đăng ký và lấy API Key từ [SourceGeek](https://sourcegeek.io/).
4. **Tài khoản LinkedIn:** Đã được liên kết với SourceGeek.
5. **Google Sheet mẫu:** Chứa các cột dữ liệu cần thiết (tham khảo cấu trúc bên dưới).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [link gốc trên n8n.io](https://n8n.io/workflows/13029) hoặc copy toàn bộ code JSON bên dưới và dán vào n8n Editor.

```json
{
  "name": "Send LinkedIn outreach messages using Google Sheets and SourceGeek",
  "nodes": [
    {
      "parameters": {},
      "id": "manual-trigger-id",
      "name": "When clicking ‘Execute workflow’",
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "batchSize": 1
      },
      "id": "split-batches-id",
      "name": "Loop Over Items",
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 3,
      "position": [470, 300]
    },
    {
      "parameters": {
        "operation": "read",
        "documentId": {
          "__rl": true,
          "mode": "list",
          "value": "YOUR_GOOGLE_SHEET_ID"
        },
        "sheetName": {
          "__rl": true,
          "mode": "list",
          "value": "Sheet1"
        },
        "options": {}
      },
      "id": "google-sheets-read-id",
      "name": "Get row(s) in sheet",
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [690, 300],
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "YOUR_CREDENTIAL_ID",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "operation": "sendMessage",
        "profileUrl": "={{ $json['LinkedIn Profile URL'] }}",
        "message": "={{ $json['1st Message'] }}"
      },
      "id": "sourcegeek-send-id",
      "name": "Send message to LinkedIn profile",
      "type": "n8n-nodes-sourcegeek.sourcegeek",
      "typeVersion": 1,
      "position": [910, 300],
      "credentials": {
        "sourcegeekCredentialsApi": {
          "id": "YOUR_CREDENTIAL_ID",
          "name": "SourceGeek account"
        }
      }
    },
    {
      "parameters": {
        "amount": 1,
        "unit": "minutes"
      },
      "id": "wait-node-id",
      "name": "Wait 1 minute before the next message is send",
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [1130, 300]
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "mode": "list",
          "value": "YOUR_GOOGLE_SHEET_ID"
        },
        "sheetName": {
          "__rl": true,
          "mode": "list",
          "value": "Sheet1"
        },
        "columns": {
          "mappingMode": "autoMapInputData",
          "value": {
            "Timestamp": "={{ $json['timestamp'] }}"
          },
          "matchingColumns": [],
          "schema": []
        },
        "options": {}
      },
      "id": "google-sheets-update-id",
      "name": "Update selected row in sheet with timestamp",
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [1350, 300],
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "YOUR_CREDENTIAL_ID",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "const timestamp = new Date().toISOString();\nreturn [{ json: { timestamp } }];"
      },
      "id": "code-node-id",
      "name": "JS code to generate timestamp",
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [1130, 450]
    }
  ],
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Loop Over Items": {
      "main": [
        [
          {
            "node": "Get row(s) in sheet",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Send message to LinkedIn profile",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get row(s) in sheet": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Send message to LinkedIn profile": {
      "main": [
        [
          {
            "node": "Wait 1 minute before the next message is send",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Wait 1 minute before the next message is send": {
      "main": [
        [
          {
            "node": "JS code to generate timestamp",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "JS code to generate timestamp": {
      "main": [
        [
          {
            "node": "Update selected row in sheet with timestamp",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Update selected row in sheet with timestamp": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "pinData": {}
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Sau khi import, các sếp cần thực hiện các bước cấu hình sau để workflow hoạt động đúng:

**1. Cấu hình Google Sheets (Node: `Get row(s) in sheet` & `Update selected row in sheet with timestamp`)**
*   **Credentials:** Chọn hoặc tạo credential Google Sheets OAuth2.
*   **Document ID:** Chọn đúng Google Sheet chứa danh sách mục tiêu.
*   **Sheet Name:** Chọn đúng tên Sheet (ví dụ: `Sheet1`).
*   **Cấu trúc dữ liệu:** Đảm bảo Google Sheet của bạn có các cột sau (tên cột phải khớp với tham số trong node):
    *   `LinkedIn Profile URL`: Link hồ sơ LinkedIn của người nhận.
    *   `1st Message`: Nội dung tin nhắn muốn gửi.
    *   `Timestamp`: Cột trống để workflow tự động điền thời gian gửi.

**2. Cấu hình SourceGeek (Node: `Send message to LinkedIn profile`)**
*   **Credentials:** Chọn hoặc tạo credential SourceGeek.
*   **Profile URL:** Tham chiếu đến cột `LinkedIn Profile URL` từ Google Sheets.
*   **Message:** Tham chiếu đến cột `1st Message` từ Google Sheets.
*   **Lưu ý:** SourceGeek yêu cầu tài khoản LinkedIn của bạn đã được liên kết và đồng bộ. Hãy đảm bảo bạn có đủ hạn mức gửi tin nhắn trong gói SourceGeek của mình.

**3. Điều chỉnh thời gian chờ (Node: `Wait 1 minute before the next message is send`)**
*   Mặc định workflow chờ **1 phút** giữa mỗi tin nhắn.
*   **Khuyến nghị:** Để an toàn tối đa, các sếp nên tăng thời gian chờ lên **2-5 phút** hoặc thêm yếu tố ngẫu nhiên (nếu n8n hỗ trợ trong phiên bản mới) để mô phỏng hành vi con người tốt hơn.

**4. Kiểm tra Logic Loop (Node: `Loop Over Items`)**
*   Node `SplitInBatches` với `batchSize: 1` đảm bảo mỗi lần chỉ xử lý 1 dòng dữ liệu.
*   Sau khi gửi tin nhắn và cập nhật timestamp, workflow sẽ quay lại vòng lặp để lấy dòng tiếp theo cho đến khi hết dữ liệu.

#### 3. Kích hoạt