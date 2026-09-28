---
title: "📅 Tự động đồng bộ công việc Notion với Google Calendar & Google Sheets"
description: "Workflow n8n giúp tự động đồng bộ công việc từ Notion sang Google Calendar và theo dõi trên Google Sheets, tránh trùng lịch và nhận thông báo khi có xung đột"
slug: "tu-dong-dong-bo-cong-viec-notion-google-calendar-google-sheets"
tags: [n8n, automation, no-code, notion, google-calendar, google-sheets]
keywords: [n8n workflow, tự động hóa, đồng bộ lịch, quản lý công việc, google sheets]
---

# 📅 Tự động đồng bộ công việc Notion với Google Calendar & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải chuyển đổi công việc từ Notion sang Google Calendar thủ công. Quá trình này tốn thời gian, dễ xảy ra lỗi và không đồng bộ được trạng thái công việc. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ công việc từ Notion sang Google Calendar
- Theo dõi trạng thái công việc trên Google Sheets
- Nhận thông báo email khi có xung đột lịch
- Tránh trùng lịch và quản lý công việc hiệu quả hơn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion với database chứa công việc
- Tài khoản Google Calendar
- Tài khoản Google Sheets
- Tài khoản Gmail để nhận thông báo
- API keys cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14773](https://n8n.io/workflows/14773)
2. Click vào nút "Import" để tải xuống file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Get Task" (notionTrigger)**:
   - Chọn credentials của tài khoản Notion
   - Chọn database chứa công việc cần đồng bộ
   - Đảm bảo database có trường "Date" để xác định thời gian công việc

2. **Node "Check Availability" (googleCalendar)**:
   - Chọn credentials của tài khoản Google Calendar
   - Chọn calendar cần kiểm tra khả dụng
   - Cấu hình thời gian kiểm tra (thường là thời gian của công việc)

3. **Node "Record" (googleSheets)**:
   - Chọn credentials của tài khoản Google Sheets
   - Chọn spreadsheet và worksheet để lưu dữ liệu
   - Map các trường dữ liệu từ Notion sang Google Sheets (ID, Task Name, Due Date, Status)

4. **Node "If"**:
   - Cấu hình điều kiện kiểm tra khả dụng lịch (nếu không có sự kiện nào trùng thời gian)
   - Kết nối với node "Create an event" nếu có sẵn và "Send Error" nếu có xung đột

5. **Node "Create an event" (googleCalendar)**:
   - Chọn credentials của tài khoản Google Calendar
   - Chọn calendar để tạo sự kiện mới
   - Map các trường dữ liệu từ Notion sang sự kiện (tiêu đề, mô tả, thời gian)

6. **Node "Send Error" (gmail)**:
   - Chọn credentials của tài khoản Gmail
   - Cấu hình email nhận thông báo (thường là email của người quản lý)
   - Tùy chỉnh nội dung email thông báo xung đột lịch

7. **Node "Update Status" và "Update Status1" (googleSheets)**:
   - Chọn credentials của tài khoản Google Sheets
   - Chọn spreadsheet và worksheet chứa dữ liệu
   - Cấu hình cập nhật trạng thái công việc (thành công/ thất bại)

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để kiểm tra workflow hoạt động đúng
- Bật Active workflow để chạy tự động khi có sự kiện mới từ Notion

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo xung đột lịch
- Tích hợp với Google Tasks để quản lý công việc hàng ngày
- Tạo báo cáo định kỳ về trạng thái công việc từ Google Sheets
- Kết hợp với Google Meet để tạo cuộc họp tự động khi có sự kiện mới

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình đồng bộ công việc từ Notion sang Google Calendar và theo dõi trên Google Sheets. Với khả năng nhận thông báo xung đột lịch và cập nhật trạng thái công việc tự động, các sếp có thể quản lý thời gian và công việc hiệu quả hơn. Hãy áp dụng ngay để tiết kiệm thời gian và tránh các lỗi thường gặp trong quá trình quản lý công việc.