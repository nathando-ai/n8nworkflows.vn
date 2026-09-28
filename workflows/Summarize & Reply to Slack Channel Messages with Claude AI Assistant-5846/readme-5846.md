---
title: "🚀 Tự động tóm tắt tin nhắn Slack bằng AI Claude - Workflow n8n"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp các sếp tóm tắt tin nhắn Slack nhanh chóng, chính xác và cá nhân hóa bằng trí tuệ nhân tạo Claude AI."
slug: "tu-dong-tom-tat-tin-nhan-slack-bang-ai-claude"
tags: [n8n, automation, no-code, slack, ai]
keywords: [n8n workflow, tự động hóa, tóm tắt tin nhắn, Claude AI, Slack automation]
---

# 🚀 Tự động tóm tắt tin nhắn Slack bằng AI Claude - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi làm việc với Slack, các sếp thường gặp khó khăn khi phải đọc và tóm tắt hàng loạt tin nhắn trong kênh công việc. Việc này tốn thời gian và dễ gây nhầm lẫn thông tin quan trọng. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này bằng cách sử dụng trí tuệ nhân tạo Claude AI của Anthropic.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đọc tin nhắn thủ công
- Tóm tắt thông tin chính xác và cá nhân hóa
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tăng hiệu suất làm việc đáng kể
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền truy cập kênh cần tóm tắt
- API Key của Anthropic để sử dụng dịch vụ Claude AI
- Kiến thức cơ bản về n8n và cách cấu hình workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, hãy làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" ở góc trên bên phải
3. Dán đường dẫn sau vào ô nhập liệu: `https://n8n.io/workflows/5846`
4. Nhấn "Import" và chờ quá trình hoàn tất

Hoặc bạn cũng có thể tải file JSON từ trang gốc và import trực tiếp từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Slash Command Webhook** (Node đầu tiên):
   - Đảm bảo cấu hình đúng path và HTTP method (POST)
   - Path mặc định là "summarize" - bạn có thể thay đổi nếu cần

2. **Fetch Unread Messages** (Node HTTP Request thứ hai):
   - Cần cấu hình đúng URL của Slack API để lấy tin nhắn
   - Đảm bảo có quyền truy cập vào kênh cần tóm tắt

3. **Anthropic Chat Model** (Node cuối cùng):
   - Cần tạo và cấu hình credentials cho Anthropic API
   - Chọn model phù hợp (mặc định là "claude-sonnet-4-20250514")

4. **Post to Slack (Ephemeral)** (Node HTTP Request cuối cùng):
   - Cấu hình đúng URL của Slack API để gửi tin nhắn
   - Đảm bảo có quyền gửi tin nhắn trong kênh

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong tất cả các node quan trọng:

1. Thực hiện test run với dữ liệu mẫu để kiểm tra workflow
2. Kiểm tra kết quả tóm tắt được gửi đến kênh Slack
3. Nếu mọi thứ hoạt động tốt, bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm chức năng lưu trữ lịch sử tóm tắt vào Google Sheets hoặc Notion
- Kết hợp với Slack Alert để thông báo khi có tin nhắn quan trọng
- Tạo nhiều slash command khác nhau cho các loại tóm tắt khác nhau
- Thêm chức năng gửi báo cáo định kỳ về các tin nhắn quan trọng

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa việc tóm tắt tin nhắn Slack bằng trí tuệ nhân tạo. Với việc cấu hình đơn giản và kết quả chính xác, các sếp có thể tiết kiệm thời gian đáng kể và tập trung vào công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự thay đổi đáng kể trong cách làm việc của bạn!