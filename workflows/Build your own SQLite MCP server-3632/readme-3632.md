---
title: "🔧 **Tự Động Hóa SQLite MCP Server: Quản Lý Cơ Sở Dữ Liệu AI An Toàn Miễn Code**"
description: "Workflow này giúp các sếp xây dựng một máy chủ SQLite MCP tự động hóa hoàn toàn, cho phép quản lý cơ sở dữ liệu SQLite thông qua giao tiếp với các agent AI (như Claude) mà không cần viết code thủ công. Giúp tiết kiệm thời gian, tăng tính bảo mật và mở rộng khả năng BI cho doanh nghiệp."
slug: "tự-dộng-hoa-sqlite-mcp-server"
tags: [n8n, automation, no-code, ai-powered, sqlite, model-context-protocol, business-intelligence]
keywords: [n8n workflow sqlite, tự động hóa cơ sở dữ liệu, MCP server, AI quản lý dữ liệu, no-code database, LangChain n8n]
---

# 🚀 **Xây Dựng Máy Chủ SQLite MCP Tự Động Hóa: Giải Pháp Quản Lý Dữ Liệu AI An Toàn**

## **💡 Giới Thiệu: Tại Sao Các Sếp Cần Workflow Này?**
Hiện nay, việc quản lý cơ sở dữ liệu thủ công không chỉ tốn thời gian mà còn dễ mắc lỗi, đặc biệt khi phải xử lý các yêu cầu phức tạp từ các agent AI như Claude. **Workflow này giúp các sếp:**
- **Tự động hóa toàn bộ quy trình** quản lý SQLite thông qua giao tiếp với agent AI (không cần code thủ công).
- **Tăng tính bảo mật** bằng cách hạn chế truy cập SQL thô, ngăn chặn SQL injection và rò rỉ dữ liệu.
- **Mở rộng khả năng Business Intelligence (BI)** bằng cách cho phép agent AI thao tác với dữ liệu một cách an toàn và hiệu quả.
- **Tích hợp hoàn toàn với hệ sinh thái AI** như Claude Desktop, Claude AI, hoặc các agent tương tự.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian** lên đến 80% trong việc quản lý cơ sở dữ liệu thủ công.
✅ **Bảo mật cao** với cơ chế kiểm soát truy cập SQL thông qua tham số hóa (không cho phép SQL thô).
✅ **Hoạt động 24/7** với n8n self-hosted, không phụ thuộc vào thời gian làm việc.
✅ **Tích hợp AI** để tự động hóa phân tích dữ liệu và báo cáo BI.
✅ **Mở rộng khả năng** cho các team BI, HR, hoặc marketing quản lý dữ liệu một cách an toàn.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Hệ Thống & Phần Mềm**
- **n8n Self-Hosted** (không hỗ trợ n8n Cloud).
- **SQLite** (cài đặt trên máy chủ hoặc VPS).
- **MCP Client/Agent** (ví dụ: [Claude Desktop](https://claude.ai/download)).
- **LangChain Node** (đã tích hợp trong n8n từ phiên bản 1.35+).

### **2. Tham Số Cần Cấu Hình**
| Tham Số | Mô Tả | Ví Dụ |
|---------|--------|--------|
| **Database File Path** | Đường dẫn đến file SQLite (`.db` hoặc `.sqlite`) | `/data/database.db` |
| **MCP Server Path** | Đường dẫn duy nhất cho server MCP (được sinh tự động trong workflow) | `3124a4cd-4e93-4c1b-b4db-b5599f4889b1` |
| **Credentials (Production)** | Tài khoản và mật khẩu để bảo mật server MCP | `admin:Passw0rd123` |
| **Agent API Key** | Khóa API của agent AI (nếu sử dụng) | `sk-abc123...` |

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
Các sếp có thể:
- **Tải file JSON** từ [n8n Workflow Library](https://n8n.io/workflows/3632) và import vào n8n Editor.
- **Copy/Paste JSON** vào tab **Import** của n8n Editor.

:::note[**Lưu Ý**]
- Workflow **chỉ hoạt động trên n8n self-hosted** vì nó đọc file SQLite trên máy chủ.
- **Không hỗ trợ n8n Cloud** do hạn chế truy cập file hệ thống.
:::

### **2. Cấu Hình Cần Thiết (Bắt Buộc)**
Sau khi import, các sếp cần chỉnh sửa **các node quan trọng** sau:

#### **🔹 Node 1: "SQLite MCP Server" (mcpTrigger)**
- **Cấu hình `path`**:
  - Giá trị mặc định đã được đặt là `3124a4cd-4e93-4c1b-b4db-b5599f4889b1` (không cần thay đổi).
  - **Lưu ý**: Nếu muốn thay đổi, các sếp phải **xóa file cũ** và tạo mới trong thư mục `~/.n8n/mcp/` trên máy chủ.

- **Bật `requireCredentials`** (trong production):
  ```yaml
  requireCredentials: true
  ```

#### **🔹 Node 2-7: Code & Tool Workflow (CRUD Operations)**
Các node này xử lý **Create, Read, Update, Delete (CRUD)** trên SQLite. Các sếp cần:
1. **Chỉnh sửa code trong `CreateRecord`, `UpdateRecord`, `ReadRecords`**:
   - Sử dụng **SQLite3** để thực hiện truy vấn an toàn.
   - Ví dụ trong `CreateRecord`:
     ```javascript
     const sqlite3 = require('sqlite3').verbose();
     const db = new sqlite3.Database(process.env.DB_PATH);

     const { tableName, columns, values } = $input.all();
     const placeholders = values.map(() => '?').join(',');
     const sql = `INSERT INTO ${tableName} (${columns.join(',')}) VALUES (${placeholders})`;

     db.run(sql, values, function(err) {
       if (err) throw err;
       $output.set('rowid', this.lastID);
     });
     ```
2. **Cấu hình `DescribeTables` và `ListTables`**:
   - Sử dụng **LangChain ToolCode** để liệt kê schema và danh sách bảng.
   - Ví dụ:
     ```javascript
     const tables = await db.all("SELECT name FROM sqlite_master WHERE type='table'");
     return { tables };
     ```

#### **🔹 Node 8-10: Tool Workflow (CreateRecords, UpdateRows, ReadRows)**
- **Kết nối với node `Operation` (Switch)** để phân loại yêu cầu.
- **Cấu hình input/output** để đảm bảo dữ liệu được truyền đúng:
  ```json
  {
    "operation": "create",
    "table": "business_insights",
    "columns": ["title", "content", "created_at"],
    "values": ["Trend 2024", "Dữ liệu mới", "2024-01-01"]
  }
  ```

---
### **3. Kích Hoạt Workflow**
1. **Test Run với dữ liệu mẫu**:
   - Gửi yêu cầu từ **Claude Desktop** hoặc **agent AI** tương tự:
     ```
     "Please create a table named 'business_insights' with columns: title, content, created_at"
     ```
   - Kiểm tra kết quả trong **n8n Dashboard**.

2. **Bật `Active`**:
   - Chuyển trạng thái workflow sang **Active** để hoạt động liên tục.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tăng Cường Bảo Mật**
- **Khóa file SQLite** bằng mật khẩu:
  ```bash
  sqlite3 database.db ".password yourpassword"
  ```
- **Sử dụng `requireCredentials`** trong node `mcpTrigger` để yêu cầu xác thực.

### **2. Tích Hợp với Slack/Telegram**
- Sử dụng **n8n Slack Node** để thông báo kết quả:
  ```
  "Database updated! New record added: {title}, {content}"
  ```

### **3. Lưu Log & Báo Cáo Định Kỳ**
- Sử dụng **n8n Schedule Node** để gửi báo cáo hàng ngày:
  ```json
  {
    "operation": "read",
    "table": "business_insights",
    "limit": 10
  }
  ```
- Gửi kết quả qua **Email** hoặc **Google Sheets**.

### **4. Hạn Chế Schema cho Mục Đích Cụ Thể**
- Ví dụ: **Chỉ cho phép truy cập bảng `hr_employees`** cho team HR:
  ```javascript
  if (tableName !== "hr_employees") {
    throw new Error("Access denied. Only 'hr_employees' table is allowed.");
  }
  ```

---
## **📌 Kết Luận: Áp Dụng Ngay để Tự Động Hóa Dữ Liệu AI**

Workflow **SQLite MCP Server** này là giải pháp **tự động hóa hoàn toàn** cho việc quản lý cơ sở dữ liệu SQLite thông qua AI, giúp các sếp:
✔ **Tiết kiệm thời gian** trong quản lý dữ liệu.
✔ **Tăng tính bảo mật** với cơ chế kiểm soát truy cập SQL.
✔ **Mở rộng khả năng BI** một cách an toàn và hiệu quả.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n self-hosted** trên VPS (sử dụng mã giảm giá **VPSN8N** tại [TinoHost](https://tino.vn/vps-n8n?affid=388)).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Kết nối với Claude Desktop** và bắt đầu tự động hóa!

---
**🔗 Tài Liệu Tham Khảo:**
- [MCP Server Trigger Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-langchain.mcptrigger)
- [LangChain Node Docs](https://docs.n8n.io/integrations/nodes/n8n-nodes-langchain/)
- [SQLite3 Node.js Docs](https://www.npmjs.com/package/sqlite3)