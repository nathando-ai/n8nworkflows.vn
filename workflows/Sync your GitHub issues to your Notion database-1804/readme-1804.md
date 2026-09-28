---
title: "🚀 Tự động đồng bộ Issues GitHub vào Notion - Workflow n8n hoàn hảo"
description: "Giải pháp tự động hóa 100% không cần code để đồng bộ Issues GitHub vào Notion database, tiết kiệm thời gian và đảm bảo dữ liệu luôn đồng bộ"
slug: "tu-dong-dong-bo-issues-github-vao-notion"
tags: [n8n, automation, no-code, github, notion]
keywords: [n8n workflow, tự động hóa, github, notion, đồng bộ dữ liệu]
---

# 🚀 Tự động đồng bộ Issues GitHub vào Notion - Workflow n8n hoàn hảo

[Các sếp đang gặp khó khăn khi phải chuyển đổi thủ công các Issues từ GitHub sang Notion database. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách hoàn hảo, đảm bảo dữ liệu luôn đồng bộ và tiết kiệm thời gian đáng kể.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ toàn bộ Issues từ GitHub sang Notion database
- Tiết kiệm thời gian đáng kể trong việc chuyển đổi thủ công
- Dữ liệu luôn đồng bộ giữa hai nền tảng
- Tự động cập nhật trạng thái Issues (mở/đóng) giữa hai nền tảng
- Giảm thiểu lỗi do nhập liệu thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với quyền truy cập vào repository chứa Issues
- Tài khoản Notion với quyền truy cập vào database cần đồng bộ
- API keys cho cả GitHub và Notion (sẽ được hướng dẫn trong phần cấu hình)
- Notion database đã được thiết lập với các trường dữ liệu tương ứng (Title, Status, Description...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n Editor](https://n8n.io/workflows/1804)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn file JSON của workflow hoặc copy/paste JSON từ trang này vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Trigger on issues" (githubTrigger)**:
   - Chọn credentials cho GitHub API
   - Cấu hình các tham số:
     - Repository: Chọn repository chứa Issues cần đồng bộ
     - Events: Chọn "issues" để theo dõi các thay đổi trên Issues

2. **Node "Create database page" (notion)**:
   - Chọn credentials cho Notion API
   - Cấu hình các tham số:
     - Database ID: ID của Notion database cần đồng bộ
     - Các trường dữ liệu cần map từ GitHub Issues (Title, Status, Description...)

3. **Node "Find database page" (notion)**:
   - Chọn credentials cho Notion API
   - Cấu hình các tham số:
     - Database ID: ID của Notion database cần đồng bộ
     - Filter: Sử dụng node "Create custom Notion filters" để tạo bộ lọc tìm kiếm

4. **Node "Create custom Notion filters" (function)**:
   - Chỉnh sửa hàm JavaScript để tạo bộ lọc tìm kiếm phù hợp với database của bạn
   - Ví dụ: `return { property: 'GitHub ID', text: { equals: $node["Trigger on issues"].json["issue"]["id"] } }`

5. **Node "Edit issue" (notion)**:
   - Chọn credentials cho Notion API
   - Cấu hình các tham số:
     - Page ID: Sử dụng output từ node "Find database page"
     - Các trường dữ liệu cần cập nhật

6. **Node "Delete issue" (notion)**:
   - Chọn credentials cho Notion API
   - Cấu hình các tham số:
     - Page ID: Sử dụng output từ node "Find database page"

7. **Node "Close issue" (notion)**:
   - Chọn credentials cho Notion API
   - Cấu hình các tham số:
     - Page ID: Sử dụng output từ node "Find database page"
     - Status: Cập nhật trạng thái thành "Closed"

8. **Node "Reopen issue" (notion)**:
   - Chọn credentials cho Notion API
   - Cấu hình các tham số:
     - Page ID: Sử dụng output từ node "Find database page"
     - Status: Cập nhật trạng thái thành "Open"

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Notion database để đảm bảo dữ liệu được đồng bộ chính xác
3. Nếu mọi thứ hoạt động tốt, click vào nút "Activate Workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động đồng bộ các comment trên Issues**: Thêm node để đồng bộ các comment từ GitHub sang Notion
2. **Thông báo qua Slack/Teams**: Kết nối với Slack hoặc Microsoft Teams để nhận thông báo khi có thay đổi trên Issues
3. **Lịch sử thay đổi**: Thêm node để ghi lại lịch sử thay đổi trên Issues trong Notion
4. **Xử lý lỗi tự động**: Thêm node để xử lý các lỗi xảy ra trong quá trình đồng bộ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình đồng bộ Issues từ GitHub sang Notion database, tiết kiệm thời gian đáng kể và đảm bảo dữ liệu luôn đồng bộ. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!