---
title: "🚀 Tự động ghi tất cả vé Linear vào Google Sheets hàng ngày"
description: "Hướng dẫn tự động hóa việc đồng bộ tất cả vé công việc từ Linear sang Google Sheets hàng ngày, tiết kiệm thời gian và nâng cao hiệu quả quản lý dự án."
slug: "tu-dong-ghi-ve-linear-vao-google-sheets"
tags: [n8n, automation, no-code, linear, google-sheets]
keywords: [n8n workflow, tự động hóa, quản lý dự án, linear, google sheets]
---

# 🚀 Tự động ghi tất cả vé Linear vào Google Sheets hàng ngày

[Các sếp đang làm việc với nhiều dự án trên Linear nhưng vẫn phải thủ công ghi lại thông tin vào Google Sheets? Hãy để workflow này tự động hóa quy trình này hàng ngày vào lúc 6:00 sáng. Workflow này sẽ tự động lấy tất cả vé công việc của team, xử lý dữ liệu và ghi vào Google Sheets một cách chính xác và liên tục.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình ghi vé hàng ngày.
- Chính xác: Dữ liệu được đồng bộ chính xác từ Linear sang Google Sheets.
- Cá nhân hóa: Có thể tùy chỉnh các trường dữ liệu theo nhu cầu.
- Hoạt động liên tục: Workflow chạy tự động hàng ngày vào lúc 6:00 sáng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Linear với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets.
- API Key của Linear.
- Thông tin xác thực Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/2148`.
4. Nhấn "Import".

Hoặc có thể copy/paste JSON sau vào n8n Editor:
```json
{
  "nodes": [
    {
      "name": "Every day at 06:00",
      "type": "scheduleTrigger",
      "parameters": {
        "options": {
          "schedule": {
            "hour": 6,
            "minute": 0,
            "dayOfMonth": "*",
            "month": "*",
            "dayOfWeek": "*"
          }
        }
      }
    },
    {
      "name": "Get all your team's tickets",
      "type": "graphql",
      "parameters": {
        "options": {
          "graphqlEndpoint": "https://api.linear.app/graphql",
          "query": "query Issues($after: String) {\n  issues(after: $after, filter: { team: { name: { eq: \"Adore\" } } }) {\n    nodes {\n      id\n      title\n      description\n      priority\n      state {\n        name\n      }\n      labels {\n        nodes {\n          name\n        }\n      }\n      assignee {\n        name\n      }\n      createdAt\n      updatedAt\n    }\n    pageInfo {\n      hasNextPage\n      endCursor\n    }\n  }\n}\n",
          "variables": "{\n  \"after\": \"\"\n}"
        }
      },
      "credentials": [
        {
          "name": "httpHeaderAuth",
          "id": "your-linear-api-key"
        }
      ]
    },
    {
      "name": "if has next page",
      "type": "if",
      "parameters": {
        "conditions": {
          "boolean": {
            "operation": "isTrue",
            "value": "={{ $node[\"Get all your team's tickets\"].json.issues.pageInfo.hasNextPage }}"
          }
        }
      }
    },
    {
      "name": "Get end cursor",
      "type": "set",
      "parameters": {
        "values": {
          "endCursor": "={{ $node[\"Get all your team's tickets\"].json.issues.pageInfo.endCursor }}"
        }
      }
    },
    {
      "name": "Get next page",
      "type": "graphql",
      "parameters": {
        "options": {
          "graphqlEndpoint": "https://api.linear.app/graphql",
          "query": "query Issues($after: String) {\n  issues(after: $after, filter: { team: { name: { eq: \"Adore\" } } }) {\n    nodes {\n      id\n      title\n      description\n      priority\n      state {\n        name\n      }\n      labels {\n        nodes {\n          name\n        }\n      }\n      assignee {\n        name\n      }\n      createdAt\n      updatedAt\n    }\n    pageInfo {\n      hasNextPage\n      endCursor\n    }\n  }\n}\n",
          "variables": "{\n  \"after\": \"{{ $node[\"Get end cursor\"].json.endCursor }}\"\n}"
        }
      },
      "credentials": [
        {
          "name": "httpHeaderAuth",
          "id": "your-linear-api-key"
        }
      ]
    },
    {
      "name": "Split out the tickets",
      "type": "splitOut",
      "parameters": {
        "options": {
          "inputDataFieldName": "issues.nodes"
        }
      }
    },
    {
      "name": "Set custom fields",
      "type": "set",
      "parameters": {
        "values": {
          "labels": "={{ $node[\"Split out the tickets\"].json.labels.nodes.map(label => label.name).join(', ') }}",
          "estimate": "1"
        }
      }
    },
    {
      "name": "Write tickets to Sheets",
      "type": "googleSheets",
      "parameters": {
        "options": {
          "operation": "appendOrUpdate",
          "spreadsheetId": "your-spreadsheet-id",
          "range": "Sheet1!A:Z",
          "data": "={{ $node[\"Set custom fields\"].json }}"
        }
      },
      "credentials": [
        {
          "name": "googleSheetsOAuth2Api",
          "id": "your-google-sheets-credentials"
        }
      ]
    },
    {
      "name": "Flatten object to have simple fields to filter by",
      "type": "code",
      "parameters": {
        "options": {
          "code": "const items = $input.all();\n\nconst flattenedItems = items.map(item => {\n  const flattenedItem = { ...item };\n  \n  // Flatten labels\n  if (item.labels && item.labels.nodes) {\n    flattenedItem.labels = item.labels.nodes.map(label => label.name).join(', ');\n  }\n  \n  // Flatten state\n  if (item.state) {\n    flattenedItem.state = item.state.name;\n  }\n  \n  // Flatten assignee\n  if (item.assignee) {\n    flattenedItem.assignee = item.assignee.name;\n  }\n  \n  return flattenedItem;\n});\n\nreturn flattenedItems;"
        }
      }
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get all your team's tickets"**:
   - Chọn credentials "httpHeaderAuth" đã được cấu hình với API Key của Linear.
   - Trong phần query, thay đổi tên team từ "Adore" thành tên team của các sếp (ví dụ: "Our Team").

2. **Node "Get next page"**:
   - Chọn credentials "httpHeaderAuth" đã được cấu hình với API Key của Linear.

3. **Node "Write tickets to Sheets"**:
   - Chọn credentials "googleSheetsOAuth2Api" đã được cấu hình.
   - Thay đổi "your-spreadsheet-id" thành ID của Google Sheet mà các sếp muốn ghi dữ liệu.
   - Thay đổi "Sheet1!A:Z" thành phạm vi cụ thể của sheet (ví dụ: "Tickets!A:Z").

4. **Node "Set custom fields"**:
   - Có thể tùy chỉnh các trường dữ liệu như "labels" và "estimate" theo nhu cầu.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Node" để test run dữ liệu mẫu.
2. Sau khi test thành công, nhấn vào nút "Activate Workflow" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có vé mới được ghi vào Google Sheets.
- Lưu log các lần chạy workflow để theo dõi lịch sử.
- Gửi báo cáo định kỳ về các vé đã được ghi vào Google Sheets.

### 📌 Kết luận
Workflow này sẽ tự động hóa việc ghi tất cả vé công việc từ Linear vào Google Sheets hàng ngày, giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả quản lý dự án. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!