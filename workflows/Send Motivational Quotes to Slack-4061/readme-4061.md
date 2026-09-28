---
title: "🚀 [Tự động gửi câu nói động viên hàng ngày vào Slack] - Workflow n8n hoàn toàn không code"
description: "Hướng dẫn chi tiết cách tự động gửi các câu nói động viên hàng ngày vào Slack thông qua workflow n8n. Tiết kiệm thời gian và nâng cao tinh thần làm việc của team."
slug: "tu-dong-gui-cau-noi-dong-vien-hang-ngay-vao-slack"
tags: [n8n, automation, no-code, slack, ai]
keywords: [n8n workflow, tự động hóa, slack, động viên, tinh thần làm việc]
---

# 🚀 [Tự động gửi câu nói động viên hàng ngày vào Slack] - Workflow n8n hoàn toàn không code

[Các sếp đang làm việc chăm chỉ nhưng lại cảm thấy chán nản, mất động lực? Hãy để workflow n8n tự động gửi các câu nói động viên hàng ngày vào Slack để nâng cao tinh thần làm việc của team. Workflow này hoàn toàn không cần code, chỉ cần cấu hình một lần là có thể hoạt động liên tục 24/7.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải nhớ và gửi các câu nói động viên hàng ngày.
- Nâng cao tinh thần làm việc: Các thành viên team sẽ nhận được động lực mỗi ngày.
- Cá nhân hóa: Có thể tùy chỉnh các câu nói động viên theo nhu cầu của team.
- Hoạt động liên tục: Workflow sẽ tự động gửi các câu nói động viên vào các khung giờ đã cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền gửi tin nhắn vào channel.
- API key của Slack (có thể lấy từ [Slack API](https://api.slack.com/)).
- Tài khoản n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Send to Slack Channel**: Cần cấu hình credentials của Slack và chọn channel để gửi tin nhắn.
- **Format Slack Message**: Có thể tùy chỉnh nội dung tin nhắn theo nhu cầu của team.
- **Fetch Daily Quote (ZenQuotes API)**: Node này sẽ tự động lấy các câu nói động viên từ API ZenQuotes.
- **08:00 – Morning Boost**, **13:00 – Midday Reminder**, **18:00 – Evening Motivation**: Các node này sẽ tự động kích hoạt workflow vào các khung giờ đã cài đặt.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Có thể kết hợp với các công cụ khác như Google Sheets để lưu trữ các câu nói động viên.
- Có thể gửi các câu nói động viên vào các nhóm Slack khác nhau.
- Có thể tùy chỉnh nội dung tin nhắn để phù hợp với nhu cầu của từng team.

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm thời gian và nâng cao tinh thần làm việc của team. Hãy áp dụng ngay để trải nghiệm sự khác biệt!