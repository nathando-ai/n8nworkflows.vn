---
title: "📊 Theo dõi Sử dụng Token OpenAI và Chỉ số AI Agent với Dashboard Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi chi tiết sử dụng token OpenAI và các chỉ số AI Agent trong workflow n8n, giúp tối ưu hóa chi phí và hiệu suất hệ thống"
slug: "theo-doi-su-dung-token-openai-va-chi-so-ai-agent"
tags: [n8n, automation, no-code, openai, google-sheets, ai-agent]
keywords: [n8n workflow, tự động hóa, openai token, ai agent metrics, google sheets dashboard]
---

# 📊 Theo dõi Sử dụng Token OpenAI và Chỉ số AI Agent với Dashboard Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý chi phí sử dụng OpenAI và theo dõi hiệu suất AI Agent. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Theo dõi chi tiết sử dụng token OpenAI và các chỉ số AI Agent
- Tối ưu hóa chi phí vận hành hệ thống AI
- Theo dõi hiệu suất và hoạt động của AI Agent
- Tích hợp dữ liệu vào Google Sheets để phân tích và báo cáo
- Tự động hóa toàn bộ quá trình theo dõi mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- API Key của OpenAI (OPENAI_API_KEY)
- Quyền truy cập vào Google Sheets OAuth2 API
- Biết cách thiết lập biến môi trường trong hệ thống
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Set • Workflow + Client Metadata**:
  - Thiết lập `client_id` cho từng khách hàng hoặc hệ thống
  - Giữ nguyên `workflow_id` và `execution_id` như mặc định

- **LangChain Chat Model + Token Callback**:
  - Thiết lập `model` (tên model OpenAI bạn sử dụng)
  - Thiết lập `input_token_cost` và `output_token_cost` theo bảng giá của OpenAI
  - Đảm bảo biến môi trường `OPENAI_API_KEY` đã được thiết lập

- **Token Usage Log**:
  - Chọn Spreadsheet và Sheet "Metrics" trong Google Sheets
  - Thay thế Sheet ID và tên Sheet theo yêu cầu của bạn

- **Log • Token Metrics to Sheets (Tool)**:
  - Chọn Spreadsheet và Sheet "Observability" trong Google Sheets
  - Thay thế Sheet ID và tên Sheet theo yêu cầu của bạn

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi `model` và giá token theo bảng giá của nhà cung cấp dịch vụ AI khác nếu cần
- Thêm các trường metadata bổ sung trong node **Set metadata** nếu cần
- Mở rộng callback để bao gồm thông tin về độ trễ hoặc ID yêu cầu từ nhà cung cấp
- Thêm node Limit hoặc Sample cho các chạy dữ liệu lớn
- Thay thế Chat Trigger bằng Webhook Trigger nếu bạn không cần tính năng chat tích hợp

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi và tối ưu hóa sử dụng token OpenAI và hiệu suất AI Agent. Bằng cách tự động hóa quá trình ghi log và tích hợp dữ liệu vào Google Sheets, các sếp có thể dễ dàng phân tích và báo cáo hiệu suất hệ thống AI của mình. Hãy áp dụng ngay để nâng cao hiệu quả vận hành hệ thống AI của bạn!