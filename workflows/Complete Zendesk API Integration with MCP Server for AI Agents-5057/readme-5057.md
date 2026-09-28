---
title: "🤖 Tích Hợp Zendesk API với MCP Server: Biến AI Agent thành Nhân viên CSKH"
description: "Hướng dẫn chi tiết cách kết nối Zendesk với AI Agent thông qua MCP Server trên n8n. Tự động hóa việc tạo, cập nhật và quản lý ticket, user, organization mà không cần viết code."
slug: "zendesk-mcp-ai-agent-n8n"
tags: [n8n, zendesk, mcp, ai-agent, customer-support, automation]
keywords: [n8n zendesk, mcp server n8n, ai agent zendesk, tự động hóa hỗ trợ khách hàng, integration zendesk api]
---

# 🤖 Tích Hợp Zendesk API với MCP Server: Biến AI Agent thành Nhân viên CSKH

Trong môi trường kinh doanh hiện đại, khối lượng ticket hỗ trợ khách hàng (CSKH) ngày càng tăng lên theo cấp số nhân. Việc nhân viên phải thủ công tra cứu dữ liệu, tạo ticket mới, hay cập nhật trạng thái trên Zendesk không chỉ tốn thời gian mà còn dễ gây sai sót.

Workflow này giải quyết triệt để bài toán đó bằng cách sử dụng **Model Context Protocol (MCP)** kết hợp với **n8n**. Thay vì viết hàng trăm dòng code để gọi API Zendesk, các sếp chỉ cần cấu hình một lần MCP Server. Kết quả là, bất kỳ AI Agent nào (như ChatGPT, Claude, hay các agent nội bộ) đều có thể "nói chuyện" trực tiếp với hệ thống Zendesk của bạn: tạo ticket, tìm kiếm user, cập nhật thông tin tổ chức... một cách tự nhiên và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo độ trễ thấp khi AI Agent gọi API, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình CSKH:** AI Agent có thể tự động tạo ticket khi nhận được email hoặc tin nhắn, giảm tải áp lực cho đội ngũ support.
- **Truy vấn dữ liệu thời gian thực:** Agent có thể tra cứu thông tin user, lịch sử ticket, hoặc thông tin tổ chức ngay lập tức mà không cần nhân viên can thiệp.
- **Tiết kiệm chi phí phát triển:** Không cần thuê lập trình viên viết middleware API phức tạp, chỉ cần cấu hình n8n một lần.
- **Mở rộng dễ dàng:** Với kiến trúc MCP, các sếp có thể dễ dàng thêm các tool khác (Slack, Google Sheets, CRM) vào cùng một Agent mà không cần thay đổi logic cốt lõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản Self-hosted hoặc Cloud (khuyến khích Self-hosted để tối ưu chi phí và bảo mật).
2. **Tài khoản Zendesk:** Cần có quyền truy cập API.
   - **API Token:** Tạo tại *Admin > Apps & Integrations > API*.
   - **Email người dùng:** Email của admin Zendesk.
   - **Subdomain:** Ví dụ: `yourcompany.zendesk.com`.
3. **Môi trường AI Agent:** Một client hỗ trợ MCP (ví dụ: n8n AI Agent, LangChain, hoặc các framework khác) để kết nối với MCP Server.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/5057](https://n8n.io/workflows/5057).
2. Nhấn nút **"Copy JSON"** hoặc tải file JSON về.
3. Mở n8n Editor, chọn **"Import from File"** hoặc dán trực tiếp JSON vào editor.
4. Workflow sẽ hiển thị 24 nodes, bao gồm 1 node `mcpTrigger` và 23 nodes `zendeskTool`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow này hoạt động dựa trên nguyên tắc **MCP (Model Context Protocol)**. Node `Zendesk Tool MCP Server` đóng vai trò là "cổng" để AI Agent giao tiếp.

**A. Cấu hình Credentials cho Zendesk**
Tất cả các node `zendeskTool` (Create a ticket, Get a user, v.v.) đều cần chung một credentials.
1. Nhấn vào node bất kỳ thuộc nhóm Zendesk (ví dụ: "Create a ticket").
2. Trong phần **Credentials**, chọn **"New Zendesk API"** hoặc chọn credentials đã có.
3. Điền thông tin:
   - **API Token:** Token đã tạo ở bước chuẩn bị.
   - **Email:** Email admin Zendesk.
   - **Subdomain:** Tên miền Zendesk của công ty (không cần `https://` hay `.zendesk.com`).

**B. Cấu hình MCP Trigger**
Node `Zendesk Tool MCP Server` (type: `mcpTrigger`) là trung tâm điều phối.
1. Nhấn vào node này.
2. Đảm bảo rằng nó được cấu hình để **expose** tất cả các tools Zendesk bên dưới.
3. *Lưu ý:* Trong n8n, các node `zendeskTool` được nối vào `mcpTrigger` sẽ tự động được đăng ký như các "tools" mà AI Agent có thể gọi. Các sếp không cần viết code để map từng hàm, n8n sẽ tự động sinh schema JSON cho AI hiểu.

**C. Kiểm tra các Tools chính**
Các sếp nên kiểm tra nhanh các node quan trọng sau để đảm bảo chúng hoạt động đúng với cấu trúc dữ liệu Zendesk của mình:
- **Create a ticket:** Kiểm tra các trường bắt buộc (Subject, Description, Requester ID).
- **Get many tickets:** Kiểm tra tham số phân trang (limit, offset) nếu cần lấy dữ liệu lớn.
- **Search a user:** Đảm bảo tham số tìm kiếm (email, name) được định nghĩa rõ ràng để AI không gọi sai.

:::note[LƯU Ý QUAN TRỌNG VỀ MCP]
MCP Server hoạt động theo chuẩn **Streamable HTTP** hoặc **SSE** (tùy phiên bản n8n). Khi kết nối từ AI Agent, các sếp cần cung cấp đúng URL endpoint của n8n (ví dụ: `https://your-n8n-domain.com/mcp/zendesk-tool-mcp-server`).
:::

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn nút **"Execute Workflow"** để kiểm tra xem có lỗi credentials hay cấu hình nào không.
   - Nếu dùng n8n AI Agent, hãy thử prompt: *"Hãy tạo một ticket mới với tiêu đề 'Test Ticket' và mô tả 'Đây là ticket test từ AI'."*
   - Kiểm tra xem ticket có xuất hiện trong dashboard Zendesk không.
2. **Bật Active:**
   - Sau khi test thành công, nhấn nút **"Active"** ở góc trên bên phải n8n.
   - Copy URL MCP Server để cấu hình vào client AI Agent của các sếp.

### ✍️ Mẹo & gợi ý nâng cao

1. **Kết hợp với LLM cho Prompt Engineering:**
   Thay vì để AI Agent tự suy luận, các sếp có thể thêm một node `LLM` trước khi gọi tool để "dịch" yêu cầu của khách hàng thành tham số API chuẩn xác hơn, giảm thiểu lỗi gọi API.

2. **Tự động hóa phản hồi:**
   Sau khi node "Create a ticket" chạy thành công, các sếp có thể nối thêm node **Zendesk (Send Email)** hoặc **Slack/Telegram** để thông báo ngay lập tức cho đội ngũ support hoặc gửi email xác nhận cho khách hàng.

3. **Log hoạt động vào Google Sheets:**
   Thêm node **Google Sheets** sau mỗi thao tác quan trọng (Create/Update ticket) để lưu lại lịch sử AI đã làm gì. Điều này cực kỳ hữu ích để audit và cải thiện chất lượng AI Agent.

4. **Phân quyền theo Organization:**
   Sử dụng tool "Get data related to an organization" để AI Agent có thể tự động gán ticket vào đúng tổ chức (Organization) dựa trên email domain của khách hàng, giúp phân loại ticket chính xác hơn.

### 📌 Kết luận

Việc tích hợp Zendesk với AI Agent thông qua MCP Server trên n8n là bước tiến lớn trong việc hiện đại hóa bộ phận CSKH. Các sếp không chỉ tiết kiệm được thời gian vận hành mà còn nâng cao trải nghiệm khách hàng nhờ phản hồi tức thì và chính xác.

Hãy import workflow này, cấu hình credentials Zendesk, và bắt đầu để AI "làm việc" thay cho các sếp ngay hôm nay! Nếu gặp khó khăn trong việc cấu hình MCP, đừng ngần ngại kiểm tra lại phiên bản n8n (khuyến nghị bản mới nhất) và đảm bảo URL endpoint được phép truy cập công khai (public) hoặc qua tunnel nếu chạy local.