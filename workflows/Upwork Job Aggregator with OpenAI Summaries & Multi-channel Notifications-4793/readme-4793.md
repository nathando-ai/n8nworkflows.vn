---
title: "🚀 Tự động hóa tìm kiếm việc làm Upwork với tóm tắt AI và thông báo đa kênh"
description: "Workflow n8n tự động hóa việc tìm kiếm việc làm Upwork, lưu vào Google Sheets, tóm tắt bằng AI và gửi thông báo qua email - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-hoa-tim-kiem-viec-lam-upwork-voi-tom-tat-ai"
tags: [n8n, automation, no-code, upwork, google-sheets, openai, email]
keywords: [n8n workflow, tự động hóa tìm việc, upwork, google sheets, openai, email]
---

# 🚀 Tự động hóa tìm kiếm việc làm Upwork với tóm tắt AI và thông báo đa kênh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi hàng trăm việc làm Upwork hàng ngày. Giới thiệu workflow như giải pháp tự động hóa hoàn chỉnh 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-4 giờ mỗi ngày khi không cần theo dõi thủ công
- Lọc và lưu trữ hàng trăm việc làm mỗi ngày vào Google Sheets
- Nhận tóm tắt thông minh từ OpenAI về các việc làm phù hợp
- Thông báo tức thời qua email với nội dung đã được định dạng sẵn
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Upwork (để xác thực với Apify)
- Tài khoản Google (cho Google Sheets và Gmail)
- Tài khoản OpenAI (cho dịch vụ tóm tắt)
- API key từ Apify (để truy cập dữ liệu việc làm)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4793](https://n8n.io/workflows/4793)
2. Chọn "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Daily Upwork Job Trigger"**:
   - Chỉnh sửa biểu thức cron để đặt tần suất chạy phù hợp (mặc định là hàng ngày)

2. **Node "Fetch Upwork Jobs (Apify)"**:
   - Thay thế `<TASK_ID>` và `<API_TOKEN>` trong URL bằng thông tin từ Apify
   - Có thể thêm các tham số tìm kiếm như `searchQuery` trong body request

3. **Node "Log Jobs to Google Sheet"**:
   - Tạo một Google Sheet mới với các cột: Title, URL, Description, Budget, Date
   - Chọn credentials Google Sheets OAuth2 và nhập ID của Google Sheet
   - Đảm bảo Sheet Name trong node khớp với tên Sheet trong Google Sheets

4. **Node "OpenAI Job Summarizer"**:
   - Chọn credentials OpenAI API
   - Có thể chỉnh sửa prompt để phù hợp với nhu cầu cụ thể
   - Đảm bảo chọn model phù hợp (gpt-4o-mini hoặc các model khác)

5. **Node "Send Job Summary Email"**:
   - Thiết lập credentials Gmail OAuth2
   - Chỉnh sửa địa chỉ email nhận thông báo
   - Có thể tùy chỉnh nội dung email theo ý muốn

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Sau khi xác nhận hoạt động bình thường, bật chế độ Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Lọc việc làm**: Thêm node để lọc các việc làm theo từ khóa cụ thể trước khi lưu vào Google Sheets
2. **Tránh trùng lặp**: Lưu trữ ID của các việc làm đã xử lý để tránh lưu trùng
3. **Thêm kênh thông báo**: Kết nối với Slack hoặc Telegram để nhận thông báo tức thời
4. **Báo cáo định kỳ**: Tạo báo cáo tổng hợp từ Google Sheets để theo dõi xu hướng việc làm

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc tìm kiếm và quản lý việc làm Upwork. Với khả năng tự động hóa hoàn chỉnh và tích hợp AI, các sếp có thể tập trung vào các công việc quan trọng hơn. Hãy thử ngay và nâng cấp quy trình tìm việc của bạn!