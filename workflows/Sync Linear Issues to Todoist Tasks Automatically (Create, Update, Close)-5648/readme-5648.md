---
title: "🚀 Tự động đồng bộ công việc từ Linear sang Todoist - Giải pháp quản lý dự án không cần code"
description: "Tự động đồng bộ công việc giữa Linear và Todoist giúp tiết kiệm thời gian, giảm lỗi và duy trì tính nhất quán giữa hai công cụ quản lý dự án."
slug: "tu-dong-dong-bo-cong-viec-linear-sang-todoist"
tags: [n8n, automation, no-code, project-management, todoist, linear]
keywords: [n8n workflow, tự động hóa, quản lý dự án, todoist, linear]
---

# 🚀 Tự động đồng bộ công việc từ Linear sang Todoist - Giải pháp quản lý dự án không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng gặp phải tình trạng này: quản lý công việc giữa hai công cụ khác nhau (Linear và Todoist) khiến việc cập nhật thông tin trở nên rối rắm và mất thời gian. Với workflow này, các sếp có thể tự động đồng bộ công việc giữa hai nền tảng này một cách liền mạch, tiết kiệm thời gian và giảm thiểu lỗi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động đồng bộ công việc giữa Linear và Todoist mà không cần can thiệp thủ công.
- **Giảm lỗi**: Tránh tình trạng thông tin không đồng bộ giữa hai công cụ quản lý dự án.
- **Tính nhất quán**: Duy trì tính nhất quán giữa các công việc trong Linear và Todoist.
- **Tự động hóa hoàn toàn**: Không cần lập trình, chỉ cần cấu hình một lần và quên đi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n với quyền truy cập OAuth2 vào **Linear** và **Todoist**.
- Email của bạn trong **Linear** đã được cấu hình trong workflow để lọc công việc.
- Một dự án Todoist mục tiêu (mặc định: *Inbox*).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [workflow gốc trên n8n](https://n8n.io/workflows/5648).
2. Nhấp vào nút **"Use Workflow"** để tải xuống file JSON.
3. Trong n8n Editor, nhấp vào **"Import from File"** và chọn file JSON vừa tải xuống.

Hoặc, các sếp cũng có thể copy/paste JSON từ trang workflow gốc vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "New issue or updated issue" (linearTrigger)**:
   - Cấu hình credentials cho Linear OAuth2 API.
   - Đảm bảo node này được kích hoạt để lắng nghe các sự kiện từ Linear.

2. **Node "Check if task already exists1" (todoist)**:
   - Cấu hình credentials cho Todoist API.
   - Đảm bảo node này được cấu hình để tìm kiếm công việc dựa trên ID của issue trong Linear.

3. **Node "If action's due date is not empty and assignee is me" (if)**:
   - Thay thế `youremail@example.com` bằng email của bạn trong Linear để lọc các công việc được giao cho bạn.

4. **Node "If it's a sub-issue" (if)**:
   - Cấu hình để kiểm tra xem issue có phải là sub-issue hay không.

5. **Node "Get parent issue" (linear)**:
   - Cấu hình để lấy thông tin của parent issue nếu issue hiện tại là sub-issue.

6. **Node "Set title with parent and sub-issue" (set)**:
   - Cấu hình để thiết lập tiêu đề của công việc trong Todoist với định dạng `[Parent] → Sub-Issue`.

7. **Node "Update task" (todoist)**:
   - Cấu hình để cập nhật công việc trong Todoist với thông tin mới từ Linear.

8. **Node "Close task" (todoist)**:
   - Cấu hình để đóng công việc trong Todoist khi issue trong Linear được đánh dấu là "Done".

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. **Test run dữ liệu mẫu**:
   - Tạo một issue mới trong Linear và kiểm tra xem workflow có hoạt động như mong đợi hay không.
   - Kiểm tra xem công việc tương ứng có được tạo, cập nhật hoặc đóng trong Todoist hay không.

2. **Bật Active workflow**:
   - Sau khi đã kiểm tra và đảm bảo workflow hoạt động đúng, các sếp có thể bật chế độ Active để workflow chạy tự động khi có sự kiện từ Linear.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể thêm các node để gửi thông báo qua Slack hoặc Telegram khi có sự kiện từ Linear.
- **Lưu log hoạt động**: Các sếp có thể thêm các node để lưu log hoạt động của workflow để theo dõi và kiểm tra.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo định kỳ về các công việc đã được đồng bộ.
- **Tích hợp với các công cụ khác**: Các sếp có thể mở rộng workflow để tích hợp với các công cụ quản lý dự án khác như Jira, Asana, v.v.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa hoàn chỉnh để đồng bộ công việc giữa Linear và Todoist, giúp tiết kiệm thời gian và giảm thiểu lỗi. Các sếp chỉ cần cấu hình một lần và quên đi, workflow sẽ tự động hoạt động khi có sự kiện từ Linear. Hãy áp dụng ngay để tối ưu hóa quy trình quản lý dự án của bạn!