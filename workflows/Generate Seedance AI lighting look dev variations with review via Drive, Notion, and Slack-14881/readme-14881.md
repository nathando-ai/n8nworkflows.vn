---
title: "🚀 Tự động hóa tạo 5 biến thể ánh sáng AI với Seedance, Google Drive, Notion và Slack trong n8n"
description: "Hướng dẫn chi tiết xây dựng hệ thống tự động hóa Look Dev ánh sáng VFX/3D bằng n8n, Seedance AI, Google Drive, Notion và Slack giúp tiết kiệm 90% thời gian."
slug: "tu-dong-hoa-tao-bien-the-anh-sang-ai-seedance-n8n"
tags: [n8n, automation, ai, seedance, google-drive, notion, slack]
keywords: [n8n workflow, seedance ai, vfx lighting look dev, tự động hóa n8n, ai video generation, notion lookbook]
---

# 🚀 Tự động hóa tạo 5 biến thể ánh sáng AI với Seedance, Google Drive, Notion và Slack

Đối với các nghệ sĩ kỹ thuật ánh sáng (Lighting TD) và giám sát kỹ xảo (VFX Supervisor), việc thử nghiệm và phát triển các phong cách ánh sáng (Look Dev) cho một cảnh quay thường tốn rất nhiều thời gian thủ công. Từ khâu lên ý tưởng, viết prompt, gọi API tạo video, kiểm tra trạng thái render, tải về, lưu trữ Google Drive đến việc tổng hợp báo cáo lên Notion và thông báo cho team qua Slack. 

Workflow n8n này sẽ giúp các sếp tự động hóa **100% quy trình từ A-Z** ngay sau khi nhận được yêu cầu từ Web Form, biến một bản brief đơn giản thành 5 biến thể ánh sáng chất lượng cao thông qua sức mạnh của Seedance AI.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận brief từ form, tự động tạo 5 biến thể ánh sáng (Key Light, Soft Diffuse, Dramatic, Plate Match, Comp Grade) song song.
- **Quản lý thông minh:** Tự động poll trạng thái render, tải video về, lưu trữ ngăn nắp trên Google Drive với tên file chuẩn hóa.
- **Báo cáo chuyên nghiệp:** Tổng hợp thành Lookbook trực quan trên Notion và sử dụng AI (OpenAI) để viết thông báo tóm tắt cực kỳ chuyên nghiệp gửi thẳng vào kênh Slack của team.
- **Giám sát lỗi chủ động:** Có sẵn Error Handler để bắn cảnh báo ngay lập tức qua Slack nếu có bất kỳ sự cố nào xảy ra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** (Self-hosted hoặc Cloud).
- **Seedance API Key:** Tài khoản và API key để gọi dịch vụ tạo video AI.
- **Google Drive account:** Tài khoản cấu hình OAuth2 để lưu trữ video render.
- **Notion account:** Tài khoản kết nối API để lưu cơ sở dữ liệu Lookbook.
- **Slack Workspace:** App/Bot Slack để gửi thông báo cho team.
- **OpenAI API Key:** Dành cho node AI tạo nội dung tin nhắn Slack thông minh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã JSON gốc từ nguồn cung cấp, mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp mã JSON vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Seedance: Generate Lighting Ref & Poll: Check Lighting Job Status (HTTP Request nodes):** Thay thế `YOUR_SEEDANCE_API_KEY` bằng API key thực tế của các sếp trong phần Header/Credentials.
- **Google Drive: Upload Lighting Ref:** Kết nối tài khoản **Google Drive OAuth2** và chỉ định ID thư mục đích (`Folder ID`) nơi lưu trữ các video render.
- **Notion: Record the log in Notion:** Kết nối **Notion API**, trỏ tới Database Look Dev đã chuẩn bị sẵn để lưu thông tin chi tiết.
- **Slack: Notify Lighting Team & Slack: Error Alert:** Kết nối **Slack OAuth2**, nhập Channel ID của team lighting vào các node Slack.
- **AI - Generate the slack message:** Cấu hình credentials cho **OpenAI API** để AI có thể tự động viết nội dung thông báo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng cách điền form thông qua node `n8n Form: Lighting Brief`.
- Kiểm tra toàn bộ luồng từ render đến khi nhận thông báo trên Slack/Notion.
- Bật công tắc **Active** để workflow chính thức hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể kết hợp thêm node Telegram hoặc Microsoft Teams để gửi thông báo song song với Slack.
- **Lưu lịch sử chi tiết:** Tích hợp thêm Google Sheets để thống kê lại số lượng request render theo ngày/tuần phục vụ việc quản lý chi phí API.
- **Tùy biến prompt AI:** Tinh chỉnh prompt trong các node Code hoặc OpenAI để phong cách thông báo phù hợp hơn với văn hóa công ty của các sếp.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc ứng dụng AI và No-Code vào quy trình sản xuất sáng tạo (VFX/3D). Hãy áp dụng ngay để giải phóng đội ngũ lighting khỏi các tác vụ thủ công nhàm chán và nâng tầm chuyên nghiệp cho doanh nghiệp của các sếp!