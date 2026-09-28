---
title: "🚀 Tích hợp eBay Browse API cho AI Agents với n8n MCP Server"
description: "Hướng dẫn cấu hình workflow n8n giúp kết nối eBay Browse API thông qua Model Context Protocol (MCP), cho phép AI Agents tìm kiếm sản phẩm và quản lý giỏ hàng tự động."
slug: "tich-hop-ebay-browse-api-ai-agents-mcp-server"
tags: [n8n, automation, no-code, ai-agents, mcp, ebay-api]
keywords: [n8n workflow, ebay browse api, ai agents, mcp server, tich hop ai, tu dong hoa]
keywords: [n8n workflow, ebay browse api, ai agents, mcp server, tich hop ai, tu dong hoa]
---

# 🚀 Tích hợp eBay Browse API cho AI Agents với n8n MCP Server

Việc kết nối các Trợ lý AI (AI Agents) với dữ liệu thương mại điện tử thực tế như eBay thường gặp nhiều rào cản về code, xác thực API phức tạp và quản lý tool. Thay vì viết code thủ công từ đầu, workflow n8n này sẽ biến n8n thành một **MCP (Model Context Protocol) Server**, giúp AI Agents của các sếp dễ dàng gọi trực tiếp eBay Browse API để tìm kiếm sản phẩm, xem chi tiết và thao tác với giỏ hàng một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Kết nối AI liền mạch:** Cho phép AI Agents tương tác trực tiếp với kho hàng khổng lồ của eBay thông qua giao thức MCP chuẩn hóa.
- **Tự động hóa toàn diện:** Hỗ trợ từ việc tìm kiếm sản phẩm (theo từ khóa, hình ảnh, mã ID), kiểm tra tính tương thích cho đến quản lý giỏ hàng (thêm, xóa, sửa số lượng).
- **Không cần code phức tạp:** Toàn bộ các HTTP Request gọi đến eBay API đã được đóng gói sẵn thành các tool dạng kéo thả trong n8n.
- **Mở rộng linh hoạt:** Dễ dàng tích hợp thêm các công cụ thương mại điện tử khác vào hệ sinh thái AI Agent của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt n8n (hỗ trợ tính năng LangChain / MCP nodes).
- **eBay Developer Account:** Tài khoản nhà phát triển trên eBay để lấy thông tin xác thực (API Keys / OAuth tokens) cho các node HTTP Request.
- **AI Client hỗ trợ MCP:** Claude Desktop, Cursor hoặc một AI Agent bất kỳ hỗ trợ kết nối Model Context Protocol (MCP Server).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn cung cấp hoặc tải file JSON, sau đó dán trực tiếp vào n8n Editor của mình thông qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 12 nodes chính đóng vai trò làm công cụ (Tools) cho MCP Server:
- **Browse MCP Server (`mcpTrigger`):** Điểm khởi đầu tiếp nhận yêu cầu từ AI Agent. Các sếp cần cấu hình kết nối MCP để AI Client có thể nhận diện các tool bên dưới.
- **Các node HTTP Request Tool (Retrieve Item Details, Search Item Summaries, Add Item to Cart, v.v.):** 
  - Các sếp cần cấu hình **Credentials** (Bearer Token hoặc OAuth2) lấy từ tài khoản eBay Developer của mình.
  - Kiểm tra lại các endpoint URL và tham số truyền vào (như định dạng query, item ID, cart ID) cho khớp với tài liệu cập nhật mới nhất của eBay Browse & Cart API.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test run** bằng cách kết nối với AI Client hỗ trợ MCP để kiểm tra xem AI có gọi được các tool tìm kiếm sản phẩm hay không.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật trạng thái **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo:** Thêm node Telegram hoặc Slack sau các thao tác giỏ hàng quan trọng để nhận thông báo thời gian thực khi AI thực hiện giao dịch hoặc tìm kiếm sản phẩm hot.
- **Lưu lịch sử tìm kiếm:** Đưa dữ liệu sản phẩm mà AI tìm kiếm vào Google Sheets hoặc PostgreSQL để phân tích xu hướng mua sắm của người dùng.
- **Bảo mật Endpoint:** Đảm bảo kênh giao tiếp MCP Server được bảo vệ an toàn nếu triển khai trên môi trường Production công khai.

### 📌 Kết luận
Với workflow tích hợp eBay Browse API qua n8n MCP Server này, các sếp đã có thể nâng cấp AI Agents của mình lên một tầm cao mới—biết tự động tìm kiếm, tra cứu và thao tác giỏ hàng trên sàn thương mại điện tử lớn như một trợ lý ảo thực thụ. Hãy triển khai ngay hôm nay!