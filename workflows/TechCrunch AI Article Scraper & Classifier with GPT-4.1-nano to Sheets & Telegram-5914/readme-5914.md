---
title: "🚀 Tự động hóa thu thập và phân loại tin tức TechCrunch bằng AI GPT-4.1-nano"
description: "Workflow n8n tự động thu thập tin tức AI từ TechCrunch, phân loại bằng GPT-4.1-nano và gửi kết quả đến Google Sheets & Telegram - tiết kiệm 90% thời gian nghiên cứu thị trường"
slug: "tu-dong-hoa-thu-thap-tin-tuc-techcrunch-ai"
tags: [n8n, automation, no-code, ai, market-research]
keywords: [n8n workflow, tự động hóa, ai research, techcrunch, gpt-4.1-nano]
---

# 🚀 Tự động hóa thu thập và phân loại tin tức TechCrunch bằng AI GPT-4.1-nano

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 90% thời gian thu thập tin tức TechCrunch hàng ngày
- Phân loại tự động tin tức AI với độ chính xác cao
- Lưu trữ dữ liệu có cấu trúc trên Google Sheets
- Nhận thông báo tức thời qua Telegram
- Hoạt động liên tục 24/7 với lịch trình tự động
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key từ OpenAI (để sử dụng GPT-4.1-nano)
- Bot Telegram và Chat ID để nhận thông báo
- URL nguồn tin tức TechCrunch (hoặc bất kỳ trang web nào có cấu trúc tương tự)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5914](https://n8n.io/workflows/5914)
2. Click "Download" để tải file JSON workflow
3. Trong n8n Editor, click "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger1"**:
   - Cấu hình lịch chạy theo nhu cầu (mặc định là hàng ngày lúc 8:00 AM UTC)

2. **Node "TechCrunchNews-AI1"**:
   - Thay đổi URL trong HTTP Request nếu nguồn tin tức thay đổi
   - Đảm bảo cấu trúc HTML của trang không thay đổi

3. **Node "Gpt-4.1-nano"**:
   - Tạo credentials mới cho OpenAI API
   - Đảm bảo tài khoản có đủ credit để sử dụng GPT-4.1-nano

4. **Node "NewsData" (Google Sheets)**:
   - Tạo credentials mới cho Google Sheets API
   - Chỉnh sửa Sheet ID và tên Sheet phù hợp
   - Cấu hình các cột dữ liệu trong Google Sheets theo cấu trúc đầu ra của workflow

5. **Node "Send a text message" (Telegram)**:
   - Tạo credentials mới cho Telegram API
   - Nhập Bot Token và Chat ID của người nhận

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ chuỗi xử lý
2. Kích hoạt workflow bằng cách nhấn nút "Active" trên thanh công cụ

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh phân loại**:
   - Chỉnh sửa prompt trong node "AI Agent1" để thay đổi tiêu chí phân loại tin tức
   - Thêm các nhãn phân loại mới vào output parser

2. **Kết hợp với Slack**:
   - Thêm node Slack sau node "Send a text message" để nhận thông báo trên Slack

3. **Lưu log hoạt động**:
   - Thêm node "Google Sheets" để lưu log các lần chạy workflow

4. **Tự động hóa báo cáo**:
   - Thêm node "Schedule Trigger" mới để tạo báo cáo hàng tuần/tuần

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc thu thập và phân tích tin tức TechCrunch. Với khả năng tự động hóa hoàn toàn và tích hợp AI, workflow này là công cụ mạnh mẽ cho nghiên cứu thị trường và theo dõi xu hướng công nghệ. Hãy thử ngay và nâng cao hiệu suất làm việc của mình!