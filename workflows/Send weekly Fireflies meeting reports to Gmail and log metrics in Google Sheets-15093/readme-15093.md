---
title: "📊 Tự động hóa báo cáo hàng tuần Fireflies: Gửi email và lưu dữ liệu vào Google Sheets"
description: "Hướng dẫn tự động hóa báo cáo hàng tuần từ Fireflies, tính toán các chỉ số quan trọng và gửi email báo cáo cùng lưu dữ liệu vào Google Sheets"
slug: "tu-dong-hoa-bao-cao-hang-tuan-fireflies-google-sheets-gmail"
tags: [n8n, automation, no-code, fireflies, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa báo cáo, fireflies, google sheets, gmail]
---

# 📊 Tự động hóa báo cáo hàng tuần Fireflies: Gửi email và lưu dữ liệu vào Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp quản lý thời gian cuộc họp khi phải làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa báo cáo hàng tuần, không cần làm thủ công
- Chính xác: Tính toán tự động các chỉ số quan trọng về cuộc họp
- Cá nhân hóa: Báo cáo được gửi đến email cá nhân của từng sếp
- Hoạt động liên tục: Chạy tự động mỗi thứ Sáu lúc 17h
- Theo dõi xu hướng: Dữ liệu được lưu vào Google Sheets để phân tích dài hạn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Fireflies với API key
- Tài khoản Google với Google Sheets và Gmail đã kích hoạt OAuth2
- Google Sheet đã tạo với tên tab "Weekly Meeting Report" và các cột: Week, Total Meetings, Total Hours, Avg Duration (min), Busiest Day, Top Participant, Longest Meeting, All Participants, Logged At
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/15093](https://n8n.io/workflows/15093)
2. Click vào nút "Import" để tải xuống file JSON của workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "2. Set — Config Values"**:
   - Thay thế `YOUR_FIREFLIES_API_KEY` bằng API key của Fireflies
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet
   - Thay thế tên tab Google Sheet (mặc định là "Weekly Meeting Report")
   - Thay thế địa chỉ email nhận báo cáo
   - Thay thế tên người gửi và tên công ty

2. **Node "6. Google Sheets — Log Weekly Summary"**:
   - Kết nối với tài khoản Google Sheets OAuth2 của bạn
   - Đảm bảo Google Sheet đã được tạo với cấu trúc cột như hướng dẫn

3. **Node "7. Gmail — Send Weekly Report"**:
   - Kết nối với tài khoản Gmail OAuth2 của bạn
   - Đảm bảo tài khoản này có quyền gửi email

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để chạy tự động mỗi thứ Sáu lúc 17h

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để gửi báo cáo cùng lúc với email
- Tạo báo cáo PDF đẹp hơn bằng các công cụ như PDFShift
- Thêm cảnh báo khi có cuộc họp quá dài hoặc quá nhiều cuộc họp trong ngày
- Tích hợp với các công cụ quản lý dự án như Asana hoặc Trello

### 📌 Kết luận
Workflow này giúp các sếp quản lý thời gian cuộc họp một cách hiệu quả hơn. Bằng cách tự động hóa báo cáo hàng tuần, các sếp có thể tập trung vào công việc quan trọng hơn và theo dõi xu hướng cuộc họp của đội nhóm một cách dễ dàng. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!