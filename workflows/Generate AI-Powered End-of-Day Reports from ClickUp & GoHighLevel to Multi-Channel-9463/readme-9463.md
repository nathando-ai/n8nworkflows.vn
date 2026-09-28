---
title: "🚀 Tự động hóa Báo cáo Cuối ngày (EOD) từ ClickUp & GoHighLevel với AI bằng n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động tổng hợp task từ ClickUp, cơ hội sales từ GoHighLevel, dùng Azure OpenAI viết báo cáo và phân phối qua Slack, Email, Google Drive."
slug: "tu-dong-hoa-bao-cao-cuoi-ngay-clickup-gohighlevel-ai"
tags: [n8n, automation, ai-agent, clickup, gohighlevel, azure-openai]
keywords: [n8n workflow, tự động hóa báo cáo, clickup automation, gohighlevel crm, azure openai gpt-4o, eod report automation]
---

# 🚀 Tự động hóa Báo cáo Cuối ngày (EOD) từ ClickUp & GoHighLevel với AI

Các sếp có đang gặp tình trạng cuối ngày mệt mỏi vì phải lục lọi khắp nơi: vào ClickUp xem team hoàn thành task gì, vào GoHighLevel xem chốt được bao nhiêu deal, rồi ngồi gõ gõ viết báo cáo gửi sếp lớn hoặc vào nhóm Slack? Việc thủ công này vừa tốn thời gian, dễ sót việc lại cực kỳ nhàm chán.

Giải pháp ở đây là gì? Workflow n8n siêu cấp xịn sò này sẽ tự động hóa **100%** quy trình trên: tự động gom dữ liệu, dùng AI (Azure OpenAI GPT-4o) phân tích thông minh và bắn báo cáo chuyên nghiệp thẳng đến Slack, Email và Google Drive lúc 18:00 hàng ngày (Thứ 2 - Thứ 6). Các sếp chỉ việc nhấp ngụm trà và đọc báo cáo!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần**: Không còn cảnh thủ công tổng hợp số liệu từ nhiều nền tảng khác nhau.
- **Báo cáo thông minh từ AI**: Azure OpenAI tự động phân tích điểm sáng (wins), các nút thắt (blockers) và lên kế hoạch cho ngày mai.
- **Đa kênh phân phối đồng thời**: Gửi tin nhắn đẹp mắt qua Slack, Email HTML chuyên nghiệp và lưu file lưu trữ cẩn thận trên Google Drive.
- **Vận hành tự động 24/7**: Chạy đều đặn mỗi 18:00 các ngày trong tuần mà không cần chạm tay vào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Bản Self-hosted hoặc Cloud.
- **Tài khoản & API Keys**:
  - ClickUp (OAuth2 credentials)
  - GoHighLevel (OAuth2 credentials)
  - Azure OpenAI (API Key / Credentials)
  - Slack API (OAuth2 / Bot Token)
  - SMTP Server (Gmail, Outlook, SendGrid...) cho Email
  - Google Drive (OAuth2 credentials)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn mã JSON của workflow này hoặc tải file từ nguồn gốc, sau đó vào giao diện n8n Editor chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 17 nodes. Các sếp cần chú ý cấu hình kỹ các điểm sau để chạy mượt mà:

- **Schedule EOD Report Trigger**: Mặc định chạy lúc 18:00 (Thứ 2 - Thứ 6). Có thể chỉnh lại biểu thức Cron nếu muốn đổi giờ.
- **Fetch ClickUp Tasks for Today**: Cần kết nối ClickUp OAuth2 và **bắt buộc thay thế các ID mẫu** bằng Team ID, Space ID, Folder ID, và List ID thực tế của workspace công ty các sếp.
- **Fetch GHL Won Opportunities**: Kết nối GoHighLevel OAuth2. Mặc định node lọc các cơ hội đã thắng (`won`). Có thể tùy chỉnh thêm khoảng thời gian nếu cần.
- **AI Agent: Generate EOD Report & Azure OpenAI Chat Model**: Kết nối Azure OpenAI Credentials, chọn model `gpt-4o` và cấu hình bộ nhớ `Simple Memory` (Memory Buffer Window) để AI có ngữ cảnh tổng hợp tốt nhất.
- **Send Slack Message**: Kết nối Slack API, thay thế Channel ID mẫu bằng channel thực tế nơi team muốn nhận báo cáo (VD: `#eod-reports`).
- **Send Email Report**: Cấu hình SMTP credentials, thay đổi email người gửi (`fromEmail`) và người nhận (`toEmail`).
- **Upload Report to Google Drive**: Kết nối Google Drive, chọn thư mục đích (Nên tạo sẵn thư mục "EOD Reports" trên Drive để lưu trữ gọn gàng).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm với dữ liệu hiện tại xem các node có chạy xanh mướt không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Zalo**: Thay vì chỉ có Slack, có thể mở rộng thêm node Telegram để gửi báo cáo về nhóm chat cá nhân hoặc phòng ban trên Telegram.
- **Lưu lịch sử vào Google Sheets**: Thêm một node Google Sheets ở bước cuối để lưu lại các chỉ số chính (tổng task hoàn thành, tổng giá trị deal GHL) nhằm vẽ biểu đồ theo dõi hiệu suất tuần/tháng.
- **Tùy biến Prompt AI**: Trong AI Agent, các sếp có thể điều chỉnh system prompt để AI viết báo cáo theo đúng văn phong hài hước hoặc nghiêm túc tùy văn hóa công ty.

### 📌 Kết luận
Tự động hóa báo cáo cuối ngày với n8n và AI không chỉ giúp giải phóng sức lao động mà còn mang lại cái nhìn minh bạch, nhanh chóng cho toàn bộ ban quản lý. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất team ngay hôm nay!