---
title: "🛠️ Xây Dựng MCP Server Hacker News Trong n8n: Kết Nối AI Với Dữ Liệu Tech Thực Chiến"
description: "Hướng dẫn chi tiết cách tạo MCP Server cho Hacker News bằng n8n. Cho phép AI Agent truy vấn bài viết, người dùng và tin tức công nghệ một cách tự động, không cần code."
slug: "xay-dung-mcp-server-hacker-news-n8n"
tags: [n8n, mcp, ai-agent, hacker-news, automation]
keywords: [n8n workflow, mcp server, hacker news api, ai agent integration, tự động hóa n8n]
---

# 🛠️ Xây Dựng MCP Server Hacker News Trong n8n: Kết Nối AI Với Dữ Liệu Tech Thực Chiến

Trong kỷ nguyên của AI Agents, việc cho phép các mô hình ngôn ngữ lớn (LLM) truy cập trực tiếp vào dữ liệu thời gian thực là một bước tiến quan trọng. Tuy nhiên, việc tích hợp API thủ công cho mỗi nguồn dữ liệu (như Hacker News) thường tốn thời gian và dễ gặp lỗi.

Workflow này giải quyết vấn đề đó bằng cách biến n8n thành một **MCP (Model Context Protocol) Server** chuyên dụng cho Hacker News. Thay vì viết code Python/Node.js để đóng gói API, các sếp chỉ cần import workflow, bật Active, và cung cấp URL cho AI Agent (như Claude, Cursor, hoặc các agent nội bộ). Kết quả là một cầu nối chuẩn hóa, an toàn và cực kỳ nhanh chóng giữa AI và cộng đồng lập trình viên lớn nhất thế giới.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo AI Agent luôn truy cập được, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian code API**: Không cần viết backend riêng, n8n xử lý mọi thứ.
- **Tương thích chuẩn MCP**: Hoạt động liền mạch với các AI Agent hỗ trợ MCP (Claude Desktop, Cursor, v.v.).
- **Truy vấn linh hoạt**: Hỗ trợ 3 thao tác chính: Lấy tất cả tin tức, Lấy chi tiết bài viết, Lấy thông tin người dùng.
- **Zero-Config**: Workflow được thiết kế sẵn, chỉ cần bật là chạy, không cần cấu hình phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted) phiên bản mới nhất hỗ trợ MCP Trigger.
- Không cần API Key cho Hacker News (API công khai).
- Một AI Agent hỗ trợ giao thức MCP (ví dụ: Claude Desktop, Cursor, hoặc n8n AI Agent).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow hoặc upload file JSON đã tải về.
4. Workflow sẽ hiển thị 4 nodes chính: 1 MCP Trigger và 3 Hacker News Tool nodes.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Mặc dù workflow được thiết kế "ready-to-use", các sếp cần kiểm tra các điểm sau để đảm bảo hoạt động trơn tru:

*   **Node: `Hacker News Tool MCP Server` (MCP Trigger)**
    *   Đây là node quan trọng nhất. Nó đóng vai trò là cổng vào cho AI Agent.
    *   **Path**: Mặc định là `hacker-news-tool-mcp`. Các sếp có thể đổi tên này nếu muốn URL ngắn gọn hơn, nhưng nhớ cập nhật lại khi kết nối với AI Agent.
    *   **Authentication**: Workflow này không yêu cầu Auth (Public), nhưng nếu các sếp muốn bảo mật, có thể thêm API Key Authentication ở đây.

*   **Node: `Get many items` (Hacker News Tool)**
    *   **Resource**: Chọn `all`.
    *   **Operation**: Chọn `get`.
    *   **Parameters**: Node này sử dụng biểu thức `$fromAI()` để AI tự động điền tham số (ví dụ: số lượng tin tức cần lấy). Các sếp có thể chỉnh sửa mặc định nếu muốn giới hạn số lượng tin trả về để tránh quá tải.

*   **Node: `Get an article` (Hacker News Tool)**
    *   **Resource**: Chọn `article`.
    *   **Operation**: Chọn `get`.
    *   **Parameters**: AI sẽ tự động truyền `id` của bài viết dựa trên ngữ cảnh hội thoại.

*   **Node: `Get a user` (Hacker News Tool)**
    *   **Resource**: Chọn `user`.
    *   **Operation**: Chọn `get`.
    *   **Parameters**: AI sẽ tự động truyền `id` hoặc `username` của người dùng Hacker News.

:::note[Lưu ý về Expressions]
Các node Tool trong workflow này sử dụng `$fromAI()` expressions. Điều này có nghĩa là AI Agent sẽ tự động quyết định giá trị cho các trường nhập liệu dựa trên câu hỏi của người dùng. Các sếp không cần hardcode giá trị, nhưng cần đảm bảo prompt của AI Agent đủ rõ ràng để nó biết khi nào nên gọi tool nào.
:::

#### 3. Kích hoạt ⚡️
1. Nhấn nút **Save** để lưu workflow.
2. Bật công tắc **Active** ở góc trên bên phải.
3. Mở node `Hacker News Tool MCP Server`, copy **Webhook URL** (đường dẫn bắt đầu bằng `https://...`).
4. Dán URL này vào cấu hình MCP của AI Agent (ví dụ: trong `claude_desktop_config.json` hoặc cài đặt của Cursor).

### ✍️ Mẹo & gợi ý nâng cao
- **Lọc theo điểm (Points)**: Các sếp có thể thêm một node `IF` hoặc `Code` sau node `Get many items` để chỉ trả về những bài viết có điểm cao hơn một ngưỡng nhất định, giúp AI tập trung vào tin tức chất lượng.
- **Tích hợp thêm Reddit/HN**: Tạo thêm các MCP Server tương tự cho Reddit, Product Hunt và kết hợp chúng vào một AI Agent duy nhất để có cái nhìn toàn diện về xu hướng tech.
- **Lưu log truy vấn**: Thêm một node `Google Sheets` hoặc `Database` để ghi lại các truy vấn mà AI Agent thực hiện, giúp các sếp phân tích hành vi người dùng và tối ưu prompt.
- **Cá nhân hóa Prompt**: Trong node MCP Trigger, các sếp có thể thêm một đoạn system prompt ngắn để hướng dẫn AI cách sử dụng các tool này một cách hiệu quả nhất (ví dụ: "Ưu tiên lấy tin tức mới nhất trong 24h").

### 📌 Kết luận
Việc xây dựng MCP Server cho Hacker News bằng n8n là một ví dụ điển hình cho sức mạnh của nền tảng no-code trong việc tích hợp AI. Thay vì mất hàng giờ viết code API wrapper, các sếp chỉ cần vài phút để import và kích hoạt workflow. Đây là bước khởi đầu hoàn hảo để các sếp bắt đầu xây dựng hệ sinh thái AI Agent mạnh mẽ, có khả năng truy cập dữ liệu thời gian thực và ra quyết định dựa trên thông tin chính xác. Hãy thử ngay và chia sẻ kết quả với cộng đồng!