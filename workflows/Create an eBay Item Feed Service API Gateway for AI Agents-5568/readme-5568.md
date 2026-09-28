---
title: "🚀 Xây Dựng API Gateway eBay Item Feed cho AI Agents với n8n & MCP"
description: "Hướng dẫn chi tiết cách tạo MCP Server trên n8n để AI Agents truy cập dữ liệu sản phẩm eBay (Item Feed, Group Feed, Priority Feed) một cách an toàn và hiệu quả."
slug: "ebay-item-feed-mcp-gateway-n8n"
tags: [n8n, mcp, ai-agents, ebay-api, automation]
keywords: [n8n workflow, mcp server, ebay item feed, ai agent tool, tự động hóa dữ liệu]
---

# 🚀 Xây Dựng API Gateway eBay Item Feed cho AI Agents với n8n & MCP

Trong kỷ nguyên của AI Agents, việc cho phép các trợ lý ảo truy cập trực tiếp vào dữ liệu thương mại điện tử là một thách thức lớn. Nếu để AI gọi thẳng API eBay, bạn sẽ đối mặt với rủi ro lộ API Key, khó kiểm soát tần suất gọi (rate limiting) và thiếu khả năng xử lý dữ liệu thô trước khi đưa vào context của LLM.

Workflow này giải quyết bài toán đó bằng cách biến n8n thành một **MCP (Model Context Protocol) Server**. Nó đóng vai trò là một "cổng" (Gateway) an toàn, nơi AI Agents có thể yêu cầu dữ liệu sản phẩm eBay (Item Feed, Group Feed, Priority Feed, Hourly Snapshot) mà không cần biết chi tiết kỹ thuật của API eBay. Các sếp chỉ cần cấu hình một lần, và AI sẽ tự động biết cách "hỏi" dữ liệu cần thiết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo độ trễ thấp cho các AI Agents, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật API Key:** API Key eBay được giấu kín trong n8n, AI Agent chỉ tương tác qua giao thức MCP an toàn.
- **Chuẩn hóa Dữ liệu:** Dữ liệu thô từ eBay được xử lý và định dạng sẵn trước khi đưa vào context của LLM, giúp AI hiểu chính xác hơn.
- **Hỗ trợ đa dạng Feed:** Truy cập linh hoạt 4 loại feed quan trọng: Item, Group, Priority, và Hourly Snapshot.
- **Tương thích AI Agents:** Hoạt động hoàn hảo với các framework hỗ trợ MCP như LangChain, LlamaIndex, hoặc các AI Agents tùy chỉnh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản Self-hosted hoặc Cloud (hỗ trợ MCP Trigger).
- **Tài khoản eBay Developer:** Cần có API Key và Secret để tạo OAuth Credentials hoặc API Key trực tiếp (tùy cấu hình HTTP Request).
- **Hiểu biết cơ bản về MCP:** Model Context Protocol là giao thức mới giúp AI giao tiếp với các công cụ bên ngoài.
- **Node.js:** Nếu chạy n8n local, đảm bảo phiên bản Node.js mới nhất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link workflow gốc: `https://n8n.io/workflows/5568` hoặc tải file JSON về và import.
4. Workflow sẽ hiển thị 5 nodes chính: 1 MCP Trigger và 4 HTTP Request Tools.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Workflow này sử dụng **MCP Trigger** làm điểm vào và 4 **HTTP Request Tools** làm công cụ (tools) cho AI.

**Node 1: Item Feed Service MCP Server (MCP Trigger)**
- Đây là node trung tâm. Nó khai báo các "tools" mà AI có thể gọi.
- **Cấu hình:** Đảm bảo tên MCP Server và mô tả rõ ràng để AI hiểu khi nào nên dùng tool nào.
- **Tools:** Trong phần cấu hình của node này, các sếp cần khai báo 4 tools tương ứng với 4 nodes HTTP Request bên dưới. Mỗi tool cần có:
    - `name`: Tên tool (ví dụ: `get_ebay_item_feed`).
    - `description`: Mô tả chi tiết tool này làm gì, input cần gì (ví dụ: "Lấy danh sách sản phẩm từ feed item của eBay").
    - `inputSchema`: Định nghĩa các tham số đầu vào (ví dụ: `feedId`, `date`, `format`).

**Node 2-5: Các HTTP Request Tools**
Mỗi node này đại diện cho một loại feed cụ thể. Các sếp cần cấu hình URL và Headers cho từng node:

1. **Download Item Feed**:
   - **Method:** GET
   - **URL:** `https://svcs.ebay.com/services/search/FindingService/v1?callname=findItems&...` (Tham khảo tài liệu eBay Finding Service hoặc Item Feed Service).
   - **Headers:** Thêm `Authorization` hoặc `X-EBAY-API-APP-NAME` với API Key của các sếp.
   - **Body:** Cấu hình các tham số query string như `itemID`, `feedType`, v.v.

2. **Download Item Group Feed**:
   - Tương tự, nhưng URL và tham số query sẽ khác để lấy dữ liệu theo nhóm sản phẩm.
   - Đảm bảo tham số `groupID` hoặc tương đương được truyền vào từ input của tool.

3. **Download Priority Item Feed**:
   - Dành cho các sản phẩm ưu tiên. Cấu hình URL và headers tương tự.
   - Lưu ý: Feed này có thể có giới hạn tần suất gọi cao hơn, hãy thêm logic delay nếu cần.

4. **Download Hourly Snapshot Feed**:
   - Lấy dữ liệu snapshot hàng giờ.
   - Tham số quan trọng: `timestamp` hoặc `hour` để xác định thời điểm snapshot.

**Lưu ý quan trọng về Credentials:**
- Tạo một **HTTP Request Credential** trong n8n chứa API Key/Secret của eBay.
- Gán credential này cho cả 4 nodes HTTP Request.
- **KHÔNG** hardcode API Key vào URL hay headers.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Chạy thử workflow bằng cách gửi một yêu cầu MCP từ một client hỗ trợ (ví dụ: một AI Agent test, hoặc dùng n8n's MCP Client nếu có).
   - Kiểm tra xem AI có gọi đúng tool không và dữ liệu trả về có đúng định dạng không.
2. **Bật Active:**
   - Sau khi test thành công, bật **Active** cho workflow.
   - Workflow sẽ lắng nghe các yêu cầu MCP từ các AI Agents.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Validation:** Trước khi gọi API eBay, thêm một node **Code** hoặc **IF** để kiểm tra xem tham số đầu vào từ AI có hợp lệ không (ví dụ: `itemID` có đúng định dạng không).
- **Cache Dữ liệu:** Nếu dữ liệu không thay đổi thường xuyên, hãy thêm một node **Redis** hoặc **Google Sheets** để cache kết quả, giảm tải cho API eBay và tăng tốc độ phản hồi.
- **Gửi Log:** Thêm một node **Slack** hoặc **Telegram** để gửi thông báo khi có lỗi xảy ra trong quá trình gọi API, giúp các sếp dễ dàng giám sát.
- **Mở rộng thêm Tools:** Các sếp có thể thêm các tool khác như "Search Items", "Get Item Details", "Get Seller Info" để biến n8n thành một gateway eBay đầy đủ.

### 📌 Kết luận
Với workflow này, các sếp đã có trong tay một API Gateway eBay chuyên nghiệp, an toàn và tương thích hoàn hảo với AI Agents. Thay vì để AI "lục lọi" trực tiếp vào API eBay, giờ đây AI chỉ cần "hỏi" qua MCP, và n8n sẽ lo phần còn lại. Đây là bước tiến quan trọng trong việc xây dựng các hệ thống AI tự động hóa thương mại điện tử. Hãy thử ngay và chia sẻ kết quả với cộng đồng!