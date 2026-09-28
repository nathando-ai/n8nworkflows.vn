---
title: "🚀 Tự động hóa chuyển đổi ghi âm cuộc họp thành tài liệu Google Docs với Groq Whisper và OpenRouter"
description: "Hướng dẫn tự động hóa chuyển đổi ghi âm cuộc họp thành tài liệu Google Docs với Groq Whisper và OpenRouter, tiết kiệm thời gian và nâng cao hiệu quả làm việc"
slug: "tu-dong-hoa-chuyen-doi-ghi-am-cuoc-hop-thanh-tai-lieu-google-docs"
tags: [n8n, automation, no-code, AI, Google Docs]
keywords: [n8n workflow, tự động hóa, AI, Google Docs, Groq Whisper, OpenRouter]
---

# 🚀 Tự động hóa chuyển đổi ghi âm cuộc họp thành tài liệu Google Docs với Groq Whisper và OpenRouter

[Các sếp đang gặp khó khăn khi phải chuyển đổi thủ công ghi âm cuộc họp thành tài liệu Google Docs. Workflow này giúp tự động hóa toàn bộ quy trình này, tiết kiệm thời gian và nâng cao hiệu quả làm việc.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian chuyển đổi ghi âm thành tài liệu Google Docs
- Tự động hóa toàn bộ quy trình, giảm thiểu lỗi do làm thủ công
- Tài liệu Google Docs được tạo tự động với cấu trúc rõ ràng
- Hỗ trợ cả văn bản và ghi âm, linh hoạt trong việc nhập liệu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Groq API Key (miễn phí, hỗ trợ 28.800 giây/ngày)
- Tài khoản OpenRouter API Key (miễn phí)
- Tài khoản Google Docs OAuth2 (để tạo và cập nhật tài liệu)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15499](https://n8n.io/workflows/15499)
2. Nhấn nút "Import" để thêm workflow vào n8n của bạn
3. Hoặc copy JSON từ trang web và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Transcribe Audio"**:
   - Tạo credential mới với loại "Header Auth"
   - Tên: `Authorization`
   - Giá trị: `Bearer YOUR_GROQ_KEY_HERE`
   - Chọn credential này trong node "Transcribe Audio"

2. **Node "Call AI API"**:
   - Tạo credential mới với loại "Header Auth"
   - Tên: `Authorization`
   - Giá trị: `Bearer YOUR_OPENROUTER_KEY_HERE`
   - Chọn credential này trong node "Call AI API"

3. **Node "Write Summary to Doc" và "Create Google Doc"**:
   - Tạo credential mới với loại "Google Docs OAuth2"
   - Đăng nhập bằng tài khoản Google của bạn và cấp quyền truy cập
   - Chọn credential này trong cả hai node Google Docs

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với các API và dịch vụ bên ngoài
2. Thử chạy workflow với dữ liệu mẫu
3. Bật chế độ Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để thông báo khi tài liệu đã được tạo
- Lưu log các cuộc họp để theo dõi lịch sử
- Gửi báo cáo định kỳ về các cuộc họp và hành động tiếp theo

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả làm việc bằng cách tự động hóa chuyển đổi ghi âm cuộc họp thành tài liệu Google Docs. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!