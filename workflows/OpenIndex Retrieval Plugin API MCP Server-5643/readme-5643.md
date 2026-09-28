---
title: "🔍 **Tự Động Hóa API OpenIndex Retrieval Plugin với MCP Server - Giải Pháp AI RAG Miễn Code cho Các Sếp**"
description: "Workflow này chuyển đổi API OpenIndex Retrieval Plugin thành giao diện MCP-compatible, cho phép AI agent truy vấn và lọc tài liệu tự động dựa trên ngôn ngữ tự nhiên. Giúp các sếp tiết kiệm thời gian tìm kiếm thông tin và tích hợp AI vào hệ thống một cách dễ dàng."
slug: "tieu-dong-hoa-api-openindex-retrieval-plugin-mcp-server"
tags: [n8n, automation, ai-rag, no-code, api-integration]
keywords: [n8n workflow ai, tự động hóa tìm kiếm thông tin, openindex retrieval plugin, mcp server, ai agent integration]
---

# 🚀 **Tự Động Hóa API OpenIndex Retrieval Plugin với MCP Server - AI RAG Miễn Code**

## 📌 **Nỗi Đau Thực Tế Của Các Sếp**
Trong thời đại AI, việc tìm kiếm và lọc thông tin từ hàng ngàn tài liệu thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Các sếp thường phải:
- **Tìm kiếm thủ công** trên nhiều nguồn dữ liệu khác nhau.
- **Lọc và tổng hợp** thông tin một cách mệt mỏi.
- **Không tích hợp được AI** vào quy trình làm việc hiện tại.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa truy vấn tài liệu** dựa trên ngôn ngữ tự nhiên.
✅ **Tích hợp AI agent** vào hệ thống một cách dễ dàng.
✅ **Giảm thiểu công việc thủ công** đến 90%.
✅ **Cung cấp kết quả chính xác** với cấu trúc dữ liệu nguyên bản.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động tìm kiếm và lọc thông tin thay vì các sếp phải làm thủ công.
- **Tăng độ chính xác**: Tránh sai sót trong quá trình tìm kiếm và tổng hợp dữ liệu.
- **Tích hợp AI vào hệ thống**: AI agent có thể tương tác với tài liệu một cách tự động.
- **Hoạt động liên tục 24/7**: Workflow chạy tự động, không cần can thiệp của con người.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
- **Tài khoản OpenIndex Retrieval Plugin**: Đăng ký tại [OpenIndex](https://openindex.ai/) để lấy API key.
- **n8n Self-hosted**: Workflow này yêu cầu n8n được cài đặt trên máy chủ riêng (VPS) để hoạt động 24/7.
- **AI Agent hỗ trợ MCP**: Các sếp cần một AI agent có khả năng tương tác với MCP server (ví dụ: LangChain, LlamaIndex, hay các agent tự xây dựng).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### 1. **Import Workflow 📥**
:::note[HƯỚNG DẪN IMPORT]
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor) và tạo một workflow mới.
2. Nhấp vào **Import** và chọn file JSON từ [đây](https://n8n.io/workflows/5643) (hoặc copy/paste JSON từ link trên).
3. Chọn **Import Workflow** để tải workflow vào n8n.
:::

### 2. **Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này chỉ có **2 node**, nhưng các sếp cần chú ý đến các bước sau:

#### **Node 1: MCP Trigger (`n8n-nodes-langchain.mcpTrigger`)**
- **Tên Node**: `OpenIndex Retrieval Plugin`
- **Cấu hình**:
  - **Path**: Đặt thành `openindex-retrieval-plugin-mcp` (không cần thay đổi).
  - **Không yêu cầu xác thực** (Authentication: None).
- **Lưu ý**:
  - Sau khi kích hoạt workflow, **copy URL webhook** từ node này để sử dụng trong AI agent.

#### **Node 2: HTTP Request Tool (`n8n-nodes-base.httpRequestTool`)**
- **Tên Node**: `Submit Query`
- **Cấu hình**:
  - **Method**: POST (được tự động thiết lập).
  - **URL**: `https://retriever.openindex.ai/sub` (không cần thay đổi).
  - **Headers**:
    - `Content-Type`: `application/json`.
  - **Body**:
    - Sử dụng `$fromAI()` để tự động truyền tham số từ AI agent.
    - Ví dụ:
      ```json
      {
        "query": "$fromAI.query",
        "metadataFilters": "$fromAI.metadataFilters"
      }
      ```
- **Lưu ý**:
  - Các tham số `$fromAI.query` và `$fromAI.metadataFilters` sẽ được AI agent tự động truyền vào khi gọi API.

### 3. **Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **Execute Workflow** để kiểm tra nếu workflow hoạt động đúng.
   - Nếu không có lỗi, chuyển sang **Active** để workflow chạy liên tục.
2. **Sử Dụng AI Agent**:
   - **Cấu hình AI agent** để sử dụng URL MCP từ node `OpenIndex Retrieval Plugin`.
   - Ví dụ với LangChain:
     ```python
     from langchain.agents import create_openai_functions_agent
     from langchain_openai import ChatOpenAI
     from langchain.tools import Tool

     tools = [
         Tool(
             name="OpenIndex Retrieval",
             func=lambda query: requests.post(
                 "https://[URL-MCP-CỦA-BẠN]/openindex-retrieval-plugin-mcp",
                 json={"query": query}
             ).json(),
             description="Query OpenIndex Retrieval Plugin"
         )
     ]
     agent = create_openai_functions_agent(llm=ChatOpenAI(), tools=tools)
     ```

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Logging & Monitoring**:
   - Sử dụng node **n8n-nodes-base.term** để log kết quả API.
   - Thêm node **n8n-nodes-base.email** để gửi báo cáo định kỳ về kết quả tìm kiếm.
2. **Tích Hợp Slack/Telegram**:
   - Sử dụng node **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để thông báo kết quả tìm kiếm.
3. **Tự Động Lưu Kết Quả**:
   - Sử dụng node **n8n-nodes-base.googleSheets** hoặc **n8n-nodes-base.notion** để lưu lịch sử truy vấn.
4. **Cải Thiện Trải Nghiệm**:
   - Thêm node **n8n-nodes-base.set** để xử lý lỗi và trả về thông báo hữu ích cho AI agent.
:::

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình tìm kiếm và lọc tài liệu bằng AI một cách **miễn code**. Bằng cách tích hợp **OpenIndex Retrieval Plugin** với **MCP Server**, các sếp có thể:
- **Tiết kiệm thời gian** trong việc tìm kiếm thông tin.
- **Tăng độ chính xác** với kết quả tự động hóa.
- **Tích hợp AI vào hệ thống** một cách dễ dàng.

**Hãy áp dụng ngay workflow này và biến AI thành đồng đội của các sếp trong việc xử lý dữ liệu!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Cần hỗ trợ thêm?** Hãy liên hệ với tác giả David Ashby trên [Discord](https://discord.me/cfomodz) hoặc tham khảo tài liệu chính thức tại [n8n LangChain MCP](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp/).