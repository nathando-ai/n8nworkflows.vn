---
title: "🚀 Tự Động Hóa WHOIS API Cho AI Agent: 8 Thao Tác Quản Lý Domain Miễn Code"
description: "Workflow này chuyển đổi API WHOIS bulk thành giao diện MCP cho AI agent, tự động hóa 8 thao tác quản lý domain (WHOIS, check, batch) chỉ với 1 dòng code. Giúp các sếp tiết kiệm thời gian nghiên cứu thị trường domain và tối ưu hóa chiến lược mua bán domain."
slug: "tieu-dong-hoa-whois-api-cho-ai-agent"
tags: [n8n, automation, no-code, ai-agent, domain-management, market-research]
keywords: [n8n workflow whois api, tự động hóa quản lý domain, ai agent integration, bulk whois automation, market research domain]
---

# 🚀 **Tự Động Hóa WHOIS API Cho AI Agent: 8 Thao Tác Quản Lý Domain Miễn Code**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Tra cứu WHOIS** cho hàng trăm domain thủ công → Tốn thời gian và dễ sai sót.
- **Kiểm tra sẵn có** của domain một cách rời rạc → Không thể bulk processing.
- **Quản lý batch domain** phức tạp → Không có API tự động hóa.
- **Không tích hợp với AI agent** → Mất cơ hội tự động hóa nghiên cứu thị trường domain.

Workflow này **giải quyết tất cả** bằng cách chuyển đổi API WHOIS bulk thành **giao diện MCP** (Multi-Tool Call Protocol) cho AI agent, cho phép tự động hóa **8 thao tác quản lý domain** chỉ với **1 dòng code**!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian** tra cứu WHOIS và kiểm tra domain bulk.
- **Tích hợp AI agent** để tự động hóa nghiên cứu thị trường domain.
- **Quản lý batch domain** một cách hiệu quả (create, delete, query).
- **Kiểm tra sẵn có & authority** của domain chỉ với 1 API call.
- **Hoạt động 24/7** trên VPS self-hosted, không phụ thuộc vào thời gian làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **API Key** của MCP Server (được tự động sinh khi kích hoạt workflow).
2. **AI Agent** (các sếp có thể sử dụng **LangChain, LlamaIndex, hay AI agent tùy chỉnh**).
3. **VPS Self-Hosted** (để workflow chạy 24/7, không bị giới hạn bởi phiên bản cloud miễn phí).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
4. **Cài đặt n8n** trên VPS (hướng dẫn [tại đây](https://docs.n8n.io/hosting/installation/)).
5. **Cấu hình API Key** trong workflow (chi tiết ở phần sau).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5528](https://n8n.io/workflows/5528).
- **Import vào n8n Editor**:
  - Mở n8n Workflow Editor.
  - Nhấn **Import** → Chọn file JSON vừa tải.
  - **Hoặc copy/paste JSON** từ file vào ô **Import Workflow**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **MCP Trigger** và **8 HTTP Request Nodes** để tương tác với API WHOIS. Các bước cấu hình **quan trọng nhất**:

#### **🔑 Cấu Hình Authentication (API Key)**
- Mở node **"Bulk WHOIS MCP Server"** (type: `mcpTrigger`).
- Trong tab **Credentials**:
  - **Type**: Chọn **API Key in header**.
  - **Key name**: Điền **`X-API-KEY`**.
  - **Value**: Sinh ra một **API Key ngẫu nhiên** (n8n sẽ tự tạo, không cần điền thủ công).

#### **🔄 Cấu Hình HTTP Request Nodes (8 Endpoint)**
Workflow có **8 node HTTP Request Tool**, mỗi node tương ứng với **1 thao tác domain**:
| **Node Name**               | **Thao Tác**               | **URL API** (mặc định)       | **Lưu Ý** |
|-----------------------------|----------------------------|-------------------------------|------------|
| Get your batches            | Lấy danh sách batch       | `http://localhost:5000/batch` | Chỉnh `host` nếu API chạy trên port khác. |
| Create batch                 | Tạo batch mới             | `http://localhost:5000/batch` | Thêm tham số `body` để tạo batch. |
| Delete batch                 | Xóa batch                  | `http://localhost:5000/batch` | Thêm `batchId` trong `path`. |
| Get batch                    | Lấy chi tiết batch         | `http://localhost:5000/batch` | Thêm `batchId` trong `path`. |
| Query domain database        | Tra cứu database domain    | `http://localhost:5000/db`    | Thêm `query` trong `body`. |
| Check domain availability     | Kiểm tra sẵn có domain    | `http://localhost:5000/domain`| Thêm `domain` trong `body`. |
| Check domain rank (authority)| Kiểm tra authority domain | `http://localhost:5000/domain`| Thêm `domain` và `metric` trong `body`. |
| WHOIS query for a domain     | WHOIS lookup               | `http://localhost:5000/domain`| Thêm `domain` trong `body`. |

**Cách chỉnh:**
- Mở mỗi node `HTTP Request Tool`.
- Trong tab **Request Configuration**:
  - **Method**: Đặt thành **`POST`** (cho create, delete, query).
  - **URL**: Điền `http://localhost:5000/{endpoint}` (ví dụ: `http://localhost:5000/batch`).
  - **Headers**:
    - `Content-Type: application/json`
    - `X-API-KEY: {{ $node["Bulk WHOIS MCP Server"].json["apiKey"] }}` (sử dụng API Key từ node MCP Trigger).
  - **Body**: Thêm JSON theo yêu cầu (ví dụ:
    ```json
    {
      "domain": "example.com"
    }
    ```
    hoặc
    ```json
    {
      "batch": {
        "name": "batch_test",
        "domains": ["example1.com", "example2.com"]
      }
    }
    ```
  ).

#### **🔄 Cấu Hình MCP Trigger**
- Node **"Bulk WHOIS MCP Server"** (type: `mcpTrigger`) sẽ tự động sinh **URL Webhook**.
- **Copy URL này** để kết nối với AI Agent (ví dụ: trong LangChain, LlamaIndex).

---

### **⚡️ Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Sử dụng **HTTP Request Tool** để gọi API và kiểm tra kết quả.
   - Ví dụ: Gọi `POST http://localhost:5000/domain` với body:
     ```json
     {
       "domain": "testdomain.vn"
     }
     ```
   - Nếu trả về `WHOIS data`, workflow hoạt động đúng.

2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Kiểm tra log** để đảm bảo không có lỗi.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Với AI Agent**
- **LangChain Example**:
  ```python
  from langchain.agents import initialize_agent
  from langchain.agents import AgentType
  from langchain.tools import Tool
  from langchain.llms import OpenAI

  # Thêm tool WHOIS API vào AI Agent
  tools = [
      Tool(
          name="WHOIS_API",
          func=lambda query: requests.post(
              "YOUR_MCP_URL_HERE",
              json={"query": query},
              headers={"X-API-KEY": "YOUR_API_KEY"}
          ).json(),
          description="Query WHOIS API for domain information"
      )
  ]

  llm = OpenAI(temperature=0)
  agent = initialize_agent(tools, llm, agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION, verbose=True)
  ```
- **LlamaIndex Example**:
  - Sử dụng **MCP Plugin** để kết nối với n8n.

### **2. Lưu Log & Monitoring**
- Thêm **node `n8n-nodes-base.terminate`** để log lỗi.
- Sử dụng **node `n8n-nodes-base.set`** để lưu kết quả vào **Google Sheets** hoặc **Database**.

### **3. Tự Động Gửi Báo Cáo**
- Thêm **node `n8n-nodes-base.email`** để gửi báo cáo WHOIS hàng ngày.
- Ví dụ: Gửi email với tiêu đề **"WHOIS Report - Domain Availability"** và nội dung là kết quả tra cứu.

### **4. Cập Nhật Batch Tự Động**
- Sử dụng **node `n8n-nodes-base.schedule`** để chạy batch WHOIS định kỳ (ví dụ: hàng tuần).

---

## **📌 Kết Luận**
Workflow này **chuyển đổi API WHOIS bulk thành giao diện MCP**, cho phép AI agent tự động hóa **8 thao tác quản lý domain** một cách hiệu quả. Các sếp không cần viết code, chỉ cần:
1. **Import workflow** vào n8n.
2. **Cấu hình API Key** và URL.
3. **Kết nối với AI Agent** (LangChain, LlamaIndex...).
4. **Bật Active** và bắt đầu tự động hóa!

**🚀 Hành động ngay:**
- [Tải workflow](https://n8n.io/workflows/5528) và cài đặt trên VPS.
- [Đăng ký VPS](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**.
- **Tích hợp với AI Agent** và tự động hóa nghiên cứu thị trường domain!

---
**💬 Cần hỗ trợ thêm?**
- **Ping David Ashby** trên [Discord](https://discord.me/cfomodz).
- **Xem tài liệu chi tiết** tại [n8n MCP Docs](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp/).