---
title: "📅 Tự động sao chép & đổi tên file Google khi có sự kiện lịch cụ thể"
description: "Tự động hóa quy trình sao chép và đổi tên file Google Drive khi có sự kiện lịch cụ thể trong Google Calendar. Tiết kiệm thời gian và đảm bảo tính nhất quán cho các file liên quan đến sự kiện."
slug: "tu-dong-sao-chep-doi-ten-file-google-khi-co-su-kien-lich-cua-google-calendar"
tags: [n8n, automation, no-code, google-calendar, google-drive]
keywords: [n8n workflow, tự động hóa, google calendar, google drive, sao chép file]
---

# 📅 Tự động sao chép & đổi tên file Google khi có sự kiện lịch cụ thể

[Các sếp] có biết rằng mỗi khi có sự kiện lịch quan trọng trong Google Calendar, các sếp lại phải thủ công sao chép và đổi tên file mẫu trên Google Drive để chuẩn bị cho sự kiện đó? Quy trình này tốn thời gian và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải thủ công sao chép và đổi tên file mỗi khi có sự kiện mới.
- **Đảm bảo tính nhất quán**: File được tạo ra luôn có tên chuẩn và đầy đủ thông tin.
- **Tự động hóa hoàn toàn**: Quy trình được thực hiện tự động mà không cần can thiệp của các sếp.
- **Tính linh hoạt cao**: Có thể tùy chỉnh tên file theo nhiều cách khác nhau dựa trên thông tin sự kiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để sử dụng Google Calendar và Google Drive).
- File mẫu trên Google Drive mà các sếp muốn sao chép.
- Quyền truy cập vào Google Calendar và Google Drive của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/2145](https://n8n.io/workflows/2145) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON vừa tải về.
3. Hoặc, copy toàn bộ nội dung JSON từ trang web và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "New event in Google Calendar"**:
   - Chọn credentials **googleCalendarOAuth2Api**.
   - Cấu hình các tham số cần thiết như Calendar ID, Event Type, và các tham số lọc sự kiện.

2. **Node "Filter specific event"**:
   - Thiết lập bộ lọc để chỉ lấy các sự kiện cụ thể mà các sếp quan tâm.
   - Ví dụ: Lọc theo tiêu đề sự kiện, mô tả, hoặc người tổ chức.

3. **Node "Search folder"**:
   - Chọn credentials **googleDriveOAuth2Api**.
   - Nhập ID của thư mục chứa file mẫu mà các sếp muốn sao chép.

4. **Node "Search file to duplicate"**:
   - Chọn credentials **googleDriveOAuth2Api**.
   - Nhập tên hoặc ID của file mẫu mà các sếp muốn sao chép.

5. **Node "Create and rename Google File"**:
   - Chọn credentials **googleDriveOAuth2Api**.
   - Cấu hình tên mới cho file sao chép bằng cách sử dụng các biến từ sự kiện lịch.
   - Ví dụ: `{Title of the event} | {date of the event} | {attendees}`.

#### 3. Kích hoạt ⚡️
- Sau khi cấu hình xong, các sếp có thể test run workflow với dữ liệu mẫu để đảm bảo hoạt động đúng.
- Khi đã kiểm tra và đảm bảo hoạt động ổn định, các sếp có thể bật **Active workflow** để tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tạo nhiều đường dẫn cho các loại sự kiện khác nhau**: Các sếp có thể tạo nhiều đường dẫn khác nhau trong workflow để xử lý các loại sự kiện khác nhau với các file mẫu khác nhau.
- **Kết hợp với các công cụ lịch khác**: Các sếp có thể thay thế node Google Calendar bằng các trigger từ các công cụ lịch khác như Calendly hoặc Hubspot.
- **Gửi thông báo qua Slack/Email**: Các sếp có thể thêm node để gửi thông báo qua Slack hoặc Email mỗi khi có sự kiện mới và file được sao chép thành công.
- **Lưu log hoạt động**: Các sếp có thể thêm node để lưu log hoạt động của workflow để theo dõi và kiểm tra lại sau này.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình sao chép và đổi tên file Google Drive khi có sự kiện lịch cụ thể trong Google Calendar. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian, đảm bảo tính nhất quán và tự động hóa hoàn toàn quy trình này. Hãy áp dụng ngay để trải nghiệm hiệu quả của tự động hóa!