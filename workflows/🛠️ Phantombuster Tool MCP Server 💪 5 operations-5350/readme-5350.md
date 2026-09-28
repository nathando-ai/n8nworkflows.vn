```yaml
---
title: "🚀 Tự động hóa Phantombuster với n8n: Quản lý MCP Server như chuyên gia"
description: "Hướng dẫn chi tiết cách tự động hóa 5 thao tác chính của Phantombuster (Delete, Get, Add agent) để tiết kiệm thời gian và tăng hiệu suất làm việc"
slug: "tu-dong-hoa-phantombuster-voi-n8n-quan-ly-mcp-server"
tags: [n8n, automation, no-code, phantombuster, ai]
keywords: [n8n workflow, tự động hóa, phantombuster, mcp server, ai automation]
---
```

# 🚀 Tự động hóa Phantombuster với n8n: Quản lý MCP Server như chuyên gia

[Các sếp đang gặp khó khăn khi phải quản lý nhiều agent trên Phantombuster một cách thủ công. Workflow này sẽ giúp các sếp tự động hóa 5 thao tác chính nhất: Delete, Get, Add agent, và nhiều hơn nữa, tiết kiệm thời gian quý giá.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn 5 thao tác chính của Phantombuster
- Tiết kiệm thời gian quản lý agent
- Giảm lỗi do thao tác thủ công
- Tăng hiệu suất làm việc
- Hoạt động liên tục 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Phantombuster với API key
- Quyền truy cập vào n8n Editor
- Kiến thức cơ bản về n8n workflows
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/5350
3. Hoặc copy/paste JSON từ file workflow vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Phantombuster Tool MCP Server"**:
  - Chọn credentials cho Phantombuster
  - Cấu hình các tham số cần thiết cho MCP Server

- **Node "Delete an agent"**:
  - Điền ID của agent cần xóa
  - Xác nhận hành động xóa

- **Node "Get an agent"**:
  - Điền ID của agent cần lấy thông tin
  - Chọn các trường thông tin cần lấy

- **Node "Get many agents"**:
  - Cấu hình bộ lọc để lấy nhiều agent cùng lúc
  - Xác định số lượng agent cần lấy

- **Node "Get the output of an agent"**:
  - Điền ID của agent cần lấy output
  - Chọn định dạng output mong muốn

- **Node "Add an agent to the launch queue"**:
  - Cấu hình các tham số cho agent mới
  - Xác định thời gian chạy và các tùy chọn khác

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu cho từng node
- Kiểm tra kết quả của mỗi thao tác
- Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi các thao tác hoàn thành
- Lưu log các thao tác vào Google Sheets để theo dõi lịch sử
- Tự động gửi báo cáo định kỳ về trạng thái các agent
- Kết hợp với các công cụ khác để tạo pipeline hoàn chỉnh

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn việc quản lý MCP Server trên Phantombuster, tiết kiệm thời gian và giảm lỗi. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!