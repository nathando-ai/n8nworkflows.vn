---
title: "🚀 Kết nối eBay Taxonomy API với AI Agents để Quản lý Danh mục Tự động"
description: "Hướng dẫn tích hợp eBay Taxonomy API vào AI Agents thông qua n8n MCP Server, giúp trợ lý AI tự động tra cứu cây danh mục, thuộc tính và gợi ý danh mục sản phẩm."
slug: "expose-ebay-taxonomy-api-ai-agents"
tags: [n8n, automation, ai-agents, mcp, ebay, ecommerce, api]
keywords: [n8n workflow, ebay taxonomy api, ai agents, mcp server, quản lý danh mục ebay, n8n langchain]
---

# 🚀 Kết nối eBay Taxonomy API với AI Agents để Quản lý Danh mục Tự động

Các sếp làm trong ngành thương mại điện tử (E-commerce) chắc chắn hiểu rõ nỗi đau khi phải quản lý hàng ngàn danh mục sản phẩm (Categories) và các thuộc tính (Aspects) phức tạp của chúng trên sàn eBay. Việc tra cứu thủ công từng cây danh mục hay cập nhật thông tin thuộc tính tốn rất nhiều thời gian và dễ xảy ra sai sót. 

Giải pháp hoàn hảo cho các sếp đây: Workflow n8n này sẽ biến hệ thống của các sếp thành một **Model Context Protocol (MCP) Server**, cho phép các AI Agents trực tiếp "trò chuyện" và gọi các API phân loại của eBay một cách tự động, thông minh và chuẩn xác 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Trợ lý AI có thể tự tra cứu cây danh mục, cây con và ID mặc định của danh mục eBay.
- **Truy xuất thông tin chuẩn xác:** Tự động lấy các thuộc tính (Aspects), thuộc tính tương thích (Compatibility Properties) của danh mục lá (Leaf Category) mà không cần tra cứu thủ công.
- **Gợi ý thông minh:** Giúp AI đưa ra gợi ý danh mục chuẩn xác dựa trên tên hoặc mô tả sản phẩm.
- **Kết nối AI linh hoạt:** Dễ dàng tích hợp với Claude, ChatGPT hoặc các AI Agents hỗ trợ chuẩn MCP (Model Context Protocol).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Có hỗ trợ các tính năng LangChain / MCP (phiên bản n8n mới nhất).
- **eBay Developer Account:** Tài khoản nhà phát triển trên eBay để lấy API credentials (App ID, Cert ID, Dev ID hoặc OAuth Token) phục vụ cho các HTTP Request Tool.
- **AI Agent (Hỗ trợ MCP):** Ví dụ như Claude Desktop hoặc một AI Agent tùy chỉnh có khả năng kết nối tới n8n MCP Server.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n hoặc copy trực tiếp.
- Trong giao diện n8n Editor, nhấn vào menu ở góc trên bên phải, chọn **Import from File** (hoặc dùng tổ hợp phím `Ctrl + V` để paste trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes, trong đó 1 node kích hoạt MCP và 8 nodes thực hiện các tác vụ gọi eBay API. Các sếp cần cấu hình kỹ các điểm sau:
- **Taxonomy MCP Server (`mcpTrigger`):** Điểm khởi đầu đóng vai trò là server giao tiếp với AI Agents. Hãy cấu hình endpoint và xác thực (nếu cần) để AI Agents có thể kết nối an toàn.
- **Các node HTTP Request Tool (Fetch Category Tree, Retrieve Leaf Category Aspects, Fetch Category Subtree, Get Category Suggestions, Retrieve Compatibility Properties, Fetch Compatibility Values, Get Item Aspects by Category, Fetch Default Category Tree ID):**
  - Cấu hình **Credentials** (Bearer Token hoặc OAuth2) để kết nối với eBay Taxonomy API.
  - Kiểm tra lại các tham số truyền vào (Query Parameters / Headers) theo đúng tài liệu API của eBay (ví dụ: `X-EBAY-C-MARKETPLACE-ID`, cấu trúc JSON payload...).

#### 3. Kích hoạt ⚡️
- Kiểm tra kết nối từ AI Agent tới node **Taxonomy MCP Server**.
- Bật công tắc **Active** ở góc trên bên phải để kích hoạt workflow chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack Notification:** Thêm node thông báo mỗi khi AI thực hiện một truy vấn lớn hoặc gặp lỗi kết nối với eBay API.
- **Mở rộng API:** Tích hợp thêm các endpoint khác của eBay (như Inventory API hoặc Fulfillment API) vào cùng hệ thống MCP Server để tạo ra một "eBay Operations AI Agent" toàn diện.
- **Lưu Log:** Lưu trữ lịch sử các câu lệnh và phản hồi của AI vào Google Sheets hoặc Database để dễ dàng kiểm tra,audit về sau.

### 📌 Kết luận
Với workflow n8n này, việc quản lý danh mục sản phẩm trên eBay không còn là nỗi ác mộng thủ công. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc với AI Agents và bứt phá doanh số thương mại điện tử của các sếp!