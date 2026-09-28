---
title: "🚀 Tự động trích xuất các khoảnh khắc huấn luyện sales từ cuộc gọi Fireflies với WayinVideo, Google Sheets và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc bắt sự kiện Fireflies, phân tích video cuộc gọi bằng WayinVideo AI, lưu log vào Google Sheets và thông báo qua Slack."
slug: "tu-dong-trich-xuat-khoanh-khac-sales-training-fireflies-wayinvideo"
tags: [n8n, automation, no-code, ai, crm, slack]
keywords: [n8n workflow, fireflies ai, wayinvideo, sales training automation, google sheets, slack integration]
---

# 🚀 Tự động trích xuất các khoảnh khắc huấn luyện sales từ Fireflies với WayinVideo, Google Sheets và Slack

Các sếp quản lý đội ngũ sales (Sales Managers) chắc chắn hiểu cảm giác tốn bao nhiêu thời gian để nghe lại hàng chục, hàng trăm cuộc gọi mỗi tuần nhằm tìm ra các "khoảnh khắc vàng" (closing thành công, xử lý từ chối xuất sắc) phục vụ cho việc huấn luyện nhân sự. Việc làm thủ công này cực kỳ ngốn thời gian và dễ bỏ sót thông tin quan trọng.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: Ngay khi Fireflies chép xong nội dung cuộc gọi (transcript), hệ thống sẽ lấy video, gửi sang WayinVideo AI để tìm các đoạn đáng chú ý bằng câu lệnh tự nhiên (natural language query), lưu chi tiết vào Google Sheets và bắn thông báo mượt mà lên Slack cho team. Không một giọt mồ hôi thủ công nào bị lãng phí!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Ngay khi cuộc gọi kết thúc và có transcript, hệ thống tự động xử lý ngầm mà không cần can thiệp thủ công.
- **AI thông minh chọn lọc:** Sử dụng WayinVideo để tìm chính xác các phân đoạn đắt giá dựa trên câu lệnh tự nhiên (ví dụ: *"tìm đoạn xử lý từ chối giá"*).
- **Lưu trữ bài bản:** Tự động tạo bảng log chi tiết trên Google Sheets gồm thời gian, điểm số, mô tả từng clip.
- **Thông báo tập trung:** Gửi bản tổng hợp toàn bộ các clip training trực tiếp vào kênh Slack của đội ngũ sales ngay khi hoàn tất.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Fireflies.ai** kèm API Key để nhận Webhook transcript.
- **Tài khoản WayinVideo** kèm API Key để sử dụng tính năng *Find Moments*.
- **Google Sheets & Slack** tài khoản kết nối qua OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 17 nodes được chia thành các cụm chức năng rõ ràng. Các sếp cần tập trung cấu hình các điểm sau:

- **1. Webhook — Fireflies Transcript Done**: Copy Webhook URL được tạo ra để cấu hình phía Fireflies (vào *Settings > Developer Settings > Webhooks* và dán URL vào).
- **2. Set — Config Values**: Đây là nơi sống còn của workflow. Các sếp cần thay thế:
  - `YOUR_FIREFLIES_API_KEY`
  - `YOUR_WAYINVIDEO_API_KEY`
  - `YOUR_GOOGLE_SHEET_ID`
  - Kênh Slack nhận thông báo (`Slack channel`)
  - Câu lệnh `findMomentsQuery` tùy chỉnh theo nghiệp vụ công ty.
- **14. Google Sheets — Log Training Clips**: Kết nối tài khoản Google Sheets (OAuth2) và trỏ tới file Google Sheet đã chuẩn bị sẵn. 
  *Lưu ý:* Tạo sẵn một tab tên là `Sales Training Clips` với các cột: `Date`, `Meeting Title`, `Clip #`, `Clip Title`, `Start`, `End`, `Duration (sec)`, `Score`, `Tags`, `Description`, `Logged At`.
- **16. Slack — Send Training Clips Alert**: Kết nối tài khoản Slack (OAuth2), mời bot vào kênh huấn luyện sales đã định nghĩa ở node Config.

#### 3. Kích hoạt ⚡️
- Thực hiện một cuộc gọi test trên Fireflies để kích hoạt Webhook.
- Kiểm tra dữ liệu chạy qua từng node trên n8n Editor.
- Sau khi chắc chắn mọi thứ trơn tru, bật công tắc **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể nhân bản nhánh thông báo để gửi thêm tin nhắn riêng qua Telegram Bot cho từng Sales Rep.
- **Tích hợp CRM:** Kết nối thêm node HubSpot hoặc Salesforce để gắn link các clip training này trực tiếp vào Deal tương ứng trên CRM.
- **Lọc thông minh bằng LLM:** Thêm một node AI (OpenAI/Anthropic) trước khi đẩy vào Google Sheets để tinh chỉnh lại mô tả tiếng Việt cho mượt mà và tự nhiên hơn với văn phong công ty.

### 📌 Kết luận
Workflow này là một "vũ khí tối tân" giúp tối ưu hóa quy trình coaching cho đội ngũ Sales, biến những dữ liệu thô từ cuộc gọi thành tài nguyên học tập quý giá một cách hoàn toàn tự động. Chúc các sếp cài đặt thành công và nâng tầm hiệu suất đội ngũ sales!