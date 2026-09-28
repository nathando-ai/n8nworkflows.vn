---
title: "🚀 Tự động hóa Salesmate với n8n: Quản lý 15 thao tác CRM một cách liền mạch"
description: "Workflow n8n này giúp các sếp tự động hóa 15 thao tác quan trọng trong Salesmate CRM (Activity, Company, Deal) mà không cần code. Tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-hoa-salesmate-voi-n8n-quan-ly-15-thao-tac-crm"
tags: [n8n, automation, no-code, salesmate, crm]
keywords: [n8n workflow, tự động hóa, salesmate, crm, quản lý hoạt động]
---

# 🚀 Tự động hóa Salesmate với n8n: Quản lý 15 thao tác CRM một cách liền mạch

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý nhiều hoạt động CRM phải làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn 15 thao tác quan trọng trong Salesmate CRM
- Tiết kiệm thời gian đáng kể cho các công việc lặp lại
- Giảm sai sót do thủ công
- Tích hợp liền mạch với các hệ thống khác thông qua n8n
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Salesmate CRM với quyền truy cập API
- API Key của Salesmate (có thể lấy từ Settings > API Keys)
- Kiến thức cơ bản về cách sử dụng n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/5356)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Salesmate Tool MCP Server** (mcpTrigger):
   - Cần cấu hình credentials cho Salesmate
   - Điền API Key đã lấy từ Salesmate vào trường tương ứng

2. Các node Salesmate Tool khác (salesmateTool):
   - Mỗi node tương ứng với một thao tác trong Salesmate:
     - Activity: Create, Delete, Get, Get Many, Update
     - Company: Create, Delete, Get, Get Many, Update
     - Deal: Create, Delete, Get, Get Many, Update
   - Các sếp cần cấu hình các tham số đầu vào cho từng thao tác cụ thể

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu cho từng node để đảm bảo hoạt động đúng
- Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các node khác trong n8n để tạo luồng làm việc phức tạp hơn
- Thiết lập thông báo qua Slack/Telegram khi các thao tác quan trọng xảy ra
- Lưu log các hoạt động quan trọng để theo dõi và báo cáo
- Tạo các báo cáo định kỳ dựa trên dữ liệu từ Salesmate

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa các thao tác quan trọng trong Salesmate CRM. Với việc tích hợp liền mạch với n8n, các sếp có thể tạo ra các luồng làm việc phức tạp và hiệu quả mà không cần viết code. Hãy thử ngay để thấy sự khác biệt trong hiệu quả làm việc của bạn!