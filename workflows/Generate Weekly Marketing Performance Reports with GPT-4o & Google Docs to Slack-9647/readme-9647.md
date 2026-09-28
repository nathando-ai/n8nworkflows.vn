---
title: "🚀 Tự động hóa Báo cáo Hiệu suất Marketing Hàng tuần với GPT-4o & Google Docs lên Slack"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động tổng hợp số liệu quảng cáo, dùng AI viết báo cáo, tạo Google Doc và bắn thông báo lên Slack."
slug: "tu-dong-hoa-bao-cao-marketing-hang-tuan-n8n-gpt4o-google-docs-slack"
tags: [n8n, automation, ai-workflow, openai, google-docs, slack, marketing-automation]
keywords: [n8n workflow, báo cáo marketing tự động, gpt-4o marketing report, google docs api n8n, slack automation]
---

# 🚀 Tự động hóa Báo cáo Hiệu suất Marketing Hàng tuần với GPT-4o & Google Docs lên Slack

Các sếp có đang tốn hàng giờ mỗi thứ Hai đầu tuần chỉ để đăng nhập vào Google Ads, Meta, TikTok, mở Google Sheets, copy-paste số liệu, rồi ngồi vắt óc viết nhận xét cho sếp lớn hoặc khách hàng không? Công việc thủ công này không chỉ nhàm chán mà còn dễ sai sót và làm lu mờ đi giá trị thực sự của một Marketer.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa **100%** quy trình trên: Tự kéo số liệu, dùng AI (GPT-4o) phân tích thắng lợi/vấn đề, tạo một Google Docs chuẩn chỉnh và gửi ngay tóm tắt kèm link báo cáo nóng hổi lên Slack cho team. Không cần một dòng code phức tạp nào cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh loay hoay tổng hợp dữ liệu từ nhiều nền tảng quảng cáo vào đầu tuần.
- **Báo cáo chuyên nghiệp & chuẩn hóa:** Mọi báo cáo đều tuân theo một cấu trúc rõ ràng, kèm nhận định sắc bén từ AI.
- **Tăng tính minh bạch:** Team và khách hàng nhận ngay số liệu cốt lõi (ROAS, Spend) và link Google Doc trực tiếp trên Slack đúng giờ hẹn.
- **Dễ dàng mở rộng:** Dễ dàng thay thế dữ liệu demo bằng API thật của Google Ads, Meta Ads, TikTok chỉ với vài thao tác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để sử dụng model GPT-4o phân tích dữ liệu và viết Executive Summary.
- **Google OAuth2 Credentials:** Cấp quyền cho n8n tương tác với Google Docs.
- **Slack Workspace & Bot:** Cấp quyền cho n8n gửi tin nhắn vào kênh Slack chỉ định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn JSON gốc.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File / Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Schedule Trigger:** Thiết lập lịch chạy tự động (Ví dụ: 8:00 sáng mỗi thứ Hai hàng tuần).
- **Google Ads Demo (Code Node):** Node này hiện đang chứa dữ liệu giả lập (Demo) cho Google Ads, Meta, TikTok và YouTube. *Các sếp có thể thay thế node này bằng các HTTP Request hoặc node API chính thức của các nền tảng quảng cáo nếu muốn lấy dữ liệu real-time.*
- **Message a model (OpenAI Node):** 
  - Chọn Credentials OpenAI của các sếp.
  - Đảm bảo model được chọn là `gpt-4o` (hoặc model tương đương) để có chất lượng phân tích tốt nhất.
- **Code in JavaScript (Build Markdown Report):** Node này gộp dữ liệu thô và bản tóm tắt từ AI thành báo cáo Markdown hoàn chỉnh. Hãy chắc chắn tên tham chiếu các node trước đó khớp với code bên trong.
- **Create a document & Update a document (Google Docs Nodes):**
  - Kết nối `googleDocsOAuth2Api`.
  - Node `Create a document` sẽ tạo file mới với tên *"Weekly Performance Report – [Start Date] to [End Date]"*.
  - Node `Update a document` sẽ chèn toàn bộ nội dung Markdown do AI tổng hợp vào file vừa tạo.
- **Send a message (Slack Node):**
  - Kết nối `slackOAuth2Api`.
  - Chọn Channel ID nơi team hoặc khách hàng sẽ nhận thông báo.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu demo xem kết quả trả về Google Doc và Slack có mượt mà không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Nâng cấp trải nghiệm với Google Docs Template
Thay vì tạo một Google Doc trắng tinh, các sếp có thể nâng cấp bằng cách sử dụng **Template chuẩn nhận diện thương hiệu (Branding)**:
1. Tạo sẵn một file Google Doc mẫu với logo, màu sắc, font chữ công ty.
2. Lấy **Document ID** của file mẫu đó.
3. Thay thế node "Create a document" bằng thao tác **Copy Document** (sao chép template thành file mới mỗi tuần).
4. Dùng node update nội dung chèn báo cáo vào bản sao đó. Kết quả là báo cáo cực kỳ chuyên nghiệp và đồng bộ!

### 📌 Kết luận
Một quy trình báo cáo tưởng chừng tốn hàng buổi nay đã được tự động hóa gọn gàng chỉ trong vài phút thiết lập với n8n và GPT-4o. Hãy áp dụng ngay vào agency hoặc doanh nghiệp của các sếp để giải phóng sức lao động và nâng tầm chuyên nghiệp trong mắt khách hàng!