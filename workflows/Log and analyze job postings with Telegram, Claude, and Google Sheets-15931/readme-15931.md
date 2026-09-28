---
title: "🚀 Xây dựng hệ thống phân tích thị trường việc làm cá nhân với Telegram, Claude và Google Sheets"
description: "Tự động hóa việc lưu trữ và phân tích tin tuyển dụng từ LinkedIn hay các job board bằng AI Claude, Google Sheets và Telegram bot cực kỳ thông minh."
slug: "phan-tich-viec-lam-tu-dong-telegram-claude-google-sheets"
tags: [n8n, automation, ai-agent, claude, telegram, google-sheets, market-research]
keywords: [n8n workflow, tự động hóa tuyển dụng, claude ai n8n, google sheets telegram, ai job analyzer]
---

# 🚀 Xây dựng hệ thống phân tích thị trường việc làm cá nhân với Telegram, Claude và Google Sheets

Các sếp có hay gặp cảnh đang lướt LinkedIn, thấy một job tuyển dụng cực kỳ ngon nhưng lười không muốn copy rồi paste vào Excel, phân tích xem mức lương ra sao, tech stack gồm những gì, rồi lại quên mất không lưu không? Việc quản lý thủ công các cơ hội việc làm thực sự tốn rất nhiều thời gian và dễ bị bỏ sót dữ liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực đỉnh, giúp biến chiếc bot Telegram thành một trợ lý AI phân tích thị trường việc làm cá nhân. Chỉ cần ném nội dung tin tuyển dụng vào Telegram, phần còn lại để Claude AI và Google Sheets lo!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Dedicate VPS cấu hình khỏe cho n8n](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lưu tin siêu tốc**: Chỉ cần copy/paste nội dung job vào Telegram, AI sẽ tự động tróc xuất các trường dữ liệu quan trọng (Công ty, Vị trí, Tech Stack, Mức lương...) và đẩy thẳng vào Google Sheets.
- **Báo cáo thông minh**: Gửi lệnh `/report` là có ngay bức tranh toàn cảnh về thị trường (xu hướng tech stack, mức lương, phân phối seniority, kỹ năng hot...).
- **Bảo mật tuyệt đối**: Cơ chế xác thực User ID Telegram giúp chỉ có một mình sếp mới dùng được bot của mình.
- **Tự động hóa 100%**: Không còn cảnh nhập liệu thủ công nhàm chán, rảnh tay tập trung ứng tuyển công việc mơ ước.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot**: Tạo qua `@BotFather` để lấy API Token.
- **Anthropic API Key**: Tài khoản Claude AI để xử lý ngôn ngữ tự nhiên.
- **Google Sheets & Google Cloud Service Account**: Tài khoản Google để lưu trữ dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Node `When Telegram Message Received` & `Send Telegram Log Confirmation` & `Send Job Report via Telegram`**: Kết nối với `telegramApi` sử dụng Token bot lấy từ `@BotFather`.
- **Node `Set Config Variables`**: Điền chính xác **Google Sheet ID** và **Sheet Name** của file Google Sheets quản lý việc làm của sếp.
- **Chuẩn bị Google Sheet**: Tạo file Google Sheet với các tiêu đề (headers) đặt tại dòng số 1 gồm: 
  `Date`, `Company`, `Role`, `Seniority`, `Hard Requirements`, `Tech Stack`, `Salary`, `Location`, `Domain`, `Key Signal`
- **Node `Check Telegram User ID`**: Thay thế ID mặc định trong điều kiện bằng **Telegram User ID** chính chủ của sếp (có thể dùng bot `@userinfobot` trên Telegram để lấy ID).
- **Node `Claude Extract Job Info` & `Claude Analyze Job Patterns`**: Cấu hình credentials với `anthropicApi`. Các sếp có thể tinh chỉnh prompt trong này nếu muốn AI tập trung trích xuất những thông tin đặc thù hơn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một tin tuyển dụng bất kỳ qua Telegram cho bot để test.
- Kiểm tra xem dữ liệu đã được bóc tách và đẩy vào Google Sheets chưa.
- Nếu mọi thứ mượt mà, bật công tắc **Active** lên để bot hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Slack/Discord**: Ngoài Telegram, các sếp có thể nhánh thêm thông báo về kênh Slack cá nhân hoặc nhóm team nếu đang săn việc cùng đồng đội.
- **Lên lịch báo cáo định kỳ**: Thay vì phải gõ `/report`, hãy gắn thêm node `Schedule Trigger` để mỗi sáng thứ Hai bot tự động gửi báo cáo thị trường vào Telegram.
- **Lọc tự động**: Thêm các điều kiện AI tự động đánh giá độ phù hợp (Match Score) của job với CV của sếp trước khi lưu vào bảng.

### 📌 Kết luận
Một hệ thống tự động hóa nhỏ gọn nhưng cực kỳ thực chiến giúp các sếp quản trị sự nghiệp và thị trường lao động trong tầm tay. Triển khai ngay thôi các sếp ơi!