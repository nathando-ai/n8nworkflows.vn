---
title: "🛠️ Tự động hóa Bảo mật Microsoft 365 với n8n: MCP Server 5 Operations"
description: "Hướng dẫn tự động hóa 5 thao tác bảo mật Microsoft 365 (Get Secure Score, Get Control Profiles, Update Profile) bằng n8n - giải pháp không cần code cho quản trị viên IT."
slug: "tu-dong-hoa-bao-mat-microsoft-365-voi-n8n"
tags: [n8n, automation, no-code, Microsoft 365, security]
keywords: [n8n workflow, tự động hóa bảo mật, Microsoft Graph Security, MCP Server]
---

# 🛠️ Tự động hóa Bảo mật Microsoft 365 với n8n: MCP Server 5 Operations

[Đoạn mở đầu: Phân tích nỗi đau thực tế của quản trị viên IT khi phải theo dõi thủ công các chỉ số bảo mật Microsoft 365. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa 5 thao tác bảo mật Microsoft 365 trong một workflow duy nhất
- Theo dõi Secure Score và Control Profiles một cách liên tục
- Cập nhật cấu hình bảo mật tự động theo lịch trình
- Giảm thời gian xử lý thủ công từ 30-50% cho các nhiệm vụ bảo mật
- Nhận cảnh báo tức thời khi chỉ số bảo mật xuống dưới ngưỡng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft 365 với quyền truy cập Microsoft Graph API
- Application ID và Client Secret từ Azure AD (đã được cấp quyền Security.Read.All và Security.ReadWrite.All)
- Quyền truy cập vào n8n instance (self-hosted hoặc cloud)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/5180)
2. Click vào nút "Copy JSON" để sao chép cấu hình
3. Trong n8n Editor, click vào menu "Workflow" > "Import from Clipboard"
4. Dán JSON đã sao chép và click "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Microsoft Graph Security Tool MCP Server** (Node đầu tiên):
   - Chọn "Create" operation
   - Điền các tham số:
     - `Name`: Đặt tên cho MCP Server (ví dụ: "Security Monitoring Server")
     - `Description`: Mô tả ngắn về mục đích của server
     - `Endpoint URL`: URL của n8n instance (ví dụ: `https://your-n8n-instance.com/webhook/mcp`)

2. **Get a secure score**:
   - Chọn credentials đã cấu hình Microsoft Graph
   - Điền `Tenant ID` của tổ chức Microsoft 365

3. **Get many secure scores**:
   - Chọn cùng credentials với node trước
   - Có thể thêm bộ lọc để lấy secure scores cho các tổ chức con

4. **Get a secure score control profile**:
   - Chọn credentials Microsoft Graph
   - Điền `Control Profile ID` (có thể tìm trong Microsoft Security & Compliance Center)

5. **Get many secure score control profiles**:
   - Chọn credentials Microsoft Graph
   - Có thể thêm bộ lọc để lấy các control profiles cụ thể

6. **Update a secure score control profile**:
   - Chọn credentials Microsoft Graph
   - Điền `Control Profile ID` cần cập nhật
   - Cấu hình các tham số cập nhật (ví dụ: `IsEnabled`, `Weight`)

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách click vào nút "Execute Workflow"
2. Kiểm tra kết quả ở các node cuối cùng
3. Bật Active workflow bằng cách click vào nút "Activate" ở góc trên bên phải

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo tức thời khi secure score xuống dưới ngưỡng
- Thiết lập lịch chạy định kỳ để cập nhật control profiles hàng tuần
- Lưu log các thay đổi bảo mật vào Google Sheets/Excel cho mục đích báo cáo
- Tạo báo cáo tự động gửi qua email hàng tháng về tình trạng bảo mật

### 📌 Kết luận
Workflow này giúp các quản trị viên IT tự động hóa 5 thao tác bảo mật Microsoft 365 quan trọng nhất một cách hiệu quả. Bằng cách triển khai workflow này, các sếp có thể tiết kiệm thời gian đáng kể và đảm bảo hệ thống luôn được bảo vệ tốt nhất. Hãy thử ngay và nâng cao khả năng bảo mật của tổ chức!