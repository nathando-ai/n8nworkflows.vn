---
title: "🚀 Tự động hóa công việc sau cuộc họp: Fireflies + GPT-4o-mini + Telegram"
description: "Tự động chuyển đổi các hành động sau cuộc họp thành công việc ClickUp, sử dụng Fireflies, GPT-4o-mini và Telegram. Tiết kiệm thời gian và đảm bảo không bỏ sót bất kỳ nhiệm vụ quan trọng nào."
slug: "tu-dong-hoa-cong-viec-sau-cuoc-hop-fireflies-gpt4o-mini-telegram"
tags: [n8n, automation, no-code, project-management, ai-summarization]
keywords: [n8n workflow, tự động hóa, quản lý dự án, AI, Fireflies, GPT-4o-mini, Telegram, ClickUp]
---

# 🚀 Tự động hóa công việc sau cuộc họp: Fireflies + GPT-4o-mini + Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải ghi chú, phân tích và tạo công việc thủ công sau mỗi cuộc họp. Giới thiệu workflow như giải pháp tự động hóa hoàn chỉnh, giúp các sếp tập trung vào công việc quan trọng hơn.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần ghi chú thủ công sau mỗi cuộc họp.
- **Chính xác cao**: GPT-4o-mini phân tích và tạo công việc với độ chính xác cao.
- **Tích hợp hoàn chỉnh**: Tự động tạo công việc trong ClickUp và thông báo qua Telegram.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào thời gian làm việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Fireflies với quyền truy cập API.
- Tài khoản ClickUp với quyền tạo công việc.
- Tài khoản OpenAI để sử dụng GPT-4o-mini.
- Tài khoản Telegram và bot API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15069](https://n8n.io/workflows/15069).
2. Nhấn nút "Import" và chọn "Import from URL".
3. Dán URL workflow vào ô nhập liệu và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 1. Webhook — Fireflies Transcript Done**:
   - Kích hoạt workflow và sao chép URL webhook.
   - Truy cập Fireflies → Settings → Developer Settings → Webhooks.
   - Dán URL webhook vào trường tương ứng.

2. **Node 5. Set — Config Values**:
   - Thay thế `YOUR_FIREFLIES_API_KEY` bằng API key của Fireflies.
   - Thay thế `YOUR_CLICKUP_API_TOKEN` bằng API token của ClickUp.
   - Thay thế `YOUR_CLICKUP_LIST_ID` bằng ID danh sách công việc trong ClickUp.
   - Thay thế `YOUR_TELEGRAM_CHAT_ID` bằng ID chat Telegram.
   - Cập nhật tên và công ty của các sếp.

3. **Node 11. OpenAI — GPT-4o-mini Model**:
   - Kết nối credential OpenAI của các sếp.

4. **Node 17. Telegram — Send Task Summary**:
   - Kết nối credential Telegram Bot API của các sếp.
   - Gửi `/start` đến bot trước khi test workflow.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thay thế node Telegram bằng node Slack để nhận thông báo trên Slack.
- **Lưu log**: Thêm node để lưu log các công việc đã tạo để theo dõi hiệu suất.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp về các công việc đã hoàn thành hàng tuần.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc chuyển đổi các hành động sau cuộc họp thành công việc ClickUp, tiết kiệm thời gian và đảm bảo không bỏ sót bất kỳ nhiệm vụ quan trọng nào. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!