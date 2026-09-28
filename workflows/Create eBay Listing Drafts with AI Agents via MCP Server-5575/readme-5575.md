---
title: "🚀 Tự Động Tạo Bản Nháp eBay Listing Bằng AI Agent qua MCP Server"
description: "Hướng dẫn thiết lập workflow n8n kết nối AI Agent với eBay API thông qua MCP Server, giúp tự động hóa việc tạo bản nháp sản phẩm (Listing Draft) chỉ với một câu lệnh."
slug: "tao-ban-nhap-ebay-listing-ai-mcp"
tags: [n8n, automation, no-code, ebay, ai-agent, mcp]
keywords: [n8n workflow, tự động hóa ebay, mcp server, ai agent, ebay api]
---

# 🚀 Tự Động Tạo Bản Nháp eBay Listing Bằng AI Agent qua MCP Server

Các sếp kinh doanh trên eBay hay đang vận hành đa kênh (Multi-channel) chắc hẳn đều hiểu nỗi đau khi phải nhập liệu thủ công từng sản phẩm. Việc sao chép mô tả, giá cả, hình ảnh từ website nội bộ hoặc các nền tảng khác sang eBay không chỉ tốn thời gian mà còn dễ xảy ra sai sót về thông tin.

Workflow này là giải pháp "chốt hạ" cho vấn đề đó. Thay vì dùng các script phức tạp, chúng ta sẽ sử dụng sức mạnh của **AI Agent** kết hợp với **MCP (Model Context Protocol)** Server trong n8n. Chỉ cần AI hiểu được ý định của bạn (hoặc dữ liệu đầu vào), nó sẽ tự động gọi API của eBay để tạo ra một bản nháp (Draft) hoàn chỉnh. Đây là bước đầu tiên trong quy trình tự động hóa bán hàng hoàn toàn không cần code (No-code).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo bảo mật cho các API keys, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** AI Agent tự động điền các trường thông tin sản phẩm vào eBay API, loại bỏ thao tác nhập liệu thủ công.
- **Tích hợp linh hoạt:** Sử dụng chuẩn MCP (Model Context Protocol), dễ dàng kết nối với bất kỳ AI Agent nào hỗ trợ MCP (như Claude, GPT-4, v.v.).
- **Giảm thiểu sai sót:** Dữ liệu được truyền trực tiếp từ AI đến API, tránh lỗi copy-paste.
- **Mở rộng dễ dàng:** Cấu trúc module hóa giúp các sếp dễ dàng thêm các bước xử lý dữ liệu (data transformation) trước khi gửi lên eBay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Phiên bản mới nhất hỗ trợ MCP Trigger và AI Nodes.
- **Tài khoản eBay Developer:** Các sếp cần có quyền truy cập vào eBay API (Lưu ý: API này có thể yêu cầu phê duyệt từ eBay cho các developer được chọn).
- **OAuth2 Credentials:** Cấu hình sẵn trong n8n để xác thực với eBay.
- **AI Agent:** Một hệ thống AI (có thể là workflow n8n khác hoặc ứng dụng bên ngoài) hỗ trợ giao tiếp qua MCP.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc: [n8n.io/workflows/5575](https://n8n.io/workflows/5575).
2. Mở n8n Editor, chọn **Import from File** hoặc dán trực tiếp code JSON vào editor.
3. Workflow sẽ hiển thị 2 node chính: `Listing MCP Server` và `Create eBay Listing Draft`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các điểm cấu hình quan trọng các sếp cần kiểm tra kỹ:

**1. Node: `Listing MCP Server` (MCP Trigger)**
- Đây là "cổng" để AI Agent kết nối vào workflow.
- **Path:** Mặc định là `listing-mcp`. Các sếp có thể đổi tên nếu muốn, nhưng cần đảm bảo đồng bộ với cấu hình phía AI Agent.
- **Webhook URL:** Sau khi kích hoạt workflow, hãy copy **Production URL** (hoặc Test URL khi đang chạy thử) của node này. Đây là địa chỉ mà AI Agent sẽ gọi tới.

**2. Node: `Create eBay Listing Draft` (HTTP Request Tool)**
- **Authentication:** Chọn **OAuth2** và gán credentials eBay đã tạo ở bước chuẩn bị.
- **URL:** Đảm bảo URL trỏ đúng đến endpoint `https://api.ebay.com` + `basePath` (thường là `/sell/fulfillment/v0/item_drafts` hoặc tương tự tùy phiên bản API).
- **Method:** Thường là `POST`.
- **Body:** Các trường thông tin sản phẩm (Title, Description, Price, Quantity, v.v.) sẽ được AI Agent tự động điền thông qua cơ chế `$fromAI()`. Các sếp không cần hardcode giá trị ở đây, mà cần đảm bảo schema dữ liệu khớp với yêu cầu của eBay API.

**3. Cấu hình AI Agent (Bên ngoài n8n)**
- Trong phần cấu hình của AI Agent (ví dụ: trong n8n AI Agent node hoặc ứng dụng bên ngoài), các sếp cần thêm MCP Server.
- **Server URL:** Dán Webhook URL lấy từ node `Listing MCP Server`.
- **Tools:** AI sẽ tự động nhận diện tool `Create eBay Listing Draft` và sử dụng nó khi người dùng yêu cầu tạo listing.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Chạy thử workflow bằng cách gửi một yêu cầu mẫu từ AI Agent (ví dụ: "Tạo một bản nháp cho sản phẩm áo thun màu đỏ, giá 10$").
2. Kiểm tra xem có lỗi xác thực (401/403) hay lỗi dữ liệu (400) không.
3. Nếu thành công, bật nút **Active** ở góc trên bên phải n8n Editor.
4. Copy lại **Production Webhook URL** và cập nhật vào cấu hình AI Agent.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước Validate Dữ liệu:** Chèn một node `Code` hoặc `IF` trước node HTTP Request để kiểm tra xem các trường bắt buộc (như Title, Price) đã có chưa trước khi gọi API, tránh lỗi không cần thiết.
- **Gửi thông báo qua Slack/Telegram:** Sau khi tạo bản nháp thành công, thêm một node `Slack` hoặc `Telegram` để gửi link quản lý bản nháp cho các sếp duyệt trước khi publish.
- **Lưu log vào Google Sheets:** Ghi lại lịch sử các listing đã tạo (ID, Title, Thời gian) vào Google Sheets để dễ dàng theo dõi và đối soát.
- **Xử lý lỗi (Error Handling):** Thêm một node `Error Trigger` hoặc cấu hình `On Error` để gửi cảnh báo khi API eBay bị lỗi hoặc hết quota.

### 📌 Kết luận
Việc kết hợp n8n, AI Agent và MCP Server mở ra một kỷ nguyên mới cho tự động hóa thương mại điện tử. Workflow này không chỉ giúp tiết kiệm hàng giờ nhập liệu mỗi ngày mà còn cho phép các sếp tập trung vào chiến lược kinh doanh thay vì các thao tác thủ công lặp đi lặp lại. Hãy bắt đầu với việc tạo bản nháp, sau đó mở rộng sang việc tự động publish và quản lý tồn kho. Chúc các sếp kinh doanh thành công!