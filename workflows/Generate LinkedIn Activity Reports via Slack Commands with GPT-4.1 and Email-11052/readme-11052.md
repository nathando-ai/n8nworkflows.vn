---
title: "🚀 Tự động tạo báo cáo hoạt động LinkedIn từ Slack với GPT-4.1 & Gmail"
description: "Hướng dẫn cấu hình workflow n8n tích hợp Slack Slash Command để quét hoạt động LinkedIn qua Apify, phân tích bằng GPT-4.1 và gửi báo cáo HTML qua Gmail."
slug: "tao-bao-cao-hoat-dong-linkedin-tu-slack-voi-gpt4-va-gmail"
tags: [n8n, automation, slack, openai, apify, gmail, lead-generation]
keywords: [n8n workflow, linkedin report slack, tich hop slack openai, apify linkedin scraper, tu dong hoa n8n]
---

# 🚀 Tự động tạo báo cáo hoạt động LinkedIn từ Slack với GPT-4.1 & Gmail

Các sếp có bao giờ tốn quá nhiều thời gian để "soi" profile LinkedIn, đọc từng bài viết cũ của khách hàng tiềm năng trước mỗi buổi họp hay chiến dịch outreach không? Việc lướt thủ công từng trang cá nhân vừa mất thời gian, vừa khó tổng hợp được insight thực sự giá trị.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó! Chỉ với một câu lệnh đơn giản trực tiếp trên **Slack**, hệ thống sẽ tự động quét thông tin LinkedIn của mục tiêu qua **Apify**, sử dụng sức mạnh AI của **GPT-4.1** để phân tích thói quen đăng bài, chủ đề chính, mức độ tương tác, và gửi ngay một bản báo cáo HTML cực kỳ chuyên nghiệp thẳng vào **Gmail** của các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần lướt thủ công từng profile LinkedIn, nhận ngay thông tin tổng hợp chỉ trong vài giây.
- **Chuẩn bị trước cuộc họp hoàn hảo:** Nắm bắt nhanh chủ đề quan tâm, bài đăng gần đây của đối tác/khách hàng để tạo ấn tượng mạnh.
- **Tự động hóa hoàn toàn từ Slack:** Kích hoạt mọi lúc, mọi nơi ngay trên ứng dụng chat quen thuộc bằng Slash Command (`/check-linkedin`).
- **Báo cáo trực quan:** Nhận email tóm tắt định dạng HTML đẹp mắt, rõ ràng với các insights có thể hành động ngay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Slack Workspace** (Quyền tạo Slack App và Slash Command).
- **Apify Account & API Key** (Sử dụng các actor trích xuất thông tin profile và bài đăng LinkedIn).
- **OpenAI API Key** (Truy cập mô hình `gpt-4.1` và `gpt-4.1-mini`).
- **Gmail Account** (Xác thực OAuth2 để gửi email báo cáo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n.io hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` / `Cmd+V` để paste trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thành phần cốt lõi sau để workflow không bị lỗi:

- **Webhook Node:** Lấy URL webhook được tạo ra sau khi active (hoặc dùng test URL) để cấu hình làm **Request URL** cho Slash Command trong bảng điều khiển Slack API (`/check-linkedin`).
- **Apify Nodes (Get Linkedin Profile URL, Find Linkedin Profile, Scrap what this person posted recently, Structure recent posts):** Kết nối `apifyApi` credentials. Đảm bảo chọn đúng Actor ID chuyên dụng cho việc tìm kiếm profile LinkedIn và cào bài viết (Posts Scraper). *Lưu ý: Khu vực này phụ thuộc vào chi phí chạy của Apify.*
- **OpenAI Nodes (GPT 4.1-mini for classification, GPT 4.1-mini to extract firstName + lastName, GPT 4.1):** Kết nối `openAiApi` credentials. Node `GPT 4.1` chịu trách nhiệm tổng hợp phân tích sâu, hãy đảm bảo tài khoản OpenAI của các sếp có đủ hạn mức (quota).
- **Send report via Email (Gmail Node):** Kết nối `gmailOAuth2` credentials và cấu hình địa chỉ email nhận báo cáo.
- **Tell on slack that no full name was found (Slack Node):** Kết nối `slackOAuth2Api` để hệ thống tự động thông báo về kênh Slack nếu người dùng nhập thiếu Họ và Tên.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng cách nhập lệnh `/check-linkedin [Tên Khách Hàng]` trên Slack để kiểm tra luồng dữ liệu qua từng node.
- Nếu mọi thứ trả về kết quả suôn sẻ, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận thông báo:** Thay vì chỉ gửi qua Gmail, các sếp có thể nối thêm node Slack hoặc Telegram để đẩy thẳng bản tóm tắt vào nhóm chat riêng của sales team.
- **Tùy chỉnh giới hạn bài đăng:** Trong node cào bài viết của Apify, mặc định hệ thống lấy 20 bài gần nhất. Các sếp có thể tăng/giảm thông số này tùy thuộc vào nhu cầu phân tích và ngân sách API.
- **Tối ưu chi phí AI:** Sử dụng cấu hình JSON Schema trong *Structured Output Parser* để kiểm soát chính xác độ dài đầu ra của GPT-4.1, tránh lãng phí token.

### 📌 Kết luận
Workflow tích hợp AI và Slack này là vũ khí bí mật giúp đội ngũ Sales và CS tăng tốc độ nghiên cứu khách hàng lên gấp nhiều lần. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa quy trình làm việc ngay hôm nay!