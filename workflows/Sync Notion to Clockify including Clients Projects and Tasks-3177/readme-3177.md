---
title: "🔄 Tự động đồng bộ dữ liệu giữa Notion và Clockify: Khách hàng, Dự án và Nhiệm vụ"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu giữa Notion và Clockify cho khách hàng, dự án và nhiệm vụ, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-notion-clockify"
tags: [n8n, automation, no-code, Notion, Clockify, HR, quản lý thời gian]
keywords: [n8n workflow, tự động hóa, đồng bộ dữ liệu, Notion, Clockify, quản lý dự án, quản lý thời gian]
---

# 🔄 Tự động đồng bộ dữ liệu giữa Notion và Clockify: Khách hàng, Dự án và Nhiệm vụ

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng gặp phải tình trạng này: quản lý dữ liệu giữa các công cụ khác nhau như Notion và Clockify là một công việc tốn thời gian và dễ gây lỗi. Bạn phải thủ công nhập liệu, cập nhật thông tin giữa hai hệ thống này, và điều này không chỉ tốn thời gian mà còn dễ gây ra sai sót. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này một cách hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể: Tự động đồng bộ dữ liệu giữa Notion và Clockify mà không cần can thiệp thủ công.
- Giảm lỗi: Loại bỏ các lỗi nhập liệu do công việc thủ công.
- Dữ liệu đồng bộ: Đảm bảo dữ liệu luôn được cập nhật và đồng bộ giữa hai hệ thống.
- Tăng hiệu quả: Tự động hóa các tác vụ lặp đi lặp lại giúp các sếp tập trung vào công việc quan trọng hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion với cơ sở dữ liệu cho Khách hàng, Dự án và Nhiệm vụ.
- Tài khoản Clockify với quyền truy cập vào các tính năng cần đồng bộ.
- API keys cho cả Notion và Clockify.
- Cơ sở dữ liệu Notion phải có cấu trúc như sau:
  - **Khách hàng**: Tên (Text), Archive (Checkbox), Clockify Client ID (Text)
  - **Dự án**: Tên (Text), Status (Status), Clockify Client ID (Rollup), Clockify Project ID (Text)
  - **Nhiệm vụ**: Tên (Text), Status (Status), Clockify Project ID (Rollup), Clockify Task ID (Text), Clients (Rollup)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/3177](https://n8n.io/workflows/3177) để tải file JSON của workflow.
2. Mở n8n Editor và chọn "Import from File" hoặc "Import from URL".
3. Chọn file JSON đã tải về và nhấn "Import".

Hoặc, các sếp có thể copy/paste JSON vào n8n Editor bằng cách:

1. Truy cập vào trang [n8n.io/workflows/3177](https://n8n.io/workflows/3177) và copy nội dung JSON.
2. Mở n8n Editor và chọn "Import from Clipboard".
3. Dán nội dung JSON đã copy và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Webhook**: Cấu hình đường dẫn và phương thức HTTP cho webhook. Mặc định là `POST` và đường dẫn là `43028c1f-7331-4fbe-bf56-d6f47c92d9be`.
- **Globals**: Cấu hình các biến toàn cục nếu cần thiết. Mặc định, workflow sử dụng workspace ID đầu tiên.
- **Schedule Trigger**: Cấu hình lịch trình chạy workflow. Mặc định là chạy một lần mỗi ngày.
- **Get first workspace ID**: Cấu hình credentials cho Clockify API.
- **Get active Clients from Notion**: Cấu hình credentials cho Notion API và chọn cơ sở dữ liệu cho Khách hàng.
- **Get active Clients from Clockify**: Cấu hình credentials cho Clockify API.
- **If unmapped in Notion**: Cấu hình điều kiện để kiểm tra xem khách hàng có được ánh xạ trong Notion hay không.
- **Set new values**: Cấu hình các giá trị mới cho khách hàng.
- **Update Client in Clockify**: Cấu hình credentials cho Clockify API và các tham số cần cập nhật.
- **Get archived Client from Notion**: Cấu hình credentials cho Notion API và chọn cơ sở dữ liệu cho Khách hàng.
- **Create Client in Clockify**: Cấu hình credentials cho Clockify API và các tham số cần tạo mới.
- **Store Clockify ID in Notion**: Cấu hình credentials cho Notion API và các tham số cần cập nhật.
- **Remove Client from Clockify**: Cấu hình credentials cho Clockify API và các tham số cần xóa.
- **Get active Projects from Notion**: Cấu hình credentials cho Notion API và chọn cơ sở dữ liệu cho Dự án.
- **Get active Projects from Clockify**: Cấu hình credentials cho Clockify API.
- **Update Project in Clockify**: Cấu hình credentials cho Clockify API và các tham số cần cập nhật.
- **Get completed Project from Notion**: Cấu hình credentials cho Notion API và chọn cơ sở dữ liệu cho Dự án.
- **Create Project in Clockify**: Cấu hình credentials cho Clockify API và các tham số cần tạo mới.
- **Remove Project from Clockify**: Cấu hình credentials cho Clockify API và các tham số cần xóa.
- **Get active Tasks from Notion**: Cấu hình credentials cho Notion API và chọn cơ sở dữ liệu cho Nhiệm vụ.
- **Get active Tasks from Clockify**: Cấu hình credentials cho Clockify API.
- **Update Task in Clockify**: Cấu hình credentials cho Clockify API và các tham số cần cập nhật.
- **Get completed Task from Notion**: Cấu hình credentials cho Notion API và chọn cơ sở dữ liệu cho Nhiệm vụ.
- **Create Task in Clockify**: Cấu hình credentials cho Clockify API và các tham số cần tạo mới.
- **Remove Task from Clockify**: Cấu hình credentials cho Clockify API và các tham số cần xóa.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình các node quan trọng, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. **Test run dữ liệu mẫu**: Chạy workflow với dữ liệu mẫu để kiểm tra xem workflow có hoạt động như mong đợi hay không.
2. **Bật Active workflow**: Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, các sếp có thể bật workflow để chạy tự động theo lịch trình đã cấu hình.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm nút báo cáo trong Notion**: Các sếp có thể thêm một trường Formula trong cơ sở dữ liệu Dự án của Notion để tạo liên kết trực tiếp đến báo cáo thời gian trong Clockify.
- **Thêm nút đồng bộ trong Notion**: Các sếp có thể thêm một nút trong Notion để gọi webhook và đồng bộ dữ liệu giữa Notion và Clockify.
- **Tự động hóa thêm các tác vụ**: Các sếp có thể mở rộng workflow để tự động hóa các tác vụ khác như gửi thông báo khi có thay đổi dữ liệu.
- **Lưu log hoạt động**: Các sếp có thể cấu hình workflow để lưu log hoạt động và gửi báo cáo định kỳ.

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ dữ liệu giữa Notion và Clockify một cách hoàn toàn không cần code. Với workflow này, các sếp có thể tiết kiệm thời gian đáng kể và giảm lỗi do công việc thủ công. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!