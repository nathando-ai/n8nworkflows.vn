---
title: "🛡️ Tự động hóa kiểm thử bảo mật WAF với AI Agent và WAFtester MCP"
description: "Hướng dẫn tự động hóa kiểm thử bảo mật WAF thông qua AI Agent và WAFtester MCP trên n8n. Tiết kiệm thời gian và nâng cao hiệu quả kiểm thử bảo mật."
slug: "tu-dong-hoa-kiem-thu-bao-mat-waf-voi-ai-agent-waftester-mcp"
tags: [n8n, automation, secops, ai-chatbot, waftester, mcp]
keywords: [n8n workflow, tự động hóa bảo mật, kiểm thử WAF, AI Agent, WAFtester MCP]
---

# 🛡️ Tự động hóa kiểm thử bảo mật WAF với AI Agent và WAFtester MCP

[Các sếp bảo mật đang gặp khó khăn khi phải thực hiện kiểm thử bảo mật WAF thủ công, tốn thời gian và dễ bỏ sót. Workflow này giúp tự động hóa toàn bộ quy trình kiểm thử WAF thông qua AI Agent và WAFtester MCP trên n8n, mang lại kết quả chính xác và hiệu quả cao.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian kiểm thử WAF lên tới 80%
- Kết quả kiểm thử chính xác và chi tiết hơn thủ công
- Tự động hóa quy trình kiểm thử bảo mật liên tục
- Tích hợp 18 công cụ kiểm thử bảo mật của WAFtester
- Tạo báo cáo bảo mật tự động với đánh giá điểm số
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để sử dụng AI Agent)
- Docker (để chạy WAFtester MCP server)
- URL của ứng dụng web cần kiểm thử bảo mật
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/13443)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu và nhấn "Import"

Hoặc bạn có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "name": "Chat Trigger",
      "type": "chatTrigger"
    },
    {
      "name": "AI Agent",
      "type": "agent"
    },
    {
      "name": "WAFtester MCP",
      "type": "mcpClientTool"
    },
    {
      "name": "OpenAI Chat Model",
      "type": "lmChatOpenAi",
      "credentials": [
        "openAiApi"
      ]
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **OpenAI Chat Model**:
   - Click vào node này và chọn credentials OpenAI API đã tạo
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng

2. **WAFtester MCP**:
   - Chạy WAFtester MCP server bằng lệnh:
     ```
     docker run -p 8080:8080 ghcr.io/waftester/waftester:latest mcp --http :8080
     ```
   - Nếu WAFtester chạy trên máy chủ khác, hãy thiết lập biến môi trường `WAFTESTER_SSE_URL` với địa chỉ IP của máy chủ đó

3. **AI Agent**:
   - Tùy chỉnh prompt hệ thống trong node này nếu cần
   - Ví dụ: "Scan https://example.com for SQLi and XSS"

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Bật Active workflow
3. Mở giao diện chat và bắt đầu kiểm thử

### ✍️ Mẹo & gợi ý nâng cao
- Thử các câu lệnh như: "Scan https://example.com for SQLi and XSS" hoặc "Find WAF bypasses for https://example.com"
- Kết hợp với Slack/Telegram để nhận thông báo kết quả kiểm thử
- Lưu log kiểm thử vào Google Sheets hoặc cơ sở dữ liệu
- Tự động gửi báo cáo bảo mật định kỳ qua email

### 📌 Kết luận
Workflow này giúp các sếp bảo mật tự động hóa toàn bộ quy trình kiểm thử WAF, từ phát hiện WAF đến tạo báo cáo bảo mật hoàn chỉnh. Bằng cách tích hợp AI Agent và WAFtester MCP, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao hiệu quả kiểm thử bảo mật. Hãy áp dụng ngay để nâng cao năng lực bảo mật của tổ chức!