---
title: "🚀 Tự động tạo Carousel triệu view cho Instagram, TikTok & LinkedIn với xAI Grok và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc lên ý tưởng, viết nội dung thu hút và thiết kế slide ảnh carousel chuyên nghiệp bằng xAI Grok AI Agent và Google Drive."
slug: "tu-dong-tao-carousel-xai-grok-n8n"
tags: [n8n, automation, xai-grok, content-creation, ai-agent, google-drive]
keywords: [n8n workflow, tao carousel tu dong, xai grok ai, content automation, tao anh tu dong n8n]
---

# 🚀 Tự động tạo Carousel triệu view cho Instagram, TikTok & LinkedIn với xAI Grok

Các sếp có bao giờ cảm thấy đuối sức khi mỗi ngày phải nghĩ ý tưởng, viết content và tự tay thiết kế từng slide ảnh carousel cho Instagram, TikTok hay LinkedIn chưa? Việc này tốn hàng giờ đồng hồ nhưng đôi khi tương tác lại lẹt đẹt.

Đừng lo, workflow n8n cực đỉnh này sẽ giúp các sếp tự động hóa 100% quy trình từ một từ khóa chủ đề (topic) cho ra lò một bộ slide ảnh hoàn chỉnh, đẹp mắt, sẵn sàng "bùng nổ" tương tác mà không cần tốn một xu thuê designer hay tốn thời gian ngồi gõ phím.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Biến một ý tưởng sơ khai thành chuỗi slide 7 trang hoàn chỉnh chỉ trong vài giây.
- **Nội dung sắc bén:** Sử dụng sức mạnh của **xAI Grok AI Agent** để viết nội dung ngắn gọn, giật gân, đúng tâm lý người xem mạng xã hội.
- **Tự động hóa thiết kế:** Node **Edit Image** tự động ghép text vào template background chuẩn chỉnh tọa độ, lưu thẳng lên Google Drive.
- **Đa nền tảng:** Phù hợp đăng tải trên Instagram, TikTok, LinkedIn hay X (Twitter).
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **xAI (Grok) API Key:** Tài khoản và API key để kết nối với mô hình LLM xAI Grok.
- **Google Drive:** Tài khoản kết nối OAuth2 để tải template background và lưu trữ ảnh slide thành phẩm.
- **Template Background:** Chuẩn bị sẵn một mẫu ảnh nền (có thể lấy mẫu Canva từ tác giả bên dưới).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow hoặc import trực tiếp file JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **xAI Grok Chat Model:** Thêm Credentials `xAiApi` để AI Agent có thể hoạt động.
- **Download file & Upload file (Google Drive):** Kết nối tài khoản Google Drive OAuth2. Tại node Download, điền `fileId` của bức ảnh template background mà các sếp muốn dùng. Tại node Upload, chọn thư mục đích lưu trữ các slide xuất ra.
- **AI Agent & Structured Output Parser1:** Tinh chỉnh System Prompt của AI Agent nếu muốn thay đổi giọng văn (brand voice) phù hợp với kênh của các sếp. Prompt mặc định sẽ đóng vai trò "The Carousel Cynic" tạo ra nội dung phản biện, thu hút cao độ.
- **Params Style Config & Img 1 - Title / Description8:** Tùy chỉnh font chữ, kích thước, màu sắc và tọa độ (coordinates) của text sao cho khớp hoàn hảo với background template của các sếp.
- *(Tham khảo mẫu Canva Background Template gốc của tác giả tại đây: [Canva Template](https://www.canva.com/design/DAG5Lh40qks/I-PL6LLfIqZBYXOrZUjYGA/edit?utm_content=DAG5Lh40qks&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton))*

#### 3. Kích hoạt ⚡️
- Bấm **"Test workflow"** bằng nút `When clicking ‘Test workflow’` hoặc gọi qua `Webhook` với payload chứa Chủ đề (`theme`) và Lời kêu gọi hành động (`CTA`).
- Kiểm tra kết quả trong thư mục Google Drive. Nếu mọi thứ hiển thị ngon lành, hãy bật nút **Active** cho workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Buffer / Hootsuite:** Nối thêm các node mạng xã hội sau bước Upload Google Drive để tự động đăng bài luôn lên LinkedIn hoặc Instagram.
- **Nhận thông báo qua Telegram/Slack:** Thêm node gửi tin nhắn thông báo kèm hình ảnh vừa tạo về nhóm chat riêng để duyệt trước khi đăng.
- **Lưu trữ lịch sử:** Lưu thông đề tài và link slide vào Google Sheets để tiện quản lý chiến dịch content marketing dài hạn.

### 📌 Kết luận
Việc sản xuất nội dung hình ảnh hàng loạt chưa bao giờ dễ dàng đến thế khi kết hợp n8n và AI. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm nội dung và đưa thương hiệu cá nhân hoặc doanh nghiệp của các sếp lên một tầm cao mới!