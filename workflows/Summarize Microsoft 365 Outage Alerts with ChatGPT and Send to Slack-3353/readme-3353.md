---
title: "🚀 Tự động hóa cảnh báo sự cố Microsoft 365 với ChatGPT và Slack"
description: "Hướng dẫn tự động hóa cảnh báo sự cố Microsoft 365 bằng n8n, ChatGPT và Slack. Tiết kiệm thời gian và nâng cao hiệu quả quản lý IT."
slug: "tu-dong-hoa-canh-bao-su-co-microsoft-365-voi-chatgpt-va-slack"
tags: [n8n, automation, no-code, Microsoft 365, Slack]
keywords: [n8n workflow, tự động hóa, Microsoft 365, ChatGPT, Slack]
---

# 🚀 Tự động hóa cảnh báo sự cố Microsoft 365 với ChatGPT và Slack

[Các sếp IT thường phải đối mặt với tình trạng phải theo dõi thủ công các cảnh báo sự cố Microsoft 365 từ email. Việc này không chỉ tốn thời gian mà còn dễ gây bỏ sót quan trọng. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình: từ nhận cảnh báo, tóm tắt bằng ChatGPT đến gửi thông báo sang Slack một cách chuyên nghiệp.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi email thủ công.
- **Tóm tắt thông minh**: ChatGPT tự động tạo bản tóm tắt ngắn gọn.
- **Thông báo chuyên nghiệp**: Slack hiển thị thông tin rõ ràng, dễ theo dõi.
- **Hệ thống hóa**: Tự động xóa email cảnh báo sau khi xử lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft 365 với quyền truy cập Outlook.
- Tài khoản Slack với quyền gửi tin nhắn.
- API Key của OpenAI để sử dụng ChatGPT.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3353](https://n8n.io/workflows/3353)
2. Click vào nút "Download" để tải file JSON workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Check for 365 Service Alert"**:
   - Cấu hình credentials cho Microsoft Outlook.
   - Đảm bảo tài khoản Outlook có quyền truy cập vào thư mục chứa email cảnh báo.

2. **Node "Summarize service alert"**:
   - Cấu hình credentials cho OpenAI.
   - Đặt prompt cho ChatGPT: "Tóm tắt ngắn gọn sự cố Microsoft 365 sau đây: [Nội dung email]".

3. **Node "Post outage to Slack"**:
   - Cấu hình credentials cho Slack API.
   - Chọn channel để gửi thông báo.

4. **Node "Clear email alert from mailbox"**:
   - Đảm bảo tài khoản Outlook có quyền xóa email.

#### 3. Kích hoạt ⚡️
1. Test run với một email cảnh báo mẫu.
2. Kiểm tra Slack để xác nhận thông báo được gửi đúng.
3. Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo cho các thành viên IT khác.
- Tích hợp với PagerDuty để tạo ticket tự động khi phát hiện sự cố nghiêm trọng.
- Lưu log các sự cố vào Google Sheets để theo dõi lịch sử.

### 📌 Kết luận
Với workflow này, các sếp IT có thể tự động hóa toàn bộ quy trình xử lý cảnh báo Microsoft 365 một cách hiệu quả. Hãy áp dụng ngay để nâng cao hiệu quả quản lý và giảm thiểu rủi ro!