---
title: "🎬 Tự động hóa tổng kết video YouTube trong Slack bằng AssemblyAI và OpenAI"
description: "Hướng dẫn tự động hóa quy trình tổng kết video YouTube trong Slack bằng n8n, tiết kiệm thời gian và nâng cao hiệu quả làm việc"
slug: "tu-dong-hoa-tong-ket-video-youtube-trong-slack"
tags: [n8n, automation, no-code, ai, slack]
keywords: [n8n workflow, tự động hóa, tổng kết video, assemblyai, openai]
---

# 🎬 Tự động hóa tổng kết video YouTube trong Slack bằng AssemblyAI và OpenAI

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải xem hàng loạt video YouTube để tìm thông tin quan trọng? Với workflow này, các sếp có thể tự động hóa quy trình tổng kết video YouTube trong Slack, tiết kiệm thời gian và nâng cao hiệu quả làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động tổng kết video YouTube trong Slack mà không cần phải xem từng video.
- Tăng hiệu quả làm việc: Nhận thông tin quan trọng từ video một cách nhanh chóng và chính xác.
- Cá nhân hóa: Tùy chỉnh độ dài video và nội dung tổng kết theo nhu cầu của từng dự án.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền tạo slash command.
- API Key của YouTube Data API.
- API Key của AssemblyAI.
- API Key của OpenAI.
- Tài khoản RapidAPI (để sử dụng các API chuyển đổi video sang audio).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/12934).
2. Click vào nút "Import" và chọn "Import from URL".
3. Dán link workflow vào ô nhập liệu và click "Import".

Hoặc có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {
        "javascriptCode": "const videoUrl = $input.all()[0].json.text;\nconst videoId = videoUrl.split('v=')[1].split('&')[0];\nreturn [{json: {videoId: videoId}}];"
      },
      "name": "Extract YouTube video ID",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [
        110,
        100
      ]
    },
    {
      "parameters": {
        "authentication": "predefinedCredentialType",
        "nodeVersion": "2.2",
        "options": {
          "headers": {
            "X-RapidAPI-Key": "={{$credentials.httpHeaderAuth.apiKey}}",
            "X-RapidAPI-Host": "youtube-video-download-info.p.rapidapi.com"
          }
        },
        "resource": "video",
        "operation": "get",
        "url": "https://youtube-video-download-info.p.rapidapi.com/dl?id={{$node[\"Extract YouTube video ID\"].json[\"videoId\"]}}"
      },
      "name": "Check Video Duration",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        350,
        100
      ]
    },
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "sift",
        "responseCode": "200",
        "responseData": "{\"status\":\"ok\"}",
        "responseMode": "lastNode"
      },
      "name": "Receive Slack command",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [
        -130,
        100
      ]
    },
    {
      "parameters": {
        "options": {
          "dataMapping": {
            "value": {
              "value": "={{$input.all()[0].json.text}}"
            }
          }
        }
      },
      "name": "Normalize Slack payload",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [
        -10,
        100
      ]
    },
    {
      "parameters": {
        "conditions": {
          "boolean": {
            "comparisonOperator": "isLessThan",
            "value1": "={{$node[\"Check Video Duration\"].json[\"lengthSeconds\"]}}",
            "value2": "3600"
          }
        }
      },
      "name": "Is video longer than limit?",
      "type": "n8n-nodes-base.if",
      "typeVersion": 1,
      "position": [
        590,
        100
      ]
    },
    {
      "parameters": {
        "authentication": "predefinedCredentialType",
        "nodeVersion": "2.2",
        "options": {
          "headers": {
            "X-RapidAPI-Key": "={{$credentials.httpHeaderAuth.apiKey}}",
            "X-RapidAPI-Host": "youtube-mp36.p.rapidapi.com"
          }
        },
        "resource": "video",
        "operation": "get",
        "url": "https://youtube-mp36.p.rapidapi.com/dl?id={{$node[\"Extract YouTube video ID\"].json[\"videoId\"]}}"
      },
      "name": "Convert YouTube video to MP3",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        830,
        100
      ]
    },
    {
      "parameters": {
        "authentication": "predefinedCredentialType",
        "nodeVersion": "2.2",
        "options": {
          "headers": {
            "authorization": "={{$credentials.httpHeaderAuth.apiKey}}"
          }
        },
        "resource": "transcript",
        "operation": "post",
        "url": "https://api.assemblyai.com/v2/transcript"
      },
      "name": "Start transcription job",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        1070,
        100
      ]
    },
    {
      "parameters": {
        "authentication": "predefinedCredentialType",
        "nodeVersion": "2.2",
        "options": {
          "headers": {
            "authorization": "={{$credentials.httpHeaderAuth.apiKey}}"
          }
        },
        "resource": "transcript",
        "operation": "post",
        "url": "https://api.assemblyai.com/v2/upload"
      },
      "name": "Submit audio for transcription",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        1310,
        100
      ]
    },
    {
      "parameters": {
        "mode": "random",
        "waitTime": {
          "unit": "seconds",
          "value": 30
        }
      },
      "name": "Wait for transcription processing",
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1,
      "position": [
        1550,
        100
      ]
    },
    {
      "parameters": {
        "authentication": "predefinedCredentialType",
        "nodeVersion": "2.2",
        "options": {
          "headers": {
            "authorization": "={{$credentials.httpHeaderAuth.apiKey}}"
          }
        },
        "resource": "transcript",
        "operation": "get",
        "url": "https://api.assemblyai.com/v2/transcript/{{$node[\"Start transcription job\"].json[\"id\"]}}"
      },
      "name": "Check transcription status",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        1790,
        100
      ]
    },
    {
      "parameters": {
        "javascriptCode": "const transcript = $input.all()[0].json.text;\nreturn [{json: {transcript: transcript}}];"
      },
      "name": "Extract transcript text",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [
        2030,
        100
      ]
    },
    {
      "parameters": {
        "conditions": {
          "boolean": {
            "comparisonOperator": "isEqual",
            "value1": "={{$node[\"Check transcription status\"].json[\"status\"]}}",
            "value2": "completed"
          }
        }
      },
      "name": "Is transcription complete?",
      "type": "n8n-nodes-base.if",
      "typeVersion": 1,
      "position": [
        2270,
        100
      ]
    },
    {
      "parameters": {
        "model": "gpt-3.5-turbo",
        "prompt": "Summarize the following text in bullet points:\n\n{{$node[\"Extract transcript text\"].json[\"transcript\"]}}",
        "temperature": 0.7
      },
      "name": "Generate AI summary",
      "type": "@n8n/n8n-nodes-langchain.openAi",
      "typeVersion": 1,
      "position": [
        2510,
        100
      ]
    },
    {
      "parameters": {
        "authentication": "predefinedCredentialType",
        "nodeVersion": "2.2",
        "options": {
          "headers": {
            "Content-type": "application/json"
          }
        },
        "resource": "slack",
        "operation": "post",
        "url": "={{$node[\"Receive Slack command\"].json[\"response_url\"]}}"
      },
      "name": "Post result to Slack",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        2750,
        100
      ]
    }
  ],
  "connections": {
    "Receive Slack command": {
      "main": [
        [
          {
            "node": "Normalize Slack payload",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Normalize Slack payload": {
      "main": [
        [
          {
            "node": "Extract YouTube video ID",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Extract YouTube video ID": {
      "main": [
        [
          {
            "node": "Check Video Duration",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Check Video Duration": {
      "main": [
        [
          {
            "node": "Is video longer than limit?",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Is video longer than limit?": {
      "main": [
        [
          {
            "node": "Convert YouTube video to MP3",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Convert YouTube video to MP3": {
      "main": [
        [
          {
            "node": "Start transcription job",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Start transcription job": {
      "main": [
        [
          {
            "node": "Submit audio for transcription",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Submit audio for transcription": {
      "main": [
        [
          {
            "node": "Wait for transcription processing",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Wait for transcription processing": {
      "main": [
        [
          {
            "node": "Check transcription status",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Check transcription status": {
      "main": [
        [
          {
            "node": "Extract transcript text",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Extract transcript text": {
      "main": [
        [
          {
            "node": "Is transcription complete?",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Is transcription complete?": {
      "main": [
        [
          {
            "node": "Generate AI summary",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Generate AI summary": {
      "main": [
        [
          {
            "node": "Post result to Slack",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "settings": {
    "saveDataErrorExecution": "all",
    "saveDataManualExecutions": false,
    "saveDataSuccessExecution": "none",
    "executionTimeout": 3600,
    "timezone": ""
  },
  "name": "Summarize YouTube videos in Slack using AssemblyAI transcription and OpenAI",
  "nodes": [
    "Receive Slack command",
    "Normalize Slack payload",
    "Extract YouTube video ID",
    "Check Video Duration",
    "Is video longer than limit?",
    "Convert YouTube video to MP3",
    "Start transcription job",
    "Submit audio for transcription",
    "Wait for transcription processing",
    "Check transcription status",
    "Extract transcript text",
    "Is transcription complete?",
    "Generate AI summary",
    "Post result to Slack"
  ],
  "active": false,
  "nodeTypes": {
    "n8n-nodes-base.code": {
      "sourcePath": "",
      "version": ""
    },
    "n8n-nodes-base.httpRequest": {
      "sourcePath": "",
      "version": ""
    },
    "n8n-nodes-base.webhook": {
      "sourcePath": "",
      "version": ""
    },
    "n8n-nodes-base.set": {
      "sourcePath": "",
      "version": ""
    },
    "n8n-nodes-base.if