---
title: "🚀 Tự động phân loại phản hồi UAT sản phẩm với OpenAI, Notion, Slack và Gmail"
description: "Hướng dẫn tự động hóa phân loại phản hồi UAT sản phẩm bằng n8n, giảm 80% thời gian xử lý thủ công với AI và Notion"
slug: "tu-dong-phan-loai-phan-hoi-uat-san-pham"
tags: [n8n, automation, no-code, openai, notion]
keywords: [n8n workflow, tự động hóa, openai, notion, slack, gmail]
---

# 🚀 Tự động phân loại phản hồi UAT sản phẩm với OpenAI, Notion, Slack và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải xử lý hàng trăm phản hồi UAT sản phẩm mỗi ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Giảm 80% thời gian xử lý phản hồi UAT thủ công
- Tự động phân loại và tổng hợp thông tin phản hồi
- Ngăn chặn trùng lặp thông tin trong Notion
- Tự động thông báo cho tester qua Slack/Email
- Hoàn toàn tự động hóa quy trình từ nhận phản hồi đến cập nhật Notion
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key
- Tài khoản Notion với API key và database đã tạo sẵn
- Tài khoản Slack với API key (tùy chọn)
- Tài khoản Gmail với OAuth2 (tùy chọn)
- Dữ liệu mẫu phản hồi UAT để test workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/12208)
2. Click "Download" để tải file JSON
3. Trong n8n Editor, click "Import from File" và chọn file vừa tải
4. Hoặc copy nội dung JSON và paste vào "Import from Clipboard"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "trigger" (Webhook)**:
   - Thay đổi path trong "Path" field (ví dụ: "/uat-feedback")
   - Đảm bảo HTTP Method là POST

2. **Node "tester email" (Gmail)**:
   - Thiết lập credentials Gmail OAuth2
   - Cấu hình "From" và "To" email fields

3. **Node "slack tester" (Slack)**:
   - Thiết lập credentials Slack OAuth2
   - Cấu hình "Channel" hoặc "User ID" để gửi thông báo

4. **Node "double check" và "update/create notion database" (Notion)**:
   - Thiết lập credentials Notion API
   - Cập nhật "Database ID" trong các node Notion
   - Đảm bảo cấu trúc database Notion phù hợp với workflow

5. **Node "AI agent" (OpenAI)**:
   - Thiết lập credentials OpenAI API
   - Điều chỉnh prompt trong "Prompt" field nếu cần
   - Cấu hình "Model" và "Temperature" phù hợp

6. **Node "Webhook response"**:
   - Đảm bảo response format phù hợp với hệ thống gửi webhook

#### 3. Kích hoạt ⚡️
1. Test workflow với dữ liệu mẫu phản hồi UAT
2. Kiểm tra tất cả các node Notion, Slack, Gmail hoạt động đúng
3. Bật Active workflow khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo thời gian thực
2. Thêm node lưu log các phản hồi đã xử lý
3. Tự động gửi báo cáo hàng ngày về các phản hồi mới
4. Kết nối với hệ thống quản lý dự án để tự động tạo task

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình phân loại phản hồi UAT sản phẩm, giảm thời gian xử lý từ hàng giờ xuống vài phút. Hãy thử ngay và trải nghiệm sự khác biệt!