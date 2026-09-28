---
title: "🚀 Tự động chuyển đổi vé Zendesk sang liên hệ Pipedrive và phân công nhiệm vụ"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi vé từ Zendesk sang liên hệ Pipedrive và phân công nhiệm vụ cho người dùng phù hợp"
slug: "tu-dong-chuyen-doi-ve-zendesk-sang-lien-he-pipedrive"
tags: [n8n, automation, no-code, sales, support]
keywords: [n8n workflow, tự động hóa, Zendesk, Pipedrive, CRM]
---

# 🚀 Tự động chuyển đổi vé Zendesk sang liên hệ Pipedrive và phân công nhiệm vụ

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý vé hỗ trợ và khách hàng trên hai hệ thống khác nhau. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ vé từ Zendesk sang Pipedrive
- Phân công nhiệm vụ cho người dùng phù hợp
- Tiết kiệm thời gian quản lý thủ công
- Giảm thiểu lỗi do nhập liệu
- Hoạt động liên tục 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zendesk với quyền truy cập API
- Tài khoản Pipedrive với quyền truy cập API
- API keys cho cả hai nền tảng
- Thời gian dự kiến để cấu hình: 30-45 phút
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/1806](https://n8n.io/workflows/1806)
2. Nhấn nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, nhấn nút "+" và chọn "Import from JSON"
4. Dán JSON đã sao chép và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get tickets created after last execution"**:
   - Cấu hình credentials cho Zendesk API
   - Đảm bảo tham số "operation" được đặt thành "getAll"

2. **Node "Search requester in pipedrive"**:
   - Cấu hình credentials cho Pipedrive API
   - Đảm bảo tham số "operation" là "search" và "resource" là "person"

3. **Node "Get owner information of Pipedrive contact"**:
   - Cấu hình credentials cho Pipedrive API
   - Đảm bảo URL endpoint đúng với cấu trúc API của Pipedrive

4. **Node "Change assignee to Pipedrive contact owner"**:
   - Cấu hình credentials cho Zendesk API
   - Đảm bảo tham số "operation" là "update"

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Node" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn nút "Activate" để kích hoạt workflow
3. Workflow sẽ chạy tự động mỗi 5 phút (có thể điều chỉnh trong node "Every 5 minutes")

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node gửi thông báo qua Slack/Teams khi có vé mới được xử lý
2. Tích hợp với Google Sheets để lưu trữ log các vé đã xử lý
3. Thêm bước xác nhận trước khi phân công nhiệm vụ
4. Tạo báo cáo hàng tuần về hiệu suất xử lý vé

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình quản lý vé hỗ trợ và khách hàng giữa Zendesk và Pipedrive, giảm thiểu công việc thủ công và tăng hiệu suất làm việc. Hãy thử ngay để trải nghiệm sự khác biệt!