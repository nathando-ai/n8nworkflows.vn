---
title: "📊 Theo dõi tinh thần đội nhóm từ tin nhắn Teams/Slack với AI Gemini"
description: "Tự động phân tích cảm xúc từ tin nhắn công việc hàng tuần, tạo báo cáo tinh thần đội nhóm và gửi kết quả lên Slack - giải pháp AI không cần code cho quản lý nhân sự."
slug: "theo-doi-tinh-than-doi-nhom-voi-ai-gemini"
tags: [n8n, automation, no-code, ai, hr, sentiment-analysis]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, tinh thần đội nhóm, báo cáo nhân sự]
---

# 📊 Theo dõi tinh thần đội nhóm từ tin nhắn Teams/Slack với AI Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của quản lý nhân sự khi phải theo dõi tinh thần đội nhóm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và phân tích tin nhắn hàng tuần
- **Phân tích chính xác**: Sử dụng AI Gemini để đánh giá cảm xúc và mức độ stress
- **Báo cáo tự động**: Tạo báo cáo tinh thần đội nhóm hàng tuần
- **Hệ thống hóa**: Theo dõi tình trạng tinh thần đội nhóm liên tục
- **Dễ theo dõi**: Gửi báo cáo trực tiếp lên Slack cho quản lý
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft Teams và Slack với quyền truy cập vào các kênh cần theo dõi
- API key từ Google Gemini (đã được cấu hình trong n8n)
- ID của các kênh Teams/Slack cần theo dõi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/9926)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Workflow Configuration** node:
   - Cập nhật các ID kênh Teams/Slack cần theo dõi
   - Thiết lập ngày bắt đầu và kết thúc phân tích (mặc định là 7 ngày trước)

2. **Sentiment Analysis (OpenAI)1** node:
   - Đảm bảo đã cấu hình Google Palm API credentials trong n8n
   - Có thể điều chỉnh prompt để phù hợp với ngữ cảnh công việc của đội nhóm

3. **Send a message1** node:
   - Cấu hình Slack credentials
   - Chỉnh sửa kênh đích để nhận báo cáo

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow và kiểm tra báo cáo đầu tiên
3. Điều chỉnh lịch trình trong **Weekly Morale Check Trigger** node nếu cần

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node lưu trữ báo cáo vào Google Sheets để theo dõi dài hạn
- Kết hợp với workflow khác để gửi báo cáo email hàng tuần
- Thêm cảnh báo khi phát hiện mức stress cao bất thường
- Tích hợp với các công cụ quản lý nhân sự khác như BambooHR

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để theo dõi tinh thần đội nhóm thông qua phân tích cảm xúc từ tin nhắn công việc hàng ngày. Với sự tự động hóa hoàn toàn và tích hợp AI, các sếp có thể nhận được báo cáo tinh thần đội nhóm hàng tuần một cách nhanh chóng và chính xác, giúp cải thiện môi trường làm việc và hiệu suất công việc.