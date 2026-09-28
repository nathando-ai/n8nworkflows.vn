---
title: "🚀 [eBay] Tự động hóa API Recommendation với MCP Server - Giải pháp tối ưu quảng cáo Promoted Listings"
description: "Hướng dẫn chi tiết cách tự động hóa API Recommendation của eBay để tối ưu quảng cáo Promoted Listings, tăng hiệu quả marketing và tiết kiệm thời gian cho các sếp"
slug: "tu-dong-hoa-api-recommendation-ebay-promoted-listings"
tags: [n8n, automation, no-code, eBay, marketing]
keywords: [n8n workflow, tự động hóa eBay, Promoted Listings, Recommendation API, tối ưu quảng cáo]
---

# 🚀 [eBay] Tự động hóa API Recommendation với MCP Server - Giải pháp tối ưu quảng cáo Promoted Listings

[Các sếp đang gặp khó khăn khi phải thủ công quản lý và tối ưu quảng cáo Promoted Listings trên eBay. Workflow này sẽ giúp tự động hóa toàn bộ quy trình, từ lấy dữ liệu đến tối ưu chiến dịch quảng cáo, giúp các sếp tiết kiệm thời gian và tăng hiệu quả marketing.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình tối ưu quảng cáo Promoted Listings
- Tiết kiệm thời gian quản lý thủ công
- Tăng hiệu quả chiến dịch quảng cáo
- Dữ liệu được cập nhật liên tục và chính xác
- Tích hợp dễ dàng với các AI agent khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản eBay Developer với quyền truy cập API
- API Key và OAuth2 credentials từ eBay Developer Portal
- Trình tự động hóa n8n đã được cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Node "Recommendation MCP Server"**:
  - Đảm bảo đường dẫn "path" được đặt là "recommendation-mcp"
  - Cấu hình OAuth2 credentials cho kết nối API eBay

- **Node "Get Promoted Listings Recommendations"**:
  - Điền đầy đủ thông tin API Key và OAuth2 credentials
  - Kiểm tra URL endpoint API eBay (https://api.ebay.com{basePath})
  - Cấu hình các tham số cần thiết cho API call

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.
- Copy URL từ MCP trigger để sử dụng trong AI agent của bạn.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm các node xử lý dữ liệu để biến đổi dữ liệu theo nhu cầu của bạn
- Thêm các node logging hoặc monitoring để theo dõi hoạt động của workflow
- Kết nối với các kênh thông báo như Slack hoặc Telegram để nhận thông báo khi có thay đổi quan trọng
- Tích hợp với các công cụ phân tích dữ liệu để theo dõi hiệu quả chiến dịch quảng cáo

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa và tối ưu quảng cáo Promoted Listings trên eBay. Bằng cách tích hợp với MCP Server, các sếp có thể dễ dàng kết nối với các AI agent khác và tự động hóa toàn bộ quy trình marketing. Hãy áp dụng ngay để tăng hiệu quả và tiết kiệm thời gian cho các chiến dịch quảng cáo của bạn!