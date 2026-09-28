---
title: "🚀 Tự động hóa tổng kết video YouTube & trò chuyện với GPT-4o-mini qua Telegram"
description: "Hướng dẫn tự động hóa tổng kết nội dung video YouTube và tương tác với AI qua Telegram bằng n8n. Tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-tong-ket-video-youtube-voi-gpt-4o-mini-qua-telegram"
tags: [n8n, automation, no-code, AI, Telegram]
keywords: [n8n workflow, tự động hóa, AI, YouTube, Telegram, GPT-4o-mini]
---

# 🚀 Tự động hóa tổng kết video YouTube & trò chuyện với GPT-4o-mini qua Telegram

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải xem hàng loạt video YouTube để tìm thông tin quan trọng? Hoặc phải tốn thời gian ghi chú và tổng kết nội dung dài? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng kết nội dung video YouTube trong vài giây.
- **Tương tác thông minh**: Trò chuyện với AI về nội dung video ngay trên Telegram.
- **Lưu trữ thông minh**: Lưu transcript và tổng kết vào Google Docs cho việc tham khảo sau.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram (cần API token).
- Tài khoản Google và Google Docs (cần OAuth2 credentials).
- Tài khoản OpenAI (cần API key).
- URL video YouTube để tổng kết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3156](https://n8n.io/workflows/3156)
2. Click vào nút "Import" để tải workflow về máy.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Trigger on Telegram Message"**:
   - Cấu hình credentials cho Telegram API.
   - Đảm bảo bot Telegram đã được thêm vào nhóm chat.

2. **Node "Extract YouTube URL from Input"**:
   - Kiểm tra biểu thức regex để trích xuất URL từ tin nhắn Telegram.

3. **Node "gpt-4o-mini"**:
   - Cấu hình credentials cho OpenAI API.
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng GPT-4o-mini.

4. **Node "Retrieve Transcript from Google Docs"**:
   - Cấu hình credentials cho Google Docs OAuth2.
   - Đảm bảo tài liệu Google Docs đã được chia sẻ với tài khoản được sử dụng.

5. **Node "Send Summary via Telegram"**:
   - Cấu hình credentials cho Telegram API.
   - Đảm bảo bot Telegram có quyền gửi tin nhắn trong nhóm chat.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách gửi URL video YouTube đến bot Telegram.
2. Kiểm tra kết quả tổng kết được gửi về Telegram.
3. Bật Active workflow để tự động hóa hoàn toàn quá trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thay thế Telegram bằng Slack để tích hợp với các nhóm làm việc khác.
- **Lưu log hoạt động**: Thêm node để lưu log các hoạt động vào Google Sheets hoặc cơ sở dữ liệu.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo tổng kết hàng ngày qua email.
- **Tích hợp với Google Calendar**: Lên lịch tự động tổng kết các video YouTube quan trọng.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể khi làm việc với nội dung video YouTube. Bằng cách tự động hóa quá trình tổng kết và tương tác với AI, các sếp có thể tập trung vào những công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!