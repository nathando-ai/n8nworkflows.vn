---
title: "🛠️ Biến AI Thành Quản Trị Viên Raindrop: Tự Động Hóa 100% Bookmark & Collection"
description: "Hướng dẫn cài đặt n8n MCP Server để cho phép AI (Claude, ChatGPT, Cursor...) trực tiếp tạo, sửa, xóa bookmark và quản lý collection trên Raindrop.io mà không cần code."
slug: "n8n-raindrop-mcp-server-ai"
tags: [n8n, mcp, raindrop, ai-automation, no-code]
keywords: [n8n workflow, raindrop api, mcp server n8n, tự động hóa bookmark, ai agent]
---

# 🛠️ Biến AI Thành Quản Trị Viên Raindrop: Tự Động Hóa 100% Bookmark & Collection

Các sếp có bao giờ cảm thấy phiền toái khi phải mở trình duyệt, tìm kiếm lại link cũ, hoặc mất thời gian phân loại hàng chục bài viết vào các Collection trên Raindrop.io? Việc quản lý kiến thức (Knowledge Management) thủ công luôn là một gánh nặng, đặc biệt khi các sếp đang làm việc song song với nhiều AI Assistant.

Workflow này giải quyết triệt để vấn đề đó bằng cách biến n8n thành một **MCP (Model Context Protocol) Server**. Điều này có nghĩa là các sếp có thể kết nối trực tiếp các AI Agent (như Claude Desktop, Cursor, hoặc các LLM hỗ trợ MCP) với Raindrop.io. AI sẽ tự động đọc, tạo, cập nhật và xóa bookmark/collection dựa trên lệnh của các sếp, hoàn toàn không cần viết một dòng code API nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo an toàn dữ liệu, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác AI trực tiếp:** Lệnh "Lưu bài này vào Collection 'Marketing'" sẽ được AI thực hiện ngay lập tức qua Raindrop API.
- **Quản lý 13 thao tác:** Hỗ trợ đầy đủ CRUD (Create, Read, Update, Delete) cho Bookmark, Collection và Tag.
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn thao tác chuột/bàn phím khi phân loại nội dung.
- **Tích hợp linh hoạt:** Hoạt động như một "công cụ" (tool) cho bất kỳ AI Agent nào hỗ trợ chuẩn MCP.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản self-hosted hoặc cloud (khuyến khích self-hosted để tối ưu chi phí và bảo mật).
- **Tài khoản Raindrop.io:** Các sếp cần có API Key của Raindrop.
    - *Cách lấy:* Vào [Raindrop.io Settings](https://app.raindrop.io/settings) -> API -> Generate New Key.
- **AI Client hỗ trợ MCP:** Ví dụ: Claude Desktop, Cursor, hoặc các framework Agent khác.
- **Node.js:** Nếu chạy local, cần có Node.js để chạy n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ link gốc [n8n.io/workflows/5346](https://n8n.io/workflows/5346) hoặc copy toàn bộ JSON code và dán vào n8n Editor.

1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from Clipboard**.
3. Dán link hoặc JSON code.
4. Workflow sẽ hiển thị với 14 nodes, bao gồm 1 node `mcpTrigger` và 13 node `raindropTool`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow này hoạt động dựa trên cơ chế **MCP Trigger**, nghĩa là nó không chạy theo lịch (cron) mà chờ AI gọi đến.

**A. Cấu hình Node `Raindrop Tool MCP Server` (mcpTrigger)**
- Node này đóng vai trò là "cổng" tiếp nhận lệnh từ AI.
- Các sếp cần đảm bảo node này được cấu hình đúng để AI có thể nhận diện được 13 tools bên dưới.
- *Lưu ý:* Trong n8n, node `mcpTrigger` thường yêu cầu cấu hình các tools con (sub-nodes) để mô tả chức năng. Các node `raindropTool` bên dưới chính là các tools đó.

**B. Cấu hình Credentials cho các Node `raindropTool`**
Mỗi node `raindropTool` (Create a bookmark, Get a collection, v.v.) đều cần gắn **Raindrop.io API Credential**.
1. Click vào từng node `raindropTool`.
2. Ở phần **Credentials**, chọn **Raindrop.io API**.
3. Nếu chưa có, tạo mới:
    - **API Key:** Dán API Key lấy từ Raindrop.io.
    - **Base URL:** Mặc định là `https://api.raindrop.io/rest/v1` (thường không cần đổi).
4. *Mẹo:* Các sếp có thể tạo một credential chung và gán cho tất cả 13 nodes để dễ quản lý.

**C. Kiểm tra các Node cụ thể**
- **Create a bookmark:** Đảm bảo các trường `url`, `title`, `collection_id` (nếu có) được mô tả rõ trong schema để AI biết cách điền dữ liệu.
- **Get many bookmarks:** Kiểm tra các tham số lọc (filter) như `tags`, `collection_id` để AI có thể truy vấn chính xác.
- **Delete a bookmark/collection:** Đây là thao tác nguy hiểm. Các sếp nên cân nhắc thêm một bước xác nhận (confirmation) trong prompt của AI hoặc giới hạn quyền truy cập của AI client.

**D. Cấu hình AI Client (Bên ngoài n8n)**
Sau khi n8n chạy, các sếp cần thêm n8n vào AI Client của mình.
- **Ví dụ với Claude Desktop:**
    1. Mở `claude_desktop_config.json`.
    2. Thêm vào phần `mcpServers`:
    ```json
    "n8n-raindrop": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-n8n",
        "--url",
        "http://localhost:5678/mcp" // Thay bằng URL n8n của các sếp
      ]
    }
    ```
    *(Lưu ý: Cú pháp chính xác có thể thay đổi tùy phiên bản n8n và MCP server client. Các sếp nên tham khảo tài liệu MCP của n8n hiện tại.)*

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Chạy thử workflow trong n8n để đảm bảo không có lỗi credentials.
   - Sử dụng AI Client để gửi lệnh: *"Hãy tạo một collection mới tên là 'Test AI'"*.
   - Kiểm tra xem collection có xuất hiện trong Raindrop.io không.
2. **Bật Active:**
   - Bật công tắc **Active** ở góc trên bên phải n8n.
   - Workflow sẽ lắng nghe các yêu cầu MCP từ AI.

### ✍️ Mẹo & gợi ý nâng cao

- **Tự động Tagging:** Kết hợp thêm một node LLM (OpenAI/Claude) trước khi gọi `Create a bookmark`. LLM sẽ phân tích nội dung bài viết và tự động gán tags phù hợp, sau đó mới lưu vào Raindrop.
- **Báo cáo tuần:** Tạo một workflow riêng chạy theo lịch (Cron) để lấy `Get many bookmarks` từ tuần trước, tổng hợp thành báo cáo và gửi qua Email/Slack.
- **Bảo mật API Key:** Nếu các sếp chia sẻ n8n instance, hãy đảm bảo MCP Server chỉ chấp nhận kết nối từ các IP hoặc User được tin cậy. Cân nhắc sử dụng OAuth thay vì API Key tĩnh nếu Raindrop hỗ trợ.
- **Tích hợp với Notion/Obsidian:** Sau khi AI lưu bookmark vào Raindrop, các sếp có thể thêm node để đồng bộ metadata vào Notion hoặc Obsidian để xây dựng hệ thống thứ cấp (Second Brain).

### 📌 Kết luận

Với workflow **Raindrop Tool MCP Server**, các sếp đã sở hữu một "trợ lý ảo" chuyên biệt cho việc quản lý kiến thức. Thay vì phải mở trình duyệt và click chuột, các sếp chỉ cần nói chuyện với AI. Đây là bước tiến lớn trong việc tích hợp AI vào quy trình làm việc hàng ngày, giúp các sếp tập trung vào tư duy thay vì thao tác thủ công.

Hãy thử ngay và chia sẻ trải nghiệm của các sếp trong bình luận nhé! 🚀