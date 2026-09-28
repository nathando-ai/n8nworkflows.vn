---
title: "💥🛠️ Xây dựng Chatbot Tìm kiếm Web với GPT-4o và Brave Search"
description: "Hướng dẫn tự động hóa chatbot tìm kiếm thông tin web sử dụng GPT-4o và Brave Search API, tiết kiệm thời gian và nâng cao hiệu quả công việc."
slug: "xay-dung-chatbot-tim-kiem-web-gpt-4o-brave-search"
tags: [n8n, automation, no-code, chatbot, ai]
keywords: [n8n workflow, tự động hóa, chatbot, ai, brave search]
---

# 💥🛠️ Xây dựng Chatbot Tìm kiếm Web với GPT-4o và Brave Search

[Các sếp đang gặp khó khăn khi phải tìm kiếm thông tin trên nhiều nguồn khác nhau và tổng hợp kết quả một cách thủ công. Với workflow này, các sếp có thể tự động hóa quy trình này hoàn toàn không cần code, tiết kiệm thời gian và nâng cao hiệu quả công việc.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tìm kiếm thông tin: Tự động hóa quy trình tìm kiếm và tổng hợp thông tin từ nhiều nguồn.
- Nâng cao hiệu quả công việc: Cung cấp thông tin chính xác và liên quan đến nhu cầu của người dùng.
- Cá nhân hóa trải nghiệm: Lưu lại lịch sử cuộc trò chuyện để cung cấp thông tin liên quan hơn.
- Hoạt động liên tục: Chatbot hoạt động 24/7 mà không cần sự can thiệp của con người.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã cài đặt và cấu hình (Self-hosted).
- API key từ OpenAI để sử dụng GPT-4o.
- API key từ Brave Search để thực hiện tìm kiếm.
- Credentials cho MCP Client Tools.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/3189](https://n8n.io/workflows/3189).
3. Hoặc tải file JSON về máy và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "When chat message received"**: Không cần cấu hình gì thêm.
- **Node "MCP Get Brave Tools"**:
  - Chọn credentials là "mcpClientApi".
- **Node "MCP Execute Brave Search"**:
  - Chọn credentials là "mcpClientApi".
  - Đảm bảo đã chọn operation là "executeTool".
- **Node "Simple Memory"**: Không cần cấu hình gì thêm.
- **Node "gpt-4o"**:
  - Chọn credentials là "openAiApi".
  - Đảm bảo đã chọn model là "gpt-4o".

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để test với dữ liệu mẫu.
2. Sau khi test thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để tạo chatbot trên các nền tảng này.
- Lưu log các cuộc trò chuyện để phân tích và cải thiện hiệu suất của chatbot.
- Gửi báo cáo định kỳ về hiệu suất của chatbot qua email hoặc Slack.

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hoàn chỉnh cho việc xây dựng chatbot tìm kiếm thông tin web sử dụng GPT-4o và Brave Search API. Với các bước cấu hình đơn giản và hiệu quả, các sếp có thể triển khai ngay và nâng cao hiệu quả công việc một cách đáng kể.