---
title: "🚀 Tự động hóa báo cáo CVE từ NVD với tóm tắt AI và gửi qua Gmail"
description: "Hướng dẫn tự động hóa nhận thông tin CVE từ NVD, xử lý bằng AI và gửi báo cáo tóm tắt qua Gmail mỗi 30 phút - giải pháp tối ưu cho quản lý an ninh thông tin"
slug: "tu-dong-hoa-bao-cao-cve-tu-nvd-voi-tom-tat-ai-va-gmail"
tags: [n8n, automation, no-code, an-ninh-thong-tin, ai, nvd, gmail]
keywords: [n8n workflow, tự động hóa báo cáo CVE, AI tóm tắt, NVD, Gmail, an ninh thông tin]
---

# 🚀 Tự động hóa báo cáo CVE từ NVD với tóm tắt AI và gửi qua Gmail

[Các sếp quản lý an ninh thông tin thường phải đối mặt với hàng trăm báo cáo CVE hàng ngày từ NVD. Việc đọc và phân tích thủ công những thông tin này không chỉ tốn thời gian mà còn dễ bỏ sót những điểm quan trọng. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình: lấy dữ liệu từ NVD, xử lý bằng AI để tóm tắt thông tin quan trọng và gửi báo cáo qua Gmail một cách định kỳ.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình xử lý hàng trăm CVE hàng ngày
- **Tăng cường an ninh**: Nhận thông tin tóm tắt chính xác về các lỗ hổng quan trọng
- **Tích hợp AI**: Sử dụng công nghệ trí tuệ nhân tạo để phân tích và tóm tắt thông tin
- **Quản lý tập trung**: Tất cả báo cáo được gửi đến một email duy nhất
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để nhận báo cáo
- API Key từ NVD (National Vulnerability Database)
- API Key từ OpenAI để sử dụng dịch vụ tóm tắt
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hãy sao chép JSON dưới đây và dán vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {
        "authentication": "oAuth2",
        "operation": "sendEmail",
        "resource": "message",
        "to": "your-email@gmail.com",
        "subject": "Daily CVE Digest",
        "body": "= {{ $node[\"OpenAI Email Crafter\"].json[\"choices\"][0][\"message\"][\"content\"] }}"
      },
      "name": "Send a message",
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 1,
      "position": [
        1000,
        400
      ]
    },
    {
      "parameters": {
        "method": "GET",
        "url": "https://services.nvd.nist.gov/rest/json/cves/2.0?resultsPerPage=100",
        "headers": {
          "apiKey": "{{$credentials.nvdApi.apiKey}}"
        }
      },
      "name": "HTTP Request",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        800,
        200
      ]
    },
    {
      "parameters": {
        "times": {
          "item": {
            "mode": "everyMinute",
            "every": 30
          }
        }
      },
      "name": "Schedule Trigger",
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1,
      "position": [
        600,
        200
      ]
    },
    {
      "parameters": {
        "code": "const data = $input.all()[0].json;\n\nconst cves = data.vulnerabilities.map(vuln => ({\n  id: vuln.cve.id,\n  description: vuln.cve.descriptions[0].value,\n  severity: vuln.cve.metrics.cvssMetricV2[0]?.cvssData.baseSeverity || 'UNKNOWN'\n}));\n\nreturn cves;"
      },
      "name": "Parse NVD",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [
        800,
        400
      ]
    },
    {
      "parameters": {
        "code": "const cves = $input.all()[0];\n\nconst digest = cves.map(cve => {\n  return `**${cve.id}** (${cve.severity}): ${cve.description}`;\n}).join('\\n\\n');\n\nreturn { digest };"
      },
      "name": "Build Digest",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [
        800,
        600
      ]
    },
    {
      "parameters": {
        "model": "gpt-4o-mini",
        "messages": [
          {
            "role": "system",
            "content": "You are a helpful assistant that summarizes CVE information."
          },
          {
            "role": "user",
            "content": "Please summarize the following CVE information in a concise and professional manner:\n\n{{ $node[\"Build Digest\"].json[\"digest\"] }}"
          }
        ],
        "temperature": 0.7,
        "maxTokens": 1000
      },
      "name": "OpenAI Email Crafter",
      "type": "@n8n/n8n-nodes-langchain.openAi",
      "typeVersion": 1,
      "position": [
        800,
        800
      ]
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "HTTP Request",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTTP Request": {
      "main": [
        [
          {
            "node": "Parse NVD",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Parse NVD": {
      "main": [
        [
          {
            "node": "Build Digest",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Build Digest": {
      "main": [
        [
          {
            "node": "OpenAI Email Crafter",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Email Crafter": {
      "main": [
        [
          {
            "node": "Send a message",
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
    "saveDataSuccessExecution": "all",
    "saveManualExecutions": false,
    "executionTimeout": 3600,
    "timezone": "Asia/Ho_Chi_Minh"
  }
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Send a message" (Gmail)**:
   - Cấu hình credentials Gmail OAuth2
   - Thay đổi địa chỉ email nhận báo cáo trong tham số "to"

2. **Node "HTTP Request"**:
   - Thêm API Key từ NVD vào credentials
   - Có thể điều chỉnh số lượng CVE mỗi lần lấy bằng cách thay đổi tham số "resultsPerPage" trong URL

3. **Node "Schedule Trigger"**:
   - Có thể thay đổi tần suất chạy từ 30 phút sang khác (hàng ngày, hàng tuần...)

4. **Node "OpenAI Email Crafter"**:
   - Cấu hình credentials OpenAI API
   - Có thể điều chỉnh model (gpt-4o-mini, gpt-4, gpt-3.5-turbo...) và các tham số khác

#### 3. Kích hoạt ⚡️
- Sau khi cấu hình xong, hãy test run workflow với dữ liệu mẫu
- Khi đã chạy ổn định, bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi báo cáo đến các kênh chat của nhóm
2. **Lưu log**: Thêm node lưu trữ các báo cáo đã gửi để theo dõi lịch sử
3. **Báo cáo định kỳ**: Có thể điều chỉnh để gửi báo cáo hàng ngày, hàng tuần hoặc theo yêu cầu
4. **Phân loại CVE**: Nâng cao node "Parse NVD" để phân loại CVE theo mức độ nghiêm trọng

### 📌 Kết luận
Workflow này giúp các sếp quản lý an ninh thông tin tự động hóa quy trình quan trọng, giảm thiểu thời gian xử lý và tăng cường khả năng phản ứng với các lỗ hổng bảo mật. Hãy áp dụng ngay để nâng cao hiệu quả quản lý an ninh thông tin của tổ chức!