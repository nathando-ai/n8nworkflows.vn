---
title: "🤖 **Tự Động Hóa MCP Server Cho n8n: Cho phép AI Chạy Workflow Bất Kỳ Mà Không Cần Code**"
description: "Workflow này biến đổi hệ thống n8n của các sếp thành một **MCP Server** chuyên dụng, cho phép AI (như Claude, LangChain) khám phá, quản lý và thực thi workflows tự động hóa phức tạp chỉ bằng lời nói. Giúp tiết kiệm thời gian lên đến 80% trong quản lý quy trình IT, tự động hóa marketing, hoặc tích hợp hệ thống."
slug: "tay-dong-hoa-mcp-server-n8n-cho-ai"
tags: [n8n, automation, no-code, ai-agent, mcp-server, redis, langchain, openai, it-ops]
keywords: [n8n workflow mcp server, tự động hóa với ai, langchain n8n, quản lý workflow bằng redis, execute workflow n8n, ai agent tự động hóa]
---

# 🚀 **Tạo MCP Server Cho n8n: Cho phép AI Chạy Workflow Bất Kỳ**

## **Giới thiệu: AI Tự Động Hóa Workflow Bằng Lời Nói**
Các sếp đang gặp phải vấn đề gì?
- **Thủ công quản lý workflows**: Phải chạy từng workflow một, mất thời gian và dễ sai sót.
- **Không tích hợp AI**: AI không thể "hiểu" và thực thi workflows phức tạp của n8n.
- **Rủi ro an toàn**: Cho phép AI truy cập toàn bộ hệ thống có thể gây nguy hiểm.

**Workflow này giải quyết tất cả!**
N8n **MCP Server** cho phép các sếp:
✅ **Tạo một "cửa hàng công cụ" AI**: AI (như Claude, LangChain) có thể **khám phá**, **quản lý**, và **thực thi** workflows của n8n **bằng lời nói**.
✅ **Lọc và kiểm soát**: Chỉ cho phép AI sử dụng những workflow **đã được đánh dấu** và **cấu hình sẵn** (không phải toàn bộ hệ thống).
✅ **Tự động hóa cao cấp**: AI có thể **lập kế hoạch** và **thực thi** nhiều workflow liên tiếp, giống như một **trợ lý ảo chuyên nghiệp**.
✅ **An toàn và linh hoạt**: Sử dụng **Redis** để lưu trữ danh sách workflows "được phép", tránh tình trạng AI chạy workflows không mong muốn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** với Redis và OpenAI API.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
👉 [Cài đặt Redis trên VPS](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-redis-on-ubuntu-22-04)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%**: AI tự động quản lý và thực thi workflows thay vì các sếp phải làm thủ công.
- **Tự động hóa phức tạp**: AI có thể **lập kế hoạch** và **thực thi** nhiều workflow liên tiếp (ví dụ: tự động hóa marketing, quản lý IT, tích hợp hệ thống).
- **Kiểm soát an toàn**: Chỉ cho phép AI sử dụng những workflow **đã được đánh dấu** và cấu hình sẵn.
- **Tích hợp AI dễ dàng**: Sử dụng **LangChain** hoặc **Claude Desktop** để tương tác với n8n bằng lời nói.
- **Lọc và quản lý workflows**: Sử dụng **Redis** để lưu trữ danh sách workflows "được phép", tránh tình trạng AI chạy workflows không mong muốn.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
1. **n8n API Key**:
   - Tạo từ **Settings > Credentials** trong n8n (dùng để lấy danh sách workflows).
   - **Lưu ý**: Chỉ cấp quyền **read-only** để tránh AI sửa đổi hệ thống.

2. **Redis Server**:
   - Cài đặt Redis trên VPS (ví dụ: [Cài đặt Redis trên Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-redis-on-ubuntu-22-04)).
   - **Credentials Redis**: Thêm vào n8n dưới **Settings > Credentials**.

3. **OpenAI API Key** (nếu sử dụng GPT-4.1-mini):
   - Tạo từ [OpenAI](https://platform.openai.com/account/api-keys) và thêm vào n8n dưới **Settings > Credentials**.

4. **Workflows đã đánh dấu "mcp"**:
   - Các workflow cần có **Subworkflow Trigger** và **Input Schema** được cấu hình.
   - **Cách đánh dấu**: Mở workflow > **Tags** > Thêm tag `mcp`.

5. **MCP Client (tùy chọn)**:
   - **Claude Desktop** (để test): [Tải về](https://claude.ai/download).
   - **LangChain** (để tích hợp vào ứng dụng Python).

6. **VPS với Docker** (nếu self-host):
   - Cài n8n + Redis trên cùng một máy chủ để tối ưu hiệu suất.
   - **Cách cài**: [Hướng dẫn self-host n8n](https://docs.n8n.io/hosting/self-hosting/).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/3770](https://n8n.io/workflows/3770).
2. **Mở n8n Editor** (n8n.io hoặc self-hosted).
3. **Nhấp vào "Import"** > Chọn file JSON vừa tải.
4. **Chọn "Import"** để hoàn tất.

#### **Cách 2: Copy/Paste JSON**
1. **Mở n8n Editor** > **Create New Workflow**.
2. **Nhấp vào "Import"** > Chọn **Paste JSON**.
3. **Dán JSON** từ [n8n.io/workflows/3770](https://n8n.io/workflows/3770) (chọn **Raw** trên trang workflow).
4. **Nhấp "Import"**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** và cần **cấu hình cẩn thận**. Dưới đây là **các bước chỉnh sửa bắt buộc**:

#### **🔹 1. Cấu hình Credentials**
| Node | Yêu cầu | Hướng dẫn |
|------|---------|-----------|
| **Get MCP-tagged Workflows** | `n8nApi` | Tạo credential từ **Settings > Credentials** > **n8n API** (chọn **read-only**). |
| **Redis (Store In Memory, Get Memory, Delete Key)** | `redis` | Thêm credential Redis vào n8n (Host: `localhost`, Port: `6379`, Password: nếu có). |
| **OpenAI Chat Model** | `openAiApi` | Tạo credential OpenAI từ **Settings > Credentials** (API Key từ OpenAI). |

#### **🔹 2. Cấu hình Workflows "mcp"**
- **Mở từng workflow** cần sử dụng MCP Server:
  - **Tags**: Thêm tag `mcp`.
  - **Subworkflow Trigger**:
    - Mở **Trigger** > Chọn **Subworkflow Trigger**.
    - **Input Schema**: Cấu hình **cẩn thận** (không để AI tự động thêm fields).
    - **Lưu ý**: Nếu **Input Schema** bị hiển thị, **reset lại** node này (AI sẽ không thể truyền tham số qua passthrough).

#### **🔹 3. Cấu hình MCP Trigger**
- Node **"N8N Workflows MCP Server"** (type: `mcpTrigger`):
  - **Path**: Giá trị mặc định là `4625bcf4-0dd9-4562-a70f-6fee41f6f12d` (không cần đổi).
  - **Active**: Đảm bảo **bật** để MCP Server hoạt động.

#### **🔹 4. Test Workflows**
1. **Chạy test** với một workflow đơn giản (ví dụ: `Add Workflow`).
2. **Kiểm tra Redis**:
   - Mở Redis CLI (`redis-cli`) và kiểm tra:
     ```bash
     KEYS *
     ```
   - Nếu thấy key `available_workflows`, thì Redis đang lưu trữ danh sách workflows "được phép".

3. **Test với Claude Desktop**:
   - Cấu hình **Production URL** của MCP Server (mặc định: `http://localhost:5678`).
   - Mở Claude Desktop > **Settings > Tools** > Thêm URL MCP Server.
   - **Gửi yêu cầu**: "List all available workflows" để kiểm tra.

---
### **3. Kích hoạt ⚡️**
1. **Bật Workflow**:
   - Nhấp vào **Active** ở góc trên bên phải.
2. **Test với AI**:
   - Sử dụng **Claude Desktop** hoặc **LangChain** để tương tác:
     ```python
     from langchain.agents import create_openai_functions_agent
     from langchain_openai import ChatOpenAI
     from langchain.tools import StructuredTool

     # Thay thế URL MCP Server
     tools = [
         StructuredTool(
             name="Add Workflow",
             description="Add a workflow to the available list",
             func=lambda x: requests.post("http://localhost:5678/tools/addWorkflow", json=x),
         ),
         # Thêm các tool khác...
     ]
     agent = create_openai_functions_agent(llm=ChatOpenAI(temperature=0), tools=tools)
     ```

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **🔹 1. Tăng tính bảo mật**
- **Chỉ cho phép AI sử dụng workflows nhất định**:
  - Thay vì dùng tag `mcp`, các sếp có thể **lọc theo tên** hoặc **role** (ví dụ: `marketing`, `it-ops`).
  - **Cách làm**:
    ```json
    // Trong node "Get MCP-tagged Workflows", thêm filter:
    {
      "jsonPath": "$[?(@.name == 'marketing-workflow')]"
    }
    ```

- **Sử dụng Redis với mật khẩu**:
  - Cấu hình Redis với **password** để tránh AI truy cập Redis trực tiếp.

### **🔹 2. Tích hợp với Slack/Telegram**
- **Gửi báo cáo định kỳ** về trạng thái workflows:
  ```json
  // Thêm node "Set" sau "listWorkflows" để lưu kết quả
  {
    "jsonPath": "$",
    "operation": "set",
    "property": "slackMessage"
  }
  ```
  - Sau đó kết nối với **Slack Webhook** để gửi thông báo.

### **🔹 3. Tự động xóa workflows cũ**
- **Thêm node "Delete Key" sau một khoảng thời gian**:
  - Sử dụng **n8n Schedule Node** để xóa key Redis cũ (ví dụ: sau 7 ngày không sử dụng).

### **🔹 4. Optimize AI Responses**
- **Cấu hình OpenAI Prompt**:
  - Trong node `lmChatOpenAi`, thay đổi **prompt** để AI trả lời chính xác hơn:
    ```json
    {
      "model": "gpt-4.1-mini",
      "system": "You are an expert workflow automation assistant. Only use the available workflows listed in Redis. If a workflow is not available, say 'I cannot perform this task.'",
      "messages": [
        {"role": "user", "content": "{{$json['question']}}"}
      ]
    }
    ```

### **🔹 5. Log tất cả hoạt động**
- **Thêm node "Set" để lưu log**:
  ```json
  {
    "jsonPath": "$",
    "operation": "set",
    "property": "log"
  }
  ```
  - Sau đó kết nối với **Google Sheets** hoặc **Database** để theo dõi.

---

## 📌 **Kết luận: AI Tự Động Hóa Workflow Bằng Lời Nói**
Workflow này **không chỉ tự động hóa**, mà còn **cho phép AI quản lý và thực thi** workflows của n8n **bằng lời nói**. Các sếp sẽ:
✔ **Tiết kiệm thời gian** lên đến 80% trong quản lý quy trình.
✔ **Tích hợp AI** vào hệ thống tự động hóa một cách an toàn.
✔ **Kiểm soát chặt chẽ** những workflow AI được phép sử dụng.

**Bắt đầu ngay!**
1. **Import workflow** và cấu hình credentials.
2. **Đánh dấu workflows** cần sử dụng tag `mcp`.
3. **Test với Claude Desktop** hoặc LangChain.
4. **Tích hợp vào hệ thống** và bắt đầu tự động hóa!

---
**🚀 Cần hỗ trợ?**
- **Hỏi Jimleuk** (tác giả): [LinkedIn](https://www.linkedin.com/in/jimleuk/) | [Twitter](https://x.com/jimle_uk)
- **Hỗ trợ kỹ thuật n8n**: [Community n8n](https://community.n8n.io/)
- **Mua VPS chất lượng**: [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm **VPSN8N**)