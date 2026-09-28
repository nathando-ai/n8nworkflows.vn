---
title: "📚 Tự động gửi bài tập IELTS hàng ngày qua Telegram với AI Gemini"
description: "Hướng dẫn tự động hóa gửi bài tập ngữ pháp, viết và đọc IELTS hàng ngày qua Telegram bằng n8n và AI Gemini"
slug: "tu-dong-gui-bai-tap-ielts-hang-ngay-qua-telegram-voi-ai-gemini"
tags: [n8n, automation, no-code, telegram, ai]
keywords: [n8n workflow, tự động hóa, ielts, telegram, ai gemini]
---

# 📚 Tự động gửi bài tập IELTS hàng ngày qua Telegram với AI Gemini

[Các sếp] có biết không? Mỗi ngày luyện tập IELTS đều là một hành trình dài. Nhưng khi phải tự tay chuẩn bị bài tập ngữ pháp, viết và đọc hàng ngày, ai cũng cảm thấy mệt mỏi. Hãy để workflow này giúp các sếp tự động hóa toàn bộ quá trình này nhé!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tự tay chuẩn bị bài tập hàng ngày
- **Chính xác**: Bài tập được tạo bởi AI Gemini, đảm bảo chất lượng
- **Cá nhân hóa**: Bài tập phù hợp với trình độ của các sếp
- **Hoạt động liên tục**: Nhận bài tập mỗi ngày mà không cần nhắc nhở
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram
- API Key của Google Gemini
- Bot Token từ Telegram BotFather
- Chat ID của các sếp (để nhận tin nhắn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/14673)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, chọn **Import from JSON** và paste JSON đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Tạo Telegram Bot**:
   - Truy cập @BotFather trên Telegram
   - Tạo bot mới và lấy Bot Token
   - Thêm credentials trong n8n: **Credentials → Add Credential → Telegram API**

2. **Cấu hình Google Gemini**:
   - Lấy API Key từ Google Cloud Console
   - Thêm credentials trong n8n: **Credentials → Add Credential → Google PaLM API**

3. **Cấu hình các node quan trọng**:
   - **Schedule Trigger**: Đặt lịch chạy workflow hàng ngày
   - **Select Test by Day**: Chọn loại bài tập theo ngày (Thứ 2: Grammar, Thứ 4: Writing, Thứ 6: Reading)
   - **Generate Grammar/Writing/Reading**: Cấu hình prompt cho AI tạo nội dung
   - **Send Grammar/Writing/Reading**: Thay thế `REPLACE_WITH_YOUR_CHAT_ID` bằng Chat ID của các sếp

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra tin nhắn trên Telegram
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi báo cáo tuần/tuần cho các sếp theo dõi tiến độ
- Kết hợp với Slack để nhận thông báo khi có lỗi xảy ra
- Lưu log các bài tập đã gửi để theo dõi lịch sử luyện tập
- Tùy chỉnh prompt cho AI tạo nội dung phù hợp với trình độ của các sếp

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn đảm bảo chất lượng bài tập hàng ngày. Hãy thử ngay và biến quá trình luyện IELTS thành một hành trình thú vị hơn nhé! 🚀