---
title: "🚀 Theo dõi các công ty mới sử dụng công cụ bổ trợ với PredictLeads, Google Sheets và OpenAI"
description: "Tự động phát hiện các công ty mới sử dụng công cụ bổ trợ cho sản phẩm của bạn, tạo email tiếp cận AI và gửi tự động qua Gmail - giải pháp hoàn toàn không cần code cho marketing đồng hành."
slug: "theo-doi-cong-ty-moi-su-dung-cong-cu-bo-tro"
tags: [n8n, automation, no-code, marketing, ai, gmail, google-sheets, openai]
keywords: [n8n workflow, tự động hóa, marketing đồng hành, phát hiện công ty, email AI, PredictLeads]
---

# 🚀 Theo dõi các công ty mới sử dụng công cụ bổ trợ với PredictLeads, Google Sheets và OpenAI

[Các sếp marketing] thường gặp khó khăn khi phải theo dõi thủ công các công ty mới sử dụng công cụ bổ trợ cho sản phẩm của mình. Quá trình này tốn thời gian, dễ bỏ sót và không thể cá nhân hóa. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ phát hiện đến tiếp cận, giúp tiết kiệm thời gian và tăng hiệu quả marketing đồng hành.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động phát hiện và tiếp cận các công ty mới sử dụng công cụ bổ trợ trong vòng 24 giờ.
- **Cá nhân hóa cao**: Email tiếp cận được tạo tự động dựa trên thông tin công ty và công cụ sử dụng.
- **Dễ quản lý**: Tất cả dữ liệu được lưu trữ trong Google Sheets, dễ theo dõi và báo cáo.
- **Tăng hiệu quả**: Giảm thiểu tiếp cận trùng lặp và tập trung vào các công ty tiềm năng nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Bảng tính chứa danh sách công cụ bổ trợ và ID công nghệ từ PredictLeads.
- **Gmail OAuth2**: Tài khoản Gmail để gửi email tiếp cận.
- **OpenAI API Key**: API key để tạo email tiếp cận tự động.
- **PredictLeads API**: Tài khoản và API key từ PredictLeads.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14099](https://n8n.io/workflows/14099)
2. Nhấn nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu và nhấn "OK"

Hoặc có thể copy/paste JSON workflow sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {
        "options": {
          "every": {
            "unit": "hours",
            "value": 24
          },
          "timezone": "Asia/Ho_Chi_Minh"
        },
        "times": {
          "item": {
            "mode": "everyDay",
            "value": ""
          }
        }
      },
      "name": "⏰ Daily Schedule",
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "additionalFields": {
          "range": "A2:B",
          "valueInputOption": "RAW"
        },
        "authenticate": "serviceAccount",
        "operation": "get",
        "resource": "data",
        "spreadsheetId": "YOUR_GOOGLE_SHEET_ID"
      },
      "name": "📑 Read Complementary Tools List",
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 1,
      "position": [
        500,
        300
      ]
    },
    {
      "parameters": {
        "options": {
          "batchSize": 1
        }
      },
      "name": "🔀 Split by Tool",
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 1,
      "position": [
        750,
        300
      ]
    },
    {
      "parameters": {
        "authentication": "queryAuth",
        "headerParameters": {
          "parameters": {
            "Authorization": "={{$credentials.predictLeadsApi.apiKey}}"
          }
        },
        "method": "GET",
        "options": {
          "ignoreSslIssues": false,
          "joinData": true,
          "redirect": "follow",
          "sendBody": false,
          "sendCredentials": false,
          "sendCookies": false,
          "sendNoCacheHeader": false,
          "timeout": 30
        },
        "queryParameters": {
          "parameters": {
            "tech_id": "={{$node[\"📑 Read Complementary Tools List\"].json[0].values[0][1]}}"
          }
        },
        "resource": "https://api.predictleads.com/v1/technology/detections"
      },
      "name": "🔍 Discover Technology Adopters",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        1000,
        300
      ]
    },
    {
      "parameters": {
        "additionalFields": {
          "range": "A2:D",
          "valueInputOption": "RAW"
        },
        "authenticate": "serviceAccount",
        "operation": "get",
        "resource": "data",
        "spreadsheetId": "YOUR_GOOGLE_SHEET_ID"
      },
      "name": "📑 Read Previous Scan Data",
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 1,
      "position": [
        1250,
        300
      ]
    },
    {
      "parameters": {
        "javascriptCode": "const newAdopters = $node[\"🔍 Discover Technology Adopters\"].json[0].data;\nconst previousAdopters = $node[\"📑 Read Previous Scan Data\"].json[0].values;\n\nconst previousDomains = previousAdopters.map(row => row[0]);\n\nconst newAdoptions = newAdopters.filter(adopter => !previousDomains.includes(adopter.domain));\n\nreturn newAdoptions;"
      },
      "name": "⚙️ Compare & Detect New Adoptions",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [
        1500,
        300
      ]
    },
    {
      "parameters": {
        "conditions": {
          "boolean": {
            "comparisonOperator": "isNotEmpty",
            "value1": "={{$node[\"⚙️ Compare & Detect New Adoptions\"].json}}"
          }
        }
      },
      "name": "✅ New Adoption Detected?",
      "type": "n8n-nodes-base.if",
      "typeVersion": 1,
      "position": [
        1750,
        300
      ]
    },
    {
      "parameters": {
        "authentication": "queryAuth",
        "headerParameters": {
          "parameters": {
            "Authorization": "={{$credentials.predictLeadsApi.apiKey}}"
          }
        },
        "method": "GET",
        "options": {
          "ignoreSslIssues": false,
          "joinData": true,
          "redirect": "follow",
          "sendBody": false,
          "sendCredentials": false,
          "sendCookies": false,
          "sendNoCacheHeader": false,
          "timeout": 30
        },
        "queryParameters": {
          "parameters": {
            "domain": "={{$node[\"⚙️ Compare & Detect New Adoptions\"].json[0].domain}}"
          }
        },
        "resource": "https://api.predictleads.com/v1/company"
      },
      "name": "🔍 Enrich Company",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        2000,
        300
      ]
    },
    {
      "parameters": {
        "javascriptCode": "const company = $node[\"🔍 Enrich Company\"].json[0].data;\nconst tool = $node[\"📑 Read Complementary Tools List\"].json[0].values[0][0];\n\nconst prompt = `\\nCompany: ${company.name}\\nDomain: ${company.domain}\\nIndustry: ${company.industry}\\nEmployees: ${company.employees}\\nLocation: ${company.location}\\n\\nDetected Technology: ${tool}\\n\\nContext: This company recently adopted ${tool}, which is complementary to our product. We should consider a co-marketing partnership.\\n\\nTask: Write a personalized outreach email to ${company.name} proposing a co-marketing partnership.`;\n\nreturn prompt;"
      },
      "name": "⚙️ Build AI Prompt",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [
        2250,
        300
      ]
    },
    {
      "parameters": {
        "authentication": "queryAuth",
        "bodyParameters": {
          "parameters": {
            "messages": "=[\n  {\n    \"role\": \"system\",\n    \"content\": \"You are a helpful assistant that writes professional outreach emails.\"\n  },\n  {\n    \"role\": \"user\",\n    \"content\": \"={{$node[\"⚙️ Build AI Prompt\"].json}}\"\n  }\n]",
            "model": "gpt-3.5-turbo",
            "temperature": 0.7
          }
        },
        "headerParameters": {
          "parameters": {
            "Authorization": "Bearer {{$credentials.openAi.apiKey}}",
            "Content-Type": "application/json"
          }
        },
        "method": "POST",
        "options": {
          "ignoreSslIssues": false,
          "joinData": true,
          "redirect": "follow",
          "sendBody": true,
          "sendCredentials": false,
          "sendCookies": false,
          "sendNoCacheHeader": false,
          "timeout": 30
        },
        "resource": "https://api.openai.com/v1/chat/completions"
      },
      "name": "🤖 Draft Co-Marketing Email",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        2500,
        300
      ]
    },
    {
      "parameters": {
        "additionalFields": {
          "cc": "",
          "from": "YOUR_EMAIL@gmail.com",
          "replyTo": "",
          "subject": "={{$node[\"🤖 Draft Co-Marketing Email\"].json.choices[0].message.content.split(\"Subject:\")[1].split(\"\\n\")[0]}}"
        },
        "authenticate": "oAuth2",
        "body": "={{$node[\"🤖 Draft Co-Marketing Email\"].json.choices[0].message.content.split(\"Body:\")[1]}}",
        "operation": "send",
        "resource": "message",
        "to": "={{$node[\"🔍 Enrich Company\"].json[0].data.email}}"
      },
      "name": "📧 Send Co-Marketing Email",
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 1,
      "position": [
        2750,
        300
      ]
    },
    {
      "parameters": {
        "additionalFields": {
          "range": "A2:D",
          "valueInputOption": "RAW"
        },
        "authenticate": "serviceAccount",
        "operation": "append",
        "resource": "data",
        "spreadsheetId": "YOUR_GOOGLE_SHEET_ID",
        "values": "=[\n  [\n    \"={{$node[\"🔍 Enrich Company\"].json[0].data.domain}}\",\n    \"={{$node[\"📑 Read Complementary Tools List\"].json[0].values[0][0]}}\",\n    \"={{$moment().format('YYYY-MM-DD HH:mm:ss')}}\",\n    \"Sent\"\n  ]\n]"
      },
      "name": "📑 Update Previous Scan Data",
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 1,
      "position": [
        3000,
        300
      ]
    },
    {
      "parameters": {
        "mode": "random",
        "value": 5
      },
      "name": "Limit",
      "type": "n8n-nodes-base.limit",
      "typeVersion": 1,
      "position": [
        1750,
        500
      ]
    }
  ],
  "connections": {
    "⏰ Daily Schedule": {
      "main": [
        [
          {
            "node": "📑 Read Complementary Tools List",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "📑 Read Complementary Tools List": {
      "main": [
        [
          {
            "node": "🔀 Split by Tool",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "🔀 Split by Tool": {
      "main": [
        [
          {
            "node": "🔍 Discover Technology Adopters",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "🔍 Discover Technology Adopters": {
      "main": [
        [
          {
            "node": "📑 Read Previous Scan Data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "📑 Read Previous Scan Data": {
      "main": [
        [
          {
            "node": "⚙️ Compare & Detect New Adoptions",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "