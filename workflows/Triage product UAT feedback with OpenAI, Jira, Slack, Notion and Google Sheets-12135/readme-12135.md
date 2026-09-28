---
title: "🚀 Tự động phân loại phản hồi UAT sản phẩm với OpenAI, Jira, Slack, Notion và Google Sheets"
description: "Hướng dẫn tự động hóa quy trình phân loại phản hồi UAT sản phẩm bằng n8n, kết hợp AI, Jira, Slack và Notion để tăng hiệu suất làm việc và giảm thời gian xử lý."
slug: "tu-dong-phan-loai-phan-hoi-uat-san-pham"
tags: [n8n, automation, no-code, ai, jira, slack, notion, google-sheets]
keywords: [n8n workflow, tự động hóa, phân loại phản hồi, UAT, AI, Jira, Slack, Notion]
---

# 🚀 Tự động phân loại phản hồi UAT sản phẩm với OpenAI, Jira, Slack, Notion và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải xử lý hàng trăm phản hồi UAT sản phẩm hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code, kết hợp AI và các công cụ quản lý sản phẩm phổ biến.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian xử lý phản hồi UAT hàng ngày
- Tăng độ chính xác phân loại phản hồi lên 95%
- Giảm thiểu sai sót do con người trong quá trình xử lý
- Tự động hóa toàn bộ quy trình từ nhận phản hồi đến thông báo kết quả
- Kết nối liền mạch giữa các công cụ quản lý sản phẩm (Jira, Notion, Slack)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Jira Software Cloud (đã cấu hình API)
- Tài khoản Slack (đã cấu hình OAuth2)
- Tài khoản Notion (đã cấu hình API)
- Tài khoản Google (đã cấu hình Google Sheets API)
- Tài khoản OpenAI (đã cấu hình API key)
- Tài khoản Gmail (đã cấu hình OAuth2)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/12135](https://n8n.io/workflows/12135)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

Hoặc bạn có thể copy/paste JSON từ trang web vào n8n Editor bằng cách:
1. Nhấn vào "Import from Clipboard"
2. Dán nội dung JSON từ trang web vào ô nhập liệu

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "trigger" (Webhook)**:
   - Cấu hình path: `/50b5cb50-43bb-42a5-9dda-1f50bf7ee356`
   - Phương thức HTTP: POST
   - Lưu ý: Đây là endpoint nhận phản hồi từ các công cụ khác (form, Slack, internal tool)

2. **Node "critical bug" (Jira)**:
   - Chọn credentials: `jiraSoftwareCloudApi`
   - Cấu hình các tham số cần thiết cho việc tạo issue mới trong Jira

3. **Node "engeneering alert" (Slack)**:
   - Chọn credentials: `slackOAuth2Api`
   - Cấu hình channel để gửi thông báo về bug nghiêm trọng

4. **Node "double check" (Notion)**:
   - Chọn credentials: `notionApi`
   - Cấu hình operation: `search`
   - Cần chỉ định database ID trong Notion để tìm kiếm

5. **Node "Append row in sheet" (Google Sheets)**:
   - Chọn credentials: `googleSheetsOAuth2Api`
   - Cấu hình operation: `append`
   - Chỉ định spreadsheet ID và tên sheet cần ghi dữ liệu

6. **Node "tester email" (Gmail)**:
   - Chọn credentials: `gmailOAuth2`
   - Cấu hình địa chỉ email người nhận và nội dung email

7. **Node "slack tester" (Slack)**:
   - Chọn credentials: `slackOAuth2Api`
   - Cấu hình channel để gửi thông báo cho tester

8. **Node "AI agent" (OpenAI)**:
   - Chọn credentials: `openAiApi`
   - Cấu hình prompt cho mô hình AI phân loại phản hồi

9. **Node "update notion database" (Notion)**:
   - Chọn credentials: `notionApi`
   - Cấu hình operation: `update`
   - Chỉ định database ID và các trường cần cập nhật

10. **Node "create notion database" (Notion)**:
    - Chọn credentials: `notionApi`
    - Cấu hình các trường cần thiết cho database mới

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả ở mỗi node để đảm bảo workflow hoạt động đúng
3. Khi đã kiểm tra xong, nhấn vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo qua Slack hoặc Telegram thay vì email
2. **Lưu log chi tiết**: Thêm node để ghi log chi tiết các phản hồi đã xử lý vào Google Sheets
3. **Gửi báo cáo định kỳ**: Thiết lập workflow con để tổng hợp và gửi báo cáo hàng tuần về các phản hồi đã xử lý
4. **Tích hợp với các công cụ khác**: Kết nối với các công cụ như Trello, Asana hoặc GitHub để mở rộng phạm vi quản lý sản phẩm

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình phân loại và xử lý phản hồi UAT sản phẩm, từ nhận phản hồi đến thông báo kết quả. Bằng cách kết hợp sức mạnh của AI với các công cụ quản lý sản phẩm phổ biến, workflow này không chỉ tiết kiệm thời gian mà còn tăng độ chính xác và hiệu quả trong quản lý sản phẩm. Hãy áp dụng ngay để nâng cao năng suất làm việc của đội ngũ!