---
title: "💰 Theo dõi chi phí token AI và lưu hóa đơn với n8n API và Data Tables"
description: "Hướng dẫn tự động hóa chi tiết theo dõi chi phí token AI của các workflow n8n, tính toán chi phí và lưu hóa đơn vào Data Table"
slug: "theo-doi-chi-phi-token-ai-voi-n8n"
tags: [n8n, automation, no-code, ai, data-table]
keywords: [n8n workflow, tự động hóa, ai token, data table, chi phí token]
---

# 💰 Theo dõi chi phí token AI và lưu hóa đơn với n8n API và Data Tables

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý chi phí token AI một cách thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi chi phí token AI hàng giờ
- Tính toán chính xác chi phí sử dụng các model AI phổ biến
- Lưu trữ hóa đơn chi tiết trong Data Table
- Hỗ trợ nhiều model AI (Claude, OpenAI, Gemini, Perplexity)
- Dễ dàng mở rộng cho các model mới
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n API (để truy cập workflow và execution data)
- Data Table `execution_receipts` với các cột:
  - `workflowid` (text)
  - `executionid` (text)
  - `receipt` (text)
  - `created_at` (text)
  - `units` (number)
- Các workflow AI agent đã được tag với `agent`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15177)
2. Chọn "Download" để tải file JSON
3. Trong n8n Editor, chọn "Import from File" và tải file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "1.1 Get AI Agent Workflows"**:
   - Cấu hình credential cho n8n API
   - Đảm bảo đã tag các workflow AI agent với `agent`

2. **Node "1.2 Get Workflow Executions"**:
   - Cấu hình credential cho n8n API
   - Đảm bảo resource được đặt là `execution`

3. **Node "1.3 Save Receipt to Data Table"**:
   - Chọn Data Table `execution_receipts` đã tạo trước đó
   - Kiểm tra các cột đã được cấu hình đúng

4. **Node "Extract Token Usage & Cost"**:
   - Nếu cần thêm model mới, thêm dòng mới vào `MODEL_RATES` trong code node
   - Ví dụ: `MODEL_RATES = { "gpt-4": 0.03, "claude-2": 0.01, "gemini-pro": 0.005 }`

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra workflow
2. Kích hoạt workflow bằng cách bật nút Active
3. Workflow sẽ tự động chạy hàng giờ để cập nhật dữ liệu

### ✍️ Mẹo & gợi ý nâng cao
- Thêm cảnh báo khi chi phí vượt ngưỡng nhất định
- Kết hợp với Slack/Telegram để nhận thông báo khi có hóa đơn mới
- Tạo báo cáo định kỳ về chi phí sử dụng AI
- Mở rộng để theo dõi các chỉ số khác như thời gian xử lý, số lượng request...

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi và quản lý chi phí token AI một cách hiệu quả. Với việc lưu trữ hóa đơn chi tiết trong Data Table, các sếp có thể dễ dàng phân tích và tối ưu hóa chi phí sử dụng AI trong doanh nghiệp. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả sử dụng tài nguyên AI!