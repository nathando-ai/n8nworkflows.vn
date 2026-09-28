---
title: "🚀 Tự động đồng bộ thẻ Fizzy với công việc Basecamp thời gian thực"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ thẻ Fizzy với công việc Basecamp trong thời gian thực, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-the-fizzy-voi-cong-viec-basecamp-thoi-gian-thuc"
tags: [n8n, automation, no-code, project management, basecamp]
keywords: [n8n workflow, tự động hóa, đồng bộ dữ liệu, project management, basecamp]
---

# 🚀 Tự động đồng bộ thẻ Fizzy với công việc Basecamp thời gian thực

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải làm thủ công việc đồng bộ dữ liệu giữa các công cụ quản lý dự án. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ dữ liệu giữa Fizzy và Basecamp mà không cần can thiệp thủ công
- Giảm lỗi: Loại bỏ các lỗi do nhập liệu sai khi chuyển đổi dữ liệu giữa các công cụ
- Đồng bộ thời gian thực: Cập nhật trạng thái công việc ngay lập tức khi có thay đổi trên Fizzy
- Tích hợp liền mạch: Kết nối các công cụ quản lý dự án một cách mượt mà
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Basecamp với quyền truy cập API
- Tài khoản Fizzy với quyền cấu hình webhook
- ID tài khoản Basecamp của bạn
- Các dự án Basecamp đã được tạo sẵn với tên trùng khớp với tên bảng Fizzy
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấp vào biểu tượng "+" ở góc trái trên cùng
3. Chọn "Import from File" và tải lên file JSON của workflow
4. Hoặc copy/paste nội dung JSON vào phần "Import from JSON"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Set Basecamp account ID" (Code)**
   - Cập nhật giá trị `accountId` với ID tài khoản Basecamp của bạn
   - Ví dụ: `return { accountId: "12345678" };`

2. **Node "Receive Fizzy webhook" (Webhook)**
   - Đảm bảo webhook URL được cấu hình chính xác trong Fizzy
   - Đường dẫn: `/webhook/fizzyxbasecamp`
   - Phương thức: POST

3. **Node "Fetch Basecamp projects" (HTTP Request)**
   - Đảm bảo credentials "basecamp4OAuth2Api" đã được cấu hình
   - URL: `https://3.basecampapi.com/{{$node["Set Basecamp account ID"].json.accountId}}/projects.json`

4. **Node "Fetch Basecamp people" (HTTP Request)**
   - Đảm bảo credentials "basecamp4OAuth2Api" đã được cấu hình
   - URL: `https://3.basecampapi.com/{{$node["Set Basecamp account ID"].json.accountId}}/people.json`

5. **Node "Create new todolist" (Basecamp)**
   - Đảm bảo credentials "basecamp4OAuth2Api" đã được cấu hình
   - Tham số cần thiết: `projectId`, `name`

6. **Node "Create new todo" (Basecamp)**
   - Đảm bảo credentials "basecamp4OAuth2Api" đã được cấu hình
   - Tham số cần thiết: `todolistId`, `content`, `description`

7. **Node "Update todo assignees" (Basecamp)**
   - Đảm bảo credentials "basecamp4OAuth2Api" đã được cấu hình
   - Tham số cần thiết: `todoId`, `assignees`

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Kích hoạt workflow bằng cách nhấp vào nút "Active" ở góc trên cùng bên phải

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo khi có thay đổi công việc
- Lưu log các thay đổi vào Google Sheets để theo dõi lịch sử
- Tự động gửi báo cáo hàng ngày về tiến độ công việc
- Kết hợp với Google Calendar để quản lý thời gian công việc

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hoàn hảo cho việc đồng bộ dữ liệu giữa Fizzy và Basecamp. Với việc tự động hóa quy trình này, các sếp có thể tiết kiệm thời gian đáng kể và giảm thiểu các lỗi do nhập liệu thủ công. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!