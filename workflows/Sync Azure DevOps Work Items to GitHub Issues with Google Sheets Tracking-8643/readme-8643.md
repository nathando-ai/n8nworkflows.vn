---
title: "🚀 Tự động đồng bộ Work Items từ Azure DevOps sang GitHub Issues với Google Sheets"
description: "Hướng dẫn tự động hóa quy trình đồng bộ Work Items từ Azure DevOps sang GitHub Issues và theo dõi trên Google Sheets để quản lý dự án hiệu quả hơn"
slug: "tu-dong-dong-bo-azure-devops-github-google-sheets"
tags: [n8n, automation, no-code, azure-devops, github, google-sheets]
keywords: [n8n workflow, tự động hóa, quản lý dự án, azure devops, github, google sheets]
---

# 🚀 Tự động đồng bộ Work Items từ Azure DevOps sang GitHub Issues với Google Sheets

[Các sếp] có biết rằng việc quản lý dự án thường tốn nhiều thời gian và dễ gây nhầm lẫn khi phải chuyển đổi thông tin giữa các công cụ khác nhau? Với workflow này, các sếp có thể tự động đồng bộ Work Items từ Azure DevOps sang GitHub Issues và theo dõi trên Google Sheets một cách liền mạch.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ thông tin giữa các công cụ mà không cần can thiệp thủ công.
- Quản lý hiệu quả: Theo dõi toàn bộ quy trình từ Azure DevOps đến GitHub trên một bảng Google Sheets duy nhất.
- Tăng tính minh bạch: Tạo liên kết trực tiếp giữa các công việc trong Azure DevOps và các Issues trên GitHub.
- Phân phối công việc: Tự động gán các Issues cho các thành viên trong nhóm để cân bằng công việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Azure DevOps với quyền truy cập vào các Work Items.
- Tài khoản GitHub với quyền tạo Issues và truy cập vào repository.
- Tài khoản Google với quyền truy cập vào Google Sheets.
- Các thông tin xác thực (credentials) cho các dịch vụ trên (Azure DevOps, GitHub, Google Sheets).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/8643](https://n8n.io/workflows/8643).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Webhook1**: Cấu hình path và HTTP method cho webhook nhận sự kiện từ Azure DevOps.
- **HTTP Request1**: Cấu hình credentials cho GitHub và URL API của Azure DevOps.
- **Code2**: Chỉnh sửa mã JavaScript để xử lý dữ liệu từ Azure DevOps.
- **HTTP Request2**: Cấu hình credentials cho GitHub và URL API của GitHub.
- **Webhook2**: Cấu hình path và HTTP method cho webhook nhận sự kiện từ Azure DevOps.
- **Google Sheets**: Cấu hình credentials cho Google Sheets và tên bảng cần ghi dữ liệu.
- **Google Sheets1**: Cấu hình credentials cho Google Sheets và tên bảng cần đọc dữ liệu.
- **Create Github Issue**: Cấu hình credentials cho GitHub và repository cần tạo Issues.
- **Filter Story Data**: Chỉnh sửa mã JavaScript để lọc và xử lý dữ liệu Story từ Azure DevOps.
- **Filter Task Data**: Chỉnh sửa mã JavaScript để lọc và xử lý dữ liệu Task từ Azure DevOps.
- **GitHub1**: Cấu hình credentials cho GitHub và các thông tin cần cập nhật cho Issues.
- **GitHub2**: Cấu hình credentials cho GitHub và các thông tin cần lấy từ Issues.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để thông báo khi có sự kiện mới.
- Lưu log các hoạt động vào Google Sheets để theo dõi lịch sử.
- Tự động gửi báo cáo hàng tuần về tiến độ dự án.
- Kết hợp với các công cụ khác như Trello, Jira để mở rộng phạm vi quản lý.

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ Work Items từ Azure DevOps sang GitHub Issues và theo dõi trên Google Sheets một cách liền mạch. Với việc tự động hóa quy trình này, các sếp có thể tiết kiệm thời gian, quản lý dự án hiệu quả hơn và tăng tính minh bạch trong quá trình làm việc. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của nhóm!