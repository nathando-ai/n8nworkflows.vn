---
title: "🚀 Chuyển đổi nội dung Markdown sang khối Notion tự động với n8n"
description: "Hướng dẫn tự động hóa chuyển đổi nội dung Markdown sang định dạng khối Notion bằng workflow n8n, tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "chuyen-doi-markdown-sang-notion-tu-dong"
tags: [n8n, automation, no-code, notion, markdown]
keywords: [n8n workflow, tự động hóa, notion api, markdown to notion, chuyển đổi nội dung]
---

# 🚀 Chuyển đổi nội dung Markdown sang khối Notion tự động với n8n

[Các sếp đang gặp khó khăn khi phải chuyển đổi thủ công nội dung Markdown sang định dạng khối Notion. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian chuyển đổi nội dung thủ công
- Đảm bảo định dạng khối Notion chính xác
- Tự động hóa toàn bộ quá trình cập nhật nội dung
- Tích hợp dễ dàng với các hệ thống khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion với quyền truy cập API
- Notion API key (có thể tạo tại [Notion Integration](https://www.notion.so/my-integrations))
- ID của trang Notion cần cập nhật nội dung
- Nội dung Markdown cần chuyển đổi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io](https://n8n.io) và đăng nhập
2. Tạo một workflow mới
3. Chọn "Import from URL" và nhập link: [https://n8n.io/workflows/5675](https://n8n.io/workflows/5675)
4. Hoặc copy/paste JSON workflow sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "name": "When clicking ‘Execute workflow’",
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "name": "Mock data",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [
        550,
        300
      ],
      "parameters": {
        "values": {
          "output": {
            "value": "```markdown\n# Tiêu đề chính\n\n## Tiêu đề phụ\n\n- Danh sách 1\n- Danh sách 2\n\n[Liên kết](https://example.com)\n```"
          }
        }
      }
    },
    {
      "name": "Convert into Notion blocks",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [
        850,
        300
      ],
      "parameters": {
        "javascriptCode": "const markdown = $input.all()[0].json.output;\n\n// Chuyển đổi Markdown sang khối Notion\nconst blocks = markdown.split('\\n').map(line => {\n  if (line.startsWith('# ')) {\n    return {\n      object: 'block',\n      type: 'heading_1',\n      heading_1: {\n        rich_text: [{\n          type: 'text',\n          text: {\n            content: line.substring(2)\n          }\n        }]\n      }\n    };\n  } else if (line.startsWith('## ')) {\n    return {\n      object: 'block',\n      type: 'heading_2',\n      heading_2: {\n        rich_text: [{\n          type: 'text',\n          text: {\n            content: line.substring(3)\n          }\n        }]\n      }\n    };\n  } else if (line.startsWith('- ')) {\n    return {\n      object: 'block',\n      type: 'bulleted_list_item',\n      bulleted_list_item: {\n        rich_text: [{\n          type: 'text',\n          text: {\n            content: line.substring(2)\n          }\n        }]\n      }\n    };\n  } else if (line.startsWith('[') && line.includes('](')) {\n    const text = line.match(/^\\[(.*?)\\]/)[1];\n    const url = line.match(/\\]\\((.*?)\\)/)[1];\n    return {\n      object: 'block',\n      type: 'paragraph',\n      paragraph: {\n        rich_text: [{\n          type: 'text',\n          text: {\n            content: text,\n            link: {\n              url: url\n            }\n          }\n        }]\n      }\n    };\n  } else if (line.trim() === '') {\n    return {\n      object: 'block',\n      type: 'paragraph',\n      paragraph: {\n        rich_text: [{\n          type: 'text',\n          text: {\n            content: '\\n'\n          }\n        }]\n      }\n    };\n  } else {\n    return {\n      object: 'block',\n      type: 'paragraph',\n      paragraph: {\n        rich_text: [{\n          type: 'text',\n          text: {\n            content: line\n          }\n        }]\n      }\n    };\n  }\n});\n\nreturn [{\n  json: {\n    blocks: blocks\n  }\n}];"
      }
    },
    {
      "name": "Insert Notion page content",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        1150,
        300
      ],
      "parameters": {
        "sendQuery": true,
        "sendBody": true,
        "returnFullResponse": true,
        "options": {
          "method": "PATCH",
          "body": "{\n  \"children\": {{ $node[\"Convert into Notion blocks\"].json.blocks }}\n}",
          "headers": {
            "Authorization": "Bearer {{ $credentials.notionApi.apiKey }}",
            "Content-Type": "application/json",
            "Notion-Version": "2022-06-28"
          },
          "url": "https://api.notion.com/v1/blocks/{{ $node[\"Mock data\"].json.pageId }}"
        }
      }
    }
  ],
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Mock data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Mock data": {
      "main": [
        [
          {
            "node": "Convert into Notion blocks",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Convert into Notion blocks": {
      "main": [
        [
          {
            "node": "Insert Notion page content",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Mock data"**:
   - Thay thế nội dung Markdown mẫu trong trường `output` bằng nội dung thực tế của các sếp
   - Thêm trường `pageId` với ID của trang Notion cần cập nhật

2. **Node "Insert Notion page content"**:
   - Cấu hình credentials "notionApi" với Notion API key của các sếp
   - Thay thế `{{ $node["Mock data"].json.pageId }}` trong URL bằng ID thực tế của trang Notion hoặc biểu thức trả về ID

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với Notion API
2. Chạy test với dữ liệu mẫu
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các node khác để tự động lấy nội dung từ các nguồn khác nhau (Google Docs, WordPress, v.v.)
- Thêm node gửi thông báo qua Slack/Email khi quá trình chuyển đổi hoàn tất
- Tạo nhiều workflow khác nhau cho các định dạng Markdown khác nhau
- Lưu trữ lịch sử chuyển đổi để theo dõi thay đổi nội dung

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình chuyển đổi nội dung Markdown sang định dạng khối Notion, tiết kiệm thời gian và đảm bảo độ chính xác cao. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!