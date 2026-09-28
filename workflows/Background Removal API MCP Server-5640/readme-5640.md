---
title: "🚀 Tự Động Hóa Xóa Nền Ảnh Với AI Agent (MCP Server) - Không Cần Code"
description: "Biến API xóa nền thành công cụ AI thông minh. Hướng dẫn cài đặt n8n MCP Server để AI tự động gọi API xóa nền, kiểm tra tài khoản và xử lý ảnh chuyên nghiệp."
slug: "tu-dong-hoa-xoa-nan-anh-ai-mcp-server"
tags: [n8n, mcp, ai-agent, image-processing, no-code]
keywords: [n8n workflow, xóa nền ảnh, mcp server, ai automation, remove.bg api]
---

# 🚀 Tự Động Hóa Xóa Nền Ảnh Với AI Agent (MCP Server) - Không Cần Code

Các sếp có từng gặp tình huống này không? Muốn tạo một chatbot hoặc AI Agent có khả năng xử lý ảnh (ví dụ: nhận một tấm ảnh sản phẩm, tự động xóa nền, rồi trả về file ảnh trong suốt). Việc này thường đòi hỏi phải viết code phức tạp để tích hợp API, xử lý lỗi, và quản lý phiên làm việc.

Workflow **Background Removal MCP Server** này chính là giải pháp "chìa khóa trao tay". Nó biến n8n thành một **MCP (Model Context Protocol) Server**, cho phép bất kỳ AI Agent nào (như Claude, GPT-4, hoặc các agent nội bộ) "nói chuyện" trực tiếp với API xóa nền. AI sẽ tự động quyết định khi nào cần xóa nền, khi nào cần kiểm tra số dư tài khoản, và tự điền các tham số cần thiết. Các sếp chỉ cần import, cấu hình API Key, và để AI làm việc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo độ trễ thấp cho các yêu cầu AI, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tích hợp AI Native**: AI Agent có thể gọi trực tiếp API xóa nền mà không cần trung gian code phức tạp.
- **3 Chức năng trong 1**: Xóa nền, kiểm tra số dư tài khoản, và tham gia chương trình cải tiến (Improvement Program) chỉ với 1 workflow.
- **Tự động hóa tham số**: Sử dụng `$fromAI()` để AI tự động điền URL ảnh hoặc file binary, giảm thiểu lỗi nhập liệu thủ công.
- **Tiết kiệm thời gian phát triển**: Không cần viết backend riêng cho AI, chỉ cần 1 workflow n8n là đủ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Bản Cloud hoặc Self-hosted (khuyến nghị Self-hosted để có quyền kiểm soát cao hơn).
- **Tài khoản Remove.bg**: Các sếp cần có API Key từ [remove.bg](https://www.remove.bg/api) để gọi API xóa nền.
- **AI Agent**: Một hệ thống AI hỗ trợ giao thức MCP (Model Context Protocol) hoặc khả năng gọi Webhook/HTTP Request (như Claude Desktop, Cursor, hoặc các agent tự xây dựng).
- **Credentials trong n8n**: Tạo một credential loại "Header Auth" hoặc "API Key" để lưu trữ API Key của Remove.bg.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Dán JSON vào và nhấn **Import**.
4. Các sếp sẽ thấy 4 nodes chính: `MCP Trigger`, `Fetch Account Balance`, `Submit Image for Improvement`, và `Remove Image Background`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow này hoạt động dựa trên giao thức MCP, vì vậy các sếp cần cấu hình đúng để AI có thể "nhìn thấy" và sử dụng các tools này.

**A. Cấu hình Credentials (API Key)**
- Click vào từng node HTTP Request (`Fetch Account Balance`, `Submit Image for Improvement`, `Remove Image Background`).
- Trong phần **Authentication**, chọn **Predefined Credential Type** -> **Header Auth**.
- Tạo mới hoặc chọn credential đã có:
  - **Name**: `X-API-Key`
  - **Value**: `[API Key của Remove.bg của các sếp]`
- *Lưu ý*: Đảm bảo API Key đúng định dạng và còn hạn.

**B. Cấu hình MCP Trigger**
- Click vào node **`Background Removal MCP Server`** (loại `mcpTrigger`).
- Kiểm tra phần **Path**: Mặc định là `background-removal-mcp`. Các sếp có thể đổi thành tên khác nếu muốn, nhưng hãy ghi nhớ đường dẫn này.
- Đảm bảo workflow đang ở chế độ **Active** (bật công tắc Active ở góc trên bên phải) để server MCP chạy liên tục.

**C. Hiểu về các Tools (Nodes HTTP)**
Workflow này đóng gói 3 API endpoints của Remove.bg thành 3 "Tools" mà AI có thể gọi:
1. **`Fetch Account Balance`**: AI sẽ gọi tool này khi cần biết tài khoản còn bao nhiêu credit để xóa ảnh.
2. **`Remove Image Background`**: Tool chính. AI sẽ truyền URL ảnh hoặc file binary vào đây. Node này sử dụng `$fromAI()` để nhận dữ liệu từ AI.
3. **`Submit Image for Improvement`**: Tool phụ trợ để gửi phản hồi về chất lượng ảnh đã xóa.

**D. Kiểm tra Expressions**
- Trong các node HTTP, các tham số quan trọng (như `image_url` hoặc `size`) thường được đặt là `={{ $fromAI("image_url") }}`.
- Điều này có nghĩa là AI Agent sẽ tự động điền giá trị này khi nó quyết định gọi tool. Các sếp **không cần** hardcode URL ảnh ở đây.

#### 3. Kích hoạt ⚡️

1. **Test Run**:
   - Vì đây là MCP Server, cách test tốt nhất là kết nối nó với một AI Agent hỗ trợ MCP (ví dụ: Claude Desktop với MCP extension, hoặc một agent n8n AI khác).
   - Nếu chưa có AI Agent, các sếp có thể dùng Postman hoặc curl để gọi endpoint MCP để kiểm tra xem server có phản hồi đúng không.
   - Hoặc, tạo một workflow n8n AI Agent khác, thêm node **`MCP Client`** (nếu có sẵn trong phiên bản n8n mới) hoặc dùng **`HTTP Request`** để gọi URL webhook của MCP Trigger này.

2. **Bật Active**:
   - Nhấn nút **Active** ở góc trên bên phải màn hình n8n.
   - Copy **Webhook URL** từ node `MCP Trigger`. Đây là địa chỉ mà AI Agent sẽ kết nối tới.

### ✍️ Mẹo & gợi ý nâng cao

- **Kết hợp với Google Drive**: Sau khi AI xóa nền xong, các sếp có thể thêm một node `Google Drive` để tự động lưu file ảnh đã xóa nền vào thư mục cụ thể.
- **Gửi thông báo qua Telegram/Slack**: Thêm node `Telegram` hoặc `Slack` sau khi hoàn tất để thông báo cho team biết đã có ảnh mới được xử lý.
- **Xử lý lỗi (Error Handling)**: Thêm một node `Error Trigger` hoặc cấu hình lỗi trong các node HTTP để gửi cảnh báo khi API Remove.bg bị lỗi hoặc hết credit.
- **Tăng tốc độ với Caching**: Nếu cùng một URL ảnh được yêu cầu xóa nhiều lần, các sếp có thể thêm logic kiểm tra cache (dùng Redis hoặc Google Sheets) để tránh tốn credit không cần thiết.

### 📌 Kết luận

Workflow **Background Removal MCP Server** là một ví dụ tuyệt vời về cách n8n có thể trở thành cầu nối giữa các API truyền thống và thế giới AI Agent hiện đại. Thay vì phải viết code phức tạp để tích hợp, các sếp chỉ cần import, cấu hình API Key, và để AI tự động làm việc.

Hãy thử ngay hôm nay để trải nghiệm sức mạnh của tự động hóa đa phương thức (Multimodal AI) với n8n! Nếu gặp khó khăn trong việc kết nối với AI Agent, đừng ngại tham khảo tài liệu MCP của n8n hoặc liên hệ cộng đồng để được hỗ trợ.

Chúc các sếp triển khai thành công! 🚀