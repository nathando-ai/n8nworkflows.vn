---
title: "🚀 Xây dựng Server MCP FileSystem của riêng bạn với n8n"
description: "Triển khai nhanh một Server MCP cho phép liệt kê, đọc, tạo thư mục và file trên hệ thống Linux mà không cần viết code."
slug: "xay-dung-server-mcp-filesystem-n8n"
tags: [n8n, automation, no-code, file-system, mcp]
keywords: [n8n workflow, tự động hóa, MCP server, file system, execute command]
---

# 🚀 Xây dựng Server MCP FileSystem của riêng bạn với n8n

Bạn đã từng phải **điều khiển thủ công** việc tạo, liệt kê, đọc file trên máy chủ Linux?  
Mỗi lần phải mở terminal, gõ lệnh, sao chép kết quả lại mất **thời gian** và **rủi ro lỗi**.  
Với workflow **Build your own FileSystem MCP server** trong n8n, các sếp có thể biến toàn bộ các thao tác này thành một **API an toàn, không cần code** chỉ bằng vài cú click.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút xuống còn vài giây để thực hiện cùng một thao tác.  
- **Độ chính xác 100 %**: Không còn lỗi gõ lệnh sai hay đường dẫn không tồn tại.  
- **Bảo mật**: Chỉ cho phép các tham số (tên file, đường dẫn) mà không cho phép chạy lệnh tùy ý.  
- **Hoạt động liên tục 24/7**: Server MCP luôn sẵn sàng đáp ứng yêu cầu từ các client như Claude Desktop.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n** (cài đặt trên Linux hoặc VPS).  
- **Môi trường Linux** (để thực thi các lệnh `ls`, `mkdir`, `cat`, …).  
- **MCP Client/Agent** (ví dụ: Claude Desktop – https://claude.ai/download).  
- **Credentials**:  
  - `Execute Command` credentials (có thể để mặc định nếu n8n chạy trên cùng máy).  
  - (Tùy chọn) `MCP Server` credentials để bật **Authentication** trước khi đưa vào production.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Truy cập link gốc: <https://n8n.io/workflows/3630>.  
2. Nhấn **Export → JSON** để tải file `filesystem-mcp-server.json`.  
3. Mở n8n → **Workflows → Import** → kéo thả file JSON hoặc dán nội dung vào **Editor**.  
4. Lưu lại và đặt tên cho workflow (mặc định: *Build your own FileSystem MCP server*).

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **các node quan trọng** và cách cấu hình chi tiết:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|-------------------|
| **FileSystem MCP Server** | `mcpTrigger` | - **Path**: giữ nguyên `0d93cfd5-2fbf-457e-9535-5bfc9a73ba9e` hoặc thay đổi thành ID tùy ý.<br>- **Authentication**: bật **Require Authentication** và tạo **MCP Credentials** (username/password). |
| **ListDirectory** | `executeCommandTool` | - **Command**: `ls -1 {{ $json.path }}`<br>- **Parameters**: `path` (được truyền từ client). |
| **CreateDirectory** | `executeCommandTool` | - **Command**: `mkdir -p {{ $json.path }}` |
| **SearchDirectory** | `executeCommandTool` | - **Command**: `find {{ $json.basePath }} -type f -name "{{ $json.pattern }}"` |
| **readOneOrMultipleFiles** | `executeCommand` | - **Command**: `cat {{ $json.filePath }}` |
| **writeOneOrMultipleFiles** | `executeCommand` | - **Command**: `printf "{{ $json.content }}" > {{ $json.filePath }}` |
| **ReadFiles** | `toolWorkflow` | - Liên kết tới **sub‑workflow** “ReadFiles” (nếu chưa có, import kèm file `ReadFiles.json`). |
| **WriteFiles** | `toolWorkflow` | - Liên kết tới **sub‑workflow** “WriteFiles” (import tương tự). |
| **Operation** | `switch` | - **Cases**: `list`, `create`, `read`, `write`, `search`.<br>- Đảm bảo mỗi case dẫn tới node tương ứng (ListDirectory, CreateDirectory, …). |
| **When Executed by Another Workflow** | `executeWorkflowTrigger` | - Dùng để cho phép các workflow nội bộ gọi lại các công cụ MCP. Không cần thay đổi nếu không dùng nội bộ. |

**Credentials**  
- Đối với các node `executeCommandTool` và `executeCommand`, chọn **Credentials → Execute Command** (hoặc tạo mới nếu chạy trên máy khác).  
- Đối với `mcpTrigger`, tạo **MCP Credentials** → nhập **Username** và **Password** đã quyết định ở bước trên.

### 3. Kích hoạt ⚡️
1. **Test run**: Dùng **Execute Node** trên `FileSystem MCP Server` và gửi một payload mẫu, ví dụ:  
   ```json
   {
     "operation": "list",
     "path": "/home/ubuntu/projects"
   }
   ```  
2. Kiểm tra **Output** của node `ListDirectory` để chắc chắn lệnh trả về danh sách thư mục.  
3. Khi mọi thứ ổn, bật **Active** ở góc phải của editor → **Activate Workflow**.

## ✍️ Mẹo & gợi ý nâng cao
- **Thêm chức năng di chuyển/đổi tên file**: tạo node `executeCommandTool` mới với lệnh `mv {{ $json.source }} {{ $json.destination }}` và kết nối vào `Operation` case `move`.  
- **Gửi thông báo Slack khi tạo file**: dùng node **Slack** (hoặc webhook) sau `WriteFiles` để push tin nhắn.  
- **Lưu log vào database**: thêm node **PostgreSQL/MySQL** để ghi lại mỗi lần thao tác (operation, path, timestamp).  
- **Lên lịch backup**: dùng node **Cron** để chạy workflow phụ định kỳ, sao chép toàn bộ thư mục tới bucket S3 hoặc Google Drive.  

## 📌 Kết luận
Với workflow này, các sếp có thể **biến máy chủ Linux thành một API FileSystem an toàn**, cho phép bất kỳ MCP client nào (Claude Desktop, custom agents…) thực hiện các thao tác cơ bản mà không cần truy cập terminal. Hãy **import, cấu hình nhanh**, bật **Active** và bắt đầu tự động hoá ngay hôm nay!  

*Author: Jimleuk – Freelance AI Automation Consultant*  
*Liên hệ: hello@jimle.uk*  
*LinkedIn: https://www.linkedin.com/in/jimleuk/*