---
title: "🚀 Tự động hóa sáng tạo nội dung đa nền tảng (Social Media) với ChatGPT, Tavily & Google Sheets"
description: "Xây dựng hệ thống AI tự động nghiên cứu thông tin thời gian thực bằng Tavily và tạo bài viết chuyên biệt cho LinkedIn, X (Twitter), Instagram từ Google Sheets."
slug: "tu-dong-hoa-tao-noi-dung-social-media-ChatGPT-Tavily-Google-Sheets"
tags: [n8n, automation, no-code, content-creation, openai, tavily, google-sheets]
keywords: [n8n workflow, tạo nội dung tự động, ChatGPT social media, Tavily AI search, Google Sheets automation]
---

# 🚀 Tự động hóa sáng tạo nội dung đa nền tảng với ChatGPT, Tavily & Google Sheets

Các sếp có đang mệt mỏi vì phải ngồi hàng giờ nghĩ ý tưởng, viết bài rồi điều chỉnh văn phong cho từng mạng xã hội (LinkedIn, X, Instagram)? Làm thủ công vừa tốn thời gian, vừa dễ cạn kiệt ý tưởng, lại khó duy trì lịch đăng bài đều đặn.

Đừng lo! Workflow n8n này từ *Mirai* sẽ giúp các sếp giải phóng hoàn toàn sức lao động. Hệ thống sẽ tự động đọc chủ đề từ **Google Sheets**, sử dụng **Tavily AI** để nghiên cứu thông tin mới nhất trên web, và nhờ **ChatGPT** viết ra những bài đăng chuẩn hóa riêng biệt cho từng nền tảng mạng xã hội chỉ trong tích tắc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh xoay sở viết bài thủ công cho từng kênh.
- **Cập nhật xu hướng thời gian thực:** Nhờ công cụ tìm kiếm Tavily, nội dung tạo ra luôn bám sát các thông tin mới nhất trên internet.
- **Cá nhân hóa đa nền tảng:** Mỗi mạng xã hội (LinkedIn chuyên nghiệp, X ngắn gọn sắc bén, Instagram trực quan) sẽ có văn phong riêng biệt được AI tối ưu hóa.
- **Vận hành tự động hoàn toàn:** Chỉ cần thêm chủ đề vào Google Sheets, mọi việc còn lại để hệ thống lo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets Account:** Tạo sẵn một bảng tính để quản lý chủ đề và nhận kết quả trả về.
- **OpenAI API Key:** Để sử dụng các model ChatGPT viết bài.
- **Tavily API Key:** Dùng cho công cụ tìm kiếm thông tin web thông minh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file JSON từ nguồn) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Google Sheets Trigger:** Kết nối tài khoản Google của các sếp, chọn đúng file Google Sheets và Sheet Name chứa danh sách chủ đề bài viết.
- **Set Search Fields:** Kiểm tra lại các biến đầu vào để đảm bảo truyền đúng từ khóa/chủ đề từ dòng mới trong Google Sheets sang các bước tiếp theo.
- **Search (Tavily):** Nhập Tavily API Key để node có quyền truy cập internet tìm kiếm dữ liệu thời gian thực.
- **ChatGPT Model for LinkedIn, X (Twitter), Instagram & các Agent nodes:** 
  - Thêm OpenAI Credentials.
  - Tinh chỉnh system prompt bên trong các AI Agent (`LinkedIn`, `X`, `IG`) nếu các sếp muốn định hình lại văn phong, giọng điệu thương hiệu riêng của mình.
- **Update Campaign (Google Sheets):** Cấu hình để node này ghi đè hoặc thêm kết quả bài viết trả về từ AI (LinkedIn, X, Instagram) ngược lại vào các cột tương ứng trên Google Sheets.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** và thêm một dòng chủ đề mới vào Google Sheets để kiểm tra xem dữ liệu có chạy xuyên suốt qua các node AI và ghi ngược lại bảng tính thành công hay không.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động túc trực 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm một node thông báo (Slack/Telegram) sau bước `Aggregate` để bắn tin nhắn thông báo cho đội ngũ Marketing ngay khi bài viết hoàn tất.
- **Thêm bước duyệt bài (Approval):** Thay vì tự động ghi trực tiếp vào Google Sheets để đăng, các sếp có thể gửi bản nháp qua email hoặc chat để quản lý duyệt trước khi xuất bản.
- **Mở rộng nền tảng:** Dễ dàng bổ sung thêm các Agent mới cho Facebook Page hoặc TikTok nếu doanh nghiệp có nhu cầu.

### 📌 Kết luận
Tự động hóa sáng tạo nội dung chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất làm việc của đội ngũ content marketing và bứt phá kênh truyền thông của các sếp ngay hôm nay!