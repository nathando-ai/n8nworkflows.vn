---
title: "🛒 Cập nhật danh sách mua sắm Asana qua Telegram bằng giọng nói & văn bản sử dụng GPT-4o mini"
description: "Hướng dẫn tự động hóa cập nhật danh sách mua sắm trong Asana thông qua Telegram bằng giọng nói và văn bản sử dụng trí tuệ nhân tạo GPT-4o mini. Tiết kiệm thời gian và tối ưu hóa quy trình mua sắm."
slug: "cap-nhat-danh-sach-mua-sam-asana-qua-telegram-gpt-4o-mini"
tags: [n8n, automation, no-code, telegram, asana, ai, gpt-4o-mini]
keywords: [n8n workflow, tự động hóa mua sắm, asana telegram, gpt-4o-mini, trí tuệ nhân tạo]
---

# 🛒 Cập nhật danh sách mua sắm Asana qua Telegram bằng giọng nói & văn bản sử dụng GPT-4o mini

[Bạn có bao giờ cảm thấy mệt mỏi khi phải cập nhật danh sách mua sắm thủ công trên Asana? Với workflow này, các sếp có thể dễ dàng cập nhật danh sách mua sắm thông qua Telegram bằng giọng nói hoặc văn bản, sử dụng trí tuệ nhân tạo GPT-4o mini để tự động hóa toàn bộ quy trình.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Cập nhật danh sách mua sắm chỉ với một tin nhắn trên Telegram.
- **Tối ưu hóa quy trình**: Tự động hóa việc tìm kiếm, kiểm tra và cập nhật thông tin sản phẩm.
- **Tích hợp đa nền tảng**: Sử dụng cả giọng nói và văn bản để tương tác với hệ thống.
- **Tăng tính chính xác**: Tránh lỗi nhập liệu thủ công nhờ vào trí tuệ nhân tạo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Asana với danh sách mua sắm đã tạo.
- Bot Telegram đã được thiết lập (chi tiết [tại đây](https://core.telegram.org/bots/tutorial)).
- Tài khoản OpenAI để sử dụng dịch vụ chuyển giọng nói thành văn bản (cần có credits) ([đăng ký tại đây](https://openai.com/index/openai-api/)).
- Tài khoản OpenRouter ([chi tiết tại đây](https://openrouter.ai/docs/api-reference/authentication)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/7845).
2. Nhấn vào nút "Download" để tải file JSON.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Telegram Trigger**: Cấu hình credentials cho Telegram API.
- **Download Voice File**: Cấu hình credentials cho Telegram API.
- **Transcribe a recording**: Cấu hình credentials cho OpenAI API.
- **GPT 4o mini**: Cấu hình credentials cho OpenRouter API và chọn model `openai/gpt-4o-mini`.
- **Search for Grocery Item**: Cấu hình credentials cho Asana OAuth2 API.
- **Check or Uncheck Grocery Items**: Cấu hình credentials cho Asana OAuth2 API.
- **Reply in Chat**: Cấu hình credentials cho Telegram API.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để kiểm tra với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram**: Thêm các node để nhận thông báo cập nhật trên Slack hoặc Telegram.
- **Lưu log**: Thêm node để lưu log các hoạt động cập nhật danh sách mua sắm.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo danh sách mua sắm qua email hoặc Telegram hàng tuần.
- **Tích hợp với Google Sheets**: Lưu trữ danh sách mua sắm trên Google Sheets để dễ dàng chia sẻ và quản lý.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tối ưu hóa quy trình mua sắm bằng cách tự động hóa việc cập nhật danh sách trên Asana thông qua Telegram và trí tuệ nhân tạo GPT-4o mini. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!