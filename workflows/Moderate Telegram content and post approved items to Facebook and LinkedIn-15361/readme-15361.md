---
title: "🚀 Tự Động Kiểm Duyệt Nội Dung Telegram và Đăng Lên Facebook, LinkedIn với n8n"
description: "Xây dựng hệ thống tự động kiểm duyệt nội dung gửi qua Telegram, phân loại ngôn ngữ và tự động xuất bản lên Facebook Page, LinkedIn chỉ với 1 cú click."
slug: "tu-dong-kiem-duyet-telegram-facebook-linkedin-n8n"
tags: [n8n, automation, telegram, facebook, linkedin, social-media, google-sheets]
keywords: [n8n workflow, tự động hóa telegram, đăng bài facebook linkedin tự động, kiểm duyệt nội dung n8n, social media automation]
---

# 🚀 Tự Động Kiểm Duyệt Nội Dung Telegram và Đăng Lên Facebook, LinkedIn

Các sếp làm nội dung hoặc quản lý cộng đồng chắc chắn đã quen với cảnh phải copy bài viết từ Telegram, dịch hoặc chỉnh sửa lại, rồi thủ công đăng lên từng nền tảng như Facebook và LinkedIn. Việc này không chỉ tốn thời gian, dễ sót việc mà còn làm giảm hiệu suất làm việc nhóm. 

Giải pháp ư? Hãy để chiếc workflow n8n này "gánh" thay các sếp! Hệ thống sẽ tự động hóa toàn bộ quy trình: nhận nội dung từ Telegram, kiểm duyệt thông qua callback, phân loại ngôn ngữ, lấy dữ liệu từ Google Sheets và tự động "lên sóng" đồng loạt lên Facebook và LinkedIn một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không còn cảnh copy-paste thủ công qua lại giữa Telegram, Facebook và LinkedIn.
- **Quy trình kiểm duyệt chuẩn hóa:** Duyệt hoặc từ chối bài viết trực tiếp ngay trên Telegram bằng các nút bấm (Inline Keyboard) tiện lợi.
- **Đa ngôn ngữ linh hoạt:** Tự động phân loại ngôn ngữ (Anh, Tây Ban Nha, Ba Lan,...) để gửi thông báo và phản hồi chuẩn xác.
- **Đồng bộ đa nền tảng:** Bài viết sau khi được duyệt sẽ tự động bắn thẳng lên cả Facebook Graph API và LinkedIn liền mạch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance:** Đã cài đặt và hoạt động ổn định.
- **Telegram Bot:** Tạo qua BotFather để lấy API Token.
- **Google Sheets:** File Google Sheets chứa dữ liệu nội dung cần quản lý.
- **Facebook Developer Account:** Đã tạo App và cấp quyền truy cập Facebook Graph API để đăng bài lên Page.
- **LinkedIn Developer Account:** Đã cấu hình LinkedIn App để lấy quyền OAuth2 đăng bài.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, paste trực tiếp vào n8n Editor của mình hoặc import file JSON tải về từ kho lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:
- **Telegram Message Trigger & Send Telegram Message:** Kết nối với Telegram Bot Credentials của các sếp. Node Trigger sẽ hứng nội dung gửi đến, trong khi các node Send Message sẽ gửi thông báo xác nhận (English, Polish, Spanish...).
- **Check Callback Query & Route by Language (Nodes: `if`, `switch`):** Kiểm tra các nút bấm xác nhận từ người quản trị (Duyệt/Từ chối) và định tuyến luồng xử lý theo đúng ngôn ngữ tương ứng.
- **Read Data from Sheets (Node: `googleSheets`):** Kết nối tài khoản Google Sheets OAuth2, trỏ tới đúng file tài liệu và Sheet Name chứa dữ liệu nội dung bài viết.
- **Post to Facebook Graph API & Post to LinkedIn (Nodes: `facebookGraphApi`, `linkedIn`):** Cấu hình Page ID/Token cho Facebook và tài khoản OAuth2 cho LinkedIn để hệ thống có quyền xuất bản bài viết tự động.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một tin nhắn test qua Telegram Bot để kiểm tra luồng chạy.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động hóa vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm AI:** Các sếp có thể chèn thêm một node AI (OpenAI / Anthropic) trước bước đăng bài để tự động tối ưu hóa, viết lại tiêu đề hoặc hashtag phù hợp cho từng nền tảng (Facebook ngắn gọn, LinkedIn chuyên nghiệp).
- **Lưu Log vào Google Sheets:** Thêm một bước cập nhật trạng thái "Published" vào Google Sheets ngay sau khi bài đăng thành công lên mạng xã hội.
- **Cảnh báo lỗi qua Slack/Telegram:** Thiết lập luồng Error Trigger để nếu Facebook hoặc LinkedIn API lỗi, hệ thống sẽ bắn tin nhắn cảnh báo ngay lập tức cho đội ngũ kỹ thuật.

### 📌 Kết luận
Workflow kiểm duyệt nội dung tự động này là mảnh ghép hoàn hảo giúp các đội ngũ marketing và quản trị cộng đồng tối ưu hóa hiệu suất làm việc. Hãy cài đặt ngay hôm nay để giải phóng bản thân khỏi các tác vụ thủ công nhàm chán!