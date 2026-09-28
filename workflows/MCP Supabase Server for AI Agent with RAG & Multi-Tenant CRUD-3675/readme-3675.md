---
title: "🚀 Xây dựng MCP Supabase Server cho AI Agent kết hợp RAG & Multi-Tenant CRUD trong n8n"
description: "Hướng dẫn cấu hình workflow n8n tích hợp MCP Server, Supabase Vector Store (RAG) và đầy đủ các công cụ CRUD (Multi-Tenant) giúp AI Agent truy vấn và quản lý dữ liệu thông minh."
slug: "mcp-supabase-server-ai-agent-rag-multi-tenant-crud"
tags: [n8n, automation, no-code, supabase, ai-agent, mcp, rag]
keywords: [n8n workflow, mcp supabase server, ai agent rag, supabase tool n8n, multi-tenant crud n8n]
---

# 🚀 Xây dựng MCP Supabase Server cho AI Agent kết hợp RAG & Multi-Tenant CRUD

Chào các sếp! Khi phát triển các ứng dụng AI Agent hiện đại, việc kết nối Agent với cơ sở dữ liệu để vừa tra cứu tài liệu thông minh (RAG), vừa thao tác dữ liệu theo thời gian thực (CRUD) luôn là một thử thách lớn. Việc viết code thủ công cho các API trung gian vừa tốn kém lại mất thời gian bảo trì. 

Được thiết kế bởi **Luciano Gutierrez** (KORE Soluções), workflow này giải quyết triệt để bài toán đó bằng cách tận dụng chuẩn **MCP (Model Context Protocol)** kết hợp với **Supabase**, giúp AI Agent của các sếp có một "hệ thần kinh" mạnh mẽ để tự động hóa mọi thao tác dữ liệu mà không cần viết một dòng code backend nào phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tích hợp RAG thông minh**: Cho phép AI Agent tìm kiếm ngữ cảnh, tài liệu lưu trữ trong Supabase Vector Store thông qua OpenAI Embeddings (`text-embedding-ada-002`).
- **Hệ thống CRUD toàn diện**: Cung cấp bộ công cụ đầy đủ cho Agent thao tác trên 4 bảng chính (`AGENT_MESSAGE`, `AGENT_TASKS`, `AGENT_STATUS`, `AGENT_KNOWLEDGE`) bao gồm Tạo, Đọc (Single/Many), Cập nhật và Xóa bản ghi.
- **Chuẩn MCP tiên tiến**: Sử dụng `mcpTrigger` giúp kết nối trực tiếp và mượt mà với các AI Client hoặc Agent framework hỗ trợ Model Context Protocol.
- **Tiết kiệm 100% thời gian code API**: Thay vì xây dựng middleware riêng, n8n đóng vai trò là MCP Server trung gian cực kỳ gọn nhẹ và dễ mở rộng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (phiên bản hỗ trợ LangChain và MCP, khuyến nghị bản self-hosted mới nhất).
- **Tài khoản Supabase**: Đã thiết lập sẵn project và các bảng dữ liệu tương ứng (`agent_message`, `agent_tasks`, `agent_status`, `agent_knowledge`) kèm cấu hình Vector extension cho phần RAG.
- **OpenAI API Key**: Để chạy mô hình `Embeddings OpenAI` (`text-embedding-ada-002`).
- **Supabase Credentials**: API Key và URL kết nối project Supabase cho các node Supabase Tool và Vector Store.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ [n8n Workflow Hub (ID: 3675)](https://n8n.io/workflows/3675).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ mã JSON và dán trực tiếp vào màn hình canvas của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 23 nodes được tổ chức bài bản theo từng module chức năng. Các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Node `MCP_SUPABASE` (`mcpTrigger`)**: Kiểm tra đường dẫn path (ví dụ: `affff59c-9c5c-4a07-b531-616c1d631601`) để đảm bảo endpoint nhận diện đúng MCP client kết nối tới.
- **Node `Embeddings OpenAI`**: Chọn đúng credential OpenAI và cấu hình mô hình `text-embedding-ada-002`.
- **Node `RAG` (`vectorStoreSupabase`)**: Kết nối với thông tin bảng Vector trong Supabase của các sếp và liên kết với Embeddings OpenAI.
- **Các Supabase Tool Nodes** (như `CREATE_ROW_AGENT_MESSAGE`, `GET_ROW_AGENT_TASKS`, `UPDATE_ROW_AGENT_STATUS`, `DELETE_ROW_INSCRICOES_CURSOS`, v.v.): 
  - Đảm bảo tất cả các node này đều được trỏ chung đến một **Supabase API Credential** chuẩn xác.
  - Kiểm tra cấu hình `operation` (get, create, update, delete, getAll) và tên bảng (table name) trong Supabase tương ứng với các phân vùng dữ liệu trên canvas (`AGENT_MESSAGE`, `AGENT_TASK`, `AGENT_STATUS`, `AGENT_KNOWLEDGE`).

#### 3. Kích hoạt ⚡️
- Nhấp vào nút **Execute Workflow** để kiểm tra tính sẵn sàng của MCP trigger.
- Sau khi xác nhận các kết nối API không báo lỗi, hãy bật nút **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng bảng dữ liệu**: Các sếp có thể nhân bản (duplicate) các cụm Supabase Tool hiện tại để mở rộng thêm các bảng quản lý user, log hệ thống hoặc cấu hình riêng cho từng khách hàng (Multi-Tenant).
- **Kết hợp Telegram/Slack**: Bổ sung thêm các thông báo qua kênh chat mỗi khi Agent thực hiện các thao tác quan trọng hoặc gặp lỗi trong quá trình xử lý CRUD.
- **Giám sát Log**: Sử dụng tính năng thực thi lịch sử của n8n để theo dõi các request mà AI Agent gọi đến MCP Server, từ đó tối ưu hóa prompt hoặc cấu trúc bảng dữ liệu trong Supabase.

### 📌 Kết luận
Việc tích hợp **MCP Supabase Server** vào hệ thống n8n mở ra một hướng đi cực kỳ mạnh mẽ để trao quyền cho AI Agent tự chủ dữ liệu, vừa bảo mật, vừa dễ quản lý theo mô hình multi-tenant. Hãy áp dụng ngay vào dự án của các sếp để tối ưu hóa quy trình tự động hóa lên một tầm cao mới!