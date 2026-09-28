---
title: "🚀 [eBay] Tự động hóa thương lượng giá với MCP Server - Workflow n8n"
description: "Tự động hóa thương lượng giá trên eBay với MCP Server của n8n, giúp các sếp tiết kiệm thời gian và tối ưu hóa chiến lược bán hàng."
slug: "tu-dong-hoa-thuong-luong-gia-ebay-voi-mcp-server-n8n"
tags: [n8n, automation, no-code, eBay, MCP Server]
keywords: [n8n workflow, tự động hóa thương lượng giá, eBay MCP Server, AI RAG, lead nurturing]
---

# 🚀 [eBay] Tự động hóa thương lượng giá với MCP Server - Workflow n8n

[Các sếp đang gặp khó khăn khi phải thủ công thương lượng giá với khách hàng trên eBay. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình thương lượng giá thông qua MCP Server của n8n, giúp tiết kiệm thời gian và tối ưu hóa chiến lược bán hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình thương lượng giá trên eBay.
- Tiết kiệm thời gian và công sức cho các sếp.
- Tối ưu hóa chiến lược bán hàng thông qua dữ liệu thực tế.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản eBay Developer với quyền truy cập vào API.
- API Key và OAuth2 Credentials từ eBay Developer Portal.
- MCP Server của n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào n8n Editor. Để làm điều này, các sếp cần:
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import" trên thanh công cụ.
3. Chọn file JSON của workflow hoặc copy/paste JSON vào ô nhập liệu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Negotiation MCP Server**: Node này là điểm đầu vào cho các yêu cầu từ AI agent. Các sếp cần cấu hình đường dẫn (path) cho node này. Mặc định là "negotiation-mcp".
- **Find Eligible Listings**: Node này dùng để tìm kiếm các danh sách sản phẩm phù hợp để thương lượng. Các sếp cần cấu hình các tham số như API Key và OAuth2 Credentials.
- **Send Discount Offer**: Node này dùng để gửi các đề nghị giảm giá cho khách hàng. Các sếp cần cấu hình các tham số như API Key và OAuth2 Credentials.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể thêm các node biến đổi dữ liệu nếu cần thiết.
- Triển khai xử lý lỗi tùy chỉnh để đảm bảo tính ổn định của workflow.
- Thêm các node ghi log hoặc giám sát để theo dõi hoạt động của workflow.
- Thay đổi các tham số mặc định trong các node HTTP Request nếu cần thiết.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình thương lượng giá trên eBay, tiết kiệm thời gian và tối ưu hóa chiến lược bán hàng. Các sếp chỉ cần cấu hình các node quan trọng và kích hoạt workflow để bắt đầu sử dụng.