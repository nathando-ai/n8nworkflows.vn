---
title: "🏛️ Tự động hóa báo cáo giao dịch cổ phiếu của Quốc hội Mỹ hàng ngày với Firecrawl + OpenAI + Gmail"
description: "Hướng dẫn tự động hóa quy trình theo dõi giao dịch cổ phiếu của Quốc hội Mỹ, chuyển đổi dữ liệu thô thành báo cáo tóm tắt và gửi qua email hàng ngày."
slug: "tu-dong-hoa-bao-cao-giao-dich-quoc-hoi-my"
tags: [n8n, automation, no-code, ai, firecrawl, openai, gmail]
keywords: [n8n workflow, tự động hóa, giao dịch quốc hội, firecrawl, openai, gmail]
---

# 🏛️ Tự động hóa báo cáo giao dịch cổ phiếu của Quốc hội Mỹ hàng ngày với Firecrawl + OpenAI + Gmail

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải theo dõi thủ công các giao dịch cổ phiếu của Quốc hội Mỹ? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ việc thu thập dữ liệu đến gửi báo cáo tóm tắt qua email hàng ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải theo dõi thủ công trang web Quiver Quant hàng ngày.
- **Chính xác**: Dữ liệu được xử lý tự động, giảm thiểu lỗi con người.
- **Cá nhân hóa**: Báo cáo được định dạng theo yêu cầu của các sếp.
- **Hoạt động liên tục**: Nhận báo cáo hàng ngày mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Firecrawl API Key**: Cần quyền truy cập Extract API.
- **OpenAI API Key**: Để sử dụng mô hình GPT-4o.
- **Gmail OAuth2 credentials**: Để gửi email tự động.
- **n8n**: Đã cài đặt và cấu hình sẵn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow trên n8n.io](https://n8n.io/workflows/4509).
2. Click vào nút "Import" và chọn "Import from URL".
3. Dán link workflow vào ô nhập liệu và nhấn "Import".

Hoặc có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "name": "Extract",
      "type": "httpRequest",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "name": "Get Results",
      "type": "httpRequest",
      "typeVersion": 1,
      "position": [500, 300]
    },
    {
      "name": "Edit Fields",
      "type": "set",
      "typeVersion": 1,
      "position": [750, 300]
    },
    {
      "name": "Schedule Trigger",
      "type": "scheduleTrigger",
      "typeVersion": 1,
      "position": [100, 300]
    },
    {
      "name": "Gmail",
      "type": "gmail",
      "typeVersion": 1,
      "position": [1000, 300]
    },
    {
      "name": "If",
      "type": "if",
      "typeVersion": 1,
      "position": [500, 150]
    },
    {
      "name": "Wait 15 secs",
      "type": "wait",
      "typeVersion": 1,
      "position": [375, 150]
    },
    {
      "name": "Code",
      "type": "code",
      "typeVersion": 1,
      "position": [625, 150]
    },
    {
      "name": "Wait 30 Secs",
      "type": "wait",
      "typeVersion": 1,
      "position": [875, 150]
    },
    {
      "name": "OpenAI",
      "type": "openAi",
      "typeVersion": 1,
      "position": [875, 450]
    }
  ],
  "connections": [
    {
      "node": "Schedule Trigger",
      "type": "main",
      "index": 0,
      "target": "Extract"
    },
    {
      "node": "Extract",
      "type": "main",
      "index": 0,
      "target": "Wait 15 secs"
    },
    {
      "node": "Wait 15 secs",
      "type": "main",
      "index": 0,
      "target": "Get Results"
    },
    {
      "node": "Get Results",
      "type": "main",
      "index": 0,
      "target": "If"
    },
    {
      "node": "If",
      "type": "main",
      "index": 0,
      "target": "Code"
    },
    {
      "node": "If",
      "type": "main",
      "index": 1,
      "target": "Wait 30 Secs"
    },
    {
      "node": "Wait 30 Secs",
      "type": "main",
      "index": 0,
      "target": "Get Results"
    },
    {
      "node": "Code",
      "type": "main",
      "index": 0,
      "target": "Edit Fields"
    },
    {
      "node": "Edit Fields",
      "type": "main",
      "index": 0,
      "target": "OpenAI"
    },
    {
      "node": "OpenAI",
      "type": "main",
      "index": 0,
      "target": "Gmail"
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Extract" (Firecrawl Extract API)**:
   - Cấu hình URL: `https://api.firecrawl.dev/v0/extract`
   - Method: POST
   - Headers: `Content-Type: application/json`
   - Body: JSON với các tham số sau:
     ```json
     {
       "url": "https://www.quiverquant.com/congresstrading",
       "extractorOptions": {
         "extractionPrompt": "Extract all trades over $50K in the past month. Include date, stock/asset, amount, and congress member's name and political party."
       }
     }
     ```
   - Thêm API Key vào Headers: `Authorization: Bearer YOUR_FIRECRAWL_API_KEY`

2. **Node "Get Results" (Firecrawl Get Result API)**:
   - Cấu hình URL: `https://api.firecrawl.dev/v0/scrape/status/{crawlId}`
   - Method: GET
   - Headers: `Authorization: Bearer YOUR_FIRECRAWL_API_KEY`
   - Thay thế `{crawlId}` bằng giá trị từ response của node "Extract".

3. **Node "OpenAI"**:
   - Chọn mô hình: `gpt-4o`
   - System Prompt:
     ```
     You are a helpful assistant that formats raw trading data into a readable summary. Include the date of transaction, stock/asset traded, amount, and congress member's name and political party.
     ```
   - User Prompt: `{{ $node["Get Results"].json["data"]["content"] }}`

4. **Node "Gmail"**:
   - Chọn tài khoản Gmail đã cấu hình credentials.
   - Subject: `Congress Trade Updates - {{ $now.format('MMMM DD') }}`
   - Body: `{{ $node["OpenAI"].json["choices"][0]["message"]["content"] }}`

5. **Node "Schedule Trigger"**:
   - Cấu hình lịch chạy hàng ngày (ví dụ: 6 PM).

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, click vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi báo cáo đến kênh Slack hoặc nhóm Telegram của các sếp.
- **Lưu log**: Thêm node để lưu trữ lịch sử báo cáo trong Google Sheets hoặc cơ sở dữ liệu.
- **Gửi báo cáo định kỳ**: Thay đổi lịch trình để gửi báo cáo hàng tuần hoặc hàng tháng.
- **Tùy chỉnh báo cáo**: Điều chỉnh prompt của OpenAI để phù hợp với nhu cầu cụ thể của các sếp.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc theo dõi giao dịch cổ phiếu của Quốc hội Mỹ. Với việc tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến gửi báo cáo, các sếp có thể tập trung vào việc phân tích và đưa ra quyết định dựa trên dữ liệu chính xác và cập nhật. Hãy áp dụng ngay workflow này để nhận báo cáo hàng ngày về các giao dịch cổ phiếu của Quốc hội Mỹ!