---
title: "🚀 Tự động hóa 9 thao tác MCP Server với Emelia Tool - Giải phóng sức lao động"
description: "Workflow n8n giúp tự động hóa 9 thao tác chính của MCP Server (Add contact, Create campaign, Duplicate campaign...) trong 1 workflow duy nhất. Tiết kiệm thời gian và tránh lỗi thủ công."
slug: "tu-dong-hoa-9-thao-tac-mcp-server-emelia-tool"
tags: [n8n, automation, no-code, emelia, mcp-server]
keywords: [n8n workflow, tự động hóa, emelia tool, mcp server, campaign management]
---

# 🚀 Tự động hóa 9 thao tác MCP Server với Emelia Tool - Giải phóng sức lao động

[Các sếp] có biết rằng mỗi ngày bạn phải thực hiện 9 thao tác cơ bản trên MCP Server (thêm liên hệ, tạo chiến dịch, sao chép chiến dịch...) bằng tay? Việc này tốn thời gian, dễ gây lỗi và không thể lặp lại được. Với workflow này, các sếp có thể tự động hóa hoàn toàn 9 thao tác này trong 1 workflow duy nhất, giúp tiết kiệm thời gian và tránh sai sót.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc quản lý MCP Server
- Giảm thiểu sai sót do thao tác thủ công
- Tự động hóa hoàn toàn 9 thao tác chính của MCP Server
- Hệ thống hoạt động liên tục 24/7 mà không cần can thiệp
- Tăng hiệu quả làm việc cho đội ngũ marketing
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Emelia Tool với quyền truy cập đầy đủ
- API Key của Emelia Tool
- Danh sách liên hệ (contacts) và chiến dịch (campaigns) đã chuẩn bị
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/5272)
2. Click vào nút "Copy Workflow"
3. Mở n8n Editor của bạn
4. Click vào nút "Import from Clipboard"
5. Dán nội dung đã copy vào và nhấn "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Emelia Tool MCP Server"**:
   - Chọn credentials của bạn trong phần "Authentication"
   - Đảm bảo API Key đã được nhập chính xác

2. **Các node Emelia Tool khác**:
   - Đối với các node như "Add a contact to a campaign", "Create a campaign"...
   - Kiểm tra và điều chỉnh các tham số đầu vào theo nhu cầu của bạn
   - Đảm bảo các trường bắt buộc đã được điền đầy đủ

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả ở mỗi node để đảm bảo hoạt động đúng
3. Sau khi test thành công, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành
2. **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets hoặc Database
3. **Tự động báo cáo**: Thêm node gửi báo cáo định kỳ qua email
4. **Xử lý lỗi tự động**: Thêm node xử lý lỗi và gửi cảnh báo khi có vấn đề

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn 9 thao tác chính của MCP Server với Emelia Tool, tiết kiệm thời gian đáng kể và giảm thiểu sai sót. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ marketing!