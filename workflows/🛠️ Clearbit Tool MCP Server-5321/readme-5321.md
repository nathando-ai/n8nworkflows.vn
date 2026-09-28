---
title: "🚀 Tự động hóa Clearbit với n8n: MCP Server cho AI Agents"
description: "Hướng dẫn chi tiết cách tự động hóa các công cụ Clearbit (autocomplete, enrich company/person) bằng n8n để tích hợp với AI agents một cách dễ dàng."
slug: "tu-dong-hoa-clearbit-voi-n8n-mcp-server"
tags: [n8n, automation, no-code, ai, clearbit]
keywords: [n8n workflow, tự động hóa, clearbit, ai agents, mcp server]
---

# 🚀 Tự động hóa Clearbit với n8n: MCP Server cho AI Agents

[Các sếp đang gặp khó khăn khi phải tích hợp thủ công các công cụ Clearbit (autocomplete, enrich company/person) với AI agents của mình. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách dễ dàng, không cần viết code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tích hợp thủ công với AI agents.
- Tự động hóa hoàn toàn các công cụ Clearbit (autocomplete, enrich company/person).
- Tích hợp dễ dàng với các AI agents khác nhau.
- Hoạt động liên tục 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Clearbit và API Key.
- n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/5321](https://n8n.io/workflows/5321).
3. Hoặc tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Clearbit Tool MCP Server"**: Cấu hình path là `clearbit-tool-mcp`.
- **Node "Autocomplete a company"**: Chọn operation là `autocomplete`.
- **Node "Enrich a company"**: Không cần cấu hình thêm.
- **Node "Enrich a person"**: Chọn resource là `person`.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Activate" để kích hoạt workflow.
2. Copy URL từ node "Clearbit Tool MCP Server" để sử dụng trong cấu hình AI agents.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có lỗi hoặc kết quả mới.
- Lưu log các kết quả vào Google Sheets để theo dõi lịch sử.
- Tự động gửi báo cáo định kỳ về hiệu suất của các công cụ Clearbit.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình tích hợp các công cụ Clearbit với AI agents một cách dễ dàng và hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!