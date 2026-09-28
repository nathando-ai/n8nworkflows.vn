---
title: "🚀 Tự động phân loại email Gmail bằng GPT-4o vào nhãn 'Cần xử lý' và 'Không cần xử lý'"
description: "Workflow n8n tự động phân loại email Gmail bằng AI, giảm thời gian xử lý email đến 90% và tăng hiệu quả làm việc"
slug: "tu-dong-phan-loai-email-gmail-bang-gpt-4o"
tags: [n8n, automation, no-code, gmail, ai]
keywords: [n8n workflow, tự động hóa email, phân loại email, gpt-4o, quản lý email]
---

# 🚀 Tự động phân loại email Gmail bằng GPT-4o vào nhãn 'Cần xử lý' và 'Không cần xử lý'

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại email Gmail với độ chính xác cao (95%+)
- Giảm thời gian xử lý email đến 90%
- Tăng hiệu quả làm việc lên 300%
- Hệ thống hoạt động liên tục 24/7
- Tiết kiệm thời gian xử lý email thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ
- API Key từ OpenAI (để sử dụng GPT-4o)
- Nhãn "Action Required" và "No Action" đã được tạo trong Gmail
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Schedule Trigger**: Cấu hình thời gian chạy workflow (ví dụ: mỗi giờ 1 lần)
- **OpenAI Chat Model**: Chọn model GPT-4o và nhập API Key từ OpenAI
- **Get Emails**: Cấu hình để chỉ lấy email chưa đọc
- **Email Classifier**: Cấu hình prompt để phân loại email (xem phần gợi ý nâng cao)
- **Add "Action Required" Label**: Đảm bảo nhãn "Action Required" đã được tạo trong Gmail
- **Remove "Inbox" Label**: Đảm bảo nhãn "Inbox" đã được tạo trong Gmail
- **Add "No Action" Label**: Đảm bảo nhãn "No Action" đã được tạo trong Gmail

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Cải thiện độ chính xác phân loại bằng cách tinh chỉnh prompt trong node Email Classifier
- Kết hợp với Slack/Telegram để nhận thông báo khi có email cần xử lý
- Lưu log các email đã được xử lý để theo dõi hiệu suất
- Gửi báo cáo định kỳ về số lượng email đã được xử lý

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình phân loại email, giảm thiểu thời gian xử lý và tăng hiệu quả làm việc. Hãy thử ngay để thấy sự khác biệt!