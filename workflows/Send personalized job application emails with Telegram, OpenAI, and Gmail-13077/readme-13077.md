---
title: "🚀 Tự động hóa ứng tuyển công việc với Telegram, OpenAI và Gmail"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình ứng tuyển công việc bằng cách gửi email cá nhân hóa thông qua Telegram, OpenAI và Gmail"
slug: "tu-dong-hoa-ung-tuyen-cong-viec-voi-telegram-openai-gmail"
tags: [n8n, automation, no-code, telegram, openai, gmail, hr, ai-chatbot]
keywords: [n8n workflow, tự động hóa ứng tuyển, email cá nhân hóa, openai api, telegram bot]
---

# 🚀 Tự động hóa ứng tuyển công việc với Telegram, OpenAI và Gmail

[Các sếp] có biết không? Mỗi lần ứng tuyển công việc, bạn phải:
- Chụp ảnh bài đăng tuyển dụng
- Tìm thông tin công việc
- So sánh với CV của mình
- Viết email ứng tuyển
- Gửi email với CV đính kèm

Quá trình này tốn thời gian và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa hoàn toàn quá trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình ứng tuyển
- **Email cá nhân hóa**: AI tạo email phù hợp với từng công việc
- **Chính xác cao**: So sánh thông tin công việc với CV của bạn
- **Tự động gửi**: Gửi email với CV đính kèm một cách tự động
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram
- API Key OpenAI
- Tài khoản Gmail
- File CV đã tải lên OpenAI Files và Google Drive
- Redis server (tùy chọn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13077](https://n8n.io/workflows/13077)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Tạo bot Telegram mới qua @BotFather
   - Lưu lại token bot
   - Cấu hình credentials trong n8n với token vừa tạo

2. **Build AI request payload**:
   - Cập nhật `file_id` của CV trong OpenAI Files

3. **Call OpenAI API**:
   - Đảm bảo đã cấu hình OpenAI credentials trong n8n

4. **Store draft in Redis**:
   - Cấu hình Redis credentials (nếu sử dụng)

5. **Download resume from Drive**:
   - Cập nhật `file_id` của CV trong Google Drive
   - Đảm bảo đã cấu hình Google Drive credentials trong n8n

6. **Send email via Gmail**:
   - Đảm bảo đã cấu hình Gmail OAuth2 credentials trong n8n

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Bật Active workflow
3. Gửi ảnh bài đăng tuyển dụng đến bot Telegram của bạn

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các email đã gửi
- Kết hợp với Slack để nhận thông báo khi có công việc mới
- Tạo báo cáo định kỳ về số lượng ứng tuyển thành công
- Tự động hóa quá trình theo dõi phản hồi từ nhà tuyển dụng

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong quá trình ứng tuyển công việc. Bằng cách kết hợp Telegram, OpenAI và Gmail, bạn có thể tự động hóa toàn bộ quá trình từ nhận thông tin công việc đến gửi email ứng tuyển cá nhân hóa. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!